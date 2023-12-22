# 🔮 Portal.js

![License](https://img.shields.io/github/license/Andrew-Gallimore/Portal.js)
![GitHub Stars](https://img.shields.io/github/stars/Andrew-Gallimore/Portal.js)
![GitHub Issues](https://img.shields.io/github/issues/Andrew-Gallimore/Portal.js)

**A library for creating a *serverless* synced database between pages in the browser.**

Portal.js is a library that allows you to create a peer-to-peer synced database in the browser. It is built on top of [VDO.ninja](https://vdo.ninja) and uses purely peer-to-peer communication through iframes. This means that you don't need any servers or complex setup to use it!

Portal.js is particularly useful for creating real-time, collaborative web applications where data needs to be shared and synchronized between multiple users.

## Features

1. 👥 **Peer-to-peer communication**: Enables direct communication between different users (peers) without the need for a central server.
2. 🔔 **Channels**: Provides a way for peers to join specific channels for communication. A channel can be thought of as a room where peers can exchange messages or data.
3. 🌎 **Real-time updates**: Changes made by one peer can be instantly seen by all other peers in the same channel.

## Basic Usage

You can include the file `Portal.js` in your page, and the main `Portal` object will be imported.

```js
// Opens the channel "test1234" with specific data that should be synced "data_1" and "data_2".
Portal.openChannel("test1234", ["data_1", "data_2"]);

// Listens for changed to "data_1" and "data_2", whether or not we made the change
Portal.on("data_1", function(data){
    console.log("data_1 updated: " + data);
});
Portal.on("data_2", function(data){
    console.log("data_2 updated: " + data);
});

// Creates push request to update the data
// (if it can't sync the change, the listener above won't be called)
Portal.setDB("data_1", "I'm the data");
```

## Channel Structure

A channel is a way to organize and group peers together, allowing them to communicate and sync stored data with each other. However, channels can be used to limit the synced data for certain peers.

Each peer has a stored database, however, in some cases there may be more data stored for some peers than what is shared on a channel. When creating a channel, you need to specify what data should be synced with other peers in that channel. If you limit what should be shared, from any other peers' perspective, there is only that limited set of data in the synced database.

> For example, you can have one 'more secure' channel that has access to all the data, and then have another 'less secure' channel with limited access to *specific* data only.
