# adjust-sre-assignment

1. Please write a simple CLI application in the language of your choice that does the following:
Print the numbers from 1 to 10 in random order to the terminal.

The script rand.py should print numbers between 1-10 in a random order using the python in built function of random.randint
The script uses the local python env to run this and hence the shebang line should be replaced with the location of the python install where this is intended to run on usually /usr/bin/python


2.Imagine a server with the following specs:
- 4 times Intel(R) Xeon(R) CPU E7-4830 v4 @ 2.00GHz
- 64GB of ram
- 2 tb HDD disk space
- 2 x 10Gbit/s nics
The server is used for SSL offloading and proxies around 25000 requests per second.
Please let us know which metrics are interesting to monitor in that specific case and how would you do that? What are the challenges of the monitoring?

First off system metrics like 
- CPU% used vs free and total. Load averages across 5,10 and 15 minute averages
- System Memory used vs free and total/paging 
- Disk I/O read/write requests/sec, await – average time to service a request in ms
- Network traffic. bytes in/out, rx/tx, number of packets recieved/dropped on an interface, ping latenices, 


For ssl offloading the following metrics:
- Inbound Traffic	
- Outbound Traffic
- Open Connections	
- New Connections per second	
- Closed connections per second
- RTT (between client and proxy if possible[read below])
- SSl connect times

The most obvious challenge of measuring https proxies is that when resolving the DNS name of the webserver, the client connects to the proxy and the proxy does the DNS resolution and connects to the webserver. At this point, it sends a message back to the client indicating that a connection has been established. The client now begins the SSL handshake, which is tunneled through the proxy’s open connection to the webserver. The SSL time is measured as the time from when the “CONNECT” message is sent until the SSL handshake is completed.. So, when making an HTTPS request, these values now become part of the SSL time and not the connection(wait) time. Hence this gets a lil tricky to monitor
