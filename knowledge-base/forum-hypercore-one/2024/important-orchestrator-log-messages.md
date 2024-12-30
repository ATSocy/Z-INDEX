Thread: important-orchestrator-log-messages
0x3639 | 2023-08-27 20:49:59 UTC | #1

## Helpful syslog messages for Orchestrator Operators

`KeyGen threshold was not met`
Key generation threshold was not met during the keygen process

`orchestrator successfully started`
Orchestrator started

`websocket: close 1006 (abnormal closure): unexpected EOF`
Orchestrator failed because znn node is down

`websocket: close 1001 (going away): upstream went away`
Orchestrator failed because eth node is down

`Stopping orchestrator`
Orchestrator stopping

`Started ECDSA Keygen`
The process to start a new key generation has started.

I think the best way to monitor the Orchestrator is to watch the `pid` (Process ID).  If it goes down or up, alert.  Also, we can look for `websocket: close 1006` or `websocket: close 1001` in the `syslog`. alert if either message is found. 

The main reason the orchestrator goes down is because it loses connection to a node.    

## Example commands to query syslog

`journalctl --unit=orchestrator -n 100000 --no-pager | grep "websocket: close 1001"`

`journalctl --unit=orchestrator -n 100000 --no-pager | grep "websocket: close 1006"`

`journalctl --unit=orchestrator -n 100000 --no-pager | grep "Stopping orchestrator"`

`journalctl --unit=orchestrator -n 100000 --no-pager | grep "Orchestrator started"`

`journalctl --unit=orchestrator -n 100000 --no-pager | grep "Keygen"`

`journalctl --unit=orchestrator -n 100000 --no-pager | grep "KeyGen threshold"`

-------------------------

sumamu | 2023-06-16 11:05:10 UTC | #2

[quote="0x3639, post:1, topic:125"]
The main reason the orchestrator goes down is because it loses connection to a node.
[/quote]

That's right. It's intentional, but it assumes there's a service to restart it automatically if it crashes, so there should always be a service that restarts it and it shouldn't run standalone.

-------------------------

