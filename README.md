# P2Web
Peer 2 Peer webserver

## Library candidates
```
libp2p
peerjs
```

## Sources
```
https://www.npmjs.com/package/peerjs-nodejs
https://www.npmjs.com/package/peerjs
https://anyconnect.com/stun-turn-ice/
https://javascript.plainenglish.io/writing-decentralized-applications-in-javascript-libp2p-basics-4fa46c5dae8a
https://stackoverflow.com/questions/61428318/is-there-any-working-example-that-uses-nodejs-peerjs
https://blog.logrocket.com/getting-started-peerjs/
https://javascript.plainenglish.io/building-a-signaling-server-for-simple-peer-f92d754edc85
https://awabot.com/en/webrtc-telepresence-teleoperation/
https://www.espressif.com/en/news/ESP-RTC
https://webrtchacks.com/sdp-anatomy/
https://github.com/seemk/WebUDP
https://github.com/zcduthie/WebRTC-Example-RTCDataChannel
https://github.com/paullouisageneau/datachannel-wasm
https://github.com/RTradeLtd/libcp2p
https://medium.com/@kanecohen/basics-of-webrtc-peer-connections-c1ed743de2f6
https://dyte.io/blog/understanding-libwebrtc/
https://github.com/newrun/peerapi
https://webrtc.googlesource.com/src/+/refs/heads/main/examples/peerconnection
```
## Turn/Stun server sources
```
https://github.com/paullouisageneau/violet
https://github.com/coturn/coturn
https://github.com/alhasanmridha/stun
```
## Turn/Stun client notes
```
https://github.com/node/turn-client/blob/master/c-stun-client-demo.c
https://gist.github.com/jyaif/e0db3a680443730c05ca36be26f22c93
https://github.com/0xFireWolf/STUNExternalIP
https://github.com/paullouisageneau/libjuice/blob/master/test/connectivity.c
https://fossies.org/linux/liblinphone/src/nat/stun-client.cpp
http://maemo.org/development/documentation/manuals/3-x/howto_use_stun_bora/
https://github.com/jselbie/stunserver
```
## Turn/Stun server notes
```
https://www.metered.ca/tools/openrelay/stun-servers-and-friends
https://github.com/paullouisageneau/libjuice
https://github.com/nodertc/stun
```
## Turn tools
```
https://ourcodeworld.com/articles/read/1526/how-to-test-online-whether-a-stun-turn-server-is-working-properly-or-not
https://icetest.info/?
https://liburtc.org/natprobe/
```
## Search Engines
```
https://github.com/quickwit-oss/tantivy
https://github.com/lnx-search/lnx
https://github.com/quickwit-oss/quickwit
```

## Peer to peer Reference source code
```
https://github.com/jsanahuja/php-peer-server
https://github.com/jsanahuja/peer-client
```

## Server
```javascript
const peerJs = require('peerjs-nodejs');
const peer = peerJs("myPeerId", {
host: '192.168.137.231',
port: 9000,
pingInterval: 5000,
path: '/myapp',
debug: 3, 
iceTransportPolicy: 'relay',
config: {
'iceServers': [
	{ urls: "stun:stun.l.google.com:19302" },
	{
		urls: "turn:34.192.149.24:5678?transport=udp",
		username: "USER", credential: "PASS"
	}
]
}
});

let conn = peer.connect('myPeerJS', {
	reliable: true
});


setTimeout(()=>{
 // NOT JSON
 // conn.serialization='none';
 // conn.send('hello from nodejs!');  

 // JSON WAY
 conn.serialization = 'json';
 conn.send({ value: 'hello from nodejs!' });

}, 3000);

setTimeout(()=>{
  conn.close();
  console.log("CONN CLOSE");
  process.exit();
}, 10000);
```

## Client
```javascript
import { Peer } from "peerjs";
const peer = new Peer("pick-an-id");
const conn = peer.connect("another-peers-id");
conn.on("open", () => {
	conn.send("hi!");
});
peer.on("connection", (conn) => {
	conn.on("data", (data) => {
		// Will print 'hi!'
		console.log(data);
	});
	conn.on("open", () => {
		conn.send("hello!");
	});
});

```
