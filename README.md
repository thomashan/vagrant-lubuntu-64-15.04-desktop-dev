# vagrant-lubuntu64-14.04

## Overview
This images contains lunbuntu 64-bit suitable for development work
It contains the following dev tools:
* sublime
* jenv (for java, sbt, scala, ant)
* sdkman (for gradle, grails)
* eclipse vX.X.X.X
* intellij vX.X.X.X
* ansible
* docker
* command line tools (yakuake, htop, curl, alien, libaio1)


It will mount guest@:/install-buck from host@:~/Downloads.
All the required software will be downloaded to guest@:/install-buck.


## Prerequisites
* Vagrant is installed
* cntlm is running on the host box if you're using the proxy


## Installation for the first time
1. > vagrant plugin install vagrant-proxyconf
2. > vagrant up [--proxy=true]

## Reload vagrant image after config change
1. > vagrant up
1. > vagrant provision
2. > vagrant reload
