# PicoCTF - Red Writeup

## Challenge Overview

The challenge provided a PNG image named `red.png`. When opened, the image appeared to be a completely red square with no visible clues or hidden text.

Since the challenge involved an image, I suspected steganography.

## Initial Enumeration

I started by running common file analysis tools:

```bash
file red.png
strings red.png
exiftool red.png
```

None of these tools revealed the flag or any useful metadata.

Since PNG files are commonly used in steganography challenges, I decided to use `zsteg`, a tool designed to detect hidden data in image bit planes.

## Using zsteg

I ran:

```bash
zsteg red.png
```

The output revealed hidden data encoded within the image's least significant bits. Among the results was a Base64-encoded string:

```text
cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==
```

## Decoding the Data

The extracted string appeared to be Base64 encoded. I decoded it using:

```bash
echo "cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==" | base64 -d
```

This produced:

```text
picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}
```

## Flag

```text
picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}
```

## Lessons Learned

This challenge demonstrates a common steganography technique where data is hidden in the least significant bits (LSBs) of image pixels. Even though the image appeared to be a solid red square, `zsteg` was able to detect and extract the concealed payload quickly.

For PNG steganography challenges, `zsteg` should be one of the first tools used during enumeration.
