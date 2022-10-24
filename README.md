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
