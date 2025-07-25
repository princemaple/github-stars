---
project: s3fs-fuse
stars: 9232
description: FUSE-based file system backed by Amazon S3
url: https://github.com/s3fs-fuse/s3fs-fuse
---

s3fs
====

s3fs allows Linux, macOS, and FreeBSD to mount an S3 bucket via FUSE(Filesystem in Userspace).  
s3fs makes you operate files and directories in S3 bucket like a local file system.  
s3fs preserves the native object format for files, allowing use of other tools like AWS CLI.

Features
--------

-   large subset of POSIX including reading/writing files, directories, symlinks, mode, uid/gid, and extended attributes
-   compatible with Amazon S3, and other S3-based object stores
-   allows random writes and appends
-   large files via multi-part upload
-   renames via server-side copy
-   optional server-side encryption
-   data integrity via MD5 hashes
-   in-memory metadata caching
-   local disk data caching
-   user-specified regions, including Amazon GovCloud
-   authenticate via v2 or v4 signatures

Installation
------------

Many systems provide pre-built packages:

-   Amazon Linux via EPEL:
    
    ```
    sudo amazon-linux-extras install epel
    sudo yum install s3fs-fuse
    ```
    
-   Arch Linux:
    
    ```
    sudo pacman -S s3fs-fuse
    ```
    
-   Debian 9 and Ubuntu 16.04 or newer:
    
    ```
    sudo apt install s3fs
    ```
    
-   Fedora 27 or newer:
    
    ```
    sudo dnf install s3fs-fuse
    ```
    
-   Gentoo:
    
    ```
    sudo emerge net-fs/s3fs
    ```
    
-   RHEL and CentOS 7 or newer via EPEL:
    
    ```
    sudo yum install epel-release
    sudo yum install s3fs-fuse
    ```
    
-   SUSE 12 and openSUSE 42.1 or newer:
    
    ```
    sudo zypper install s3fs
    ```
    
-   macOS 10.12 and newer via Homebrew:
    
    ```
    brew install --cask macfuse
    brew install gromgit/fuse/s3fs-mac
    ```
    
-   FreeBSD:
    
    ```
    pkg install fusefs-s3fs
    ```
    
-   Windows:
    
    Windows has its own install, seening in this link
    

Otherwise consult the compilation instructions.

Examples
--------

s3fs supports the standard AWS credentials file stored in `${HOME}/.aws/credentials`. Alternatively, s3fs supports a custom passwd file. Finally s3fs recognizes the `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, and `AWS_SESSION_TOKEN` environment variables.

The default location for the s3fs password file can be created:

-   using a `.passwd-s3fs` file in the users home directory (i.e. `${HOME}/.passwd-s3fs`)
-   using the system-wide `/etc/passwd-s3fs` file

Enter your credentials in a file `${HOME}/.passwd-s3fs` and set owner-only permissions:

```
echo ACCESS_KEY_ID:SECRET_ACCESS_KEY > ${HOME}/.passwd-s3fs
chmod 600 ${HOME}/.passwd-s3fs
```

Run s3fs with an existing bucket `mybucket` and directory `/path/to/mountpoint`:

```
s3fs mybucket /path/to/mountpoint -o passwd_file=${HOME}/.passwd-s3fs
```

If you encounter any errors, enable debug output:

```
s3fs mybucket /path/to/mountpoint -o passwd_file=${HOME}/.passwd-s3fs -o dbglevel=info -f -o curldbg
```

You can also mount on boot by entering the following line to `/etc/fstab`:

```
mybucket /path/to/mountpoint fuse.s3fs _netdev,allow_other 0 0
```

If you use s3fs with a non-Amazon S3 implementation, specify the URL and path-style requests:

```
s3fs mybucket /path/to/mountpoint -o passwd_file=${HOME}/.passwd-s3fs -o url=https://url.to.s3/ -o use_path_request_style
```

or(fstab)

```
mybucket /path/to/mountpoint fuse.s3fs _netdev,allow_other,use_path_request_style,url=https://url.to.s3/ 0 0
```

Note: You may also want to create the global credential file first

```
echo ACCESS_KEY_ID:SECRET_ACCESS_KEY > /etc/passwd-s3fs
chmod 600 /etc/passwd-s3fs
```

Note2: You may also need to make sure `netfs` service is start on boot

Limitations
-----------

Generally S3 cannot offer the same performance or semantics as a local file system. More specifically:

-   random writes or appends to files require rewriting the entire object, optimized with multi-part upload copy
-   metadata operations such as listing directories have poor performance due to network latency
-   non-AWS providers may have eventual consistency so reads can temporarily yield stale data (AWS offers read-after-write consistency since Dec 2020)
-   no atomic renames of files or directories
-   no coordination between multiple clients mounting the same bucket
-   no hard links
-   inotify detects only local modifications, not external ones by other clients or tools

References
----------

-   CSI for S3 - Kubernetes CSI driver
-   docker-s3fs-client - Docker image containing s3fs
-   goofys - similar to s3fs but has better performance and less POSIX compatibility
-   s3backer - mount an S3 bucket as a single file
-   S3Proxy - combine with s3fs to mount Backblaze B2, EMC Atmos, Microsoft Azure, and OpenStack Swift buckets
-   s3ql - similar to s3fs but uses its own object format
-   YAS3FS - similar to s3fs but uses SNS to allow multiple clients to mount a bucket

Frequently Asked Questions
--------------------------

-   FAQ wiki page
-   s3fs on Stack Overflow
-   s3fs on Server Fault

License
-------

Copyright (C) 2010 Randy Rizun rrizun@gmail.com

Licensed under the GNU GPL version 2
