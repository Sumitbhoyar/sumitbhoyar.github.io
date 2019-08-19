# BASE 64 Encoding
When you have some binary data that you want to ship across a network, you generally don't do it by just streaming the bits and bytes over the wire in a raw format. Why? because some media are made for streaming text. You never know -- some protocols may interpret your binary data as control characters (like a modem), or your binary data could be screwed up because the underlying protocol might think that you've entered a special character combination (like how FTP translates line endings).

So to get around this, people encode the binary data into characters. Base64 is one of these types of encodings.

Why 64?
Because you can generally rely on the same 64 characters being present in many character sets, and you can be reasonably confident that your data's going to end up on the other side of the wire uncorrupted.

Common use uses 
##### Hashes:

Hashes are one-way functions that transform a block of bytes into another block of bytes of a fixed size such as 128bit or 256bit (SHA/MD5). Converting the resulting bytes into Base64 makes it much easier to display the hash especially when you are comparing a checksum for integrity. Hashes are so often seen in Base64 that many people mistake Base64 itself as a hash.

##### Cryptography:

Since an encryption key does not have to be text but raw bytes it is sometimes necessary to store it in a file or database, which Base64 comes in handy for. Same with the resulting encrypted bytes.

Note that although Base64 is often used in cryptography is not a security mechanism. Anyone can convert the Base64 string back to its original bytes, so it should not be used as a means for protecting data, only as a format to display or store raw bytes more easily.

###### Certificates:

x509 certificates in PEM format are base 64 encoded. 