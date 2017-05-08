# Performance Testing (Lower Environment)

The following steps show how to use JMeter and New Relic for performance testing a Bluemix application.

## Prerequisites

Download and install the latest release of [Apache JMeter](http://jmeter.apache.org/) and access to a [New Relic](https://newrelic.com/) account.

### Create a New Test in JMeter

1. Open JMeter > Templates > Create.

2. Thread Group > # of Threads = 3 > Loop Count = 2.

3. Thread Goup > Recording Controller > Add > Listener > View Results in Table.

4. HTTP Request Defaults > Server Name = aa-dynamic-reaccom-ui-dev.mybluemix.net

5. Make sure FireFox > Options > Network > Settings > Manual proxy configuration 
	⋅⋅* HTTP Proxy = localhost
	⋅⋅* Port = 8888
	⋅⋅* Use this proxy server for all protocols = checked

6. Start WorkBench > HTTP(S) Test Script Recorder. In FireFox browser refresh the URL to test.

7. After running the initial test for recording,
 
   Rename: 
	⋅⋅* Main | Transaction Controller - "4 / - Main Dynamic Reaccom Transaction"
	⋅⋅* Main | HTTP Request - "4 / - Main Dynamic Reaccom Request"
	⋅⋅* Reservation | Transaction Controller - "27 /reservations/NPUNJW - AJAX Transaction"

   Remove: 
	⋅⋅* "success.txt" from the test.
	⋅⋅* "save browsing..." from the test.
	⋅⋅* (And others as you see fit.)

8. After running the initial test and updating the script, reset browser network settings
	⋅⋅* FireFox > Options > Network > Settings > Use system proxy settings

9. Stop WorkBench > HTTP(S) Test Script Recorder, if still running before running a test.

### Run Existing Test in JMeter

10. Open your saved .jmx test plan. 

11. CTRL + E to clear any previous results in "View Results in Table". Then press green start button at top again if results are not in table.

12. Identify the pieces and owner of items taking a long time to load (i.e. 200ms = 2 milliseconds).

### Transaction Details Using New Relic

13. Login to [New Relic](https://rpm.newrelic.com/) and go to "Service Maps" section.

14. Identify the "aa-reservation-service-dev" microservice, click on white space top view 4 metrics (response time, Apdex, Throughput, and Error rate).  Note the Response time (i.e. 2.29k ms).

15. If external connections of the app is not showing, click on the half-moon next to the elipse and add external services to the map. Click on the white space of the external connection to view two metrics (throughput and response time). Note the Response time (i.e. 271 ms).

16. Click on the link within the external connection to view more detail. Make sure to change the "Time Picker" to "Last 30 minutes ending now". The Response Time should be close to the figure seen (i.e. 291 ms) during the previous step (271 ms).
