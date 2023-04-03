## Purpose
This page was created to demonstrate the usage and benefits of encryption, along with the differences between symmetric and assymetric encryption.

## Symmetric Encryption
### Definition
**In short:** Uses the __same key__ to encrypt and decrypt. 
Examples of Symmetric encryption are DES (Broken) and AES. These algorithms tend to be faster than asymmetric cryptography, and use smaller keys (128 or 256 bit keys are common for AES, DES keys are 56 bits long).
### Examples
In this example, we will encrypt a text file containing sensitive information, using the aes256 algorithm. 
Let's first create the file:
```shell
echo "This is a super dupper secret file! " > secret-plain.txt
cat secret-plain.txt
```
Now let's encrypt it using the gpg tool. Enter the desired password/passphrase when prompted.
```shell
gpg -c -o secret-encrypted.txt --cipher-algo aes256 secret-plain.txt
```
This should have created a new file secret-encrypted.txt
```shell
file secret-encrypted.txt
cat secret-encrypted.txt
```
