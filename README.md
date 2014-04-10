btcgui
======

[![Build Status](https://travis-ci.org/conformal/btcgui.png?branch=master)]
(https://travis-ci.org/conformal/btcgui)

btcgui is a graphical frontend to btcwallet and btcd written using
gotk3.

Full btcwallet installation instructions can be found
[here](https://github.com/conformal/btcwallet).

This project is currently under active development is not production
ready yet.  Because of this, support for connecting to a mainnet
btcwallet is currently disabled, and testnet must be used instead.

## Installation

### Windows - MSI Available

Install the btcd suite MSI available here:

https://opensource.conformal.com/packages/windows/btcdsuite/

### Linux/BSD/POSIX - Build from Source

- Install Go according to the installation instructions here:
  http://golang.org/doc/install

- Install GTK.  As btcgui relies on
  [GoTK3](https://github.com/conformal/gotk3) for GTK binding support, a
  version compatible with GoTK3 is required.

- Run the following commands to install btcwallet and btcd:
```bash
$ go get -u -v github.com/conformal/btcd/...
$ go get -u -v github.com/conformal/btcwallet/...
```

- Run the following command to install btcgui, using the correct GoTK3
  build tag if you are not running the latest supported GTK:
```bash
$ go get [-tags gtk_#_#] -u -v github.com/conformal/btcwallet/...
```
  Alternatively, a Makefile is provided which will determine and use the
  correct GTK build tag.  You will have to clone the repo manually first,
  though.
```bash
$ cd $GOPATH/src
$ git clone https://github.com/conformal/btcgui.git
$ cd btcgui
$ make
```

- btcd, btcwallet, and btcgui will now be installed in either ```$GOROOT/bin```
  or ```$GOPATH/bin``` depending on your configuration.  If you did not already
  add to your system path during the installation, we recommend you do so now.

## Updating

### Windows

Install a newer btcd suite MSI here:

https://opensource.conformal.com/packages/windows/btcdsuite/

### Linux/BSD/POSIX - Build from Source

- Run the following commands to update btcgui, all dependencies, and install it:
```bash
$ go get -u -v github.com/conformal/btcd/...
$ go get -u -v github.com/conformal/btcwallet/...
$ go get [-tags gtk_#_#] -u -v github.com/conformal/btcgui/...
```
  Alternatively, running ```make update``` from the btcgui directory will
  determine the correct GTK build tag for your system and call ```go get```
  for you.

## Getting Started

### Windows (Installed from MSI)

Open ```Btcd Suite``` from the ```Btcd Suite``` folder in the Start Menu.

### Linux/BSD/POSIX/Source

- Run the following command to start btcd:

```bash
$ btcd --testnet -u rpcuser -P rpcpass
```

- Copy btcd's autogenerated rpc.cert to ~/.btcwallet/ so btcwallet can 
  securely communicate with btcd over a TLS-encrypted websocket.  This
  step is only necessary for the first time starting btcwallet or if  
  btcd's autogenerated cert and key are removed and regenerated. 

```bash
$ mkdir ~/.btcwallet/   
$ cp ~/.btcd/rpc.cert ~/.btcwallet/btcd.cert
```

- Run the following command to start btcwallet:

```bash
$ btcwallet -u rpcuser -P rpcpass
```

- Copy btcwallet's autogenerated rpc.cert to ~/.btcgui/ so btcgui can
  securely communicate with btcwallet over a TLS-encrypted websocket.
  This step is only necessary for the first time starting btcgui or
  if btcwallet's autogenerated cert and key are removed and regenerated.

```bash
$ mkdir ~/.btcgui/
$ cp ~/.btcwallet/rpc.cert ~/.btcgui/btcwallet.cert
```

- Run the following command to start btcgui:

```bash
$ btcgui -u rpcuser -P rpcpass
```

## TODO
- Implement an address book
- Documentation
- Code cleanup
- Optimize
- Much much more.  Stay tuned.

## GPG Verification Key

All official release tags are signed by Conformal so users can ensure the code
has not been tampered with and is coming from Conformal.  To verify the
signature perform the following:

- Download the public key from the Conformal website at
  https://opensource.conformal.com/GIT-GPG-KEY-conformal.txt

- Import the public key into your GPG keyring:
  ```bash
  gpg --import GIT-GPG-KEY-conformal.txt
  ```

- Verify the release tag with the following command where `TAG_NAME` is a
  placeholder for the specific tag:
  ```bash
  git tag -v TAG_NAME
  ```

## License

btcgui is licensed under the liberal ISC License.
