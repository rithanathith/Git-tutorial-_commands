## How to connect SSH key to Github?
----------------------------------------------
# Check for existing SSH keys
Before you proceed to create an SSH key, quickly check if you have generated any keys previously. Open your Git Bash and enter the following command:

$ ls -al ~/.ssh

If you get an output something like this, you've your keys generated already. Please proceed with Adding your SSH key to ssh agent.

# Generate a new SSH key
After you've checked for existing SSH keys, and if you don't see any output, generate a new SSH key to use for authentication, then add it to the ssh-agent.


Run the command below to generate a new set of keys, by substituting your_email@example.com with your GitHub email address.:

$ ssh-keygen -t ed25519 -C "your_email@company.com"

Note: If you are using a legacy system that doesn't support the Ed25519 algorithm, use:

$ ssh-keygen -t rsa -b 4096 -C "your_email@company.com"

When you're prompted to "Enter a file in which to save the key," press Enter. This accepts the default file location.

Enter a file in which to save the key (/c/Users/your.user.name/.ssh/id_ed25519):[Press enter]

At the prompt, type a secure passphrase or press Enter for no passphrase without writing anything.

Enter passphrase (empty for no passphrase): [Type a passphrase]
Enter same passphrase again: [Type passphrase again]


# Add your SSH key to ssh agent

Before adding a new SSH key to the ssh-agent you should ensure that ssh-agent is running. Enter the command below to confirm.

$ eval "$(ssh-agent -s)"
> Agent pid 2030

Then add your SSH private key to the ssh-agent.

$ ssh-add ~/.ssh/id_ed25519


# Add your public SSH key to your GitHub account
Copy the SSH public key from the set of SSH keys you just generated and added to your ssh-agent. This is the step where the commands for Windows and Linux users would differ.


If you are a Windows user use the command below to copy the content of the public key file. The command copies the public key to your clipboard. You can verify by trying to paste it into a notepad.


$ clip < ~/.ssh/id_ed25519.pub

If you are a Linux use the command below to display the content of the public key file. Then, select and copy the long string displayed in the terminal to your clipboard.



$ cat ~/.ssh/id_ed25519.pub
> ssh-ed25519 ZZZZC3QzaC1lZDI1NTE5BBBBICiv7GatnQaTdOe1YoucU40UeoMLQOCHZP6LEpHuLOWg your_email@company.com


# Verify the authentication with the below command.

$ ssh -T git@github.gatech.edu

On successful authentication you will get the below output.

> Hi your.user.name! You've successfully authenticated, but GitHub does not provide shell access.

# Push your project on your GitHub account

git remote add origin "ssh link"

git branch -M main

git push -u origin main
