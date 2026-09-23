# ONE-PIECE — Forensics CTF

> A forensic reconstruction of a steganography challenge.

## Case Overview

The challenge provided a single PNG file, `meme.png`, containing
multiple layers of hidden evidence.

The objective was not simply to locate a flag-shaped string. The
challenge deliberately introduced a decoy, requiring the evidence
to be validated and correlated before determining the genuine result.

### Investigation Workflow

Metadata Analysis
      ↓
LSB Steganography
      ↓
PNG Structure Validation
      ↓
Appended ZIP Discovery
      ↓
File Carving
      ↓
Archive Decryption
      ↓
Evidence Correlation

## Tools Used

- ExifTool
- zsteg
- pngcheck
- binwalk
- dd
- file
- unzip

## Investigation Summary

### 01 — Metadata Analysis
Inspection of the PNG metadata revealed a Base64-encoded comment.
After decoding, the message indicated that the password had already
been exposed somewhere in the evidence.

### 02 — LSB Analysis
LSB analysis revealed a flag-shaped value. Instead of immediately
accepting it as the solution, it was treated as a potential password
candidate based on the previous metadata clue.

### 03 — Structural Analysis
`pngcheck` reported additional data after the PNG IEND chunk.

Further analysis with `binwalk` identified an encrypted ZIP archive
embedded after the legitimate PNG data.

### 04 — File Carving
The archive was carved from the identified byte offset and validated
before extraction.

The password candidate recovered earlier successfully decrypted the
archive.

### 05 — Evidence Correlation
The recovered files contained separate pieces of evidence.

Using the challenge hint, the relevant fragments were correlated to
reconstruct the final result.

## Result

The recovered evidence was successfully correlated to reconstruct
the genuine challenge flag.

**Flag intentionally omitted from this README.**

The focus of this repository is the forensic methodology and
evidence-validation process rather than publishing the solution string.

## Key Takeaway

A recognizable signature is not proof.

One of the early false paths involved treating every apparent ZIP
signature discovered during steganographic analysis as a valid archive.
The investigation became reliable only after each extraction was
validated and supported by structural evidence.
