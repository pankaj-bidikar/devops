=======
# Configuring Git with SSH keys
=======  
Here’s a step-by-step guide to configuring Git with SSH keys:

1. ## Check for Existing SSH Keys

   First, see if you already have SSH keys:
   
   ls -al ~/.ssh
   
   Look for files like id_ed25519 and id_ed25519.pub (recommended) or id_rsa and id_rsa.pub. If you see them, you can skip to **Step 4**.

2. ## Generate a New SSH Key

   If you don’t have a key or want a new one, generate it:  
   
   ssh-keygen -t ed25519 -C "pankaj.bidikar07@gmail.com"
      
      * -t ed25519 specifies the key type (Ed25519 is more secure and recommended over RSA).  
      * -C "email@example.com" adds a label to the key with your email.

  You’ll be prompted to:  
      * **Choose a file to save the key**: Press Enter to accept the default (\~/.ssh/id\_ed25519).  
      * **Set a passphrase**: (Optional) Adds extra security to your key.

3. ## Add the SSH Key to the SSH Agent

   Start the SSH agent and add your key:  

   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_ed25519

4. ## Add Your SSH Key to GitHub/GitLab/Bitbucket

   1. **Copy your public key to the clipboard**:  
   
      cat ~/.ssh/id\_ed25519.pub

   Copy the output.  
   
   2. **Add the key to your Git hosting service**:  
      1. **GitHub**:
         Go to **Settings** → **SSH and GPG keys** → **New SSH key** → **Paste the key**.
      
      2. **GitLab**:
         Go to **Preferences** → **SSH Keys** → **Paste the key**.

      3. **Bitbucket**:
         Go to **Personal Settings** → **SSH Keys** → **Add key**.

5. ## Configure Git to Use SSH

   1. **Check your Git remote URL:**

      git remote -v

   If it shows https://, you’ll need to switch it to SSH.

   2. **Change from HTTPS to SSH:**

      git remote set-url origin git@github.com:username/repo.git

   Replace username/repo.git with your actual GitHub repo path.

6. ## Test Your SSH Connection

   Run the following command to test your SSH setup:  

      ssh -T git@github.com

   You should see:  
      Hi PankajBidikar! You've successfully authenticated, but GitHub does not provide shell access.

   That’s it! You’re now set up to use Git over SSH. Let me know if you run into any issues. 😊  
