# Filtering Logs based on Response Code

Example Logs with return 200 and 500

Namefile : Logs.txt
```
172.10.36.38 - - [09/Sep/2015:08:01:27 +0000] "GET / HTTP/1.1" 200 999 "-" "kube-probe/1.9" "-"
172.10.36.38 - - [09/Sep/2015:08:01:32 +0000] "GET / HTTP/1.1" 500 999 "-" "kube-probe/1.9" "-"
172.10.36.38 - - [09/Sep/2015:08:01:37 +0000] "GET / HTTP/1.1" 200 999 "-" "kube-probe/1.9" "-"
172.10.36.38 - - [09/Sep/2015:08:01:42 +0000] "GET / HTTP/1.1" 500 999 "-" "kube-probe/1.9" "-"
172.10.36.38 - - [09/Sep/2015:08:01:47 +0000] "GET / HTTP/1.1" 500 999 "-" "kube-probe/1.9" "-"
172.10.36.38 - - [09/Sep/2015:08:01:52 +0000] "GET / HTTP/1.1" 500 999 "-" "kube-probe/1.9" "-"
172.10.36.38 - - [09/Sep/2015:08:01:57 +0000] "GET / HTTP/1.1" 500 999 "-" "kube-probe/1.9" "-"
172.10.36.38 - - [09/Sep/2015:08:02:02 +0000] "GET / HTTP/1.1" 200 999 "-" "kube-probe/1.9" "-"
172.10.36.38 - - [09/Sep/2015:08:02:07 +0000] "GET / HTTP/1.1" 200 999 "-" "kube-probe/1.9" "-"
172.10.36.38 - - [09/Sep/2015:08:02:12 +0000] "GET / HTTP/1.1" 500 999 "-" "kube-probe/1.9" "-"
172.10.36.38 - - [09/Sep/2015:08:02:17 +0000] "GET / HTTP/1.1" 200 999 "-" "kube-probe/1.9" "-"
172.10.36.38 - - [09/Sep/2015:08:02:22 +0000] "GET / HTTP/1.1" 200 999 "-" "kube-probe/1.9" "-"
```

We can create filter using bash script and dynamic response code.

First, we need to define variable for input there is filename and response code filter.  

Namefile : filter.bash
```
#!/bin/bash

namefile=$1
responsecode=$2
tail -n 100 $namefile | grep $responsecode

```

Variable "namefile" will be read name of logging file.
```
namefile=$1
```


Then, we will read response code by this variable.
```
responsecode=$2
```

Tail will show all logging in that file, after that grep will be filtering rows by response code.
So, all file including correct response code will be shown.
```
tail -n 100 $namefile | grep $responsecode
```


How to use
```
chmod +x filter.bash
./filter.bash <<NAMEFILE>> <<REPONSE_CODE>>
```

Result 
```
test-folder $ ./filter.bash test.txt 500
172.10.36.38 - - [09/Sep/2015:08:01:32 +0000] "GET / HTTP/1.1" 500 999 "-" "kube-probe/1.9" "-"
172.10.36.38 - - [09/Sep/2015:08:01:42 +0000] "GET / HTTP/1.1" 500 999 "-" "kube-probe/1.9" "-"
172.10.36.38 - - [09/Sep/2015:08:01:47 +0000] "GET / HTTP/1.1" 500 999 "-" "kube-probe/1.9" "-"
172.10.36.38 - - [09/Sep/2015:08:01:52 +0000] "GET / HTTP/1.1" 500 999 "-" "kube-probe/1.9" "-"
172.10.36.38 - - [09/Sep/2015:08:01:57 +0000] "GET / HTTP/1.1" 500 999 "-" "kube-probe/1.9" "-"
172.10.36.38 - - [09/Sep/2015:08:02:12 +0000] "GET / HTTP/1.1" 500 999 "-" "kube-probe/1.9" "-"
```

