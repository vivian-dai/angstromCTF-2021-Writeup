# Archaic

## Description

The archaeological team at ångstromCTF has uncovered an archive from over 100 years ago! Can you read the contents?

Access the file at /problems/2021/archaic/archive.tar.gz on the shell server.

## Hint

What is a .tar.gz file?

## Approach

I connected to the shell server to download the file locally using:

```bash
ssh shell.actf.co -l <teamname> cat "/problems/2021/archaic/archive.tar.gz" > archive.tar.gz
```

It prompted for the team password (which is found in the profile).

The hint suggests the file is actually a `.tar.gz` file but I decided to check anyways.

```bash
file archive.tar.gz
```

gave

```bash
archive.tar.gz: gzip compressed data, from Unix, original size modulo 2^32 10240
```

I used

```bash
gzip -d archive.tar.gz
```

which recovered the `archive.tar` file.

For whatever reason I was unable to untar the file in terminal (probably I'm just bad but shhhh). I used [7-Zip](https://www.7-zip.org/) to open `archive.tar` which contains `flag.txt`.

Alternatively, Python could also have been used (make sure script is in the same directory):

```python
import tarfile
tar = tarfile.open("archive.tar.gz")
tar.extractall()
tar.close()
```

## Flag

actf{thou_hast_uncovered_ye_ol_fleg}
