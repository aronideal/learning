
## Create format PKCS#12 file

#### 1. Create key pair

    openssl genrsa -out mycert.key 2048

#### 2. Create CSR

    openssl req -new -sha256 -key mycert.key -out mycert.csr

    note: 打开编辑器打开mycert.csr。首尾的分隔符除外，中间的BASE64数据可当成P10数据使用

#### 3. Create X509 cer

    ...ellipsis

#### 4. Convert the certificate

    openssl x509 -inform DER -outform PEM -in mycert.cer -out mycert.pem

#### 5. Build the PKCS#12

    openssl pkcs12 -inkey mycert.key -in mycert.pem -export -out mycert.p12
