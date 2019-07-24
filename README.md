# flask-counter-app


Deploy Kubernetes App

Steps followed →


1. I have used GKE to deploy application


2. Cloned docker image from https://hub.docker.com/r/tarunbhardwaj/flask-counter-app


3. Deployed redis with 1 replica considering it as master. Created 2 files →
redis-deployments.yml and, redis-services.yml

akshits-MacBook-Pro:fulfil-app akshitsinghal$ kubectl create -f redis-deployment.yaml
deployment.extensions/redis created
akshits-MacBook-Pro:fulfil-app akshitsinghal$ kubectl create -f redis-service.yaml
service/redis created



4. Then deployed counter application and have used redis-url from the above deployed
redis. I have created 2 files for the deployment → app-deployments.yml &
app-services.yml


5. Then I checked application logs and pod/svc/deployment status just to make sure if
everything is fine or not.

akshits-MacBook-Pro:fulfil-app akshitsinghal$ kubectl logs

pods/fulfil-io-app-7cdbcf8976-d7j4k

[2019-07-24 22:01:22 +0000] [6] [INFO] Starting gunicorn 19.9.0

[2019-07-24 22:01:22 +0000] [6] [INFO] Listening at: http://0.0.0.0:5000 (6)

[2019-07-24 22:01:22 +0000] [6] [INFO] Using worker: gevent

[2019-07-24 22:01:22 +0000] [9] [INFO] Booting worker with pid: 9


6. Tested the application by hitting the application url on browser
http://34.67.121.227:5000/


7. Also tested the deployment via apache benchmark (ab)

akshits-MacBook-Pro:flask-counter-app akshitsinghal$ ab -l -c 100 -t 10

http://34.67.121.227:5000/

This is ApacheBench, Version 2.3 <$Revision: 1826891 $>

Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/

Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking 34.67.121.227 (be patient)

Finished 1579 requests

Server Software: gunicorn/19.9.0

Server Hostname: 34.67.121.227

Server Port: 5000

Document Path: /

Document Length: Variable

Concurrency Level: 100

Time taken for tests: 10.001 seconds

Complete requests: 1579

Failed requests: 0

Total transferred: 273167 bytes

HTML transferred: 20527 bytes

Requests per second: 157.88 [#/sec] (mean)

Time per request: 633.387 [ms] (mean)

Time per request: 6.334 [ms] (mean, across all concurrent requests)

Transfer rate: 26.67 [Kbytes/sec] received

Connection Times (ms)

min mean[+/-sd] median max

Connect: 263 281 10.0 278 351

Processing: 265 298 110.9 282 1925

Waiting: 265 298 111.0 282 1925

Total: 528 579 112.4 562 2206

Percentage of the requests served within a certain time (ms)

50% 562

66% 571

75% 578

80% 586

90% 621

95% 646

98% 667

99% 676

100% 2206 (longest request)
