## Purpose
This page was created to demonstrate the usage and benefits of encryption, along with the differences between symmetric and assymetric encryption.

## Symmetric Encryption
### Definition
**In short:** Uses the __same key__ to encrypt and decrypt. 
Examples of Symmetric encryption are DES (Broken) and AES. These algorithms tend to be __faster than asymmetric cryptography__, and use smaller keys (128 or 256 bit keys are common for AES, DES keys are 56 bits long).
### Examples
In this example, imagine you want to send a secret file to somebody else, and chose to use symmetric encryption. We will encrypt a text file containing sensitive information, using the `aes256` algorithm. Once encrypted, we would send the file to the recipient, and share the key (password/passphrase) with them.  
Let's first create the file:
```shell
echo "This is a super dupper secret file! " > secret-plain.txt
cat secret-plain.txt
```
Now let's encrypt it using the `gpg` tool. Enter the desired password/passphrase when prompted.
```shell
gpg -c -o secret-encrypted.txt --cipher-algo aes256 secret-plain.txt
```
This should have created a new file `secret-encrypted.txt`
```shell
file secret-encrypted.txt
cat secret-encrypted.txt
```
Now, once you have sent the file and shared the password/passphrase you used to encrypt it, the recipient should be able to decrypt the file using:
```shell
gpg --decrypt secret-encrypted.txt
```
They would have to enter the correct password/passphrase when prompted.
### Problematic
As you may have noticed, this is nice and cool, but now the problem is the following: how do you securely share the secret key (password/passphrase) required to decrypt the file? Should someone be able to interect the key exchange, they would be able to decrypt any file that used the same passphrase during the encryption process.

This is where assymetric encryption comes in handy, and probably more suited for such use cases.
## Assymetric Encryption
### Definition
**In short:** Uses __a pair of keys__, one to encrypt and the other in the pair to decrypt. Examples are RSA and Elliptic Curve Cryptography. Normally these keys are __referred to as a public key and a private key__. Data encrypted with the private key can be decrypted with the public key, and vice versa. Your private key needs to be kept private, hence the name. Asymmetric encryption tends to be __slower and uses larger keys__, for example RSA typically uses 2048 to 4096 bit keys.
### Examples
In this example, imagine Antoine wants to send a secret file to Maxime, and chose to use asymmetric encryption to avoid potential issues while sending a key. Antoine will encrypt a text file containing sensitive information, using `openssl`. Note we could also use `gpg` to create a key pair, but chose to use `openssl` instead, so we learn to use another tool.
Let's first create the file:
```shell
echo "This is another super dupper secret file! " > top_secret.txt
cat top_secret.txt
```
Now let's encrypt it using the `openssl` tool. First both Antoine and Maxime need to generate their respective key pairs:
```shell
# Generate the private key using RSA with a size of 2048 bits
openssl genrsa -aes128 -out antoine_private.pem 2048
# Check the type of file we have created
file antoine_private.pem
# Check how the content looks like
head antoine_private.pem
# Now extract the public key we would like to share, from the private key
openssl rsa -in antoine_private.pem -pubout > antoine_public.pem
```
Of course, Maxime would follow the same steps as outlined above, creating his own key pair. Both would keep their private key secret and won't share it with anybody. Then, they would exchange their public keys, using the medium of their chosing (email for example).

Now, to encrypt his secret message, Antoine needs to use the `openssl -encrypt` command as follow:
```shell
openssl rsautl -encrypt -inkey maxime_public.pem -pubin -in top_secret.txt -out top_secret.enc
# Check the type of file we have created
file top_secret.enc 
# Try to display its content
cat top_secret.enc
```
Then, Antoine transmits the encrypted file to Maxime, who would then decrypt it using his own private key:
```shell
openssl rsautl -decrypt -inkey maxime_private.pem -in top_secret.enc > top_secret.txt
cat top_secret.txt
```
### Extra mile
If Maxime wants to reply to Antoine, how would he do it?
## Conclusion
Try to answer those 2 questions to make sure you understood the differences between the encyption types:
- When is it best to use symmetric encryption?
- When is it best to use assymetric encryption?
