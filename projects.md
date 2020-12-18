---
layout: default
permalink: /projects
---

## This homepage

guide to come...

## Documentation on using multiple Git account on one machine

This guide is a condensed version of the tutorial on [Free Code Camp](https://www.freecodecamp.org/news/manage-multiple-github-accounts-the-ssh-way-2dadc30ccaca/). Mostly used by myself when in need.

#### 1. Generating SSH key
Check current keys with `ls -al ~/.ssh`. Look for an id_rsa in the right hand
column. If there is no key available, generate a new with `ssh-keygen -t rsa`. Press
enter to accept default location (~/.ssh). Two keys will be generated, one private
and one public with ending name `id_rsa.pub`. If you only have one account this
key is enough and go to next part, for multiple accounts continue below.

For each account we have different keys. To generate a key with a name use
`ssh-keygen -t rsa -C "name@mail.com" -f "id_rsa_account1"`.

#### 2. Adding keys to Github account
In each key-pair, we give the public key to Github and keep the private key...
private. To copy the public key to the clipboard use `pbcopy < ~/.ssh/id_rsa.pub`.
If you have a "named" key with the `ssh-keygen -t rsa -C "name@mail.com" -f "id_rsa_account1"`
command the corresponding copycommand is `pbcopy < ~/.ssh/id_rsa_work_user1.pub`.

Paste the key on Github. Settings -> SSH and GPG keys -> New SSH key -> Add key

#### 3. Registering the key with the SSH-agent
Run the agent in the background with `eval "$(ssh-agent -s)"` and it should return
a PID for the process. For each key use `ssh-add ~/.ssh/id_rsa`. If it is a named key
replace id_rsa with the "named" key ie `ssh-add ~/.ssh/id_rsa_account1`.

#### 4. Make SSH-agent use correct key for different hosts
To check if the config file exists use `cat ~/.ssh/config` otherwise create it with
```
cd ~/.ssh/
touch config
```
To edit the created config use `vi config` or if you have Atom installed `atom config` for
a comfortable texteditor.
With the vi command: to inter text press i (insert) and to exit and save user colon
(:) followed by wq for Write and Quit.

Int the config file write:
```
# Default account
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa

# Other named accounts
Host github.com-account1
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_account1

Host *
  AddKeysToAgent yes
  UseKeychain yes
```

Host * will match to anything and make sure keychain is enabled. Please see SSH
config documentation for more info. 
## Algorithms on the PYNQ boards

Have not started. Will start spring 2021 when the cash is back in.
