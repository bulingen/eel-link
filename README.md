# Eel Link

Stuff to configure Raspberry PI to talk to the Eel.

## Initial setup

1. Install Ubuntu Server 20.04. Follow [this guide](https://ubuntu.com/tutorials/how-to-install-ubuntu-on-your-raspberry-pi#1-overview), where you also get to know how to set a static IP.
1. Add your SSH public key to `/home/ubuntu/.ssh/authorized_keys`.
1. In `/etc/ssh/sshd_config`, set:
    1. `LoginGraceTime 30s`
    1. `PermitRootLogin no`
    1. `PasswordAuthentication no`
    1. `ChallengeResponseAuthentication yes`
    1. `UsePAM no`
    1. `AllowAgentForwarding yes`
    1. `AllowTcpForwarding yes`
    1. `X11Forwarding yes`
    1. `ClientAliveInterval 600`
    1. `ClientAliveCountMax 0`
    1. `Banner /etc/ssh/custom_banner`
        1. Create a file `/etc/ssh/custom_banner` and paste contents of `custom_banner` located in this repo.
1. On your working machine, add to `~/.ssh/config`:
    ```
    Host eellink
        HostName <the static IP you set earlier>
        User ubuntu
        ForwardAgent yes
    ```
1. SSH into the PI: `ssh eellink`.
1. Update packages: `sudo apt update` and `sudo apt upgrade`.
1. Set hostname:
    1. Edit this file: `sudo nano /etc/hostname`.
    1. Update any occurrences in this file: `sudo nano /etc/hosts`
1. Change sudo timeout to 30 minutes:
    1. `sudo visudo`
    1. Add this line: `Defaults        timestamp_timeout=30`.
    1. Save and exit.
1. Set Git environment variables, so that different Git users can be used:
    1. On the remote machine, edit `/etc/ssh/sshd_config` and add: `AcceptEnv GIT_*`.
    1. On your local machine, add environment variables to your `~/.ssh/config` so that it looks like this:
    ```
    Host eellink
        HostName <the static IP you set earlier>
        User ubuntu
        ForwardAgent yes
        SetEnv GIT_AUTHOR_NAME=<username> GIT_AUTHOR_EMAIL=<email> GIT_COMMITTER_NAME=<username> GIT_COMMITTER_EMAIL=<email>
        SendEnv GIT_AUTHOR_NAME GIT_AUTHOR_EMAIL GIT_COMMITTER_NAME GIT_COMMITTER_EMAIL
    ```
1. Log out and log in again.
