# Repository Guidelines

## Project Structure & Module Organization
This repository is a single .NET Framework plugin solution for Hearthstone built on BepInEx. The solution file is `HsMod.sln`, and the main project lives in `HsMod/`.

Core runtime code is in top-level C# files such as `Main.cs`, `Patcher.cs`, `PluginConfig.cs`, `WebApi.cs`, and `WebServer.cs`. Localized strings are embedded from `HsMod/Languages/*.json`. Embedded web UI assets live under `HsMod/WebResources/`. Bundled runtime dependencies required for compilation are checked in under `HsMod/BepInExCore/`, `HsMod/LibHearthstone/`, and `HsMod/UnstrippedCorlib*`.

## Build, Test, and Development Commands
Use the solution root unless noted otherwise.

- `dotnet build HsMod.sln -c Release --no-restore` builds `HsMod.dll` for release.
- `dotnet build HsMod.sln -c Debug` builds a debug version for local iteration.
- `msbuild HsMod.sln /p:Configuration=Release` is a reasonable fallback for older Visual Studio setups targeting .NET Framework 4.8.
- `HsMod\\install.bat` copies `Release\\HsMod.dll` into a default Windows Hearthstone BepInEx plugin folder after a successful build.

## Coding Style & Naming Conventions
Follow the existing C# style in `HsMod/`: 4-space indentation, braces on their own lines, `PascalCase` for types and methods, `camelCase` for locals and parameters, and `ALL_CAPS` only for true constants. Keep namespace usage explicit and match the current file-per-feature layout. Preserve existing bilingual comments where they add context. There is no formatter config in the repo, so keep edits consistent with surrounding code.

## Testing Guidelines
There is no dedicated automated test project in this repository today. Validate changes by building successfully and smoke-testing in a BepInEx-based Hearthstone install. For features touching config, patching, or web endpoints, verify startup logs, plugin load behavior, and the relevant in-game or HTTP flow. If you add automated tests later, place them in a separate `*.Tests` project rather than inside `HsMod/`.

## Commit & Pull Request Guidelines
This checkout has very limited history, but visible commits use short, direct subjects and GitHub merge PR titles such as `Merge pull request #273 ...`. Prefer concise imperative commit messages, for example `Fix web config reload`. Keep pull requests focused, describe gameplay or plugin behavior changes, link related issues or discussions, and include screenshots or log excerpts when UI, web resources, or runtime patch behavior changes.

## Security & Configuration Tips
Do not commit personal `client.config`, tokens, or machine-specific Hearthstone paths. Treat bundled DLLs and unstripped corlib files as version-sensitive inputs; avoid replacing them casually unless the target Hearthstone version changes.

## 实际使用情况
我已经将本项目安装到炉石传说目录中C:\Program Files (x86)\Hearthstone，写了启动脚本"C:\Users\syj\Downloads\HsMod\launch_hsmod.bat"让我直接启动美服，我国服用战网登录不使用插件，防止被封。