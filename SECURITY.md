# Wolfi security information

## Reporting security incidents to Wolfi

At present, Wolfi's security incidents are handled by the Chainguard security team.

### Your concern is about CVE scanner results, missing CVE patches, etc.

**Please note that the bootstrap repositories are unsuitable for production
use and for the most part do not receive security fixes.
Security maintenance is only provided for the production repositories.**

Please open an issue in the [os](https://github.com/wolfi-dev/os/issues/new) repository
against the package which is flagged by a CVE scanner or is missing a CVE patch.

These issues will be triaged as normal.

### Your concern is about anything else or otherwise concerns embargoed data

Please write to <security@chainguard.dev>, outlining the concern and explicitly note
that the concern is about Wolfi.

## Retrieving security feeds from Wolfi

Wolfi provides CVE remediation feeds for its production repositories, which may be
used for any purpose without any royalty, provided that attribution is provided to
the Wolfi project.

The present feeds offered are:

* `[https://packages.wolfi.dev/os/security.json](https://packages.wolfi.dev/os/security.json)`,
  a feed for the production Wolfi `os` repository.

These feeds contain a list of `package` objects under `packages`, which contain a mapping
of versions and security issue identifiers (e.g. `CVE-XXXX-YYYYY`).  An example `package`
object is:

```json
{
  "pkg": {
    "name": "binutils",
    "secfixes": {
      "2.39-r1": [
        "CVE-2022-38126"
      ],
      "2.39-r2": [
        "CVE-2022-38533"
      ]
    }
  }
}
```

This format is used across APK distributions, including Alpine and others, so your
CVE scanning software likely already understands how to ingest them.

Please open any requests for improvement to the security feeds to the [Wolfi
security database project](https://github.com/wolfi-dev/secdb).
