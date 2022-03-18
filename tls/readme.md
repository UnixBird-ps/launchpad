
# Create self-signed SSL certificate for a server

Generate private key for CA.

	openssl genrsa -aes256 -out ca-key.pem 4096


Generate CA cert.

	openssl req -new -x509 -nodes -sha256 -days 365 -key ca-key.pem -out ca-cert.pem


Generate signing key for server.

	openssl genrsa -out cert-key.pem 4096


Generate server cert request.

	openssl req -new -sha256 -key cert-key.pem -out server-cert.csr


Create extension configuration file.

	cat > extfile.cnf <<< "subjectAltName=DNS:host.example.com[,IP:#.#.#.#]"


Generate server cert.

	openssl x509 -req -sha256 -days 365 -in server-cert.csr -CA ca-cert.pem -CAkey ca-key.pem -CAcreateserial -extfile extfile.cnf -out server-cert.pem


Create chain file by combining server-cert.pem with ca-cert.pem.

	cat server-cert.pem > fullchain.pem
	cat ca-cert.pem >> fullchain.pem


Import CA-cert in Windows with PowerShell.

	Import-Certificate -FilePath .\ca-cert.pem -CertStoreLocation Cert:\LocalMachine\Root


The last step is to import the certificate on the server.


For example, to import CA-cert and chain in Proxmox.
Copy/paste to Datacenter -> pve -> System -> Certificates
