---
title: "Encrypting and decrypting data using OpenSSL"
categories: ["openssl", "encryption", "devops"]
---

Note: You will be prompted for a password when encrypting or decrypt.

## Encrypting data

openssl enc -aes-256-cbc -in un_encrypted.data -out encrypted.data

## Decrypting data

openssl enc -d -aes-256-cbc -in encrypted.data -out un_encrypted.data

Sources: 
 * <https://stackoverflow.com/questions/16056135/how-to-use-openssl-to-encrypt-decrypt-files>