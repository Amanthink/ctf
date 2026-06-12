# picoCTF - hideme

## Category
Forensics

## Description

We are given a JPEG image named `img.jpg`. The objective is to recover the hidden flag.

---

## Step 1: Examine Metadata

A common first step in image forensics is checking metadata.

```bash
exiftool img.jpg
```

Output:

```text
Comment : c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9
```

The comment looks like Base64.

---

## Step 2: Decode the Comment

Decode the string:

```bash
echo 'c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9' | base64 -d
```

Output:

```text
steghide:cEF6endvcmQ=
```

The second part also appears to be Base64 encoded.

Decode it:

```bash
echo 'cEF6endvcmQ=' | base64 -d
```

Output:

```text
pAzzword
```

This suggests that `pAzzword` may be the password for a steganography tool.

---

## Step 3: Extract Hidden Data

Since the hint explicitly references **steghide**, try extracting embedded data:

```bash
steghide extract -sf img.jpg
```

Enter the passphrase:

```text
pAzzword
```

Steghide successfully extracts a file:

```text
wrote extracted data to "flag.txt"
```

---

## Step 4: Read the Extracted File

```bash
cat flag.txt
```

Output:

```text
picoCTF{h1dd3n_1n_1m4g3_54e31417}
```

---

## Flag

```text
picoCTF{h1dd3n_1n_1m4g3_54e31417}
```

---

## Lessons Learned

- Always inspect image metadata using `exiftool`.
- Base64-encoded strings are common hints in forensic challenges.
- References to tools such as `steghide` often indicate the intended extraction method.
- Hidden files can be embedded directly inside images and recovered with the correct passphrase.

## Tools Used

- exiftool
- base64
- steghide
- cat
