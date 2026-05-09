# WinUHid

WinUHid is a Windows virtual HID device emulation framework that builds native user-mode components, a UMDF driver, and an installer package from the `WinUHid.sln` solution.

## Documentation

- `BUILDING.md` - local and CI-oriented build prerequisites
- `SECURITY.md` - security reporting and maintenance policy

## Security and maintenance

The repository now uses a few baseline maintenance controls:

- GitHub Actions are pinned to reviewed release commits and run with read-only repository contents permission.
- CI installs the WDK explicitly so the driver build stays compatible with current `windows-latest` runners.
- Dependabot is configured for GitHub Actions and NuGet manifests so routine update PRs can be opened automatically.
- Shared native compiler/linker hardening flags live in `WinUHidCppProps.props`.
- vcpkg dependencies are tracked through `WinUHidUnitTests/vcpkg-configuration.json`; update that baseline manually when refreshing SDL3.
