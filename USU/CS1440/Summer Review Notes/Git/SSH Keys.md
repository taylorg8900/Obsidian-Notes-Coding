# Creating SSH Key
`ssh-keygen -t rsa -b 2048`
- `-t rsa` means to create a key with the RSA encryption algorithm
- `-b 2048` means a 2048 bit random number

# Checking SSH Key
Default location is in `~/.ssh`
- Check if there are existing SSH keys with `ls -al ~/.ssh`
- Private SSH key in `id_rsa`
- Public SSH key in `id_rsa.pub`