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
$ python3 ./pybeacon/metadata.py
raw AES key: d48a3a7104fc1754
raw HMAC key: 4d5a3752c6eeaed4
AES key: bca4caea1b3172aa979a5eac6c813184
HMAC key: 94b64efcf87b13c6828bcf14373bb2f9
ver: 10.0
host: 192.168.203.183
computer: DESKTOP-MRTTON7
user: admin
pid: 2560
id: 1605207936
barch: x86
is64: 1
charset: 1252
port: 0
raw AES key: 60b9dfe7b5806f01
raw HMAC key: 44adeddc44547b7e
AES key: 441bbd3de3d52997298a8625def8f40c
HMAC key: 1ede48669d4346c0b0cf2ca15e498c10
ver: 6.2
host: 172.16.229.131
computer: DESKTOP-MRTTON7
user: admin
pid: 6480
id: 29957
barch: x86
is64: 1

$ python3 ./pybeacon/tasks.py                                                                                                        1 ⨯
[*] Test decrypting a tasking from the server..
Counter: 1587768044
Output length: 19
Received task: DOWNLOAD_START
Arguments length: 11
Arguments: b'testing.txt'

[*] Test decrypting a download callback and modifying it..
Encrypted size: 80
Counter: 17
Output length: 46
Callback type: DOWNLOAD_START (2)
Fid: 4
Flen: 11
Filename: b'C:\\Users\\admin\\Desktop\\testing.txt'

$ python3 ./stager-decode.py -d 10.0.2.15 -o debug/beacon34v3.bin
[*] Index: 76
[*] Initial Key: 0x66c20f4e
[*] DLL Size: 213504
[+] Beacon decoded and written to: debug/beacon34v3.bin

$ python3 ./register.py -t 10.0.2.15 -u neo -c kali -i 1.2.3.4 -p 1 --pid 12345 -k MIG...IDAQAB -v3
raw AES key: 60b9dfe7b5806f01
raw HMAC key: 44adeddc44547b7e
AES key: 441bbd3de3d52997298a8625def8f40c
HMAC key: 1ede48669d4346c0b0cf2ca15e498c10
ver: 6.2
host: 1.2.3.4
computer: kali
user: neo
pid: 12345
id: 1069220239
barch: x86
is64: 1
Sending metadata blob: b'BSC...Sm9MXHG0='

$ python3 ./tasktool.py -v3 -a '441bbd3de3d52997298a8625def8f40c' -k '1ede48669d4346c0b0cf2ca15e498c10' download -f tasktool.py
Fid: 1674910815
Flen: 11
Filename: tasktool.py
Data size: 48
Data: b'AAAAMAFBkazERrI4XuH+r4xGTjEb2BnC4Ys9KujO0ykC4Ut4foPhIBR/aGR9iqL89K1sgw=='
```
