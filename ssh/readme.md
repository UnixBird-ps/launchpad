
# Some useful commands when using ssh


Generate 4096 bit long RSA private/public keys.

	ssh-keygen -t rsa -b 4096 -C 'label' -f ~/.ssh/output-keyfile


Generate 384 bit long ECDSA private/public keys.

	ssh-keygen -t ecdsa -b 384 -C 'label' -f ~/.ssh/output-keyfile


Remove a host from known_hosts file.

	ssh-keygen -f ~/.ssh/known_hosts -R #.#.#.#


Copy your public keyfile to a remote host to use key based authentication instead of passwords.

	ssh-copy-id -p ssh-port -i ~/.ssh/keyfile.pub user@host
