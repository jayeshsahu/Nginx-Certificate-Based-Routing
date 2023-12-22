# Nginx-Certificate-Based-Routing
Certificate based routing with nginx

Key concepts: mutual Transport Layer Security (mTLS), Nginx, locks, X509 Certificate, Public Private Key, SHA1, Security.

This project is a proof of concept (POC) and needs additional improvements to be prepared for production. Feel free to provide any suggestions or criticisms. Please submit an issue to propose enhancements or engage in a discussion regarding any inconsistencies you have identified, and I will gladly provide a response.


Key Tasks:
=> Create Server certificates and keys
=> Create CA.crt file ( Trusted certificate file) 
=> Create CA authority certificate and keys (option)
=> Configure nginx map
=> Configure nginx upstream



Creating CA Authority
CA authority is required if you want to sign the certificate with your own self-signed root certificate.

#Create private key for CA
openssl genrsa -des3 -out ca.key 4096

#Create self signed certificate
openssl req -new -x509 -days 1365 -key ca.key -out ca.crt

#create private key for client
openssl genrsa -des3  -out server1.key 4096

#create CSR for client
openssl req -new -key server1.key -out server1.csr 

#Sign CSR with root CA certificate
openssl x509 -req -days 1365 -in server1.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out server1.crt

Sample CA certificates are added here so that we can use publicly signed certificates as trusted certificates.
We can also download the mozilla root CAs from : https://wiki.mozilla.org/CA/Included_Certificates




