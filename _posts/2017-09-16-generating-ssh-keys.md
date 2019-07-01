---
layout: post
title: Generating SSH Keys
description: "" 
tags: [git]
categories: [TIL]
---

SSH, or secure shell, is a secure protocol and the most common way of safely administering remote servers. It's important to understand how SSH is used for authentication with Git and similar tools. 

I have multiple accounts in Github and Bitbucket for the usage of work and personal. So I had to set up multiple SSH keys on a single machine.

[Generate a SSH key-pair](https://help.github.com/articles/connecting-to-github-with-ssh/)
```bash
$ ssh-keygen -t rsa -C "public.hodoo@gmail.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/davidlee/.ssh/id_rsa): /Users/davidlee/.ssh/id_rsa_github
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/davidlee/.ssh/id_rsa_github.
Your public key has been saved in /Users/davidlee/.ssh/id_rsa_github.pub.
```
 
[Adding a new SSH key](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)  
```bash
# Mac
$ pbcopy < ~/.ssh/id_rsa_github.pub
```

#### Set a config file  
```bash
# ~/.ssh/config
Host hodoogithub
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_github
```
#### Let's connect!  
```bash
$ ssh -T git@hodoogithub
Hi hodoolee! You've successfully authenticated, but GitHub does not provide shell access.
```
#### Set a remote-url
```bash
$ git remote set-url origin git@hodoogithub:hoodoolee/project.git
```