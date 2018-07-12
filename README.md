hashpipe
==========

Hashpipe is will transparenty create a file with a hash of the stream send to it
via stdin while outputting the same steam to stdout.

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
  -a {sha256, md4, md5, sha1, sha512, sha224, sha384}
                        The hash alogrtithm to be used, default sha256
  -b BUFFSIZE           Set the read buffer

Example Usage:
 tar -c /home | hashpipe -o /mnt/backup/backup.sha256 > /mnt/backup/home.tar
 cat /mnt/backup/backup.sha256
 sha256sum /mnt/backup/home.tar

Performance
-----------
Currently a 32k buffer is used for default. A 32768 or 65536 byte buffer seems
to perform equally well while smaller or larger ones are worse.
Depending on your architecture you might want to change this. 

Benchmark on a i7-3520M with an SSD and cached reads.
comparison: 
tar -c 3gb.iso | pv -rb > /dev/null
2.91GB [2.91GB/s]

command used:
tar -c 3gb.iso | ./hashpipe -o hash.txt -a $alogrithm | pv -rb > /dev/null

algorithm:
-a sha1:    2.91GB [ 487MB/s]
-a sha224:  2.91GB [ 215MB/s]
-a sha256:  2.91GB [ 211MB/s]
-a sha384:  2.91GB [ 324MB/s]
-a sha512:  2.91GB [ 314MB/s]
-a md5:     2,91GB [ 486MB/s]

License
-------

The scripts are released under the MIT License.  The license is
included on the file headers.  The MIT License is registered with
and approved by the Open Source Initiative [1].

[1] https://opensource.org/licenses/MIT
