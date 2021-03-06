Encryption Algorithms : Symmetric, Public-key, Hybrid-key
----------------------------------------------------------


**Cryptography Algorithms:**

A mathematical procedure for performing encryption on data. Through the use of an algorithm, information is made into meaningless cipher text and requires the use of a key to transform the data back into its original form. Blowfish, AES RC4, RC5, and RC6 are examples of encryption algorithms.

- **Symmetric-key algorithms: **
An encryption system in which the sender and receiver of a message share a single, common key that is used to encrypt and decrypt the message.

> Symmetric-key cryptography is sometimes called secret-key cryptography. The most popular symmetric-key system is the Data Encryption Standard (DES).

- **Public-key encryption**
Public-key encryption is a cryptographic system that uses two keys -- a public key known to everyone and a private or secret key known only to the recipient of the message.

> Example: When John wants to send a secure message to Jane, he uses Jane's public key to encrypt the message. Jane then uses her private key to decrypt it.

> An important element to the public key system is that the public and private keys are related in such a way that only the public key can be used to encrypt messages and only the corresponding private key can be used to decrypt them. Moreover, it is virtually impossible to deduce the private key if you know the public key.

> For example, if Bob wants to send sensitive data to Alice, and wants to be sure that only Alice may be able to read it, he will encrypt the data with Alice's Public Key. Only Alice has access to her corresponding Private Key and as a result is the only person with the capability of decrypting the encrypted data back into its original form.

> As only Alice has access to her Private Key, it is possible that only Alice can decrypt the encrypted data. Even if someone else gains access to the encrypted data, it will remain confidential as they should not have access to Alice's Private Key.

> Two of the best-known uses of public key cryptography are:

> **Public key encryption**, in which a message is encrypted with a recipient's public key. The message cannot be decrypted by anyone who does not possess the matching private key, who is thus presumed to be the owner of that key and the person associated with the public key. This is used in an attempt to ensure confidentiality.

> **Digital signatures**, in which a message is signed with the sender's private key and can be verified by anyone who has access to the sender's public key. This verification proves that the sender had access to the private key, and therefore is likely to be the person associated with the public key. This also ensures that the message has not been tampered with, as a signature is mathematically bound to the message it originally was made with, and verification will fail for practically any other message, no matter how similar to the original message.

> An analogy to public key encryption is that of a locked mail box with a mail slot. The mail slot is exposed and accessible to the public – its location (the street address) is, in essence, the public key. Anyone knowing the street address can go to the door and drop a written message through the slot. However, only the person who possesses the key can open the mailbox and read the message.

> An analogy for digital signatures is the sealing of an envelope with a personal wax seal. The message can be opened by anyone, but the presence of the unique seal authenticates the sender.

> A central problem with the use of public key cryptography is confidence/proof that a particular public key is authentic, in that it is correct and belongs to the person or entity claimed, and has not been tampered with or replaced by a malicious third party. The usual approach to this problem is to use a public key infrastructure (PKI), in which one or more third parties – known as certificate authorities – certify ownership of key pairs. PGP, in addition to being a certificate authority structure, has used a scheme generally called the "web of trust", which decentralizes such authentication of public keys by a central mechanism, and substitutes individual endorsements of the link between user and public key. 

- **Hybrid-key Encryption**
A hybrid encryption scheme is one that blends the convenience of an asymmetric encryption scheme with the effectiveness of a symmetric encryption scheme.

> Hybrid encryption is achieved through data transfer using unique session keys along with symmetrical encryption. Public key encryption is implemented for random symmetric key encryption. The recipient then uses the public key encryption method to decrypt the symmetric key. Once the symmetric key is recovered, it is then used to decrypt the message.

** Example: SSL / TLS **

- Sumit types facebook.com

- facebook.com sends 30x series redirect code and provides new Location:https://www.facebook.com/

- Browser redirects to https://www.facebook.com/

- Server sends the certificate and public key

- Browser creates its own symmetric key. Then encrypts it with public key from facebook. Send it to facebook.

- Facebook take this encrypted assymetric key and decrypt it using its own private key.

- Now facebook and server, both has symmetric key.

- Client gets the certificate and checks with certification authority. If CA verifies it, then browser marks or glows the url in broser, otherwise marks as crossed https.

**Terminologies**

- **Encoding** is for maintaining data usability and can be reversed by employing the same algorithm that encoded the content, i.e. no key is used.

- **Encryption** is for maintaining data confidentiality and requires the use of a key (kept secret) in order to return to plaintext.

- **Hashing** is for validating the integrity of content using  private key by detecting all modification thereof via obvious changes to the hash output.

- **Obfuscation** is used to prevent people from understanding the meaning of something, and is often used with computer code to help prevent successful reverse engineering and/or theft of a product’s functionality.- 

