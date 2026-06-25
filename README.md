# EasyScripts - Sequential Macro Editor

C# Avalonia (.NET10 / Avalonia 12)
  - Targets Windows, MacOS, and Linux

# PROJECT ARCHITECTURE
  - ProjectRoot/
      - src/
          - EasyScripts.AppHost/
              - appsettings.json // Is bundled to assembly. Creates a user copy in %LOCALAPPDATA%
              - Program.cs // Composition root. Wires up Serilog. Wires up Host and DI container.
              - MacroCanvas.AppHost.csproj // OutputType set to Exe (WinExe on release). References all other csproj and this csproj is never referenced
          - EasyScripts.Core/
              - Abstractions/
                  - IAppInfo.cs
                  - IAppPaths.cs
                  - IAppSettingsProvider.cs // Will be wired in Program.cs as a Singleton to be accessible as a service for all csprojs
                  - IFileExplorerService.cs **IN PROGRESS**
                  - INativePlatform.cs **IN PROGRESS**
                  - IThemeService.cs // AXAML files uses DynamicResource bindings to keys defined in EasyScripts.UI/Assets/Accents & Themes. Loads AXAML into Avalonia ResourceDictionary with a pointer (private field)
              - Configuration/
                  - AppSettings.cs // Honestly its a full POCO class. Was deciding to keep in AppHost, but decided to keep AppHost clean and minimal with only Program.cs
                  - CoreConstants.cs // Internal static
              - Data/
                  - Enums.cs // All enums used in this software are all through services. Services all inherit from interfaces in Core. Thus, all enums are centralised here
                  - FileIconMapping.cs
                  - Structs.cs // Same reasoning as Enums.cs
              - Engine/ **IN PROGRESS**
                  - ExecContext.cs **IN PROGRESS**
                  - PauseToken.cs **IN PROGRESS**
              - Exceptions/
                  - Exceptions.cs **IN PROGRESS** // All exceptions with error codes here
              - Factories/
                  - FileExplorerItemFactory.cs **IN PROGRESS**
              - Models/
                  - FileExplorerClipboard.cs
                  - FileExplorerItem.cs
                  - FileIcon.cs
              - Utils/
                  - FormatterHelper.cs
              - EasyScripts.Core.csproj
          - EasyScripts.Infrastructure/
              - Configuration/
                  - InfrastructureConstants.cs
              - DependencyInjection/
                  - InfrastructureServices.cs
              - Services/
                  - AppInfo.cs
                  - AppPaths.cs
                  - AppSettingsProvider.cs
              - Utils/
                  - LogsHandler.cs
                  - Prelogger.cs
              - EasyScripts.Infrastructure.csproj
          - EasyScripts.UI/
              - Assets/
                  - Accents/
                      - BlackAccent.axaml, WhiteAccent.axaml
                  - Icons/
                      - app.ico, KeyEvent.png, MouseEvent.png, ConditionalEvent.png, etc.
                  - Markdowns/
                      - TERMS_CONDITIONS.md
                  - Styles/
                      - Base.axaml, Buttons.axaml, Index.axaml, Lists.axaml, etc.
                  - Themes/
                      - DarkTheme.axaml, LightTheme.axaml
              - Configuration/
                  - UIConstants.cs
              - DependencyInjection/
                  - UIServices.cs
              - Properties/
                  - GlobalSuppression.cs
              - Services/
              - Views/
              - App.axaml
              - App.axaml.cs
              - EasyScripts.UI.csproj
          - EasyScripts.Platform.Windows/ **IN PROGRESS**
          - EasyScripts.Platform.Linux/ **NOT IMPLEMENTED YET**
          - EasyScripts.Platform.MacOS/ **NOT IMPLEMENTED YET**
      - Directory.Build.props
      - Directory.Packages.props
      - EasyScripts.slnx
      - LICENSE.md
  

# Purpose

I needed a macro software that could perform beyond what TinyTasks and other free macro software could offer:
  - OCR or image capture
  - Conditional logic; If window shows X instead of Y, proceed to branch 1, otherwise proceed to branch 2
  - Async running of multiple macro sequences in parallel
  - Scheduling


# Current status

- AppHost
  -> Completed
- UI
  -> Wiring up EditorWindow and all the required DataTemplates for the View
  -> Aiming to make a modern UI similar to RPA automation tools
- Core
  -> Wiring up in conjunction with UI
  -> Currently included: Mouse steps, Key steps, Power shell steps, Pixel Color check steps, Image (bitmap) check steps, Conditional steps
  -> More on the way as I am still thinking on how to expand this further

# Screenshots
<img width="1243" height="798" alt="image" src="https://github.com/user-attachments/assets/2a4c68b0-60a2-4948-a013-f15edb8f6dfb" />



