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

## Key Takeaway

A recognizable signature is not proof.

One of the early false paths involved treating every apparent ZIP
signature discovered during steganographic analysis as a valid archive.
The investigation became reliable only after each extraction was
validated and supported by structural evidence.
