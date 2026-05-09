# Building WinUHid

## Prerequisites

Builds are expected to run on Windows with the same toolchain used by CI:

- Visual Studio 2022 or Build Tools with the v143 C++ toolset
- MSBuild
- Windows 10/11 SDK
- Windows Driver Kit 10.0.26100 or newer
- Visual Studio WDK component (`Microsoft.VisualStudio.Component.WDK`)
- NuGet package restore enabled
- vcpkg for the SDL3-based unit test dependency

On fresh GitHub-hosted runners, install the WDK with:

```powershell
winget install --source winget --exact --id Microsoft.WindowsWDK.10.0.26100 --accept-source-agreements --accept-package-agreements --silent
```

Then register the Visual Studio WDK component:

```powershell
$vsWhere = "${env:ProgramFiles(x86)}\Microsoft Visual Studio\Installer\vswhere.exe"
$vsPath = & $vsWhere -latest -property installationPath
$vsInstaller = "${env:ProgramFiles(x86)}\Microsoft Visual Studio\Installer\setup.exe"
& $vsInstaller modify --installPath $vsPath --add Microsoft.VisualStudio.Component.WDK --quiet --norestart
```

## Build flow

The repository's supported build flow matches `.github/workflows/build.yml`:

```powershell
msbuild -t:restore -p:RestorePackagesConfig=true
vcpkg integrate install
msbuild WinUHid.sln /p:Configuration=Release /p:Platform=x64 /m /verbosity:minimal
```

## Notes

- The UMDF driver project depends on the WDK toolset, so Linux environments without MSBuild/WDK cannot build the full solution.
- `WinUHidCppProps.props` carries the shared native hardening settings used by the user-mode libraries, test executable, and installer custom action.
- `WinUHidUnitTests/vcpkg-configuration.json` controls the vcpkg baseline for SDL3 and should be updated manually when refreshing that dependency.
