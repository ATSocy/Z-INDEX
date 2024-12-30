Thread: invalid-host-specified-403-error
0x3639 | 2023-02-08 22:34:59 UTC | #1

I'm working on a fully integrated znnd node on Docker that includes znnd, caddy for SSL certs, Uptime Kuma for public reporting, and Grafana with Loki for internal management.  

On initial setup with Caddy I was getting an `invalid host specified` error 403.  I previously faced this issue with my stand alone NGINX load balancer setup.  I documented the issue on stackoverflow and never was able to fix it.  I ultimately disabled the load balancer in NGINX and could run queries on 35997.  But not in load balance mode.    

https://stackoverflow.com/questions/72973080/nginx-load-balancer-403-error-invalid-host-specified-when-using-upstream

Fast forward to this new node project and I transitioned to [Caddy](https://caddyserver.com/) because it's VERY easy to setup SSL certs on Letsencrypt.  The server block is 2 lines and Caddy handles everything behind the scenes. 

On initial setup I ran the following query:
```
curl -X GET https://00.deeznnutz.com:35997 -H "content-type: application/json" -d '{"jsonrpc": "2.0", "id": 40, "method": "stats.networkInfo", "params": []}'
```
And got the same `invalid host specified` error as before in the NGINX setup.  I documented the problem here:

https://caddy.community/t/ssl-on-different-post-returns-403-error/18245/4

I inspected the headers and found the flowing

Failing Request:
```
4648","proto":"HTTP/1.1","method":"GET","host":"00.deeznnutz.com:35997","uri":"/","headers":{"User-Agent":["curl/7.84.0"],"Accept":["*/*"],"Content-Type":["application/json"],"Content-Length":["73"],"X-Forwarded-For":["50.247.129.189"],"X-Forwarded-Proto":["http"],"X-Forwarded-Host":["00.deeznnutz.com:35997"]}},"headers":{"Content-Type":["text/plain; charset=utf-8"],"X-Content-Type-Options":["nosniff"],"Date":["Mon, 26 Dec 2022 15:28:06 GMT"]},"status":403}
```

Successful Request:
```
":"12714","proto":"HTTP/1.1","method":"GET","host":"70.34.152.117:35997","uri":"/","headers":{"Content-Type":["application/json"],"Content-Length":["73"],"User-Agent":["curl/7.84.0"],"X-Forwarded-For":["50.247.129.189"],"X-Forwarded-Proto":["http"],"X-Forwarded-Host":["70.34.152.117:35997"],"Accept":["*/*"]}},"headers":{"Content-Type":["application/json"],"Date":["Mon, 26 Dec 2022 15:58:43 GMT"],"Vary":["Origin"]},"status":200}
":"12714"
```

For some reason, znnd will not accept `"host" : "ANY DOMAIN NAME"`

![image|560x308](upload://eIJ4Kd8wpNgamhIOdf5dsJdRp4O.png)

I had to change the `"host"` name to an IP address with the following block in `Caddyfile`

```
00.deeznnutz.com:35997 {
        reverse_proxy znnd:35997 {
                header_up host "70.34.152.117:35997"
        }
}
```

Now the request looks like this.

```
":"12714","proto":"HTTP/1.1","method":"GET","host":"70.34.152.117:35997","uri":"/","headers":{"Content-Type":["application/json"],"Content-Length":["73"],"User-Agent":["curl/7.84.0"],"X-Forwarded-For":["50.247.129.189"],"X-Forwarded-Proto":["http"],"X-Forwarded-Host":["00.deeznnutz.com:35997"],"Accept":["*/*"]}},"headers":{"Content-Type":["application/json"],"Date":["Mon, 26 Dec 2022 15:58:43 GMT"],"Vary":["Origin"]},"status":200}
":"12714"
```

You might notice that `"X-Forwarded-Host":["00.deeznnutz.com:35997"]` seems to be acceptable in the header.  Not sure why.  I left it as to be researched another day.

-------------------------

