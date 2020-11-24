# Authentication
---
## Cryptography
- **Cryptography** is a way to use algorithms and secret keys to keep information secure.  It is comprised of techniques for secure communication for **adversaries**
    - **Adversaries** are third-parties who could possibly fake a user's identity to gain their secret values.

#### Encryption
- Encryption is the practice of scrambling information in a way that only someone with a corresponding key can unscramble and read it.
- Encryption is a two-way function. When you encrypt something, you’re doing so with the intention of decrypting it later.
  - To encrypt data you use something called a cipher (or encryption key), which is an **algorithm** – a series of well-defined steps that can be followed procedurally – to encrypt and decrypt information.

  <img src="https://www.clickssl.net/wp-content/uploads/2019/12/symmetric-encryption-vs-asymmetric-encryption.jpg" width="500" />

  - **Symmetric encryption** uses a private key to encrypt and decrypt an encrypted email.
    - An example of a symmetric encryption technique is the [Caesar Cipher](https://www.geeksforgeeks.org/caesar-cipher-in-cryptography/) algorithm.
  - **Asymmetric encryption** uses two pieces of information called the **public and private keys**.
    - The **public key** is shared with anyone wanting to encrypt a message for the recipient.
    - The **private** key is used to decrypt the message.
      - It's known as asymmetric, because one key does the encrypting and the other key does the decrypting


  [comment]: <> (Symmetric encryption uses a private key to encrypt and decrypt an encrypted email. Asymmetric encryption uses the public key of the recipient to encrypt the message)

##### Encryption between Client and Server
<img src="https://gbnet.in/wp-content/uploads/2020/08/Encryption.png" width="600"/>

<u>Steps of Encryption between Client and Server:</u>
1. The server passes on its public key to encrypt data along with its SSL certificate.
2. The browser client uses the server's public key to encrypt a value and generate a new private key.
3. The client sends the encrypted value and the client's new private key to the server.
4. The browser's private key is used to decrypt messages that have been encrypted with the server's public key.
5. The server sends encrypted data to the client using the client's public key.
6. The browser decrypts the data from the server and renders the decrypted information.


##### Encoding
- If you know the encoding scheme, you are able to manually decipher the encoded data into it's original form.

#### Hashing
- **Hashing** is the practice of using an algorithm to map data of any size to a fixed length. This is called a hash value (or sometimes hash code or hash sums or even a hash digest if you’re feeling fancy).
  - Whereas encryption is a two-way function, hashing is a one-way function. **Hashed values cannot be translated back to their original input values.**
  - Now, whereas encryption is meant to protect data in transit, hashing is meant to verify that a file or piece of data hasn’t been altered—that it is authentic
    - Every hash value is unique. If two different files produce the same unique hash value this is called a collision and it makes the algorithm essentially useless.
- Hashing is a popular way to


#### Salting
<img src="https://www.thesslstore.com/blog/wp-content/uploads/2019/03/salt.png" width="80"/>  

- **Salting** is a concept that typically pertains to password hashing. Essentially, it’s a unique value (`salt`) that can be added to the end of the password to create a different hash value. This adds a layer of security to the hashing process, specifically against brute force attacks.
  - A **brute force attack** is where a computer or botnet attempt every possible combination of letters and numbers until the password is found.
