# Configuring Git with SSH Keys

## Step-by-Step Guide

### 1. Check for Existing SSH Keys

First, see if you already have SSH keys:

```sh
ls -al ~/.ssh
```

Look for files like `id_ed25519` and `id_ed25519.pub` (recommended) or `id_rsa` and `id_rsa.pub`. If you see them, you can skip to Step 4.

### 2. Generate a New SSH Key

If you don’t have a key or want a new one, generate it:

```sh
ssh-keygen -t ed25519 -C "pankaj.bidikar07@gmail.com"
```

- `-t ed25519` specifies the key type (Ed25519 is more secure and recommended over RSA).
- `-C "email@example.com"` adds a label to the key with your email.

You’ll be prompted to:

- Choose a file to save the key: Press Enter to accept the default (`~/.ssh/id_ed25519`).
- Set a passphrase: (Optional) Adds extra security to your key.

### 3. Add the SSH Key to the SSH Agent

Start the SSH agent and add your key:

```sh
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### 4. Add Your SSH Key to GitHub/GitLab/Bitbucket

Copy your public key to the clipboard:

```sh
cat ~/.ssh/id_ed25519.pub
```

Copy the output and add the key to your Git hosting service:

#### GitHub:
- Go to **Settings → SSH and GPG keys → New SSH key** → Paste the key.

#### GitLab:
- Go to **Preferences → SSH Keys** → Paste the key.

#### Bitbucket:
- Go to **Personal Settings → SSH Keys → Add key**.

### 5. Configure Git to Use SSH

Check your Git remote URL:

```sh
git remote -v
```

If it shows `https://`, you’ll need to switch it to SSH:

```sh
git remote set-url origin git@github.com:username/repo.git
```

Replace `username/repo.git` with your actual GitHub repository path.

### 6. Test Your SSH Connection

Run the following command to test your SSH setup:

```sh
ssh -T git@github.com
```

You should see:

```sh
Hi PankajBidikar! You've successfully authenticated, but GitHub does not provide shell access.
```

That’s it! You’re now set up to use Git over SSH.

---

# [alias] Section in `.gitconfig`

Git aliases are shortcuts for common or complex Git commands, designed to make your workflow faster and more efficient. Below is a list of useful Git aliases and their purposes:

## Basic Commands

```ini
st = status
co = checkout
br = branch
ci = commit
df = diff
lg = log --oneline --graph --decorate --all
```

## Working with Commits and Branches

```ini
aa = add .
cm = commit -m
ca = commit --amend
cam = commit -am
```

## Fetching and Pushing

```ini
pl = pull
pf = push --force
plr = pull --rebase
```

## Branch Operations

```ini
cb = checkout -b
bclean = "!git branch --merged | grep -v '\*\|main\|master' | xargs -n 1 git branch -d"
rb = rebase
rba = rebase --abort
rbc = rebase --continue
```

## Logs and History

```ini
hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
last = log -1 HEAD
unpushed = log --branches --not --remotes
```

## Undoing Changes

```ini
undo = reset --soft HEAD~1
unstage = reset HEAD --
discard = checkout --
hard = reset --hard
```

## Stash Operations

```ini
ss = stash save
sl = stash list
sa = stash apply
sp = stash pop
```

## Remote Operations Aliases

```ini
r = remote -v
ru = remote update
rprune = remote prune origin
```

These aliases will make your Git workflow much more efficient. Happy coding! 🚀
