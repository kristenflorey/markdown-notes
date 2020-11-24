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

##### Differences between Symmetric and Asymmetric
| The Basis for Comparison              | Symmetric Encryption                                                                                                                       | Asymmetric Encryption                                                                                                                                                                                        |
|---------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| The Number of Cryptographic Keys Used | It requires just one key to help with both encryption (encoding) and decryption (decoding) of confidential data.                           | Requires a pair of matching keys i.e., public and private keys, to help with encryption and decryption purposes.                                                                                             |
| The Primary Purpose                   | Symmetric Encryption is mostly required when dealing with the transmission of bulk data. This is because it’s quicker and easy to execute. | Asymmetric Encryption is a viable option if you only wish to get a secure environment for exchanging your secret keys. This is because of the complexity it has in execution and the slow speed in using it. |
| The Algorithms Used                   | Symmetric encryption uses these algorithms;  AES QUAD RC4 3DES DES                                                                         | Asymmetric encryption uses the following algorithms;  DSA RSA EL GAMAL ECC Diffie Hellman                                                                                                                    |
| Ease of Use                           | Requires just one key hence very easy to use. No matching keys required for decrypting the encrypted data.                                 | It requires both public and private keys, which must match for you to decrypt information. This makes it a bit difficult to use.                                                                             |
| Performance                           | Simple in nature and easy to execute. Very swift.                                                                                          | There must be a pair of matching keys for it to work. Besides, comparing these keys can be a bit time confusing, making it another work on its own.                                                          |

##### Encoding
- If you know the encoding scheme, you are able to manually decipher the encoded data into it's original form.

#### Hashing
- **Hashing** is the practice of using an algorithm to map data of any size to a fixed length. This is called a hash value (or sometimes hash code or hash sums or even a hash digest if you’re feeling fancy).
  - Whereas encryption is a two-way function, hashing is a one-way function. **Hashed values cannot be translated back to their original input values.**
  - Now, whereas encryption is meant to protect data in transit, hashing is meant to verify that a file or piece of data hasn’t been altered—that it is authentic
    - Every hash value is unique. If two different files produce the same unique hash value this is called a collision and it makes the algorithm essentially useless.
- Hashing is a popular way of storing passwords.


#### Salting
<img src="https://www.thesslstore.com/blog/wp-content/uploads/2019/03/salt.png" width="80"/>  

- **Salting** is a concept that typically pertains to password hashing. Essentially, it’s a unique value (`salt`) that can be added to the end of the password to create a different hash value. This adds a layer of security to the hashing process, specifically against brute force attacks.
  - A **brute force attack** is where a computer or botnet attempt every possible combination of letters and numbers until the password is found.

## [Bcrypt](https://www.npmjs.com/package/bcrypt)
- BCrypt is a password hashing function that's widely used to hash user passwords.
- Installing Bcrypt:
```
npm install bcryptjs
```
- Requiring it in your application:
```
const bcrypt = require('bcryptjs');
```
- You can either use BCrypt synchronously or asynchronously.
  - It is recommended to generate hashes asynchronously. As of version 2.4.0, bcryptjs's asynchronous methods return a promise if a callback is omitted.
#### Usage

##### async (recommended)
```
const bcrypt = require('bcrypt');
const saltRounds = 10;
const myPlaintextPassword = 's0/\/\P4$$w0rD';
const someOtherPlaintextPassword = 'not_bacon';
```
##### To hash a password:
- Technique 1 (generate a salt and hash on separate function calls):
  ```
  bcrypt.genSalt(saltRounds, function(err, salt) {
      bcrypt.hash(myPlaintextPassword, salt, function(err, hash) {
          // Store hash in your password DB.
      });
  });
  ```
- Technique 2 (auto-gen a salt and hash):
  ```
  bcrypt.hash(myPlaintextPassword, saltRounds, function(err, hash) {
      // Store hash in your password DB.
  });
  ```
Note that both techniques achieve the same end-result.

##### To check a password:
```
// Load hash from your password DB.
bcrypt.compare(myPlaintextPassword, hash, function(err, result) {
    // result == true
});
bcrypt.compare(someOtherPlaintextPassword, hash, function(err, result) {
    // result == false
});
```
##### `compareSync()`
```
bcrypt.compareSync("B4c0/\/", hash); // true
bcrypt.compareSync("not_bacon", hash); // false
```
#### Promises
- Bcrypt uses whatever Promise implementation is available in `global.Promise`
- Async methods that accept a callback, return a `Promise` when callback is not specified if Promise support is available.
```
bcrypt.hash(myPlaintextPassword, saltRounds).then(function(hash) {
    // Store hash in your password DB.
});
// Load hash from your password DB.
bcrypt.compare(myPlaintextPassword, hash).then(function(result) {
    // result == true
});
bcrypt.compare(someOtherPlaintextPassword, hash).then(function(result) {
    // result == false
});
```
##### with `async/await`
```
async function checkUser(username, password) {
    //... fetch user from a db etc.

    const match = await bcrypt.compare(password, user.passwordHash);

    if(match) {
        //login
    }

    //...
}
```

#### API

- `genSaltSync(rounds, minor)`
  - `rounds` - [OPTIONAL] - the cost of processing the data. (default - 10)
  - `minor - [OPTIONAL] - minor version of bcrypt to use. (default - b)
- `genSalt(rounds, minor, cb)`
  - `rounds` - [OPTIONAL] - the cost of processing the data. (default - 10)
  - `minor` - [OPTIONAL] - minor version of bcrypt to use. (default - b)
  - `cb` - [OPTIONAL] - a callback to be fired once the salt has been generated. uses eio making it asynchronous. If `cb` is not specified, a `Promise` is returned if `Promise` support is available.
    - `err` - First parameter to the callback detailing any errors.
    - `salt` - Second parameter to the callback providing the generated salt.
- `hashSync(data, salt)`
  - `data` - [REQUIRED] - the data to be encrypted.
  - `salt` - [REQUIRED] - the salt to be used to hash the password. if specified as a number then a salt will be generated with the specified number of rounds and used (see example under Usage).
- `hash(data, salt, cb)`
  - `data` - [REQUIRED] - the data to be encrypted.
  - `salt` - [REQUIRED] - the salt to be used to hash the password. if specified as a number then a salt will be generated with the specified number of rounds and used (see example under Usage).
  - `cb` - [OPTIONAL] - a callback to be fired once the data has been encrypted. uses eio making it asynchronous. If `cb` is not specified, a `Promise` is returned if `Promise` support is available.
    - `err` - First parameter to the callback detailing any errors.
    - `encrypted` - Second parameter to the callback providing the encrypted form.
- `compareSync(data, encrypted)`
  - `data` - [REQUIRED] - data to compare.
  - `encrypted` - [REQUIRED] - data to be compared to.
- `compare(data, encrypted, cb)`
  - `data` - [REQUIRED] - data to compare.
  - `encrypted` - [REQUIRED] - data to be compared to.
  - `cb` - [OPTIONAL] - a callback to be fired once the data has been compared. uses eio making it asynchronous. If `cb` is not specified, a `Promise` is returned if `Promise` support is available.
    - `err` - First parameter to the callback detailing any errors.
    - `same` - Second parameter to the callback providing whether the data and encrypted forms match [true | false].
`getRounds(encrypted)` - return the number of rounds used to encrypt a given hash
  - `encrypted` - [REQUIRED] - hash from which the number of rounds used should be extracted.
