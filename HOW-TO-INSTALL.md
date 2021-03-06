# Notes

EOTK requires Tor 0.2.9.9+

EOTK requires recent `nginx` with the following modules/features enabled:

* `headers_more`
* `ngx_http_substitutions_filter_module`
* `http_sub`
* `http_ssl`

# Fresh Installations (by platform)

Where you don't have Tor, NGINX or OnionBalance, or much other stuff
currently installed:

## OSX Sierra (prebuilt via homebrew)

* install Homebrew: http://brew.sh
* `git clone https://github.com/alecmuffett/eotk.git`
* `cd eotk`
* `./opt.d/install-everything-on-osx.sh`

## Ubuntu 16.04 (prebuilt via tor and canonical)

* `git clone https://github.com/alecmuffett/eotk.git`
* `cd eotk`
* `./opt.d/install-everything-on-ubuntu-16.04.sh`

## Raspbian Jessie / Jessie-Lite (manual builds)

* `git clone https://github.com/alecmuffett/eotk.git`
* `cd eotk`
* `./opt.d/build-nginx-on-raspbian.sh`
* `./opt.d/build-tor-on-raspbian.sh`
* `./opt.d/install-onionbalance-on-raspbian.sh`

# Piecemeal Installation Notes

You only need this section if you have to do installation in bits
because pre-existing software:

## Ubuntu Tor Installation

In a browser elsewhere, retreive the instructions for installing Tor
from https://www.torproject.org/docs/debian.html.en

* Set the menu options for:
  * run *Ubuntu Xenial Xerus*
  * and want *Tor*
  * and version *stable*
  * and read what is now on the page.
* Configure the APT repositories for Tor
  * I recommend that you add the tor repositories into a new file
    * Use: `/etc/apt/sources.list.d/tor.list` or similar
* Do the gpg thing
* Do the apt update thing
* Do the tor installation thing

## Ubuntu NGINX Installation

Through `apt-get`; logfiles are tweaked to be writable by admin users.

* `sudo apt-get install nginx-extras`
* `sudo find /var/log/nginx/ -type f -perm -0200 -print0 | sudo xargs -0 chmod g+w`

## Ubuntu OnionBalance Installation

Through `apt-get` and `pip`; using `pip` tends to mangle permissions,
hence the find/xargs-chmod commands.

* `sudo apt-get install socat python-pip`
* `sudo pip install onionbalance`
* `sudo find /usr/local/bin /usr/local/lib -perm -0400 -print0 | sudo xargs -0 chmod a+r`
* `sudo find /usr/local/bin /usr/local/lib -perm -0100 -print0 | sudo xargs -0 chmod a+x`
