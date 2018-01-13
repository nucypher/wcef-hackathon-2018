# wcef-hackathon-2018
Guidelines for hackathon at WCEF 2018

# Background info about NuCypher

NuCypher is a key management system which leverages proxy re-encryption to control access over encrypted data.
You can find the white paper [here](https://cdn2.hubspot.net/hubfs/2807639/NuCypher%20KMS%20Technical%20White%20Paper.pdf?t=1510526466105) (although you don't have to read it all!).
If you have any questions, you can ask in person at the hackathon, or go to our [developer slack channel](https://nucypher-kms-slack.herokuapp.com/).

# Possible taks for the hackathon

## Implementing proxy re-encryption library in languages other than Python or Javascript

We use a split-key proxy re-encryption scheme. The reference implementation in its most readable, self-explaining form can be found [here](https://github.com/nucypher/nucypher-pre-python/blob/master/npre/umbral.py). In brief, encryption and decryption is just [ECIES](https://en.wikipedia.org/wiki/Integrated_Encryption_Scheme), but the ciphertext (or, to be more correct, the ephemeral public key) can be transformed so that the data can be shared with more than one recepient through re-encryption.

Please check the [tutorial](https://blog.nucypher.com/proxy-re-encryption-playground-in-python-3bc66170b9bf) in order to set up the environment and play with re-encryption.

We need client libraries for the following languages: Go, Rust, C. If you wish to play with low-level cryptography in any of these languages (or even different ones if you like) - feel free to hack on this task.

## UI for mining node management console

Our mining nodes will be the workhorses of the network.
They stake the token and, instead of confirming transactions, they re-encrypt ciphertexts.
Mining works in the follwing manner:

* Miner deposits the token (should be no less than minimum amount);
* Miner locks the tokens for a specified time T (T >= 1 month);
* Mining is happening, and the miner re-encrypts during this time;
* Miner can chose to either reinvest block rewards back into mining; or to take profits; or to start gradual spindown of the node in the time T.

We also would need to have a visual graph so that the miner can compare how many tokens he gets over time if choosing different options.

The UI should be a web UI.
Can be built using any web tool (Python frameworks, nodejs frameworks, or whatever you love).

## UI for granting permissions

The purpose of NuCypher is key management / access management as a service.
It can grant permissions to different people (which means, different public keys + ethereum addresses) indefinitely, for a specified timeframe, or with an on-pay condition.
The permissions need be able to be revoked at any time.
This can be a web UI or a cross-platform desktop app.
Use your favourite web framework, Qt, Electron, or anything you think is appropriate.


## Public keys/certificates for TLS tied to Ethereum address

Our nodes have to establish TLS connections.
But instead of using DNS, we want to tie the certificates to the Ethereum addresses.
The idea is that the certificate (or its hash) is signed and stored on Ethereum blockchain, and for the sake of TLS it's self-signed.
When the connection is being established, the client will read the Ethereum address info (stored in cert metadata?), check if this certificate is signed by the owner of that address, and if it is the case, the connection is established, or otherwise failed.

The code needs to be written in Python.
