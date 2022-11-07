# CFSSL mTLS certificate generation demo

## About

TODO

## Steps

### Generate CA certificate

```
cfssl genkey -initca ca-csr.json | cfssljson -bare ca
```

### Generate DB server certificate (signed by CA)

```
cfssl gencert -ca ca.pem -ca-key ca-key.pem mariadb-csr.json | cfssljson -bare mariadb
```

NOTE: Should work for other types of servers, not just the DB server

### Generate client certificate (signed by CA)

```
cfssl gencert -ca ca.pem -ca-key ca-key.pem app-client-csr.json | cfssljson -bare app-client
```

### Verify certificates using OpenSSL

```
openssl verify -CAfile ca.pem -show_chain mariadb.pem keycloak-client.pem
```

