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

show key id

```
gpg --list-keys --keyid-format long
```



## delete keys

```
gpg --delete-key <key ID>
```

## print private keys
public key file（.gnupg/pubring.gpg）storage as binary file. --armor to show ascii format
```
gpg --armor --output public-key.txt --export <key ID>
```

show private key to ascii file
```
gpg --armor --output private-key.txt --export-secret-keys
```

## upload public keys

public key upload to subkeys.pgp.net. sync all the public key servers.
```
gpg --send-keys <key ID> --keyserver hkp://subkeys.pgp.net
```

Anyone can upload keys in your name. You must make fingerprint for others to valid your public key.
```
gpg --fingerprint <key ID>
```

## add public keys of other users

```
gpg --import <key ID>
gpg --import <public key file>
```

or find keys from servers

```
gpg --keyserver hkp://subkeys.pgp.net --search-keys <key ID>
```

# encrypt & decrypt

## encrypt

encypt demo.txt

```
gpg --recipient <key ID> --output demo.en.txt --encrypt demo.txt
```

## decrypt

```
gpg --output demo.de.txt --decrypt demo.en.txt
```
or
```
gpg demo.en.txt
```


用 <key id> 进行加密文件并输出到 output.enc ：
```
gpg --encrypt --recipient <key id> --output output.enc demo.txt
```
解释：

--encrypt：表示要加密文件。
--recipient <key id>：指定要使用的公钥的 ID。
--output output.enc：将加密后的文件输出到 output.enc 文件中。
demo.txt：要加密的文件。
用 <key id> 进行解密文件并输出到 output.dec ：

```
gpg --decrypt --output output.dec input.enc
```

or

解释：

--decrypt：表示要解密文件。
--output output.dec：将解密后的文件输出到 output.dec 文件中。
input.enc：要解密的加密文件。
注意：

解密时不需要指定密钥 ID，因为 GPG 会自动使用匹配的私钥进行解密。
在进行加密或解密之前，请确保您已导入要使用的密钥。

```
gpg --decrypt --output output.dec --encoding utf-8 input.enc
```



# sign

## sign files

Tell others this file is sending by me.
```
gpg --sign demo.txt
```
or
```
gpg --local-user <key id> --sign demo.txt
```


Signed file name as demo.txt.gpg with binary format.

## gen ascii signed file

```
gpg --clearsign demo.txt
```

or

```
gpg --local-user <key id> --clearsign demo.txt
```


Signed file name as demo.txt.asc with ascii format.

single sign file without source file content:
```
gpg --detach-sign demo.txt
```
or

```
gpg --local-user <key id> --detach-sign demo.txt
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
or

```
gpg --local-user <key id> --verify demo.txt.asc demo.txt
```

