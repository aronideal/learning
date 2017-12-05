
## Create PKCS#12 format File

1. Create key pair :  openssl genrsa -out aps_development.key 2048

2. Create CSR : openssl req -new -sha256 -key aps_development.key -out aps_development.csr

3. Upload the CSR to developer portal to get the certificate aps_development.cer

4. Convert the certificate: openssl x509 -inform DER -outform PEM -in aps_development.cer -out aps_development.pem

5. Build the PKCS#12: openssl pkcs12 -inkey aps_development.key -in aps_development.pem -export -out aps_development.p12
