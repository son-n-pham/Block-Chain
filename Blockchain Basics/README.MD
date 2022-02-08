```javascript
geth --networkid "12345" console // Select a local network id


// Create 2 account and 2 nodes Node_1 and Node_2
geth account new --datadir ./Node_1
{"address":"2275582859651c141e2bda868cd2681e08a96ab6","crypto":{"cipher":"aes-128-ctr","ciphertext":"eba7441d8fbbeaf65e9977be26d44e66de27046ddab4a4762b8ef15813b13774","cipherparams":{"iv":"bfa84889b6a7f103ac81665b793e6199"},"kdf":"scrypt","kdfparams":{"dklen":32,"n":262144,"p":1,"r":8,"salt":"202feafdfffd64999a3ae9f3b8479eeb34342f0f2da1ef382eab2e37eafd30a8"},"mac":"80ee36e056f75b52e66a1ae417f0df52b0105172317365f0d517bd6d95a260ed"},"id":"28a96aab-8bec-4a79-814f-acd4145601fe","version":3}

geth account new --datadir ./Node_2
{"address":"f264fe6945ded4edd3edc6ece8a9b463d5a6bd4d","crypto":{"cipher":"aes-128-ctr","ciphertext":"24b5648760055c111f1d5ac33c74287878dc8806fda20e1863ace78fe7dccccc","cipherparams":{"iv":"70cf12bc4683f02daf5b3d52d372b231"},"kdf":"scrypt","kdfparams":{"dklen":32,"n":262144,"p":1,"r":8,"salt":"7b12c172d2fc8a105988cdb23eadc982cf8a835b81baa6129a240856631712a2"},"mac":"2ecfb30cc91dbd9320256304599314dbd41a9f9a865a1fa2f8010af1714f0744"},"id":"43a88009-71c0-4c35-872d-527d1ca7017c","version":3}


// genesis.json file. What is the meaning of chainId, can it be any number? What the difference of chainId and networkid
// What is the meaning of all other params
genesis.json
{
  "config": {
    "chainId": 15,
    "homesteadBlock": 0,
    "eip150Block": 0,
    "eip155Block": 0,
    "eip158Block": 0,
    "byzantiumBlock": 0,
    "constantinopleBlock": 0,
    "petersburgBlock": 0,
    "ethash": {}
  },
  "alloc": {},
  "coinbase": "0x0000000000000000000000000000000000000000",
  "difficulty": "0x20000",
  "extraData": "",
  "gasLimit": "0x2fefd8",
  "nonce": "0x0000000000000042",
  "mixhash": "0x0000000000000000000000000000000000000000000000000000000000000000",
  "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
  "timestamp": "0x00"
}


// Initiate Node_1 and Node_2 with genesis.json file. What is the meanings of this compare to the 2nd step.
geth init genesis.json --datadir ./Node_1

geth init genesis.json --datadir ./Node_2



// What is the meaning of this compare to the previous one?
geth --datadir ./Node_1 --networkid 12345 --port 30301 --http --http.port 8554 --http.api "eth,admin,net,personal,miner,txpool" --nodiscover --ipcdisable console

geth --datadir ./Node_2 --networkid 12345 --port 30302 --http --http.port 8555 --http.api "eth,admin,net,personal,miner,txpool" --nodiscover --ipcdisable console


// Have new client console to attach to Node_1. Why we need to do so? Why don't we just run on the console of Node_1
geth attach http://127.0.0.1:8554 --datadir ./Node_1
> admin.nodeinfo
"enode://7f6423c7d0a13bf9a96fb2aeb40769e3ce7f6c2553a2f87c060a760a4e64701c94f53aa21875c46f244ce22f8a0f208d4bcf6ab513c890a77b7fe26a2be746b7@127.0.0.1:30301?discport=0"
> admin.addPeer("enode://cd1d892fb68d9c0178f4aa25eedcd66ec4be8381b69b55c77628fc851cc5b3855d65e29c4bbf4df8872e0f2fa5aeb810cdc62330434650d90353cd80937ce923@127.0.0.1:30302?discport=0")
> admin.peers[0].enode
"enode://cd1d892fb68d9c0178f4aa25eedcd66ec4be8381b69b55c77628fc851cc5b3855d65e29c4bbf4df8872e0f2fa5aeb810cdc62330434650d90353cd80937ce923@127.0.0.1:52088"
> personal.newAccount("b") // Make new account with the password of "b"
"0x7a922484c9eb59f8c91b66c375953323691f0c3c"
> personal.newAccount("b")
"0xca64818a76028a05e67aa8006cb0049d17595bbc"
> eth.accounts
["0x2275582859651c141e2bda868cd2681e08a96ab6", "0x7a922484c9eb59f8c91b66c375953323691f0c3c", "0xca64818a76028a05e67aa8006cb0049d17595bbc"]
> miner.start() // I have 3 accounts, which account is mining. What is it actually doing? eth.getBalance is always 0


// Have new client console to attach to Node_2
geth attach http://127.0.0.1:8555 --datadir ./Node_2
> admin.nodeinfo
"enode://cd1d892fb68d9c0178f4aa25eedcd66ec4be8381b69b55c77628fc851cc5b3855d65e29c4bbf4df8872e0f2fa5aeb810cdc62330434650d90353cd80937ce923@127.0.0.1:30302?discport=0"
> admin.addPeer("enode://7f6423c7d0a13bf9a96fb2aeb40769e3ce7f6c2553a2f87c060a760a4e64701c94f53aa21875c46f244ce22f8a0f208d4bcf6ab513c890a77b7fe26a2be746b7@127.0.0.1:30301?discport=0")
> admin.peers[0].enode
"enode://7f6423c7d0a13bf9a96fb2aeb40769e3ce7f6c2553a2f87c060a760a4e64701c94f53aa21875c46f244ce22f8a0f208d4bcf6ab513c890a77b7fe26a2be746b7@127.0.0.1:30301?discport=0"
> personal.newAccount("b") // Make new account with the password of "b"
"0x4ad87e7932b4c92ebf45568c7a6fe2a9af0cbb44"
> personal.newAccount("b")
"0xc4596cb4cfa9eceb5ffc97fcca0df81bb12d4b35"
> eth.accounts
["0xf264fe6945ded4edd3edc6ece8a9b463d5a6bd4d", "0x4ad87e7932b4c92ebf45568c7a6fe2a9af0cbb44", "0xc4596cb4cfa9eceb5ffc97fcca0df81bb12d4b35"]
```
