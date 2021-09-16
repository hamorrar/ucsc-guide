---
date: 2021-09-15
title: "SSH Keys"
linkTitle: "SSH Keys"
description: "An explanation of SSH keys for Git"
weight: 3
author: Steven Mak
---

In the last article, you got Git on your computer if it wasn't already installed and created an account for Git on either the school's or some other remote repo site. There is one more optional but highly recommended step we must go through before actually using Git, setting up an SSH key.

## Background

When interacting with a remote repo, you must authenticate yourself so that the remote repo hosts know you really are who you say you are. This is because it would be a huge security flaw if anyone could modify anyone's repo without the proper permissions. 

There are two protocols that can be used to do this in Git, HTTPS and SSH. In the simplest terms, a protocol is a way something gets done. HTTPS and SSH are both cryptographically secure ways to transmit data from one point to another (the servers hosting the remote repo to your computer and vice-versa in this case) through the Internet. You likely have seen HTTPS before at the beginning of URLs because this is one of the main protocols used to send data from you to a website and vice-versa. The reason why it's recommended to use SSH over HTTPS is that when authenticating over HTTPS, you have to type your username and password of the account you made on the site of the remote repo host, which can be quite inconvenient. This is as opposed to SSH where you're authenticated automatically once you set it up.

To do this, you must generate an SSH key pair, one public key and one private key. Afterwards, you must store the keys on your computer, and give the remote repo host a copy of the public key. The private key is sensitive because it's used for authentication purposes so keep it safe and don't give it out.

## Generating SSH keys and storing them on your device

If you're using Windows, open Git Bash. If you're on a Mac or Linux, open Terminal. Then, type ``ssh-keygen -t RSA -b 4096``. This will generate a public and private SSH key using RSA-4096 as the encryption algorithm. 

You will then be prompted for where to store the private key file. Press Enter/Return so that it gets stored in the default place. If it's asking whether to overwrite a file called ``id_rsa`` or not, then type N, press enter/return, and skip to the [Giving the public key to the remote repo host](#giving-the-public-key-to-the-remote-repo-host).

After this, you will be prompted to create a passphrase. As an added security measure, SSH private keys can be further protected with a passphrase. However, if you're using a personal computer and it's just for school or personal projects, you can just press enter and leave the passphrase blank because it isn't much of a concern in that case. 

Now that the public/private key pair is generated, we will now need to give the public key to the remote repo host, allowing us to authenticate automatically.

## Giving the public key to the remote repo host

This next step depends on what host is being used, such as Gitlab, the school's self-hosted GitLab server, or GitHub, but it's all generally the same process. First, go to your account settings/preferences on the remote repo site. Then, find the settings tab/page for SSH keys. 

<div class="card rounded p-2 td-post-card mb-4 mt-4" style="max-width: 700px">
	<img class="card-img-top" src="../ssh-keys-github.png" width="1096" height="840">
	<div class="card-body px-0 pt-2 pb-0">
		<p class="card-text">
		What the SSH Keys section in the settings for GitHub look like 
		<small class="text-muted"><br>Photo: github.com</small>
		</p>
	</div>
</div>

<div class="card rounded p-2 td-post-card mb-4 mt-4" style="max-width: 900px">
	<img class="card-img-top" src="../ssh-keys-gitlab.png" width="1594" height="854">
	<div class="card-body px-0 pt-2 pb-0">
		<p class="card-text">
		What the SSH Keys section in the settings for GitLab look like 
		<small class="text-muted"><br>Photo: gitlab.com</small>
		</p>
	</div>
</div>

[picture of GitHub SSH settings]
[picture of GitLab SSH settings]

Once the page is open, navigate to the user directory by typing ``cd ~`` into Git Bash on Windows or Terminal for Mac and Linux.

Then, if you're on Windows, type ``cat id_rsa.pub | clip``. 

If you're in Mac, type
``cat id_rsa.pub | pbcopy``.

If you're on Linux, then type
``cat id_rsa.pub``
and find the shortcut to copy the output from Terminal, including the lines marking the beginning and end of the key.

It is extremely important that you type it **with** the ``.pub`` extension to copy the public key. Once it's copied paste the key into the appropriate text-box on the SSH key settings page in your browser, setting the expiration date to never if there is an option for that and give the key a title telling what device the key is for. When you've typed all the information, add the key.

---

This concludes this group of articles. The next group of articles, [Basics](../../basics/), will talk about how to do many of the operations that were described in [How Git Works](../how_git_works/).