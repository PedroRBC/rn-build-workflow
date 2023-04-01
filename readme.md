# APK Pipeline Workflow for React Native

This workflow automates the build, signing, and distribution of an Android APK for React Native apps to both Github Releases and Firebase Distribution. It includes steps to set up JDK and Node.js, cache Gradle dependencies, and generate a signed APK.

## Setup

### Secrets

The following secrets are required to be setup in your repository:

- `GOOGLE_SERVICES_JSON`: Base64 encoded Google Services JSON used in app.
- `ANDROID_SIGNING_KEY`: Base64 encoded string of your Android keystore.
- `ANDROID_ALIAS`: The alias name of your keystore.
- `ANDROID_KEY_STORE_PASSWORD`: The password of your keystore.
- `ANDROID_KEY_PASSWORD`: The password of your keystore's alias.
- `ANDROID_FIREBASE_APP_ID`: The Firebase App ID.
- `ANDROID_FIREBASE_TOKEN`: The Firebase API token.

### Setup Secrets and Permission

### Secret

To set up these secrets, go to your repository on GitHub, then go to `Settings` > `Secrets and variables` > `Actions`. Click on `New repository secret` and add each secret key-value pair.

### Permissions

To set up these permissions in the workflow, go to `Settings` > `Actions` > `General`. In **Workflow permissions** section, check the `Read and Write permissions` option.

### Variables

The following variable is required to be passed as an input to the workflow:

- `version`: The version for naming the APK file and creating tags in the release for GitHub.

### Note

The `GOOGLE_SERVICES_JSON` file and `ANDROID_SIGNING_KEY` are encoded in base64 for security purposes.

## Workflow

The workflow consists of three jobs:

1. `setup_and_build`: This job sets up JDK and Node.js, caches gradle dependencies, installs dependencies, generates a signed APK, and uploads the signed APK as an artifact.
2. `Github_Release`: This job renames the signed APK and creates a Github release.
3. `Firebase_distribution`: This job renames the signed APK and uploads it to Firebase Distribution.

The workflow can be triggered manually by providing the `version` input.
