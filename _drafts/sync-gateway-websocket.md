---
layout: post
title:  "How to connect to the Couchbase Sync Gateway over Websockets"
date:  
categories: couchbase sync-gateway websocket programming
---

Over the last year or so, I've been working with Couchbase Mobile to handle data persistance and syncing for our mobile applications at work.  One component of Couchbase Mobile is the Sync Gateway, which acts as the middleman between Couchbase Lite on devices and the Couchbase database on the server.  

The Sync Gateway has a straightforward REST API, which includes a variety of mechanisms for subscribing to change notifications.  One way to receive these notifications is over websockets, but my attempts to get this working haven't succeeded in the past.  Since I've started to learn and work with Go, I was able to look at the Sync Gateway's source code and finally figure it out.  They key is to send the query parameters as a JSON object once you connect to the socket.  

Here is a skeleton example using NodeJS: 


```
var WebSocket = require('ws');
var ws = new WebSocket('ws://<server-address>:4984/db/_changes?feed=websocket');

var wsOptions = {
  include_docs : true,
  channels : "test",
  filter: "sync_gateway/bychannel",
};

ws.on("open", function() {
  ws.send(JSON.stringify(wsOptions));
});

ws.on("message", function(message) {
  // now process the change data here...
});
```
