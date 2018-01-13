# wcef-hackathon-2018
Guidelines for hackathon at WCEF 2018

# Background info about NuCypher

NuCypher is a key management system which leverages proxy re-encryption to control access over encrypted data.
You can find the white paper [here](https://cdn2.hubspot.net/hubfs/2807639/NuCypher%20KMS%20Technical%20White%20Paper.pdf?t=1510526466105) (although you don't have to read it all!).
If you have any questions, you can ask in person at the hackathon, or go to our [developer slack channel](https://nucypher-kms-slack.herokuapp.com/).

# Possible taks for the hackathon

## Implementing proxy re-encryption library in languages other than Python or Javascript

We use split-key proxy re-encryption scheme. The reference implementation in its most readable, self-explaining form can be found [here](https://github.com/nucypher/nucypher-pre-python/blob/master/npre/umbral.py). In brief, encryption and decryption is just [ECIES](https://en.wikipedia.org/wiki/Integrated_Encryption_Scheme), but the ciphertext (or, to be more correct, the ephemeral public key) can be transformed so that the data can be shared with more than one recepient through re-encryption.

Please checke the [tutorial](https://blog.nucypher.com/proxy-re-encryption-playground-in-python-3bc66170b9bf) in order to set up the environment and play with re-encryption.

We need client libraries for the following languages: Go, Rust, C. If you wish to play with low-level cryptography in any of these languages (or even different ones if you like) - feel free to hack on this task.
