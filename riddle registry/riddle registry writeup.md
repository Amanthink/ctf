# picoCTF - Confidential

## Category

Forensics

## Description

We are given a PDF file named `confidential.pdf`. The goal is to find the hidden flag.

---

## Initial Inspection

First, identify the file type:

```bash
file confidential.pdf
```

Output:

```text
confidential.pdf: PDF document, version 1.7
```

The PDF opens normally and does not visibly contain a flag.

---

## Extracting Strings

A common forensic technique is to inspect printable strings inside the file:

```bash
strings confidential.pdf
```

Among the output, an interesting metadata field appears:

```text
/Producer (PyPDF2)
/Author (cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9lZTQ1NDk1MH0=)
```

The Author value looks like Base64.

---

## Using ExifTool

PDF metadata can be viewed more cleanly with ExifTool:

```bash
exiftool confidential.pdf
```

Output:

```text
Producer : PyPDF2
Author   : cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9lZTQ1NDk1MH0=
```

The Author field contains the same Base64 string.

---

## Decoding the Metadata

Decode the Base64 value:

```bash
echo 'cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9lZTQ1NDk1MH0=' | base64 -d
```

Output:

```text
picoCTF{puzzl3d_m3tadata_f0und!_ee454950}
```

---

## Flag

```text
picoCTF{puzzl3d_m3tadata_f0und!_ee454950}
```

---

## Key Takeaway

Metadata is often overlooked during forensic analysis. Tools such as:

* `strings`
* `exiftool`
* `pdfinfo`

can reveal hidden information stored in document properties without needing to inspect the document's visible contents.
