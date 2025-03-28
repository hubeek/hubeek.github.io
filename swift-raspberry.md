# Swift raspberry

_Status: Published_
_Created: 2017-01-23 08:36:46_
_Tags: swift raspberry_

sudo apt-get update
sudo apt-get install -y clang
 wget https://s3-us-west-2.amazonaws.com/swiftpi.swiftlite.v1/swift-lite-3.0-raspberrypi-universal.tar.gz
sudo tar -xzpf swift-lite-3.0-raspberrypi-universal.tar.gz -C/

examples
wget https://s3-us-west-2.amazonaws.com/swiftpi.swiftlite.v1/helloworld3.tar.gz
 tar -xzpf helloworld3.tar.gz

cleanup
rm swift-lite-3.0-raspberrypi-universal.tar.gz helloworld3.tar.gz

to build
cd swiftProjects
swift-lite-build helloworld.swift

test/run
./helloworld.swapp