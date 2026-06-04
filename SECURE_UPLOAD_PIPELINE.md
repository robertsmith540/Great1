# spareke Secure Image and Document Upload Pipeline

spareke will handle sensitive files such as:

- Vehicle documents
- Insurance policies
- Mechanic certificates
- Garage verification papers
- Business registration documents
- Product images
- Dispute evidence
- Service reports
- Award badge assets

This pipeline is designed to keep those files private and reduce malware risk.

## Routes

Secure upload UI:

```text
/documents/manage
```

Upload API:

```http
POST /api/uploads/secure
```

List uploads:

```http
GET /api/uploads/secure
```

Download clean private file:

```http
GET /api/uploads/:id/download
```

Existing metadata validation endpoint:

```http
POST /api/uploads/validate
```

## Database Model

```text
DocumentAsset
```

Fields include:

- ownerId
- purpose
- entityType/entityId
- originalName
- random storageKey
- MIME type
- file size
- SHA-256 checksum
- scan status
- visibility
- audit timestamps

## Security Controls Added

### 1. Private Storage

Files are stored outside the public web folder:

```text
storage/private_uploads/{userId}/{random-id}.ext
```

They are not directly accessible by URL.

### 2. Random File Names

Original filenames are not used as storage paths. The system generates a random UUID-based storage key.

### 3. Path Traversal Protection

Download and upload paths are resolved and checked to ensure they remain inside the private storage root.

### 4. File Type Allowlist

Allowed:

- JPG
- PNG
- WEBP
- PDF

Blocked:

- EXE
- BAT
- CMD
- SH
- APK
- MSI
- DMG
- JAR
- JS/MJS
- PHP
- Python/Ruby scripts

### 5. Magic-Byte Verification

The system checks file signatures, not just claimed browser MIME type.

### 6. Size Limit

Maximum size:

```text
8MB
```

### 7. Malware Heuristic Scan

Current MVP scanner blocks:

- EICAR test signature
- Script-like payload markers
- PDF JavaScript/OpenAction markers

### 8. Private Download Authorization

Only the owner or admin can download a clean file.

### 9. Audit Logging

Audit logs are created for:

- Secure upload creation
- Secure file download

## Production Upgrade

For production, replace local private storage with:

- S3-compatible object storage, or
- Firebase Storage, or
- Supabase Storage

Add:

- Signed upload URLs
- ClamAV or cloud malware scanning
- File byte MIME detection service
- Object quarantine bucket
- Document access logs
- Data retention policies
- Admin approval before public visibility

## Why This Matters

Vehicle and insurance documents are legally sensitive. Files must not be public by default, and dangerous uploads must be blocked before they can harm users or staff.
