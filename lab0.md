# Lab Checkpoint 0: networking warmup

## Networking by hand

### 1. Fetch a Web Page

After establishing the telnet connection between remote server and local machine, you need to type in the request content a bit quickly. Otherwise, connection will be closed by foreign host.

```bash
telnet cs144.keithw.org http
```

It's better to type in the whole content at one time.

```http
GET /hello HTTP/1.1
Host: cs144.keithw.org 
Connection: close
# enter: Sends an empty line
```

You will get the following output and the connection will be closed.

```http
HTTP/1.1 200 OK
Date: Sat, 06 May 2023 12:04:47 GMT
Server: Apache
Last-Modified: Thu, 13 Dec 2018 15:45:29 GMT
ETag: "e-57ce93446cb64"
Accept-Ranges: bytes
Content-Length: 14
Connection: close
Content-Type: text/plain

Hello, CS144!
```

:pencil: _Assignment_

Now lets give it a try. I have no SUNet ID so I replace it with a series of random number: `2023955801`.

```bash
telnet cs144.keithw.org http

GET /lab0/2023955801 HTTP/1.1
Host: cs144.keithw.org 
Connection: close
```

I receive `X-Your-Code-Is: 217225`.

```http
HTTP/1.1 200 OK
Date: Sat, 06 May 2023 12:22:09 GMT
Server: Apache
X-You-Said-Your-SunetID-Was: 2023955801
X-Your-Code-Is: 217225
Content-length: 114
Vary: Accept-Encoding
Connection: close
Content-Type: text/plain

Hello! You told us that your SUNet ID was "2023955801". Please see the HTTP headers (above) for your secret code.
```

### 2. Send yourself an email

I have no SUNet ID. If everything goes well you will get the output as follow.

```bash
telnet 148.163.153.234 smtp
```

```bash
MAIL FROM: sunetid @stanford.edu
# 250 2.1.0 Sender ok
RCPT TO: sunetid @stanford.edu
# 250 2.1.5 Recipient ok
DATA
# 354 End data with <CR><LF>.<CR><LF>
From: sunetid@stanford.edu
To: sunetid@stanford.edu
Subject: Hello from CS144 Lab 0!
.
# 250 2.0.0 33h24dpdsr-1 Message accepted for delivery
QUIT
```

### 3. Listening and connecting

Now it’s time to experiment with being a simple
**server**: the kind of program that waits around for clients to connect to it.

- `netcat` terminal window

    ```bash
    netcat -v -l -p 9090
    # netcat output here
    Listening on 0.0.0.0 9090
    Connection received on localhost 34206
    hahaha
    ^C
    ```

- `telnet` terminal window

    ```bash
    telnet localhost 9090
    # telnet output here
    Trying 127.0.0.1...
    Connected to localhost.
    Escape character is '^]'.
    hahaha
    Connection closed by foreign host.
    ```
