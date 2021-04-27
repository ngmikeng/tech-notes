
## Use case
- Use RSA to encrypt the payload data which send by a app client.
- Use openssl to generate the pair key (public key & private key)
- The app client will use the public key for encrypting the payload data before send it to the server.
- The backend server will use the private key for decrypting the payload data
- After decrypt, the backend will use the decrypted payload data for handling the logic.

## Dependence
- node@12.13.0
- node-rsa@1.1.1

## Implement
Generate private key & public key with type cipher PKCS1
```shell
# Generate rsa private key with type cipher PKCS1
openssl genrsa -out rsa-private.pem 2048
# Generate rsa public key from rsa private key
openssl rsa -in rsa-private.pem -out rsa-public.pem -RSAPublicKey_out
```

Convert keys to type cipher PKCS8
```shell
# Convert rsa private key to type cipher PKCS8
openssl pkcs8 -in rsa-private.pem -topk8 -out rsa-private-p8.pem -nocrypt
# Generate rsa public key from rsa private key type cipher PKCS8
openssl rsa -in rsa-private-p8.pem -out rsa-public-p8.pem -pubout
```