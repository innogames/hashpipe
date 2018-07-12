hashpipe
==========

Hashpipe is will transparenty create a file with a hash of the stream send to it
via stdin while outputting the same steam to stdout.

Currently a 32k buffer is used, depending on your architecture you might want
to raise this. At the moment the difference for sha256 was 170MB/s whitout 
hashpipe vs. 125MB/s with hashpipe on a i7-3520M with an SSD and cached reads.

Language
--------
The scripts should run on Python 3 and later.
The set of supported algorothms depends on your hashlib -h will give you the
hash algorithms supported on your system.

Usage
-----
Use like a pipe, get the hash in a file

optional arguments:
  -h, --help            show this help message and exit
  -o FILENAME           The file where the hash is written to
  -a {sha256,SHA1,md4,dsaWithSHA,SHA256,ripemd160,sha,SHA512,DSA-SHA,SHA384,\
        MD5,md5,sha1,whirlpool,sha512,ecdsa-with-SHA1,DSA,MD4,SHA224,RIPEMD160,\
        sha224,sha384,dsaEncryption,SHA}
                        The hash alogrtithm to be used, default sha256
  -b BUFFSIZE           Set the read buffer

Example Usage:
 tar -c /home | hashpipe -o /mnt/backup/backup.sha256 > /mnt/backup/home.tar
 cat /mnt/backup/backup.sha256
 sha256sum /mnt/backup/home.tar

License
-------

The scripts are released under the MIT License.  The license is
included on the file headers.  The MIT License is registered with
and approved by the Open Source Initiative [1].

[1] https://opensource.org/licenses/MIT
