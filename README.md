# PyBeacon3

PyBeacon3 is a collection of scripts for dealing with Cobalt Strike's encrypted traffic.

It can encrypt/decrypt beacon metadata, as well as parse symmetric encrypted taskings

# Scripts included

There is a small library which includes encryption/decoding methods, however some example scripts are included.

* stager-decode.py - this tool will simply decode a beacon DLL from a stager URL (you can use it to extract the public key).
* register.py - this tool deals with RSA encrypted metadata and can register a new (fake) beacon on a target Teamserver.
* tasktool.py - this tool deals with AES encrypted taskings to/from the teamserver. Use it to send callbacks to the teamserver, or for decoding taskings from a Teamserver to the beacon.

# Original 

Just an adapted version for Python3 repo - https://github.com/nccgroup/pybeacon/

# Demo
```console
$ python3 ./stager-decode.py -d 10.0.2.15 -o debug/beacon34v3.bin
[*] Index: 76
[*] Initial Key: 0x66c20f4e
[*] DLL Size: 213504
[+] Beacon decoded and written to: debug/beacon34v3.bin
```
