# picoCTF - Forensics Analysis

## Category

Forensics

## Description

A file containing a long stream of binary digits (`0` and `1`) was provided. The objective was to recover the hidden flag.

---

## Step 1: Convert Binary Data

The file consisted of binary digits. Each group of 8 bits represents one byte.

The binary data was converted back into raw bytes and saved as a file.

After reconstruction, the resulting file was named:

```text
output.jpg
```

---

## Step 2: Identify the File Type

Checking the file type:

```bash
file output.jpg
```

Output:

```text
output.jpg: PNG image data, 896 x 1152, 8-bit/color RGB, non-interlaced
```

Although the file was named `.jpg`, it was actually a PNG image.

Rename it:

```bash
mv output.jpg output.png
```

---

## Step 3: Additional Verification

Using Binwalk:

```bash
binwalk output.png
```

Output:

```text
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------
0             0x0             PNG image
41            0x29            Zlib compressed data
```

This confirmed that the recovered file was a valid PNG image.

---

## Step 4: Open the Image

```bash
feh output.png
```

The image displayed a hacker-themed illustration.

At the bottom of the image there was a hexadecimal string:

```text
7069636F4354467B666F72656E736963735F616E616C797369735F69735F616D617A696E675F35636363376362307D
```

---

## Step 5: Decode the Hex String

Convert the hexadecimal data to ASCII:

```bash
echo '7069636F4354467B666F72656E736963735F616E616C797369735F69735F616D617A696E675F35636363376362307D' | xxd -r -p
```

Output:

```text
picoCTF{forensics_analysis_is_amazing_5ccc7cb0}
```

---

## Flag

```text
picoCTF{forensics_analysis_is_amazing_5ccc7cb0}
```

## Tools Used

* Base64 decoding
* file
* binwalk
* feh
* xxd
