# eunomia-bpf: eBPF as a service

## Our target: Run <abbr title="Compile Once - Run Everywhere">CO-RE</abbr> eBPF function as a service

- Run `CO-RE` eBPF code without provisioning or managing infrastructure
- simply requests with a json and run `any` pre-compiled eBPF code on `any` kernel version
- very small and simple! Only a binary about `3MB`
- as fast as `100ms` to load and run a eBPF program
- `Distributed` and `decentralized`, No compile helper server

In general, we develop an approach to compile, transmit, and run most libbpf CO-RE objects with some user space config meta data to help us load and operator the eBPF byte code.

So, the only thing you need to do is focus on writing a single eBPF program in the kernel. We have a compiler here: [eunomia-cc](https://github.com/eunomia-bpf/eunomia-cc)

## Our function

we have these parts:

### An eunomia-bpf library

A wrapper of main functions of libbpf, some helper functions for user development.

- provide the ability to load eBPF code to the kernel and run it.
- Use some additional data to help load and config the eBPF bytecode.
- multiple language bindings

#### Install and Run

To install, just download and use the `binary`:

```bash
wget https://aka.pw/bpf-ecli -O ecli && chmod +x ecli
```

see [eunomia-bpf](eunomia-bpf) folder for details. With the library, we have provide [a simple cli](https://github.com/eunomia-bpf/eunomia-bpf/releases/), you can simply run pre-compiled eBPF data with a url or path, on most eBPF supported kernel versions:

```bash
sudo ./ecli run https://gitee.com/yunwei37/eunomia-bpf/raw/master/bpftools/examples/package.json
sudo ./ecli run bpftools/examples/package.json
sudo ./ecli server # run as a simple server
```

The cli tool can also run as a simple server to receive requests, or as a client to send requests to another server. see [doc/ecli-usage.md](doc/ecli-usage.md) for more usages.

### A compile toolchain for you to generate pre compiled eBPF data

The toolchain can be used as a docker to generate pre-compiled eBPF data in one command:

see the compile toolchains [eunomia-cc](https://github.com/eunomia-bpf/eunomia-cc) for details.

you can also simply use the [ebpm-template](https://github.com/eunomia-bpf/ebpm-template) repo as a template in github, just push to it and github action can help you compile CO-RE eBPF code!

### An eBPF package manager: ebpm

see <https://github.com/eunomia-bpf/ebpm> for details.

## Road-map

- [x] refactor the code from project `Eunomia` and provide quick examples
- [x] support `tracepoints`, `fentry`, `kprobe`, and ring buffer output in userspace.
- [x] make the compile easier to use, and more flexible. Don't need any code modified to compile.
- [ ] use lua for eBPF package load config and add more eBPF support
- [ ] support more eBPF program types:
- [ ] add more possibilities from `libbpf`
- [ ] provide python, go and others sdk
- [ ] add support of `etcd` and enhance server
- [ ] fix ci and docs, multi proto supports

## License

MIT LICENSE
