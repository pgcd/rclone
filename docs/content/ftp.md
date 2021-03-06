---
title: "FTP"
description: "Rclone docs for FTP backend"
date: "2017-01-01"
---

<i class="fa fa-file"></i> FTP
------------------------------

FTP is the File Transfer Protocol. FTP support is provided using the
[github.com/jlaffaye/ftp](https://godoc.org/github.com/jlaffaye/ftp)
package.

Here is an example of making an FTP configuration.  First run

    rclone config

This will guide you through an interactive setup process. An FTP remote only
needs a host together with and a username and a password. With anonymous FTP
server, you will need to use `anonymous` as username and your email address as
the password.

```
No remotes found - make a new one
n) New remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
n/r/c/s/q> n
name> remote
Type of storage to configure.
Choose a number from below, or type in your own value
 1 / Amazon Drive
   \ "amazon cloud drive"
 2 / Amazon S3 (also Dreamhost, Ceph, Minio)
   \ "s3"
 3 / Backblaze B2
   \ "b2"
 4 / Dropbox
   \ "dropbox"
 5 / Encrypt/Decrypt a remote
   \ "crypt"
 6 / FTP Connection 
   \ "ftp"
 7 / Google Cloud Storage (this is not Google Drive)
   \ "google cloud storage"
 8 / Google Drive
   \ "drive"
 9 / Hubic
   \ "hubic"
10 / Local Disk
   \ "local"
11 / Microsoft OneDrive
   \ "onedrive"
12 / Openstack Swift (Rackspace Cloud Files, Memset Memstore, OVH)
   \ "swift"
13 / SSH/SFTP Connection
   \ "sftp"
14 / Yandex Disk
   \ "yandex"
Storage> ftp
FTP host to connect to
Choose a number from below, or type in your own value
 1 / Connect to ftp.example.com
   \ "ftp.example.com"
host> ftp.example.com
FTP username, leave blank for current username, ncw
user>
FTP port, leave blank to use default (21)
port>
FTP password
y) Yes type in my own password
g) Generate random password
y/g> y
Enter the password:
password:
Confirm the password:
password:
Remote config
--------------------
[remote]
host = ftp.example.com
user = 
port =
pass = *** ENCRYPTED ***
--------------------
y) Yes this is OK
e) Edit this remote
d) Delete this remote
y/e/d> y
```

This remote is called `remote` and can now be used like this

See all directories in the home directory

    rclone lsd remote:

Make a new directory

    rclone mkdir remote:path/to/directory

List the contents of a directory

    rclone ls remote:path/to/directory

Sync `/home/local/directory` to the remote directory, deleting any
excess files in the directory.

    rclone sync /home/local/directory remote:directory

### Modified time ###

FTP does not support modified times.  Any times you see on the server
will be time of upload.

### Checksums ###

FTP does not support any checksums.

### Limitations ###

Note that since FTP isn't HTTP based the following flags don't work
with it: `--dump-headers`, `--dump-bodies`, `--dump-auth`

Note that `--timeout` isn't supported (but `--contimeout` is).

FTP could support server side move but doesn't yet.
