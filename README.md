# TV AutoBuild

Automated release pipeline for customized Mobile and Leanback APKs with AV3A, Dolby Vision, HEVC-FLV, and real-time AI subtitle support.

## APK variants

Each successful build publishes four release APKs:

- `TV-mobile-arm64-v8a.apk`
- `TV-mobile-armeabi-v7a.apk`
- `TV-leanback-arm64-v8a.apk`
- `TV-leanback-armeabi-v7a.apk`

## Build behavior

- Checks for updates every 15 minutes.
- Builds only when monitored inputs change, unless a build is forced manually.
- Builds the speech-recognition and AV3A JNI runtimes from source for both supported ABIs.
- Runs Mobile and Leanback unit tests before packaging.
- Applies R8 optimization to release APKs.
- Verifies APK signatures before publishing.
- Publishes build metadata, exact input revisions, and SHA-256 checksums with every release.

GitHub scheduled workflows can be delayed. Use **Actions → Monitor sources and build APKs → Run workflow** for an immediate manual build.

## Versioning

Each build receives a monotonically increasing Android `versionCode` and a traceable version name:

```text
<base-version>-autobuild.<run>+<revision>
```

This allows newer builds of the same variant to update earlier AutoBuild installations while retaining traceability.

## Signing

All APKs are signed with a persistent dedicated release key stored in GitHub Actions secrets. The private key and passwords are never committed.

The public signing certificate is available as [`autobuild-signing-cert.pem`](autobuild-signing-cert.pem). Its SHA-256 certificate fingerprint is:

```text
17:8A:B4:F2:5C:CC:E5:BC:B4:FA:7A:9D:38:B6:7C:7E:1F:3C:54:D2:56:D0:D2:CB:A0:6C:6E:FE:A7:10:A4:AB
```
