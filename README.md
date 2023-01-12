# `scalehpa`: Easy way to scale your workload when keda is active

![Latest GitHub release](https://img.shields.io/github/release/sergiomacedo/scalehpa.svg)
![GitHub stars](https://img.shields.io/github/stars/sergiomacedo/scalehpa.svg?label=github%20stars)
![Proudly written in Bash](https://img.shields.io/badge/written%20in-bash-ff69b4.svg)

## What is `scalehpa`?

**scalehpa** is a tool to overcome a limitation seen in keda until version 2.8.x, where the keda controller will revert any attempt to scale the deployment to a value different from the `minReplicaCount` present on the `scaledobject`.

It's written in a way to execute the scale even if the deployment doesn't have scaledobjects defined, by calling the default `kubectl scale`.

### Examples

```sh
Set a new size for a deployment or a statefulset when keda is installed.

Examples:
# Set a minimum number of replicas for the deployment on the default or current namespace
# This will set the minReplicas to 3 and keep HPA active
scalehpa deploy foo --replicas=3
scalehpa deploy foo -r 3

# This will set the maxReplicas to 10 and keep HPA active
scalehpa deploy foo --maxreplicas=10
scalehpa deploy foo -m 10

# This will set the minReplicas to 10, maxReplicas to 20 and keep HPA active
scalehpa deploy foo -r 10 -m 20

# scale a deployment on the default or current namespace and DISABLE HPA
# This will create a fixed set of 3 replicas, disabling autoscale
# To reenable HPA, use the --replicas option
scalehpa deploy foo --freeze=3

# scale a statefulset on a specific namespace
scalehpa sts -r 3 foo -n bar
scalehpa statefulset foo -n bar -r 3

# show this message
scalehpa -h,--help
```
-----
## Installation
### Installing as a krew plugin

```sh
$ kubectl krew index add scalehpa https://github.com/sergiomacedo/scalehpa.git
$ kubectl krew install scalehpa/scalehpa
$ kubectl scalehpa 
Set a new size for a deployment or a statefulset when keda is installed.

Examples:
# Set a minimum number of replicas for the deployment on the default or current namespace
# This will set the minReplicas to 3 and keep HPA active
kubectl scalehpa deploy foo --replicas=3
kubectl scalehpa deploy foo -r 3

# This will set the maxReplicas to 10 and keep HPA active
kubectl scalehpa deploy foo --maxreplicas=10
kubectl scalehpa deploy foo -m 10

# This will set the minReplicas to 10, maxReplicas to 20 and keep HPA active
kubectl scalehpa deploy foo -r 10 -m 20

# scale a deployment on the default or current namespace and DISABLE HPA
# This will create a fixed set of 3 replicas, disabling autoscale
# To reenable HPA, use the --replicas option
kubectl scalehpa deploy foo --freeze=3

# scale a statefulset on a specific namespace
kubectl scalehpa sts -r 3 foo -n bar
kubectl scalehpa statefulset foo -n bar -r 3

# show this message
kubectl scalehpa -h,--help
```


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
