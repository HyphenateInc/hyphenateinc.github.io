---
title: Message roaming
keywords: web
sidebar: web_sidebar
toc: true
permalink: web_message_roaming.html
folder: web
---

You can pull historical messages from the server to the local, so that it can synchronize messages when users switch to different device

## You can call this API to get historical messages


``` javascript
/**
 * Get conversation history messages
 * @param {Object} options
 * @param {String} options.queue   - The user id of the other party (if the user id contains uppercase letters, please change to lowercase letters)/group id/chat room id
 * @param {String} options.count   - Number of items pulled at a time
 * @param {Boolean} options.isGroup - Whether it is a group chat, the default is false
 * @param {String} options.start - (not required) The message ID of the starting position, starting from the latest one by default
 * @param {Function} options.success
 * @param {Funciton} options.fail
 */
var options = {
    queue: "user1", //Pay special attention to the queue attribute value mixed with uppercase and lowercase letters, and pure uppercase letters, which will cause the pull roaming to be an empty array, so pay attention to replace the attribute value to pure lowercase
    isGroup: false,
    count: 10,
    success: function(res){
       console.log(res) //Get historical news of successful pull
    },
    fail: function(){}
}
WebIM.conn.fetchHistoryMessages(options)
```

PS：If need to reset the cursor of the pull history message interface, you can reset it through the "WebIM.conn.mr_cache = \[\]" method.
