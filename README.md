# Forensics
## Observe Closely

A simple image with a couple of twists...

Running binwalk on the given picture reveals a zip file inside. We can extract it with dd and unzip it, which gives us a hidden binary that gives the flag when run.

## [basics] forensics

My friend said they hid a flag in this picture, but it's broken! Now that I think about it, I don't even know if it really is a picture...

The given file with a jpeg extensions appreas to actually be a text file, and we can use strings and grep to find the flag.

## 1 Frame per Minute

I recently received this signal transmission known as SSTV in a mode called Martian? This technology is all very old so I'm not sure what to do with it. Could you help me out?

As, the problem suggests, this is an SSTV signal. We can play the given wav file and use QSSTV to convert the audio into a picture which contains the flag.

## The Legend of Hackerman, Pt. 1

My friend Hackerman tried to send me a secret transmission, but I think some of it got messed up in transit. Can you fix it?

We are given a file with a png extension, but it won't open. Viewing it in a hex editor reveals that part of the file signature is correct, but part of it has been changed. Fixing the file signature allows the picture to open properly, and it shows the flag.

# Cryptography
## One True Problem

Two of my friends were arguing about which CTF category is the best, but they encrypted it because they didn't want anyone to see. Lucky for us, they reused the same key; can you recover it?

Here are the ciphertexts:

213c234c2322282057730b32492e720b35732b2124553d354c22352224237f1826283d7b0651

3b3b463829225b3632630b542623767f39674431343b353435412223243b7f162028397a103e

The title suggests that the ciphertexts were encyrpted with a one time pad. We can use a crib dragging attack to find the common pad, which consists of the flag.

## Hill

I found these characters on top of a hill covered with algae ... bruh I can't figure it out can you help me?

wznqca{d4uqop0fk_q1nwofDbzg_eu}

This is encrypted using a hill cipher. Some trial and error reveals that the decryption matrix is 2x2, and we can calculate the entries using 4 linear congruences, created from the ciphertext and knowing the flag starts with "utflag". This reveals the decryption matrix to be [[13,6],[3,21]], and we can use this to decrypt the rest.

## Galois

nc crypto.utctf.live 9004

Examining the given code reveals that the ciphertext given is encrypted with the same key and iv as any text we enter, using AES GCM mode. By entering some text and xoring with the resulting ciphertext, we can reveal the keystream and xor this with the flag ciphertext to find the flag.

## Cube Crypto

Mr. Anshel and Mr. Goldfeld were trying to exchange some asymmetric keys to get a shared key. They aren't very good at math, so they decided to use a Rubik's Cube instead to do the crypto. I don't think it's very secure though, I think you might be able to guess some of their keys :hmm:

Mr. A public key: [B' U', F B F, R' D, B D']
Mr. G public key: [R D L', D U' B, U F', L' F]

Mr. A sends: [B D' R' D R D L' D' R D B', B D' R' D D U' B D' R D B', B D' R' D U F' D' R D B', B D' R' D L' F D' R D B']
Mr. G sends: [U F' R D L' B' U' L D' R' F U', U F' R D L' F B F L D' R' F U', U F' R D L' R' D L D' R' F U', U F' R D L' B D' L D' R' F U']

Let's denote the public keys as [a1,a2,a3,a4] and [g1,g2,g3,g4]. Examining the messages shows us that they are of the form [a4a3g1a3'a4',a4a3g2a3'a4', ...] and [g3g1a1g1'g3',g3g1a2g1'g3', ...]. Using the Anshel-Anshel-Goldfeld key exchange protocol as suggested, the shared secret will be a4a3g3g1a3'a4'g1'g3'.
