# ADR 0003 - APTrust Synchronization

Date: March 6, 2023

## Status

Accepted

## Context

We would like to use the APTrust API to update the PATSy database by a) querying
for assets stored in APTrust, b) creating new location records, and c) linking
the location records to accession records.

[LIBITD-2253](https://umd-dit.atlassian.net/browse/LIBITD-2253)

## Decision

We will store the APTrust location in the existing locations table with
storage_provider set to 'APTrust' and storage_location set to the
'umd.edu/{batch}/.../{filename}', e.g.
'umd.edu/archive0166/data/umd169/31430059836660/00000021.tif'.

We will add a `patsy sync` sub-command which will perform the synchronization
and update the database. After the initial full synchronization, a CronJob will
run nightly to find all assets added to APTrust within the last 7 days and
perform the synchronization.

## Consequences

If the synchronization process fails or does not run for more than 7 days then
new APTrust assets could be missed and never added to PATSy without a manual
update.

New APTrust assets will be processed repeatedly for 7 days in a row, but will
only be added to PATSy once.
