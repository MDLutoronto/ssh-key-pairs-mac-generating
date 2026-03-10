---
title: "Generating SSH Key Pairs on a Mac"
layout: "home"
staff:
    - name: Kara Handren
      link: https://library.utoronto.ca/staff/kara-handren 
description: "These instructions will help you create SSH key pairs on a Mac computer, for access to the Web of Science PostgreSQL Database."
created_date: 2022-02-07
permalink: "/"  #! Remove this if not the homepage
---

# Generating SSH Key Pairs on a Mac

These instructions will help you create SSH key pairs on a Mac computer, for access to the [Web of Science PostgreSQL Database](https://mdl.library.utoronto.ca/technology/text-data-mining-software/web-science-postgresql-database).

### What are SSH Key Pairs?

SSH uses a pair of public and private keys instead of a password, in order to authenticate and establish an encrypted communication channel between a client and a remote machine over the internet. The private key must be kept secret on your machine, but the public key can may be shared freely. To use SSH key pairs to access the [Web of Science PostgreSQL Database](https://mdl.library.utoronto.ca/technology/text-data-mining-software/web-science-postgresql-database), you'll need to generate a key pair (private and public), and upload the public key to the Compute Canada database.

### Generate an SSH Key Pair

1. Open a new Terminal window
2. Type `ssh-keygen -b 4096 -t rsa`
3. You will be prompted to enter a filename. By default, your keys will be saved as **id_rsa** and **id_rsa.pub**. Simply press *Enter* to confirm the default - there is no need to change this unless you have multiple keys! (Note: if you would like to change the default filename, you'll need to include the complete file path)
4. When prompted, enter a passphrase.
5. This will created a hidden directory called **.ssh** that contains both your public (id_rsa.pub) and private (id_rsa.) key files.

### View your public key

1. In the same Terminal window, type `cat .ssh/id_rsa.pub`. This will print your public key. (Note: if you are not using the default key filename, please substitute your public key name in place of id_rsa.pub).
2. Copy this complete key, starting with **ssh** and ending with a username such as **[user@Admins-MacBook-Pro.local](mailto:user@Admins-MacBook-Pro.local)**
3. Paste this public key into the *SSH Key* field on the [CCDB website](https://ccdb.computecanada.ca/ssh_authorized_keys). Click *Add Key.* (Note: it could take up to 30 minutes for you key to be registered on the Cluster).

### Log in via SSH

1. To login to the remote host, open a new Terminal window and use this command: `ssh <computercanadausername>@niagara.scinet.utoronto.ca`. (Note: if you are not using the default key filename, you will need to specify the file path and name, for example: `ssh -i .ssh/myprivatekeyname <computercanadausername>@niagara.scinet.utoronto.ca).`The system will prompt you to enter the passphrase for your key. See instructions below if you would like to bypass having to enter your password each time you connect to the environment.
	* When connecting for the first time, you may see a warning that the authenticity of the host cannot be established. Enter "yes" to continue. This is a security feature that you should only see the first time you connect (the host is "known" moving forward).

### Bypassing the Passphrase

1. If you do not want to have to enter this passphrase every time you log in to the environment, this can be bypassed using the ssh-agent program. This is a key manager, which means that it will store your private key in memory on your local computer and provides it whenever another program on your computer requests it for authentication. To use ssh-agent
	1. Open a Terminal window on your local machine
	2. Open run the command `eval` ``ssh-agent``
	3. Run the command `ssh-add`, and enter your passphrase when prompted (Note: if you are not using the default filename, you'll need to specify your key filename`ssh-add ~/.ssh/myprivatekeyname`). The system will print *Identity Added* if successful.
	4. That's it! Note that ssh agent needs to run in the background. If you have logged out or restarted your local computer, you may need to repeat these steps