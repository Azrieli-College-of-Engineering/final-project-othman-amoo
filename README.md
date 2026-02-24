[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/Nt4zUlkt)

# OWASP Juice Shop - Symlink Attack Challenge

This project implements a new security challenge in OWASP Juice Shop: the **Symlink Attack**.

**Developed by:**
- Mohammad Othman, 211354931
- Ibrahim Amo, 213942972

## Overview
Participants must exploit a file upload vulnerability to access sensitive system files (specifically `data/static/users.yml`) by uploading a malicious ZIP archive containing a symbolic link.

## Implementation Highlights
- **Vulnerable Extraction**: The ZIP extraction logic in `routes/fileUpload.ts` has been modified to robustly handle (and incorrectly trust) symbolic links using the Central Directory metadata.
- **Challenge Verification**: A new verification middleware in `routes/verify.ts` monitors access to the uploaded symlinks and marks the challenge as solved when `users.yml` is successfully exposed.
- **Payload Automation**: A Python script is provided to generate symlink payloads.

## How to Run
1. Navigate to the `JUICE-SHOP` directory: `cd JUICE-SHOP`
2. Install dependencies: `npm install`
3. Start the application: `npm start`
4. Visit the application at: `http://localhost:3000`

## How to Test the Attack
1. **Generate the Payload**:
   Run the following command in the project root:
   ```bash
   python3 create_exploit.py
   ```
2. **Upload the Exploit**:
   - Login via any Juice Shop account.
   - Go to the **Complaint** form in Juice Shop.
   - Fill in the required fields and upload the generated `exploit.zip`.
4. **Verify Access**:
   - Navigate to `http://localhost:3000/complaints/exploit.md`.
   - The content of `users.yml` should be displayed.
5. **Solve Status**:
   - Check the **Score Board** to confirm the "Symlink Attack" challenge is marked as solved.

---
*Created as part of the Final Project for Azrieli College of Engineering.*
