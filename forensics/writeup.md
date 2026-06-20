# Disko 1 – PicoCTF Writeup

## Challenge

A compressed disk image named `disko-1.dd.gz` was provided. The objective was to recover the hidden flag.

## Analysis

First, identify the file type:

```bash
file disko-1.dd.gz
```

Output:

```text
disko-1.dd.gz: gzip compressed data, was "disko-1.dd"
```

The file is a gzip-compressed disk image, so extract it:

```bash
gunzip disko-1.dd.gz
```

This produces the raw disk image:

```text
disko-1.dd
```

Since flags are often stored as plaintext within forensic images, I searched the image for printable strings and filtered for the PicoCTF flag format:

```bash
strings disko-1.dd | grep -i 'pico'
```

Output:

```text
picoCTF{1t5_ju5t_4_5tr1n9_c63b02ef}
```

## Flag

```text
picoCTF{1t5_ju5t_4_5tr1n9_c63b02ef}
```

## Conclusion

This challenge did not require mounting the disk image or performing filesystem analysis. A simple `strings` search was enough to locate the flag directly within the raw disk image.
