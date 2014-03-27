This repository contains an example for getting a Mac OSX machine up and joining a tinc network on startup. It assumes that a tinc network is already up at {l04,l05}.kitesplex.com and has RSA public keys already installed matching the user's.

# USAGE

ref: http://www.tinc-vpn.org/examples/osx-install/#index3h3

## Install

```
brew install tuntap tinc
```

You can optionally install Bonjour Browser to see all workgroup machines.

## Configure

1. Setup a symlink `/usr/local/etc/tinc -> /Users/eshao/wsp/tinc` or wherever this folder is.
2. PEM encode your .ssh/id\_rsa.pub and put it into mesh0/hosts/{USER}. E.g.: `ssh-keygen -f id\_rsa.pub -e -m PEM`
3. Change the IP address in `tinc-up` to mirror your dev machine. For example, if your dev machine is `10.77.4.10`, your mac's IP should be `10.77.30.10`. The only thing that chnages is the second-to-last octet.
4. Try it via `sudo tincd -n mesh0 -D`.
5. Test via `ping 10.77.12.4` or `ping l05.local`

## Startup Automatically

1. Copy tinc.plist to `/Library/LaunchDaemons/`
2. Run `sudo launchctl -w /Library/LaunchDaemons/tinc`

That's it! It should now run on every startup.


