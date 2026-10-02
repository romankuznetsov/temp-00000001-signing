# temp-00000001-signing

Release signing for
[temp-00000001-staging](https://github.com/romankuznetsov/temp-00000001-staging).

## What this is

temp-00000001-staging builds the qWDTT packages and publishes them to its
release page. The individual packages are not signed - only the feed index is,
and a router trusts a package by the hash the signed index records for it. That
index signing is done here, with the project's release keys, which live in this
repository rather than the main one so they can be rotated or relocated on their
own.

This repository's workflow downloads the packages temp-00000001-staging
published, builds the index over those exact files, signs it, and serves the
signed feed from this repository's GitHub Pages site. Nothing is rebuilt from
source and nothing is swapped: the bytes signed here are the bytes the main
repository published.

## Verify it yourself

Download any package from temp-00000001-staging's release and the matching file
from this feed - they are identical. The index is signed with the keys
temp-00000001-staging has always published:

- apk (OpenWrt 25.12): key in `qwdtt.pem`, served with the feed
- opkg (OpenWrt 24.10): usign key id `fa06b754936d35c5`

A router that already trusts those keys needs no change beyond the feed URL.

## The feed

    https://romankuznetsov.github.io/temp-00000001-signing/

See temp-00000001-staging's installation docs for how to point a router at it.

## Secrets

Only the signing private keys live here, in this repository's Actions secrets
(`APK_PRIVATE_KEY`, `IPK_PRIVATE_KEY`); they are never written to the tree. This
repository needs no write access to temp-00000001-staging - it only reads its
public releases.
