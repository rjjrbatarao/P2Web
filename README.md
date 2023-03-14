# P2Web
Peer 2 Peer webserver

## test using https://www.npmjs.com/package/peerjs-nodejs
```
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
