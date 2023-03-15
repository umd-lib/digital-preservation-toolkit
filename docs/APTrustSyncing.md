
# APTrust Syncing

## Context

This is the algorithm for retrieving metadata from the APTrust cloud storage and
adding as locations in the patsy database. The following is the object and file
metadata obtained from using the APTrust API. These are the two we use in the program
but there are more metadata the API can retrieve.

## Representation

### Objects

```json
{
  "id": 0,
  "title": "string",
  "description": "string",
  "identifier": "string",
  "alt_identifier": "string",
  "access": "consortia",
  "bag_name": "string",
  "institution_id": 0,
  "created_at": "2023-02-06T19:35:59.102Z",
  "updated_at": "2023-02-06T19:35:59.102Z",
  "state": "A",
  "etag": "string",
  "bag_group_identifier": "string",
  "storage_option": "Glacier-Deep-OH",
  "bagit_profile_identifier": "https://github.com/dpscollaborative/btr_bagit_profile/releases/download/1.0/btr-bagit-profile.json",
  "source_organization": "string",
  "internal_sender_identifier": "string",
  "internal_sender_description": "string",
  "institution_name": "string",
  "institution_identifier": "string",
  "institution_type": "MemberInstitution",
  "institution_parent_id": 0,
  "file_count": 0,
  "size": 0,
  "payload_file_count": 0,
  "payload_size": 0
}
```

### Files

```json
{
  "count": 0,
  "next": "string",
  "previous": "string",
  "items": [
    {
      "id": 0,
      "file_format": "string",
      "size": 0,
      "identifier": "string",
      "intellectual_object_id": 0,
      "object_identifier": "string",
      "access": "consortia",
      "state": "A",
      "last_fixity_check": "2023-02-06T19:56:26.010Z",
      "institution_id": 0,
      "institution_name": "string",
      "institution_identifier": "string",
      "storage_option": "Glacier-Deep-OH",
      "uuid": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "md5": "string",
      "sha1": "string",
      "sha256": "string",
      "sha512": "string",
      "created_at": "2023-02-06T19:56:26.011Z",
      "updated_at": "2023-02-06T19:56:26.011Z"
    }
  ]
}
```

## Algorithm

1. First the APTrust objects are retrieved.

2. The names of the batches are obtained through the objects and are then verified
if they are in the database.

3. If a batch is in the database then the corresponding batches files are grabbed
from APTrust and the corresponding batches accessions are obtained from the database.

4. Then the identifiers from the bag are matched against those relpath, one by one.
If there's a match then there would be a check to make sure the identifer doesn't
already exist before being adding a new location to the database.
