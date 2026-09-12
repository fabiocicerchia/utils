# Utils

## Requirements

 - Python3
 - Ghostscript

## Install

One liner:

```shell
wget -O - https://raw.githubusercontent.com/fabiocicerchia/utils/master/installer | sudo sh
```

## Tools

### `ago` - File Modification Age

```shell
$ ago FILE
3 days, 8:16:14 ago
```

### `benchmark` - Benchmark URL

```shell
$ benchmark URL
0.12345 sec
```

### `blink_port` - Blink NIC led

```shell
$ blink_port [NIC=eth0] [TIME=5]
```

### `cert_expire` - SSL/TLS Certificate Expiration

```shell
$ cert_expire DOMAIN
notBefore=May 20 11:55:41 2020 GMT
notAfter=Aug 12 11:55:41 2020 GMT
```

### `check_accessibility` - Check Accessibility

```shell
$ check_accessibility URL
CHECK ACCESSIBILITY
Validate Accessibility (BITV 1.0 - Level 2):
OK|FAIL
Validate Accessibility (Section 508):
OK|FAIL
Validate Accessibility (Stanca Act):
OK|FAIL
Validate Accessibility (WCAG 1.0 - Level AAA):
OK|FAIL
Validate Accessibility (WCAG 2.0 - Level AAA):
OK|FAIL
```

### `check_validation` - Check Validation

```shell
$ check_validation URL
CHECK VALIDATION
Validate W3C:
OK|FAIL
Validate CSS 3:
OK|FAIL
Validate CSS 2.1:
OK|FAIL
Validate CSS 2:
OK|FAIL
Validate CSS Mobile:
OK|FAIL
Validate Feed:
OK|FAIL
Validate HTTP Headers:
OK|FAIL
Validate Semantics:
OK|FAIL
Validate Links:
OK|FAIL
```

### `dotenv` - Export current env vars in .env file

```shell
$ eval `dotenv`
COLORTERM=truecolor
HOME=/home/user
LC_CTYPE=UTF-8
PAGER=less
PATH=/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/go/bin:PATH=$PATH:/opt/utils-master
PWD=/
SHELL=/bin/zsh
TERM=xterm-256color
...
```

```shell
$ dotenv > /dev/null
```

### `expose` - Expose Folder to HTTP port

```shell
$ expose [PORT=8080]
Serving HTTP on 0.0.0.0 port 8080 (http://0.0.0.0:8080/) ...
```

### `gen_passwd` - Generate Password

```shell
$ gen_passwd [LEN=16]
*******
```

### `git_change_date` - Git Change Date

```shell
$ git_change_date "Mon 08 Jun 2020 20:19:19 CET"
```

### `git_commit` - Git Commit Random Message

```shell
$ git_commit
```

### `ip_location` - IP Location

```shell
$ ip_location 123.123.123.123
Italy
IT
Rome
```

### `ip_public` - Public IP Address

```shell
$ ip_public
123.123.123.123
```

### `mac_random` - Random MAC Address

```shell
$ mac_random
86:ed:59:63:20:58
```

### `pdf_compress` - Compress PDF's size

```shell
$ pdf_compress FILE.PDF
```

### `retry` - Repeat Until Success

Runs the command until it exits zero. Without `-n` it retries forever.

```shell
$ retry [-n MAX] [-d DELAY=5] COMMAND [ARGS...]
```

### `server_specs` - Server Specs

```shell
$ server_specs
CPU: 4
RAM: 16384 MB
Swap: 2048 MB
Disk: 10Gi
Avg load: 1.53 1.87 1.91
IP Private: 192.168.0.2
IP Public: 123.123.123.123
Location: Italy
```

### `spider` - Launch a spider on a URL

```shell
$ spider URL [HTTP_AUTH_USER HTTP_AUTH_PASS]
...
```

### `spin_container` - Launch a temp docker container

```shell
$ spin_container IMAGE [TAG=latest]
```

### `stealth` - Disable Command History

```shell
$ stealth
```

### `timestamp` - Convert Timestamp

```shell
$ timestamp 1234567890
Fri Feb 13 15:26:30 EST 2009
```

### `todo_scan` - Pending Code Markers

Finds the `TODO`, `FIXME`, `HACK`, `XXX`, `BUG`, `KLUDGE`, `FIXIT`, `WIP` and
`TBD` markers left behind in a code base. `--all` adds the softer ones (`NOTE`,
`REVIEW`, `QUESTION`, `OPTIMIZE`, `REFACTOR`, `DEPRECATED`, `TEMP`).

Inside a git work tree the file list comes from git, so `.gitignore` is honoured
and vendored dependencies stay out of the report. Binaries, build output and
dot directories are skipped as well.

```shell
$ todo_scan [PATH...]
src/api.py:42: TODO wire up the retry budget
src/api.py:87: FIXME(fabio) off-by-one on the last page
src/cache.go:13: HACK sleep until the socket settles
todo_scan: 3 marker(s) in 2 file(s)
```

The count goes to stderr, so the findings stay pipeable. Markers are reported
with the author when written as `TODO(fabio):` or `TODO @fabio:`, and `--owner`
keeps only theirs:

```shell
$ todo_scan --owner fabio
src/api.py:87: FIXME(fabio) off-by-one on the last page
```

Counts per marker, rather than the findings themselves:

```shell
$ todo_scan --summary
TODO         12
FIXME        4
HACK         1
TOTAL        17
```

`--format json` and `--format csv` print the same findings for a ticket
importer, `--files` lists only the file names, and `--strict` exits `1` as soon
as a marker is found, to gate a build on it:

```shell
$ todo_scan --strict --marker FIXME,XXX src || echo "unfinished business"
```

### `wipe_free_space` - Overwrite Free Disk Space

Fills the filesystem with a large file and deletes it, so the blocks freed by
previously deleted files get overwritten. POSIX `sh`, so it runs under busybox
`ash` as well as bash — free space usually needs wiping inside a minimal
container image, which is where bash is not.

```shell
$ wipe_free_space [-r X] [-s]
  -r X   Number of rounds
  -s     Secure way (uses random instead of zero fillings)
Wiping...
ROUND #1 / 1
Progress : [########################################] 100%
Done
```

This fills the disk to 100% by design, so do not run it on a live system that
still needs to write anything.

It is also only meaningful on **spinning disks with no full-disk encryption**.
On an SSD the flash translation layer writes to fresh erase blocks and leaves
the old pages untouched in over-provisioned capacity you cannot address; under
LUKS/BitLocker the free blocks are already unreadable ciphertext; on btrfs/ZFS
copy-on-write allocates elsewhere and snapshots keep the old data referenced;
on a cloud volume the data lives in the snapshot chain and filling the guest
just inflates a thin-provisioned disk you then pay for. In those cases use
`fstrim -av`, `blkdiscard`, `nvme format --ses=1`, `cryptsetup luksErase`, or
delete the snapshots — not this.

## Credits

`ago` and `retry` are independent rewrites of ideas from
[skx/sysadmin-util](https://github.com/skx/sysadmin-util) (archived, Artistic
License / GPL-2.0-or-later). No code was copied from it.

`wipe_free_space` started life as
[fabiocicerchia/wipe-free-space](https://github.com/fabiocicerchia/wipe-free-space)
on 2020-02-20 (MIT), now archived and folded in here. The idea is from
[David Spillett](https://superuser.com/users/4129/david-spillett)'s answer to
[How to wipe free disk space in Linux?](https://superuser.com/a/19488).

## Notes

 - Freeze the requirements: `pip3 freeze > requirements.txt`
 - Install the requirements: `pip3 install -r requirements.txt`
