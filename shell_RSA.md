






## ssh-keygen
Requirement: from serverA, login serverB without Password
### Process
### on serverA, generate RSA key pair
To do this, we can use a special utility called ssh-keygen, which is included with the standard OpenSSH suite of tools. By default, this will create a 2048 bit RSA key pair, which is fine for most uses
```
ssh-keygen -t rsa
```
If you had previously generated an SSH key pair, you may see a prompt that looks like this:
```
/home/username/.ssh/id_rsa already exists.
Overwrite (y/n)?
```
If you choose to overwrite the key on disk, you will not be able to authenticate using the previous key anymore. Be very careful when selecting yes, as this is a destructive process that cannot be reversed.
```
Created directory '/home/username/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again: 
```
Next, you will be prompted to enter a passphrase for the key. This is an optional passphrase that can be used to encrypt the private key file on disk.

#### man ssh-keygen
```
SSH-KEYGEN(1)                                                           BSD General Commands Manual                                                          SSH-KEYGEN(1)

NAME
     ssh-keygen — authentication key generation, management and conversion
SYNOPSIS
     ssh-keygen [-q] [-b bits] [-t type] [-N new_passphrase] [-C comment] [-f output_keyfile]
DESCRIPTION
     ssh-keygen generates, manages and converts authentication keys for ssh(1).  ssh-keygen can create RSA keys for use by SSH protocol version 1 and DSA, ECDSA, ED25519
     or RSA keys for use by SSH protocol version 2.  The type of key to be generated is specified with the -t option.  If invoked without any arguments, ssh-keygen will
     generate an RSA key for use in SSH protocol 2 connections.
     
     -b bits
             Specifies the number of bits in the key to create.  For RSA keys, the minimum size is 768 bits and the default is 2048 bits.  Generally, 2048 bits is consid‐
             ered sufficient.
     -t type
             Specifies the type of key to create.
             The possible values are “rsa1” for protocol version 1 and “dsa”, “ecdsa”, “ed25519”, or “rsa” for protocol version 2.     
FILES
     ~/.ssh/id_rsa
             Contains the protocol version 2 DSA, ECDSA, ED25519 or RSA authentication identity of the user.
     ~/.ssh/id_rsa.pub
             Contains the protocol version 2 DSA, ECDSA, ED25519 or RSA public key for authentication.             
```

### copy your public key to serverB
There are 3 ways to copy your public key to serverB.
#### Copying your Public Key Using SSH-Copy-ID
The easiest way to copy your public key to an existing server is to use a utility called ssh-copy-id. Because of its simplicity, this method is recommended if available.

To use the utility, you simply need to specify the remote host that you would like to connect to and the user account that you have password SSH access to. This is the account where your public SSH key will be copied.

The syntax is:
```
ssh-copy-id username@remote_host
```
#### Copying your Public Key Using SSH
If you do not have ssh-copy-id available, but you have password-based SSH access to an account on your server, you can upload your keys using a conventional SSH method
We will use the >> redirect symbol to append the content instead of overwriting it. This will let us add keys without destroying previously added keys.

The full command will look like this:
```
cat ~/.ssh/id_rsa.pub | ssh username@remote_host "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```
#### Copying your Public Key Manually
If you do not have password-based SSH access to your server available, you will have to do the above process manually.

The content of your id_rsa.pub file will have to be added to a file at ~/.ssh/authorized_keys on your remote machine somehow.

To display the content of your id_rsa.pub key, type this into your local computer:
```
cat ~/.ssh/id_rsa.pub
```
You will see the key's content, which may look something like this:
```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCqql6MzstZYh1TmWWv11q5O3pISj2ZFl9HgH1JLknLLx44+tXfJ7mIrKNxOOwxIxvcBF8PXSYvobFYEZjGIVCEAjrUzLiIxbyCoxVyle7Q+bqgZ8SeeM8wzytsY+dVGcBxF6N4JS+zVk5eMcV385gG3Y6ON3EG112n6d+SMXY0OEBIcO6x+PnUSGHrSgpBgX7Ks1r7xqFa7heJLLt2wWwkARptX7udSq05paBhcpB0pHtA1Rfz3K2B+ZVIpSDfki9UVKzT8JUmwW6NNzSgxUfQHGwnW7kj4jp4AT0VZk3ADw497M2G/12N0PPB5CnhHf7ovgy6nL1ikrygTKRFmNZISvAcywB9GVqNAVE+ZHDSCuURNsAInVzgYo9xgJDW8wUw2o8U77+xiFxgI5QSZX3Iq7YLMgeksaO4rBJEa54k8m5wEiEE1nUhLuJ0X/vh2xPff6SQ1BL/zkOhvJCACK6Vb15mDOeCSq54Cr7kvS46itMosi/uS66+PujOO+xt/2FWYepz6ZlN70bRly57Q06J+ZJoc9FfBCbCyYH7U/ASsmY095ywPsBo1XQ9PqhnN1/YOorJ068foQDNVpm146mUpILVxmq41Cj55YKHEazXGsdBIbXWhcrRf4G2fJLRcGUr9q8/lERo9oxRm5JFX6TCmj6kmiFqv+Ow9gI0x8GvaQ== demo@test
```

