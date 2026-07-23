# TREK for LazyCat

This repository packages the unmodified official TREK container image as a LazyCat LPK v2 application.

- Upstream: <https://github.com/liketrek/TREK>
- Initial image: `mauriceboe/trek:3.4.1`
- License: GNU AGPL-3.0
- LazyCat package: `community.lazycat.app.trek`

## Integration

- LazyCat OIDC is connected to TREK's `/api/auth/oidc/callback` endpoint.
- `OIDC_ONLY=true` provides passwordless LazyCat account login. The first OIDC user becomes the TREK administrator.
- TREK data and uploads persist under `/lzcapp/var/`.
- TREK's upload and download flows load the official LazyCat file chooser interception script.

## Automated publishing

The reusable `ca-x/lazycat-github-action@v1` workflow checks stable upstream image tags, remotely copies the selected image to the LazyCat registry, builds a versioned LPK Release asset, and reconciles both the official and private stores. It does not require local Docker.

The `lazycat-contrib` organization must expose these GitHub Actions Secrets to this repository:

- `LAZYCAT_TOKEN`
- `APPSTORE_URL`
- `APPSTORE_TOKEN`
- `APP_ID` (optional)
- `PRIVATE_STORE_GROUP_CODES` (optional)

Run the **Publish TREK to LazyCat stores** workflow manually for the first release. It also checks for stable updates every day at 03:17 UTC.

## License and trademark

TREK is distributed under AGPL-3.0. The exact corresponding source for the initial package is the upstream [`v3.4.1` release](https://github.com/liketrek/TREK/releases/tag/v3.4.1). This package does not modify the TREK image.

TREK's trademark policy permits retaining the TREK name and marks when redistributing an unmodified official distribution. This repository does not claim upstream endorsement.
