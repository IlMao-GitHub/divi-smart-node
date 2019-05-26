# Divi Smart Node
Get a Divi core node up and running on a Raspberry Pi device in a flash (pun intended).

# System requirements
We recommend a Raspberry Pi 3b+ device with a 64GB Class 10 microSD card. This is the only configuration on which this implementation has been tested.

**Note: While no issues have been found with this implementation, this software is considered to be in an Alpha stage. Use at your own risk and *always* back up your mnemonic seed phrase before transacting with any real funds**

# Instructions
1. [Download](https://divi-smart-node.sfo2.cdn.digitaloceanspaces.com/divi-smart-node-0.0.1-alpha.img.gz) the latest image.
2. Use [Etcher](https://www.balena.io/etcher/) or similar software to flash the image to a microSD Card (64GB recommended).
3. Insert the flashed microSD card into your Raspberry Pi 3b+ device and turn on.
4. On boot, you will be prompted to enter an RPC username, type one of your choosing and press `ENTER`.
5. The node will configure itself and begin to sync automatically, use the node as usual via the command line.

For more information on CLI commands, see our [wiki page](https://wiki.diviproject.org/#divi-cli)

# FAQ
Q. Can I run a masternode on a Raspberry Pi?
A. Yes, see our [wiki page](https://wiki.diviproject.org/#masternode-setup-guide) for instructions.

Q. Can I use this Raspbian image as a "stake box?"
A. Yes, just be sure to back up your mnemonic seed phrase in case of SD card errors or any other issues.
