# `scalehpa`: Easy way to scale your workload when keda is active

![Latest GitHub release](https://img.shields.io/github/release/sergiomacedo/scalehpa.svg)
![GitHub stars](https://img.shields.io/github/stars/sergiomacedo/scalehpa.svg?label=github%20stars)
![Proudly written in Bash](https://img.shields.io/badge/written%20in-bash-ff69b4.svg)

## What is `scalehpa`?

**scalehpa** is a tool to overcome a limitation seen in keda until version 2.8.x, where the keda controller will revert any attempt to scale the deployment to a value different from the `minReplicaCount` present on the `scaledobject`.

It's written in a way to execute the scale even if the deployment doesn't have scaledobjects defined, by calling the default `kubectl scale`.

### Examples

```sh
# scale a deployment on the default or current namespace
$ scalehpa deploy foo --replicas=3

# scale a statefulset on a specific namespace
$ scalehpa sts -r 3 foo -n bar
$ scalehpa statefulset foo -n bar -r 3
```
-----
## Installation

### Manual Installation (macOS and Linux)

Since `scalehpa` is written in Bash, you should be able to install them to any POSIX environment that has Bash installed.

- Download the `scalehpa` script.
- Either:
  - save them all to somewhere in your `PATH`,
  - or save them to a directory, then create symlinks to `scalehpa` from
    somewhere in your `PATH`, like `/usr/local/bin`
- Make `scalehpa` executable (`chmod +x ...`)

Example installation steps:

``` bash
sudo git clone https://github.com/sergiomacedo/scalehpa /opt/scalehpa
sudo ln -s /opt/scalehpa/scalehpa /usr/local/bin/scalehpa
```



- [manually (macOS & Linux)](#manual-installation-macos-and-linux)
