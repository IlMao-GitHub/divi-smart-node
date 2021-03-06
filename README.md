# Divi Smart Node
Get a Divi core node up and running on a Raspberry Pi device in a flash (pun intended).

# System requirements
We recommend a Raspberry Pi 4 device with a 32GB Class 10 microSD card and 4GB of RAM. This is the only configuration on which this implementation has been tested.

**Note: While no issues have been found with this implementation, this software is considered to be in an Alpha stage. Use at your own risk and *always* back up your mnemonic seed phrase before transacting with any real funds**

# Instructions
1. [Download](https://divi-smart-node.sfo2.cdn.digitaloceanspaces.com/divi-smart-node-0.0.3-alpha.img.gz) the latest image.
*Note: The latest image is for the Raspberry Pi 4. If you would like the older, 3b+ image, [click here](https://divi-smart-node.sfo2.cdn.digitaloceanspaces.com/divi-smart-node-0.0.2-alpha.img.gz)*
2. Use [Etcher](https://www.balena.io/etcher/) or similar software to flash the image to a microSD Card (64GB recommended).
3. Insert the flashed microSD card into your Raspberry Pi 3b+ device and turn on.
4. On boot, you will be prompted to enter an RPC username, type one of your choosing and press `ENTER`.
5. The node will configure itself and begin to sync automatically, use the node as usual via the command line.

For more information on CLI commands, see our [wiki page](https://wiki.diviproject.org/#divi-cli)

# Filepaths

### Autostart Configuration

The autostart configuration can be found at `~/.config/lxsession/LXDE-pi/autostart`

* Scripts will be run at startup using the autostart file
* Always keep scripts above the `@xscreensaver -no-splash` line

### Divi Config Script (first run)

This process is automated and does not require any user input. The divi daemon (`divid`) is run at the system level as a service. 

A script called `divisetup-run.sh` will run the first time the image is booted. It is located at `/home/pi/divisetup-run.sh` and performs the following actions:

* Searches the `.divi` data directory for `divi.conf`
* Randomly generates an rpc username & password using the SHA256 hashing algorithm and writes it to `divi.conf`
* Writes `daemon=0` to the `divi.conf` file
* Renames `divisetup-run.sh` to `divisetup-complete.sh`
* Starts `divid.service`
*If `~/.divi/divi.conf` exists already, only the final step will run.*

### Divi Config Script (subsequent runs)

After the initial setup, a script named `divi-startup.sh` runs on boot. It is located at `/home/pi/divi-startup.sh` and performs the following actions:

* Checks for `divisetup-complete.sh`
* If not found, runs `divisetup-run.sh`

### Divi Shutdown Script

**Note: Shutdown script has not been confirmed as working and should be considered a known issue.**

# Aliases

Several bash aliases are present in the root directory's `.bash_aliases` file. 

| ALIAS | FUNCTION  |
| ---   | ---       |
| `aliasfile`       | opens the alias file for editing  |
| `aliasreload`     | reloads the shell                 |
| `sweep`           | deletes `.bash_history` and closes the terminal |
| `init-divi-conf`  | resets `divisetup-run.sh` to reconfigure `divid` on next boot |
| `dli`             | alias for `./divi-cli`. Run any `divi-cli` command with `dli <command>` |
| `dividebug`       | tails the debug log |
| `divistart`       | starts `./divid`  |
| `diviservicestart`| starts the `divid.service` system service |
| `diviservicestop` | stops `divid.service` |
| `diviservicestatus`| prints the `divid.service` status for debugging |
| `diviclearcache`  | removes unnecessary data directory files |
| `divirefresh`     | starts `./divid` with the `-reindex` flag |
| `divirescan`      | starts `./divid` with the `-rescan` flag |
| `dividir`         | quick access to the `DIVI` directory  |
| `datadir`         | quick access tho the Divi data directory where config files, etc. are found | 
| `diviuserdelete`  | **DANGER:** This command removes all user-specific files, including `wallet.dat`. Use with extreme caution|




# FAQ

Q. Can I run a masternode on a Raspberry Pi?

A. Yes, see our [wiki page](https://wiki.diviproject.org/#masternode-setup-guide) for instructions.

Q. Can I use this Raspbian image as a "stake box?"

A. Yes, just be sure to back up your mnemonic seed phrase in case of SD card errors or any other issues.
