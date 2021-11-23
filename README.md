# pythonsslservers

Simple Webservers can be run using

Python2:

```bash
python2 -m SimpleHTTPServer
```
Python3:

```bash
python3 -m http.server
```
SSL enabled simple servers take a bit more:
### Generate Self-signed Certificate
openssl req -newkey rsa:4096 -nodes -sha256 -keyout key.pem -x509 -days 365 -out cert.pem

### Deploy Simple SSL Server

Python3:

```bash
# HTTPS server Python3 

from http.server import HTTPServer, SimpleHTTPRequestHandler
import ssl

httpd = HTTPServer(('localhost', 4443), SimpleHTTPRequestHandler)
httpd.socket = ssl.wrap_socket (httpd.socket, keyfile="./key.pem", certfile='./cert.pem', server_side=True)

httpd.serve_forever()

```

Python2

```bash
# HTTPS server Python2

import BaseHTTPServer, SimpleHTTPServer
import ssl

httpd = BaseHTTPServer.HTTPServer(('localhost', 4443),
        SimpleHTTPServer.SimpleHTTPRequestHandler)

httpd.socket = ssl.wrap_socket (httpd.socket,
        keyfile="./key.pem",
        certfile='./cert.pem', server_side=True)

httpd.serve_forever()
```
