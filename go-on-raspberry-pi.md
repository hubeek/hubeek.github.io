# Go on raspberry pi

_Status: Published_
_Created: 2023-01-08 04:48:51_

## Download page  
[Golang download](https://golang.org/dl/)  
## Latest package
[latest package for ARM v6](https://go.dev/dl/go1.19.4.linux-armv6l.tar.gz)  
```
mkdir ~/src && cd ~/src
wget https://dl.google.com/go/go1.14.4.linux-armv6l.tar.gz
sudo tar -C /usr/local -xzf go1.14.4.linux-armv6l.tar.gz
rm go1.14.4.linux-arm64.tar.gz
vi ~/.profile

```
adjust PATH
```
PATH=$PATH:/usr/local/go/bin
GOPATH=$HOME/go
```
update shell
```
source ~/.profile
```
