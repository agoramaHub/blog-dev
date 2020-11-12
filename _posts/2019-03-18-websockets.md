---
layout: post
title:  "Sensor IoT Workshop - Websockets"
date:   2019-03-15 12:30:00 0000
categories: education
thumbnail: /images/websocket.png
excerpt: Working with RPI and Websockets
---

# Raspberry Pi & Websockets

![alt text](/images/rpi.png)
So you have your sensory data coming into the raspberry pi - perhaps you want to send that data to another computer?

# Install Tornado on the Raspberry PI

We are going to use Tornado a python package that handles web sockets.
We are going to use version 5.1 because it is the last version compatible with python 2.7
```
$ pip install tornado==5.1
```
# Create a Websocket on the Raspberry PI

![alt text](/images/websocket.png)
Create a file on the Raspberry pi that will communicate with the client (your computer)
```
import tornado.httpserver
import tornado.websocket
import tornado.ioloop
import tornado.web

class WSHandler(tornado.websocket.WebSocketHandler):
  def check_origin(self, origin):
        return True
  def open(self):
    print 'New connection was opened'
    self.write_message("Welcome to my websocket!")

  def on_message(self, message):
    print 'Incoming message:', message
    self.write_message("You said: " + message)

  def on_close(self):
    print 'Connection was closed...'

application = tornado.web.Application([
  (r'/', WSHandler),
])

if __name__ == "__main__":
  http_server = tornado.httpserver.HTTPServer(application)
  http_server.listen(9999)
  tornado.ioloop.IOLoop.instance().start()

```
Save this file as something e.g. websocket.py and run it using the command

```
python websocket.py
```
# Create a website to interact with the Raspberry PI
```
<!doctype html>
<html>
  <head>
    <title>WebSockets with Python & Tornado</title>
    <meta charset="utf-8" />
    <style type="text/css">
      body {
        text-align: center;
        min-width: 500px;
      }
    </style>
    <script src="//ajax.googleapis.com/ajax/libs/jquery/1.8.3/jquery.min.js"></script>
    <script>
      $(function(){
        var ws;
        var logger = function(msg){
          var now = new Date();
          var sec = now.getSeconds();
          var min = now.getMinutes();
          var hr = now.getHours();
          $("#log").html($("#log").html() + "<br/>" + hr + ":" + min + ":" + sec + " ___ " +  msg);
          //$("#log").animate({ scrollTop: $('#log')[0].scrollHeight}, 100);
          $('#log').scrollTop($('#log')[0].scrollHeight);
        }

        var sender = function() {
          var msg = $("#msg").val();
          if (msg.length > 0)
            ws.send(msg);
          $("#msg").val(msg);
        }

        ws = new WebSocket("ws://172.16.0.9:9999/"); <!––Change the IP address to the IP of your Rasperry PI!––>
        ws.onmessage = function(evt) {

          logger(evt.data);
        };
        ws.onclose = function(evt) {
          $("#log").text("Connection was closed...");
          $("#thebutton #msg").prop('disabled', true);
        };
        ws.onopen = function(evt) { $("#log").text("Opening socket..."); };

        $("#msg").keypress(function(event) {
          if (event.which == 13) {
             sender();
           }
        });

        $("#thebutton").click(function(){
          sender();
        });
      });
    </script>
  </head>

  <body>
    <h1>WebSockets with Python & Tornado</h1>
    <div id="log" style="overflow:scroll;width:500px; height:200px;background-color:#ffeeaa; margin:auto; text-align:left">Messages go here</div>

    <div style="margin:10px">
      <input type="text" id="msg" style="background:#fff;width:200px"/>
      <input type="button" id="thebutton" value="Send" />
    </div>

  </body>
</html>
```

The key thing to remember to change in the web client script is the IP address of your pi
```
  ws = new WebSocket("ws://172.16.0.9:9999/");
```
Without this the client webpage does not know where to look and find your rpi on the local network.

# View your website and interact with RPI using websocket
```
cd /DIRECTORY/TO/FOLDER/
```
Viewing and serving a website
```python -m SimpleHTTPServer ```

Open up your favorite browser and enter ``` localhost:8000 ``` into the searchbar. You should be shown a file directory of where you are creating a python server.
This is not limited to one client - what happens when someone else goes to your website and begins interacting with your Raspberry pi?

references for this Tutorial
Mainly from
[Rasperry Pi Tornado websockets](https://lowpowerlab.com/2013/01/17/raspberrypi-websockets-with-python-tornado/)
[Controlling GPIO pins](https://www.hackster.io/innat/raspberry-pi-websocket-acef41)
[tutorial 4](http://niltoid.com/blog/raspberry-pi-arduino-tornado/)
[Temperature sensor website display](https://gist.github.com/joewashear007/8276467)
[Node guide ](https://www.jaredwolff.com/raspberry-pi-getting-interactive-with-your-server-using-websockets/#show1)
