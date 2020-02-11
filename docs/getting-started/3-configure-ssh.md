---
permalink: /getting-started/configure-ssh
sidebarDepth: 1
---


# Step 3. Configure your SSH

This step configure your SSH connection to and from your local machine and your lab.

::: warning Requirement
Successful verification of Step 1 and 2.
:::

In this step you will configure SSH connections for two (2) machines in your lab. One machine that we call **`entry`** used for security purposes, and one machine called **`home`** were you will do your analysis and store your data.

## 3.1 Identify required info 

Open the **`ssh-config.txt`** file that you collected in Step 1 in your favourite text editor. 

This file contains the necessary information for your SSH configuration. Take note of your **`lab-name`**, your **`lab-IP`** and your **`username`**.

**Example contents of `ssh-config.txt`**

```bash
Host <your-lab-name>-entry
    HostName <your-lab-IP>
    User <your-username>
```





## 3.2 Configure you entry machine


1. Start your favorite terminal program which supports SSH. 

::: warning Windows

We strongly recommend that you complete this initial setup using the **`Putty`** executable that you download from this specific link: [putty.exe](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) (the putty.exe 64-bit version).
:::

2. Type **`ssh <your-username>@<your-lab-IP>`**
3. You should then be prompted to enter a password `<your-username>@<your-lab-IP>'s password:`
4. Enter your `SSH temporary key` sent to you from HUNT over Signal _two_ times.
5. Enter your new `passphrase` (see below for a how to). Retype for verification. You will be kicked off the entry server by completion.

::: tip Designing your own passphrase

We prefer that you give a `passphrase` instead of a password. A passphrase is a series of words that creates a phrase. It should be:

- long enough to be hard to guess
- not a famous quotation from the literature (but could be pretty close)
- hard to guess by intuition (even by someone who knows you well)
- easy to remember

Oh, and, it should be unique to this site only (not to mention at least
_12 characters_ long and include both _lower_ and _upper_ cases).

Making a good passphrase is great fun and good security hygiene. Here is one to get you going:

```bash
AnalysingPokemon4Funinthemorning
```

:::


6. Login again to your entry server, `ssh <your-username>@<your-lab-IP>`, with your newly generated passphrase.

## 3.3 Configure your home machine

7. When on your entry server, connect to your home server by typing `ssh home`.
8. Similar to step 3, you will be prompted to retype your `SSH temporary key` sent to you from HUNT over Signal and to repeat your new passphrase two times (it is fine to use the same passphrase as on your entry node). You will be kicked back to your entry server by completion.
9. Log into your home server using `ssh home` using your new passphrase.
10. With a tiny bit of luck, you should now be inside your project lab which should look something like below. Enjoy!

::: details Example when logged in to a lab's home server

```
Welcome to Ubuntu 16.04.3 LTS (GNU/Linux 4.4.0-98-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

66 packages can be updated.
0 updates are security updates.

Welcome to TEST-LAB.

For the record, if you shouldn't be here - please
leave and report the incident to cloud@hunt.ntnu.no.

Last login: Sun Dec  3 12:29:28 2017 from 10.10.10.10
testuser1@test-lab-home:~$
```

:::



## 3.4 Simplify your life

Do not skip this chapter... We hope that you will log into your lab a lot over the coming months and years, so we need to make sure that you simplify that process to the point where you get instant access to your lab.

::: details Windows
We recommend MobaXterm as a free X server that allow you to connect with both SSH and SFTP. Here is a [step wise guide](/working-in-your-lab/technical-tools/mobaxterm) on how to establish a password less login directly to your home-machine.
:::

::: details Mac and Linux

#### Establish an SSH alias

1. Open the `ssh-config.txt` file your received.
2. Add this content to the file named `config`in the hidden ssh-folder in your home directory (`~/.ssh/config`) using your favourite file editor. You may need to generate this file if it is your first ssh-configuration.

You should now be able to connect to your lab with the SSH-command `ssh <your-lab-name>`.

#### Establish a password-less login

If you already have a RSA certificate on your local computer that you would like to use, start from step 3

1. Log out from your project lab typing `exit` (you should now be in your local computer)
2. Generate a new RSA certificate with `ssh-keygen`. Hint enter three times. When this finish:
3. Enter `ssh-copy-id <your-lab-name>-entry` to add your certificate to your entry node. Enter the entry-node passphrase you generated in the section above.
4. Enter `ssh-add`to add the certificate to the ssh-agent. If you don't have a running ssh-agen you may see an error message. In such a case, first enter `eval "$(ssh-agent -s)"` and next enter `ssh-add`
5. You should now be able to log directly into your home node with the command `ssh <your-lab-name>`, e.g. 'ssh demolab'.

Simple and secure, you should now be able to directly enter your home node with this command:

```bash
ssh <your-lab-name>
```

:::

::: tip
Time for coffee!
:::