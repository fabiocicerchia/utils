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

## Notes

 - Freeze the requirements: `pip3 freeze > requirements.txt`
 - Install the requirements: `pip3 install -r requirements.txt`
