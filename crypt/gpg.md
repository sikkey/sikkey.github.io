# GPG Guide

GnuPG a free software as PGP.

## install GPG

Download and build source code.

```
./configure
make
make install
```

Install binary package

```
# Debian / Ubuntu 环境
sudo apt-get install gnupg

# Fedora 环境
yum install gnupg
```

test

```
gpg --help
```

P.S. : GnuPG is part of Debian

## generate private key

For example, I need a private key use RSA algorithm.

```
gpg --gen-key
```

choose algorithm (RSA)

choose length (2048)

choose term (0, forever)

input y

```
您需要一个用户标识来辨识您的密钥；本软件会用真实姓名、注释和电子邮件地址组合成用户标识，如下所示：
"Heinrich Heine (Der Dichter) <heinrichh@duesseldorf.de>"

真实姓名：
电子邮件地址：
注释：

input form

更改姓名(N)、注释(C)、电子邮件地址(E)或确定(O)/退出(Q)？
O
```

## generate revoke key

```
gpg --gen-revoke [uid: your email, or hash code]
```

# manage keys

## list keys

```
gpg --list-keys
```

## delete keys

```
gpg --delete-key [uid]
```

## print private keys
public key file（.gnupg/pubring.gpg）storage as binary file. --armor to show ascii format
```
gpg --armor --output public-key.txt --export [uid]
```

show private key to ascii file
```
gpg --armor --output private-key.txt --export-secret-keys
```

## upload public keys

public key upload to subkeys.pgp.net. sync all the public key servers.
```
gpg --send-keys [uid] --keyserver hkp://subkeys.pgp.net
```

Anyone can upload keys in your name. You must make fingerprint for others to valid your public key.
```
gpg --fingerprint [uid]
```

## add public keys of other users

```
gpg --import [uid]
```

or find keys from servers

```
gpg --keyserver hkp://subkeys.pgp.net --search-keys [uid]
```

# encrypt & decrypt

## encrypt

encypt demo.txt

```
gpg --recipient [uid] --output demo.en.txt --encrypt demo.txt
```

## decrypt

```
gpg --output demo.de.txt --decrypt demo.en.txt
```
or
```
gpg demo.en.txt
```

# sign

## sign files

Tell others this file is sending by me.
```
gpg --sign demo.txt
```
Signed file name as demo.txt.gpg with binary format.

## gen ascii signed file

```
gpg --clearsign demo.txt
```
Signed file name as demo.txt.asc with ascii format.

single sign file without source file content:
```
gpg --detach-sign demo.txt
```

## sign + encrypt

--armor means ascii format
```
gpg --local-user [sender uid] --recipient [reciver uid] --armor --sign --encrypt demo.txt
```

## verify signature

```
gpg --verify demo.txt.asc demo.txt
```
