layout: post
title:  "How to connect to the Couchbase Sync Gateway over Websockets"
date:  
categories: couchbase sync-gateway websocket programming
---

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
