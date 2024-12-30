Thread: chatgpt-api-healthcheck-api-endpoint-in-python-with-telegram-integration
0x3639 | 2023-06-14 23:31:21 UTC | #1

For anyone who is not a coder (like me).  I just used ChatGPT to create an API endpoint for the my.hc1hode.com.  Here is the code that I iteratively produced.  It took me about 25 revisions.  Each revision I added and tested the code.   

This code is designed to respond to a healthcheck query on the endpoint `:8080/healthcheck`  It returns an HTTP status along with json message to the browser.  Then it logs error messages and keeps track of the status with a simple txt file.  Then it sends a notification to Telegram of status change in a threaded process so as to not slow down the healthcheck response to the load balancer. 

I did this in python because I'm most familiar with it.  Anyone here, any non-dev can use chatGPT to help read the go-zenon code.  Anyone can contribute to the code base with the help of chatGPT.  Just gotta try!

```
from flask import Flask, jsonify
import requests
import json
import logging
import telegram_send
import threading

app = Flask(__name__)

# Set up logging
logging.basicConfig(level=logging.INFO)

# The filename of the text file where we'll store the last status code
status_file = "healthstatus.txt"

# Define node name
node_name = "Node-02"

def read_last_status_code():
    try:
        with open(status_file, 'r') as f:
            return f.read().strip()
    except Exception:
        return '200 OK'  # If we can't read the file for any reason, assume the last status was 200 OK

def write_last_status_code(code):
    with open(status_file, 'w') as f:
        f.write(str(code))

def send_telegram_message(message):
    telegram_send.send(messages=[message])

@app.route("/healthcheck", methods=['GET'])
def healthcheck():
    url = "https://my.hc1node.com:35997"
    headers = {"content-type": "application/json"}
    data = {"jsonrpc": "2.0", "id": 21, "method": "stats.syncInfo", "params": []}
    timeout = 5  # in seconds

    try:
        response = requests.get(url, headers=headers, data=json.dumps(data), timeout=timeout)

        if response.status_code == 200:
            json_response = response.json()
            if "result" in json_response and "state" in json_response["result"] and json_response["result"]["state"] in [2, 3]:
                state = json_response["result"]["state"]
                logging.info(f"Health check OK, state: {state}")

                # If the last status code was not 200, send a message to Telegram
                if read_last_status_code() != '200 OK':
                    threading.Thread(target=send_telegram_message, args=(f"{node_name}: Healthcheck is now OK",)).start()
                    write_last_status_code('200 OK')

                return jsonify({"message": "OK"}), 200
    except requests.Timeout as e:
        logging.error(f"Request timeout: {e}")
        if read_last_status_code() != '504 Timeout Error':
            threading.Thread(target=send_telegram_message, args=(f"{node_name}: Healthcheck resulted in Timeout Error",)).start()
            write_last_status_code('504 Timeout Error')

        return jsonify({"message": "Timeout Error"}), 504
    except requests.ConnectionError as e:
        logging.error(f"Connection error: {e}")
        if read_last_status_code() != '503 Connection Error':
            threading.Thread(target=send_telegram_message, args=(f"{node_name}: Healthcheck resulted in Connection Error",)).start()
            write_last_status_code('503 Connection Error')

        return jsonify({"message": "Connection Error"}), 503

    if read_last_status_code() != '503 Bad Gateway':
        logging.warning("Bad Gateway")
        threading.Thread(target=send_telegram_message, args=(f"{node_name}: Healthcheck resulted in Bad Gateway",)).start()
        write_last_status_code('503 Bad Gateway')

    return jsonify({"message": "Bad Gateway"}), 503

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=8080)
```

-------------------------

0x3639 | 2023-06-16 22:44:52 UTC | #2

updated code.  I wrote this entire code in ChatGPT 4.  Still testing to make sure everything works.

```
import sqlite3
from sqlite3 import Error
import time
import requests
from flask import Flask, jsonify, request
from datetime import datetime, timedelta  # added timedelta
import logging
import subprocess

logging.basicConfig(level=logging.INFO)

DATABASE = 'healthcheck.db'

def create_connection():
    conn = None;
    try:
        conn = sqlite3.connect(DATABASE)  # Creates database file if it doesn't exist
        logging.info(f'Successful connection with {DATABASE}')
    except Error as e:
        logging.error(f'Error occurred: {e}')
    return conn

def create_table(conn):
    try:
        sql_create_table = """CREATE TABLE IF NOT EXISTS healthcheck (
                                id integer PRIMARY KEY,
                                state integer NOT NULL,
                                status_code integer,
                                timestamp text NOT NULL
                            ); """
        c = conn.cursor()
        c.execute(sql_create_table)  # Creates the table only if it doesn't exist
    except Error as e:
        logging.error(f'Error occurred: {e}')

def insert_healthcheck(conn, state, status_code):
    try:
        sql_insert_query = '''INSERT INTO healthcheck(state, status_code, timestamp)
                              VALUES(?,?,?)'''
        c = conn.cursor()
        c.execute(sql_insert_query, (state, status_code, datetime.now().isoformat()))
        conn.commit()
    except Error as e:
        logging.error(f'Error occurred: {e}')

def get_latest_status_code(conn):
    try:
        sql_select_query = '''SELECT status_code FROM healthcheck ORDER BY timestamp DESC LIMIT 1'''
        c = conn.cursor()
        c.execute(sql_select_query)
        result = c.fetchone()
        return result[0] if result else None
    except Error as e:
        logging.error(f'Error occurred: {e}')
        return None

def clean_old_records(conn):
    try:
        thirty_days_ago = datetime.now() - timedelta(days=30)
        sql_delete_query = '''DELETE FROM healthcheck WHERE timestamp < ?'''
        c = conn.cursor()
        c.execute(sql_delete_query, (thirty_days_ago.isoformat(),))
        conn.commit()
    except Error as e:
        logging.error(f'Error occurred: {e}')

conn = create_connection()
create_table(conn)
previous_status_code = get_latest_status_code(conn)

app = Flask(__name__)

@app.route('/healthcheck', methods=['GET'])
def healthcheck():
    conn = create_connection()  # Moved inside the function
    global results, previous_status_code
    if not results:
        status_code = 503
        insert_healthcheck(conn, 0, status_code)
        if previous_status_code and previous_status_code != status_code:
            subprocess.run(['telegram-send', f'Status code changed: {status_code}'])
        previous_status_code = status_code
        return 'Service Unavailable', status_code
    elif results.get('result', {}).get('state') == 1:
        status_code = 500
        insert_healthcheck(conn, 1, status_code)
        if previous_status_code and previous_status_code != status_code:
            subprocess.run(['telegram-send', f'Status code changed: {status_code}'])
        previous_status_code = status_code
        return 'Internal Server Error', status_code
    status_code = 200
    insert_healthcheck(conn, results.get('result', {}).get('state'), status_code)
    if previous_status_code and previous_status_code != status_code:
        subprocess.run(['telegram-send', f'Status code changed: {status_code}'])
    previous_status_code = status_code
    return jsonify(results), status_code

@app.route('/publish', methods=['POST'])
def publish():
    global results
    results = request.get_json()
    current_time = datetime.now().isoformat()
    return jsonify({'message': f'Data received successfully at {current_time}!'}), 200

def send_requests():
    headers = {
        "content-type": "application/json",
    }
    data = {
        "jsonrpc": "2.0",
        "id": 40,
        "method": "stats.syncInfo",
        "params": [],
    }

    global results
    results = {}

    while True:
        try:
            response = requests.get('http://127.0.0.1:35997', headers=headers, json=data, timeout=5)
            data_to_send = response.json()
            logging.info(f'Received data: {data_to_send}')
            requests.post('http://127.0.0.1:8080/publish', json=data_to_send)
        except requests.exceptions.Timeout:
            logging.error('Request timeout')
            results = {}
        except Exception as e:
            logging.error(f'An error occurred: {e}')
        time.sleep(10)

if __name__ == '__main__':
    from threading import Thread

    # Start the Flask application on another thread
    Thread(target=app.run, kwargs={
        'host': '0.0.0.0',
        'port': 8080
    }).start()

    # Start the SQLite database cleanup on another thread
    Thread(target=clean_old_records, args=(conn,)).start()

    send_requests()
```

-------------------------

