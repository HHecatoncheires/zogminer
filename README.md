#PSA

The solo mining portion of Zogminer has moved (temporarily) to a clone of the zcash repo found at https://github.com/nginnever/zcash We will make a PR to zcash when it is ready. This repo can still serve as pool miner. 

# ZCash-gpu-miner
An OpenCL [Zcash](https://z.cash) miner solving [Equihash](https://www.internetsociety.org/sites/default/files/blogs-media/equihash-asymmetric-proof-of-work-based-generalized-birthday-problem.pdf) PoW.

## Project Status

**Status:** *In active development*

Check the project's [roadmap](https://github.com/nginnever/zogminer/blob/master/ROADMAP.md) to see what's happening at the moment and what's planned next.

[![Project Status](https://badge.waffle.io/nginnever/zogminer.svg?label=In%20Progress&title=In%20Progress)](https://waffle.io/nginnever/zogminer)
[![Build Status](https://travis-ci.org/nginnever/zogminer.svg?branch=master)](https://travis-ci.org/nginnever/zogminer)
[![Gitter chat](https://badges.gitter.im/gitterHQ/gitterHQ.github.io.svg)](https://gitter.im/zogminer/dev)

## Building

First make sure OpenCL is correctly installed in your system. If you are having issues, take a look at our [Ubuntu Guide](https://github.com/nginnever/zogminer/wiki/Ubuntu-16.04-Setup) or [Fedora Guide](https://github.com/nginnever/zogminer/wiki/Fedora-24-Setup). 

If you are getting ```/usr/bin/ld: cannot find -lOpenCL```, the error has to do with the driver installing ```libOpenCL.so``` as ```libOpenCL.so.1```. You can create a symlink:

```
$ sudo ln -s /usr/lib/libOpenCL.so.1 /usr/lib/libOpenCL.so
```

Or for people that do not want to mess with this:

```
$ sudo apt-get install ocl-icd-opencl-dev
```

### Unix

Install the dependencies. On Debian/Ubuntu-based systems:

```
$ sudo apt-get install \
      build-essential pkg-config libc6-dev m4 g++-multilib \
      autoconf libtool ncurses-dev unzip git python \
      zlib1g-dev wget bsdmainutils automake opencl-headers \
      mesa-common-dev
```

On Fedora-based systems:

```
$ sudo dnf install \
      git pkgconfig automake autoconf ncurses-devel python wget \
      gtest-devel gcc gcc-c++ libtool patch opencl-headers mesa-libGL-devel
```

Fetch our repository with git and run fetch-params.sh like so:

```
$ git clone https://github.com/nginnever/zogminer.git
$ cd zogminer/
$ ./zcutil/fetch-params.sh
```
Ensure you have successfully installed all system dependencies as described above. Then run the build, e.g.:

```
$ ./zcutil/build.sh -j$(nproc)
```

This should compile our dependencies and build zcash-miner. (Note: if you don't have nproc, then substitute the number of your processors.)

## Running

### Run GPU test miner

```
$ ./src/zcash-miner -G
```

Usage:

```
$ ./src/zcash-miner -help
```

### Stratum

```
./src/zcash-miner -G -stratum="stratum+tcp://<address>:<port>" -user=<user> -password=<pass>
```

### Solo mine ZCash

This currently only works on the zcash branch https://github.com/nginnever/zcash

zcashd -G -allgpu (this will load all your cards and solo mine)
zcashd -G -deviceid= (this will run a specific card)
zcashd -G -allgpu -genproclimit=2 (this will run two threads per card. If you're card has 4gb or more this can work)

First create or modify ```~/.zcash/zcash.conf``` with the following:

```
testnet=1
addnode=betatestnet.z.cash
rpcuser=username
rpcpassword=password
gen=1
GPU=1
deviceid=<device> (default: 0)
```

Next run zcashd:

```
./src/zcashd
```

## Donations


@omaralvarez

ZEC: t1MEUYR6yu9hYQ31ECWmijVwx9R6pAXQSTy

BTC: 18tvCqDFAFWv3jwDqXe5SBs6bmy9Xn4bnN

ETH: 0x000DCB7ccB55faDaEc5C4A13E173a1E30e643867


@AgeManning

ZEC: t1MfAaj8YDwiwFb6RAnNtW4EtzvTvkFGBvV

BTC:1EdijwWG3jYczjWLAqVgg3WgV8prXo5M5C

ETH: 0a9e0a4cfffc9a7c7df37d8300e9f79ad15b986f


@nginnever

ZEC: t1PGgRgVQ14utsD7mp2dzGdykTDFUCKzPQ5

BTC: 1A67XmfyukPNbrMmckBToE8xZPesuM6Ti1

ETH: 0x82a642cAFD6bFc228C7B5Ea0394A0Ad702A7c03D
