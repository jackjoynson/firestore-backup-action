# firestore-backup-action

This repository contains a Github action to backup data from Firebase firestore to a Google Cloud bucket. 

## Requirements

- A Firebase Firestore instance in a project which has billing enabled.
- A Google Cloud bucket in the same project as the firestore instance. There are some region restrictions when using `firestore export` - using the a region close to the region of your Firestore instance, or a multi-region that contains the region is likely to work.
- A service account with the necessary permissions. See [the Firebase docs](https://firebase.google.com/docs/firestore/manage-data/export-import#default_service_account_permissions).

For more information on the requirements and the potential charges please see [the Firebase docs](https://firebase.google.com/docs/firestore/manage-data/export-import#before_you_begin).

## Information

This action uses:
- https://github.com/google-github-actions/auth
- https://github.com/google-github-actions/setup-gcloud

This is not an official action.

## Getting started

Here is an example workflow using this action. It runs at midnight every night and can also be run manually.

```yaml
name: Backup Firestore

on:
  workflow_dispatch:
  schedule:
    - cron:  '0 0 * * *'
  
jobs:
  backup:
    runs-on: ubuntu-latest
    timeout-minutes: 15 # Note: you may need to increase this if you are exporting a large amount of data. 
    steps:
      - name: Run backup
        uses: jackjoynson/firestore-backup-action@v1
        with:
          project-id: 'my-cool-project'
          bucket-path: 'gs://my-backups'
          service-account-key: '${{ secrets.GCP_SA_KEY }}'
          collection-ids: 'my-user-data,my-admin-data' # Optional - omit to backup the entire Firestore instance.
```