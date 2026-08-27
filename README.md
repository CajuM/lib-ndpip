# SlimTCP

SlimTCP is a lightweight, high-performance TCP/IP stack for reliable, in-order channels.

It was written to prove that stripping away some optional TCP features would improve performance.
It assumes that the underlying channel provides in-order reliable packet delivery.
An example of one such channel is Ultra Ethernet's ROD profile.

To this end it does not implement the following features, normally found on a stack running on the internet:
* Selective Acknowledgments
* Timestamps
* Protection Against Wrapped Sequence Numbers
* Congestion control
* Fast Re-transmit
* Re-order buffers

According to my benchmarks, it's twice as fast as mTCP and even more scaleable.
The benchmarks can be found at: https://github.com/CajuM/eqds-cloudlab

## Features

* Support for some packet loss through a minimal RTO timer
* Support for IPv4, no IPv6(for now)
* Static ARP tables, loaded through an API
* A UDP implementation, that unlike its TCP counterpart, is usable over the internet
* Support for Linux+DPDK
* Some left-over glue code for Unikraft support
* A POSIX-like sockets API
* A zero-copy RX and TX API
* An epoll-like API.

## Use-cases

* Applications running over TCP in a data-center, that **do connect to the internet**
* An AI training pipeline?
* A **fast** UDP implementation, that can be coupled with QUIC

## Building

It was built and tested with DPDK 23.11 on NixOS.
It also builds with DPKK 25.11 on Ubuntu 26.04 .

The dependencies can be installed on Ubuntu with:
```
apt-get install dpdk-dev gcc make pkg-config
```

As long as DPDK was installed at the default location, or is in PKG_CONFIG_PATH, the Makefile should find it.

To install it in `/usr`, run:
```
make -f Makefile.linux-dpdk
sudo make install -f Makefile.linux-dpdk
```

## Future plans

* Make it run over the internet while maintaining performance?
* A in-hypervisor stack?
* A Unikraft stack?

## Examples

A sample application can be found at: https://github.com/CajuM/eqds-cloudlab/tree/master/pkgs/libndpip-perf

## Referencing
```
@misc{caju2026slimtcpitsfastits,
      title={SlimTCP: It's fast, but not because it's slim},
      author={Mihai Drosi Caju and Costin Raiciu},
      year={2026},
      eprint={2608.25834},
      archivePrefix={arXiv},
      primaryClass={cs.NI},
      url={https://arxiv.org/abs/2608.25834},
}
```
