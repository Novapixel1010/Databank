# what is this ?

First this mostly is still minio when it was apache 2.0 license. The plan is to rebrand it and keep the apache 2.0 license. 👇 To do list 👇

[ ] add docs
[ ] make sure software is stable


# Databank Quickstart Guide


# Docker Installation

Use the following commands to run a standalone MinIO server on a Docker container.

Standalone MinIO servers are best suited for early development and evaluation. Certain features such as versioning, object locking, and bucket replication
require distributed deploying MinIO with Erasure Coding. For extended development and production, deploy MinIO with Erasure Coding enabled - specifically,
with a *minimum* of 4 drives per MinIO server. See [MinIO Erasure Code Quickstart Guide](https://docs.min.io/docs/minio-erasure-code-quickstart-guide.html)
for more complete documentation.

## Stable

Run the following command to run the latest stable image of MinIO on a Docker container using an ephemeral data volume:

```sh
docker run -p 9000:9000 minio/minio server /data
```

The MinIO deployment starts using default root credentials `minioadmin:minioadmin`. You can test the deployment using the MinIO Browser, an embedded
web-based object browser built into MinIO Server. Point a web browser running on the host machine to http://127.0.0.1:9000 and log in with the
root credentials. You can use the Browser to create buckets, upload objects, and browse the contents of the MinIO server.

You can also connect using any S3-compatible tool, such as the MinIO Client `mc` commandline tool. See
[Test using MinIO Client `mc`](#test-using-minio-client-mc) for more information on using the `mc` commandline tool. For application developers,
see https://docs.min.io/docs/ and click **MINIO SDKS** in the navigation to view MinIO SDKs for supported languages.


> NOTE: To deploy MinIO on Docker with persistent storage, you must map local persistent directories from the host OS to the container using the
  `docker -v` option. For example, `-v /mnt/data:/data` maps the host OS drive at `/mnt/data` to `/data` on the Docker container.



## Binary Download

Use the following command to download and run a standalone MinIO server on macOS. Replace ``/data`` with the path to the drive or directory in which you want MinIO to store data.

```sh
wget https://dl.min.io/server/minio/release/darwin-amd64/minio
chmod +x minio
./minio server /data
```

The MinIO deployment starts using default root credentials `minioadmin:minioadmin`. You can test the deployment using the MinIO Browser, an embedded
web-based object browser built into MinIO Server. Point a web browser running on the host machine to http://127.0.0.1:9000 and log in with the
root credentials. You can use the Browser to create buckets, upload objects, and browse the contents of the MinIO server.

You can also connect using any S3-compatible tool, such as the MinIO Client `mc` commandline tool. See
[Test using MinIO Client `mc`](#test-using-minio-client-mc) for more information on using the `mc` commandline tool. For application developers,
see https://docs.min.io/docs/ and click **MINIO SDKS** in the navigation to view MinIO SDKs for supported languages.


# GNU/Linux

Use the following command to run a standalone MinIO server on Linux hosts running 64-bit Intel/AMD architectures. Replace ``/data`` with the path to the drive or directory in which you want MinIO to store data.

```sh
wget https://dl.min.io/server/minio/release/linux-amd64/minio
chmod +x minio
./minio server /data
```

Replace ``/data`` with the path to the drive or directory in which you want MinIO to store data.

The following table lists supported architectures. Replace the `wget` URL with the architecture for your Linux host.

| Architecture                   | URL                                                        |
| --------                       | ------                                                     |
| 64-bit Intel/AMD               | https://dl.min.io/server/minio/release/linux-amd64/minio   |
| 64-bit ARM                     | https://dl.min.io/server/minio/release/linux-arm64/minio   |
| 64-bit PowerPC LE (ppc64le)    | https://dl.min.io/server/minio/release/linux-ppc64le/minio |
| IBM Z-Series (S390X)           | https://dl.min.io/server/minio/release/linux-s390x/minio   |

The MinIO deployment starts using default root credentials `minioadmin:minioadmin`. You can test the deployment using the MinIO Browser, an embedded
web-based object browser built into MinIO Server. Point a web browser running on the host machine to http://127.0.0.1:9000 and log in with the
root credentials. You can use the Browser to create buckets, upload objects, and browse the contents of the MinIO server.

You can also connect using any S3-compatible tool, such as the MinIO Client `mc` commandline tool. See
[Test using MinIO Client `mc`](#test-using-minio-client-mc) for more information on using the `mc` commandline tool. For application developers,
see https://docs.min.io/docs/ and click **MINIO SDKS** in the navigation to view MinIO SDKs for supported languages.


> NOTE: Standalone MinIO servers are best suited for early development and evaluation. Certain features such as versioning, object locking, and bucket replication
require distributed deploying MinIO with Erasure Coding. For extended development and production, deploy MinIO with Erasure Coding enabled - specifically,
with a *minimum* of 4 drives per MinIO server. See [MinIO Erasure Code Quickstart Guide](https://docs.min.io/docs/minio-erasure-code-quickstart-guide.html)
for more complete documentation.

# Install from Source

Use the following commands to compile and run a standalone MinIO server from source. Source installation is only intended for developers and advanced users. If you do not have a working Golang environment, please follow [How to install Golang](https://golang.org/doc/install). Minimum version required is [go1.16](https://golang.org/dl/#stable)

```sh
GO111MODULE=on go get github.com/minio/minio
```

The MinIO deployment starts using default root credentials `minioadmin:minioadmin`. You can test the deployment using the MinIO Browser, an embedded
web-based object browser built into MinIO Server. Point a web browser running on the host machine to http://127.0.0.1:9000 and log in with the
root credentials. You can use the Browser to create buckets, upload objects, and browse the contents of the MinIO server.

You can also connect using any S3-compatible tool, such as the MinIO Client `mc` commandline tool. See
[Test using MinIO Client `mc`](#test-using-minio-client-mc) for more information on using the `mc` commandline tool. For application developers,
see https://docs.min.io/docs/ and click **MINIO SDKS** in the navigation to view MinIO SDKs for supported languages.


> NOTE: Standalone MinIO servers are best suited for early development and evaluation. Certain features such as versioning, object locking, and bucket replication
require distributed deploying MinIO with Erasure Coding. For extended development and production, deploy MinIO with Erasure Coding enabled - specifically,
with a *minimum* of 4 drives per MinIO server. See [MinIO Erasure Code Quickstart Guide](https://docs.min.io/docs/minio-erasure-code-quickstart-guide.html)
for more complete documentation.

MinIO strongly recommends *against* using compiled-from-source MinIO servers for production environments.

# Deployment Recommendations

## Allow port access for Firewalls

By default MinIO uses the port 9000 to listen for incoming connections. If your platform blocks the port by default, you may need to enable access to the port.

### ufw

For hosts with ufw enabled (Debian based distros), you can use `ufw` command to allow traffic to specific ports. Use below command to allow access to port 9000

```sh
ufw allow 9000
```

Below command enables all incoming traffic to ports ranging from 9000 to 9010.

```sh
ufw allow 9000:9010/tcp
```

### iptables

For hosts with iptables enabled (RHEL, CentOS, etc), you can use `iptables` command to enable all traffic coming to specific ports. Use below command to allow
access to port 9000

```sh
iptables -A INPUT -p tcp --dport 9000 -j ACCEPT
service iptables restart
```

Below command enables all incoming traffic to ports ranging from 9000 to 9010.

```sh
iptables -A INPUT -p tcp --dport 9000:9010 -j ACCEPT
service iptables restart
```

## Pre-existing data
When deployed on a single drive, MinIO server lets clients access any pre-existing data in the data directory. For example, if MinIO is started with the command  `minio server /mnt/data`, any pre-existing data in the `/mnt/data` directory would be accessible to the clients.

The above statement is also valid for all gateway backends.

# Test MinIO Connectivity

## Test using MinIO Browser
MinIO Server comes with an embedded web based object browser. Point your web browser to http://127.0.0.1:9000 to ensure your server has started successfully.

![Screenshot](https://github.com/minio/minio/blob/master/docs/screenshots/minio-browser.png?raw=true)

## Test using MinIO Client `mc`
`mc` provides a modern alternative to UNIX commands like ls, cat, cp, mirror, diff etc. It supports filesystems and Amazon S3 compatible cloud storage services. Follow the MinIO Client [Quickstart Guide](https://docs.min.io/docs/minio-client-quickstart-guide) for further instructions.

# Upgrading MinIO
MinIO server supports rolling upgrades, i.e. you can update one MinIO instance at a time in a distributed cluster. This allows upgrades with no downtime. Upgrades can be done manually by replacing the binary with the latest release and restarting all servers in a rolling fashion. However, we recommend all our users to use [`mc admin update`](https://docs.min.io/docs/minio-admin-complete-guide.html#update) from the client. This will update all the nodes in the cluster simultaneously and restart them, as shown in the following command from the MinIO client (mc):

```
mc admin update <minio alias, e.g., myminio>
```

> NOTE: some releases might not allow rolling upgrades, this is always called out in the release notes and it is generally advised to read release notes before upgrading. In such a situation `mc admin update` is the recommended upgrading mechanism to upgrade all servers at once.

## Important things to remember during MinIO upgrades

- `mc admin update` will only work if the user running MinIO has write access to the parent directory where the binary is located, for example if the current binary is at `/usr/local/bin/minio`, you would need write access to `/usr/local/bin`.
- `mc admin update` updates and restarts all servers simultaneously, applications would retry and continue their respective operations upon upgrade.
- `mc admin update` is disabled in kubernetes/container environments, container environments provide their own mechanisms to rollout of updates.
- In the case of federated setups `mc admin update` should be run against each cluster individually. Avoid updating `mc` to any new releases until all clusters have been successfully updated.
- If using `kes` as KMS with MinIO, just replace the binary and restart `kes` more information about `kes` can be found [here](https://github.com/minio/kes/wiki)
- If using Vault as KMS with MinIO, ensure you have followed the Vault upgrade procedure outlined here: https://www.vaultproject.io/docs/upgrading/index.html
- If using etcd with MinIO for the federation, ensure you have followed the etcd upgrade procedure outlined here: https://github.com/etcd-io/etcd/blob/master/Documentation/upgrades/upgrading-etcd.md

# Contribute to MinIO Project
Please follow MinIO [Contributor's Guide](https://github.com/Novapixel1010/Databank/blob/master/CONTRIBUTING.md)

# License
Use of Databank is governed by the Apache 2.0 License found at [LICENSE](https://github.com/Novapixel1010/Databank/blob/master/LICENSE).
