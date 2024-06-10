To generate certificates for Docker with `DOCKER_TLS_CERTDIR=/certs`, you can use the `openssl` command to create a certificate authority (CA) and server/client certificates. Here's a step-by-step guide:

### Step 1: Create a Certificate Authority (CA)

1. **Generate the CA private key:**

   ```bash
   openssl genpkey -algorithm RSA -out ca-key.pem -pkeyopt rsa_keygen_bits:4096
   ```

2. **Create the CA certificate:**

   ```bash
   openssl req -x509 -new -nodes -key ca-key.pem -days 365 -out ca.pem -subj "/CN=ca"
   ```

### Step 2: Create the Server Certificate

1. **Generate the server private key:**

   ```bash
   openssl genpkey -algorithm RSA -out server-key.pem -pkeyopt rsa_keygen_bits:4096
   ```

2. **Create the server certificate signing request (CSR):**

   ```bash
   openssl req -new -key server-key.pem -out server.csr -subj "/CN=server"
   ```

3. **Sign the server certificate with the CA:**

   ```bash
   openssl x509 -req -in server.csr -CA ca.pem -CAkey ca-key.pem -CAcreateserial -out server-cert.pem -days 365
   ```

### Step 3: Create the Client Certificate

1. **Generate the client private key:**

   ```bash
   openssl genpkey -algorithm RSA -out key.pem -pkeyopt rsa_keygen_bits:4096
   ```

2. **Create the client certificate signing request (CSR):**

   ```bash
   openssl req -new -key key.pem -out client.csr -subj "/CN=client"
   ```

3. **Sign the client certificate with the CA:**

   ```bash
   openssl x509 -req -in client.csr -CA ca.pem -CAkey ca-key.pem -CAcreateserial -out cert.pem -days 365
   ```

### Step 4: Organize the Certificates

1. **Create the `/certs` directory:**

   ```bash
   mkdir -p /certs/client /certs/server
   ```

2. **Move the certificates to the appropriate directories:**

   ```bash
   mv ca.pem ./certs/ca.pem
   mv server-cert.pem ./certs/server/cert.pem
   mv server-key.pem ./certs/server/key.pem
   mv cert.pem ./certs/client/cert.pem
   mv key.pem ./certs/client/key.pem
   ```

### Step 5: Configure Docker to Use the Certificates

Set the environment variable `DOCKER_TLS_CERTDIR`:

```bash
export DOCKER_TLS_CERTDIR=/certs
```

Start the Docker daemon with TLS enabled:

```bash
dockerd --tlsverify --tlscacert=/certs/ca.pem --tlscert=/certs/server/cert.pem --tlskey=/certs/server/key.pem
```

### Step 6: Configure the Docker Client

Set the environment variables for the Docker client to use the TLS certificates:

```bash
export DOCKER_CERT_PATH=/certs/client
export DOCKER_TLS_VERIFY=1
```

Now you can connect to the Docker daemon securely using the generated TLS certificates.

This setup ensures secure communication between the Docker client and daemon using TLS certificates stored in the `/certs` directory.