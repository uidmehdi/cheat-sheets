# Yum Cheat Sheet

Yum (Yellow Dog Updater, Modified), is the package manager used on RPM (RedHat Package Manager) based Linux systems. 
It is an interactive, rpm based, package manager. It can automatically perform system updates, including dependency analysis and obsolete processing based on "repository" metadata. It can also perform installation of new packages, removal of old packages and perform queries on the installed and/or available packages among many other commands/services (see below). yum is similar to other high level package managers like apt-get and smart.

## Table of Contents
* [Getting Help](#getting-help)
* [Update](#update)
* [Repositories](#repositories)
* [List, Search, Info](#list-search-info)
* [Install & Remove Packages](#install-remove-packages)
* [History](#history)
* [Clean](#clean)
* [General Options](#general-options)
* [Related Files](#related-files)

## Getting Help

**To get help about yum command and it's options:**

```
$ man yum
$ yum help
$ yum help install
$ yum help erase
```

## Update

Yum is able to Update the whole system, an individual package or even downgrade the package to an earlier version.

#### Check the whole system for available updates:
`$ sudo yum check-update`

#### Update the whole packages to the latest version:
`$ sudo yum update`

#### Apply only security related updates:
`$ sudo yum update --security`

#### Update an individual package:
`$ sudo yum update <packagename>`

#### Update all packages in a group:
`$ sudo yum groupupdate <Group Name>`

#### Update an individual package to an specific version:

 1. Query available versions of package: `$ yum --showduplicates list <packagename>`
 2. Update to desired version: `$ sudo yum update-to <packagename-version>`

#### Update a package from a specific repository: *RHEL/CentOS 7*
`$ sudo yum repo-pkgs <repo id> upgrade <package-name>`

## Repositories

#### Enable/Disable a repository:

 1. Find the repository related `.repo` file in `/etc/yum.repos.d/` or it's related section in `/etc/yum.conf`.
 2. Set `enabled=1` to enable or `enabled=0` to disable the repository.

#### Add a repostiry:
Add a `[repository]` section to the `/etc/yum.conf` file, or to a `.repo` file in the `/etc/yum.repos.d/` directory.

#### Remove a repostiry:
Remove a `[repository]` section to the `/etc/yum.conf` file, or to a `.repo` file in the `/etc/yum.repos.d/` directory.

#### Display enabled repositories:
`$ yum repolist`

#### Display all enabled/disabled repositories:
`$ yum repolist all`

#### Get information about repositories: *RHEL/CentOS 7*
```
$ yum repoinfo
$ yum repoinfo <repo-id>
```

#### List all packages in the specified repository: *RHEL/CentOS 7*
`$ yum repo-pkgs <repo id> list`

#### Download yum repository data to cache:
`$ yum makecache`

## List, Search, Info

#### List all installed and available Install packages:
`$ yum list`
`$ yum list all`

#### List all installed packages:
`$ yum list installed`

#### List all available Install packages:
`$ yum list available`

#### List installed and available kernel packages
`$ yum list kernel`

#### Check if a package is installed:
`$ yum list installed <packagename>`

#### List all available groups:
`$ yum grouplist`

#### List dependencies of a package:
`$ yum deplist <package-name>`

#### Search packages by name:
```
$ yum search <string>
$ yum search <packagename>
```

#### Find packages that provide the queried file:
```
$ yum provides <string>
$ yum provides <foldername/filename>
$ yum provides <filename>
```

#### Display information about a package:
`$ yum info <packagename>`

#### Display description and contents of a package group:
`$ yum groupinfo <group name>`


## Install & Remove Packages

#### Install a package from repository:
`$ sudo yum install <packagename>`
`$ sudo yum install <packagename1> <packagename2>`

#### Install an rpm package:
```
$ sudo yum localinstall packagename.rpm
$ sudo yum localinstall http://myrepo.org/packagename.rpm
```

#### Install a package from a specific disabled repository:
`$ sudo yum --enablerepo=<repo id> install <package-name>`

#### Install all packages in a group:
`$ sudo yum groupinstall <Group Name>`

#### Install a package from a specific repository: *RHEL/CentOS 7*
`$ sudo yum repo-pkgs <repo id> install <package-name>`

#### Install all package from a specific repository:
`$ sudo yum repo-pkgs <repo id> install`

#### Remove an installed package:
`$ sudo yum remove <packagename>`
`$ sudo yum remove <packagename1> <packagename2>`

#### Reinstall a package that will replace any deleted files:
`$ sudo yum reinstall <packagename>`

#### Remove all packages in a group:
`$ sudo yum groupremove <Group Name>`

#### Remove one package and install another:
`$ sudo yum swap <package-to-remove> <package-to-install>`

#### Remove un-needed packages and dependencies: *RHEL/CentOS 7*
`$ sudo yum autoremove`

#### Remove a package installed from a specific repository: *RHEL/CentOS 7*
`$ sudo yum repo-pkgs <repo id> remove <package-name>`

#### Remove all packages installed from a specific repository: *RHEL/CentOS 7*
`$ sudo yum repo-pkgs <repo id> remove`

## History
#### View all the past transactions of yum command:
`$ sudo yum history`
`$ sudo yum history list`

#### Show details of yum transaction ID:
`$ sudo yum history info <ID>`

#### Undo the yum action from transaction ID:
`$ sudo yum history undo <ID>`

#### Redo the undone yum action from transaction ID:
`$ sudo yum history redo <ID>`

## Clean
#### Clear out cached package data:
`$ sudo yum clean all`

#### Delete packages saved in cache:
`$ sudo yum clean packages`

## General Options

 * `-y` Assume that the answer to any question  which  would be asked is yes.
 * `--assumeno` Assume that the answer to any question which would be asked is no.
 * `-q` Run without output.  Note that you likely also want to use -y.
 * `-v` Run with a lot of debugging output.
 * `--showduplicates` Doesn’t limit packages to their latest versions in the info, list and search commands
 * `--enablerepo` Enable currently disabled repo for a single command
 * `--disablerepo` Disable currently enabled repo for a single command
 * `--downloadonly` Don’t update, just download to `/var/cache/yum/arch/prod/repo/packages/`
 * `--changelog` Display changelog information of package

## Related Files
```
/etc/yum.conf
/etc/yum/version-groups.conf
/etc/yum.repos.d/
/etc/yum/pluginconf.d/
/var/cache/yum/
```
