THE CERTIFICATES AND PRIVATE KEY ENCLOSED WITHIN THIS ARE INTENDED SOLELY FOR THE PURPOSE OF TESTING AND POC.
USE YOUR OWN KEYS AND CERTIFICATES IN REAL SETUP.

You can also generate keys and certiciates using following commands:

#Generate root private key
openssl genrsa -des3 -out root-enc.key 4096
#(optional) remove password from private key
openssl rsa -in root-enc.key -out root.key

#create root certificate
openssl req -new -x509 -days 1365 -key root.key -out root.crt


#Generate client private key
openssl genrsa -des3  -out client-1_enc.key 4096
#(optional) remove password from private key
openssl rsa -in client-1_enc.key -out client-1.key

#Create CSR for client
openssl req -new -key client-1.key -out client-1.csr

#Sign client certificate
openssl x509 -req -days 1365 -in client-1.csr -CA root.crt -CAkey root.key -CAcreateserial -out client-1.crt
