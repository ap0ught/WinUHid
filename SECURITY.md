# Security Policy

## Supported versions

Security fixes are expected to land on the current `main` branch. Older snapshots and topic branches should be treated as unsupported unless they are explicitly updated.

| Version | Supported |
| --- | --- |
| `main` | :white_check_mark: |
| older commits and branches | :x: |

## Reporting a vulnerability

Please avoid filing public issues with exploit details.

If you discover a security issue:

1. Open a GitHub issue that requests a private security contact without including proof-of-concept details.
2. Share reproduction details only after a maintainer responds with a safe channel.
3. Allow time for a fix before public disclosure.

## Maintenance expectations

- Keep GitHub Actions and NuGet dependencies current through the Dependabot configuration in `.github/dependabot.yml`.
- Review pinned action SHAs when Dependabot proposes action updates.
- Update the vcpkg baseline manually when refreshing SDL3 or other manifest-managed native dependencies.
