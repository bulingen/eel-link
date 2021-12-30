# Eel Link

Stuff to configure Raspberry PI to talk to the Eel.

## Initial setup

1. Install Ubuntu Server 20.04.
1. With SD card still plugged in to your computer, add your local wifi credentials to `network-config`.
1. Also, add your SSH public key to `~/.ssh/authorized_keys`.
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
        1. Create a file `/etc/ssh/custom_banner` and paste contents of `custom_banner` in this repo.
