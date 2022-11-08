<img src=./image.png width=50%>

# Librarify requests failure report
Recently it was reported that the Librarify platform was returning 500 Error on all requests made on the platform routes, 
all the services were down.  100% of the users were affected by the outage.
The root cause was the failure of the master server web-01.

## Timeline
The error was realized on Saturday 26th February 1200 hours (EAT) when the Site Reliability Engineer, Mr Esco saw the master server lagging in speed.
Our engineers on call disconnected the master server web-01 for further system analysis and channelled all requests to client server web-02. 
The problem was dealt with by Sunday 27th Febraury 2200 hours (EAT).

## Root cause
The Librarify platform is served by 2 ubuntu cloud servers. 
The root cause of the hiccup was that master server web-01 was connected to serve all requests, 
and it stopped functioning due to memory outage as a results of so many requests.
This happened because during a previous test, the client server web-02 was disconnected temporarily for testing and was not connected to the load balancer afterwards. 

## Resolution
The issue was fixed when the master server was temporarily disconnected for memory clean-up then connected back to the loadbalancer 
and round-robin algorithm was configured so that both the master and client servers can handle equal amount of requests.

## Measures against such problem in future
- Balance: Choose the best loadbalancing algorithm for your programs.
- Vigilance: Always keep an eye on your servers to ensure they are running properly.
- Redundancy: Have extra back-up servers to prevent your program fro completely going offline during an issue.
