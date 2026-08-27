# SlimTCP

SlimTCP is a lightweight TCP/IP stack, written from scratch, meant to run on reliable in-order channels, such as Ultra Ethernet's ROD profile.
It was written to prove that stripping away some optional TCP features would make it faster. 
According to my benchmarks, it's twice as fast as mTCP and even more scaleable.

They can be found at: https://github.com/CajuM/eqds-cloudlab

To this end it does not implement the following features, normally found on a stack running on the internet:
* Selective Acknowledgments
* Timestamps
* Protection Against Wrapped Sequence Numbers
* Congestion control
* Fast Re-transmit
* Re-order buffers

In order to support some packet loss, it implements a minimal RTO timer.

It presently supports, only, IPv4.

It also has UDP support, that unlike its TCP implementation, is usable over the internet.

Originally, it was meant to run on Unikraft, with some bits of glue-code still present. 

Right now, it only runs on DPDK.

It supports a POSIX-like sockets API, a zero-copy RX and TX API, as well as an epoll-like API.

It requires one dedicated core to run the DPDK workhorse thread.

It only runs on Linux.

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
