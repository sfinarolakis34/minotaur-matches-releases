# Minotaur Matches releases

Public distribution repository for Minotaur Matches update packages and signed
release manifests. It does not contain application source, private signing keys,
credentials, databases, logs or user data.

## Current state

Distribution infrastructure only. No application release, installer, APK or
active update manifest has been published. A missing manifest is intentional.
Production paths are reserved and do not enable production distribution.

## Manifest endpoints

GitHub Pages publishes the `main` branch root with HTTPS:

- `https://sfinarolakis34.github.io/minotaur-matches-releases/manifests/staging/test/manifest.json`
- `https://sfinarolakis34.github.io/minotaur-matches-releases/manifests/staging/stable/manifest.json`
- `https://sfinarolakis34.github.io/minotaur-matches-releases/manifests/production/test/manifest.json`
- `https://sfinarolakis34.github.io/minotaur-matches-releases/manifests/production/stable/manifest.json`

Each environment/channel has its own signed payload and monotonically increasing
sequence. Placeholder directories intentionally contain no `manifest.json`.
The endpoints return HTTP 404 until an explicit, approved manifest publication.

## Release contract

Use tags `<environment>-<channel>-v<version>-b<build>`. Upload final Setup/APK
files as GitHub Release assets, not repository blobs or Pages files. Do not use
the global `latest` release as the environment/channel selector.

Sign using the existing offline release tool after verifying package identity,
version and Android certificate. Publish immutable assets first, verify their
anonymous HTTPS delivery and SHA-256, then publish the signed manifest last.
Do not upload unsigned drafts or any private key. Do not alter package bytes
after signing. Clients must verify the pinned RSA signature, SHA-256, package
identity, release channel, backend compatibility and anti-downgrade rules.

Public download URLs contain no personal GitHub credentials. Private signing
keys stay outside repositories and hosting. Publishing is a manual owner action;
there is no auto-publishing workflow or release in this preparation.
