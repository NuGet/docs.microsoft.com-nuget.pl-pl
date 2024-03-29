# [Co to jest NuGet?](what-is-nuget.md)
# Wprowadzenie
## [Instalowanie narzędzi klienta programu NuGet](install-nuget-client-tools.md)
## [Instalowanie i używanie pakietu (wiersz polecenia dotnet)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md)
## [Instalowanie i używanie pakietu (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md)
## [Instalowanie i używanie pakietu (Visual Studio dla komputerów Mac)](quickstart/install-and-use-a-package-in-visual-studio-mac.md)
## [Tworzenie i publikowanie pakietu platformy .NET Standard (interfejs wiersza polecenia dotnet)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
## [Tworzenie i publikowanie pakietu platformy .NET Standard (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md)
## [Tworzenie i publikowanie pakietu platformy .NET Framework (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
# Korzystanie z pakietów
## [Omówienie i przepływ pracy](consume-packages/overview-and-workflow.md)
## [Znajdowanie i wybieranie pakietów](consume-packages/finding-and-choosing-packages.md)
## Instalowanie pakietów i zarządzanie nimi
### [Visual Studio](consume-packages/install-use-packages-visual-studio.md)
### [Visual Studio dla komputerów Mac](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)
### [Interfejs wiersza polecenia dotnet](consume-packages/install-use-packages-dotnet-cli.md)
### [Interfejs wiersza polecenia nuget.exe](consume-packages/install-use-packages-nuget-cli.md)
### [Konsola menedżera pakietów (PowerShell)](consume-packages/install-use-packages-powershell.md)
## Konfigurowanie narzędzia NuGet
### Opcje przywracania pakietów
#### [Przywracanie pakietów](consume-packages/package-restore.md)
#### [Rozwiązywanie problemów](consume-packages/package-restore-troubleshooting.md)
### [Ponowne instalowanie i aktualizowanie pakietów](consume-packages/reinstalling-and-updating-packages.md)
### [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](consume-packages/managing-the-global-packages-and-cache-folders.md)
### [Zarządzanie granicami zaufania pakietów](consume-packages/installing-signed-packages.md)
### [Praca z uwierzytelnionymi źródłami danych](consume-packages/consuming-packages-authenticated-feeds.md)
### [Praca z systemami kontroli źródła](consume-packages/packages-and-source-control.md)
### [Typowe konfiguracje narzędzia NuGet](consume-packages/configuring-nuget-behavior.md)
## Odwołania do pakietów w projekcie
### [Odwołania do pakietu w plikach projektu](consume-packages/package-references-in-project-files.md)
### [Migrowanie pliku packages.config do elementu PackageReference](consume-packages/migrate-packages-config-to-package-reference.md)
### [packages.config](reference/packages-config.md)
# Tworzenie pakietów
## [Omówienie i przepływ pracy](create-packages/overview-and-workflow.md)
## [Tworzenie pakietu (interfejs wiersza polecenia dotnet)](create-packages/creating-a-package-dotnet-cli.md)
## [Tworzenie pakietu (interfejs wiersza polecenia nuget.exe)](create-packages/creating-a-package.md)
## [Tworzenie pakietu (program MSBuild)](create-packages/creating-a-package-msbuild.md)
## [Najlepsze rozwiązania dotyczące tworzenia pakietów](create-packages/Package-authoring-best-practices.md)
## [Tworzenie pakietu w wersji wstępnej](create-packages/prerelease-packages.md)
## [Tworzenie pakietu symboli](create-packages/symbol-packages-snupkg.md)
## [Obsługa wielu platform docelowych w pliku projektu](create-packages/multiple-target-frameworks-project-file.md)
## Zaawansowane zadania
### [Obsługa wielu platform docelowych](create-packages/supporting-multiple-target-frameworks.md)
### [Modyfikowanie kodu źródłowego i plików konfiguracji](create-packages/source-and-config-file-transformations.md)
### [Wybieranie zestawów przywoływanych w projektach](create-packages/select-assemblies-referenced-by-projects.md)
### [Ustawianie typu pakietu](create-packages/set-package-type.md)
### [Tworzenie zlokalizowanego pakietu](create-packages/creating-localized-packages.md)
## Przewodniki dotyczące określonej zawartości
### [Tworzenie pakietu platformy UWP (C++)](guides/create-uwp-packages.md)
### [Tworzenie pakietu platformy UWP (C#)](guides/create-uwp-packages-CS.md)
### [Tworzenie pakietu natywnego](guides/native-packages.md)
### [Tworzenie kontrolek interfejsu użytkownika jako pakietu NuGet](guides/create-UI-controls.md)
### [Tworzenie analizatora jako pakietu NuGet](guides/analyzers-conventions.md)
### [Tworzenie pakietu dla platformy Xamarin za pomocą programu Visual Studio 2017 lub 2019](guides/create-packages-for-xamarin.md)
### [Tworzenie pakietu za pomocą zestawów usługi międzyoperacyjnej modelu COM](create-packages/author-packages-with-COM-interop-assemblies.md)
## Podpisywanie pakietów
### [Podpisywanie pakietu](create-packages/sign-a-package.md)
### [Podpisy i wymagania dotyczące podpisanych pakietów](reference/signed-packages-reference.md)
# Publikowanie pakietów
## Publikowanie w witrynie NuGet.org
### [Publikowanie pakietu](nuget-org/publish-a-package.md)
### [Klucze interfejsu API](nuget-org/scoped-api-keys.md)
## Publikowanie w prywatnym kanale informacyjnym
### [Omówienie](hosting-packages/overview.md)
### [Artefakty platformy Azure](/azure/devops/artifacts/nuget/publish?view=azure-devops)
### [NuGet.Server](hosting-packages/nuget-server.md)
### [Lokalne źródła danych](hosting-packages/local-feeds.md)
# Pojęcia
## [Proces instalacji pakietu](concepts/package-installation-process.md)
## [Przechowywanie wersji pakietów](concepts/package-versioning.md)
## [Rozwiązywanie zależności](concepts/dependency-resolution.md)
## [Najlepsze rozwiązania dotyczące bezpiecznego łańcucha dostaw oprogramowania](concepts/Security-Best-Practices.md)
## [Rozwiązywanie problemów z zainstalowanymi pakietami](concepts/troubleshooting-installed-packages.md)
# Tematy pomocy
## [.nuspec](reference/nuspec.md)
## [Plik nuget.config](reference/nuget-config-file.md)
## [Platformy docelowe](reference/target-frameworks.md)
## [Pakowanie i przywracanie jako elementy docelowe programu MSBuild](reference/msbuild-targets.md)
## [Interfejs wiersza polecenia dotnet](reference/dotnet-Commands.md)
## [Dokumentacja interfejsu wiersza polecenia programu nuget.exe](reference/nuget-exe-cli-reference.md)
### [add](reference/cli-reference/cli-ref-add.md)
### [config](reference/cli-reference/cli-ref-config.md)
### [delete](reference/cli-reference/cli-ref-delete.md)
### [help or ?](reference/cli-reference/cli-ref-help.md)
### [init](reference/cli-reference/cli-ref-init.md)
### [install](reference/cli-reference/cli-ref-install.md)
### [list](reference/cli-reference/cli-ref-list.md)
### [locals](reference/cli-reference/cli-ref-locals.md)
### [mirror](reference/cli-reference/cli-ref-mirror.md)
### [pakiet](reference/cli-reference/cli-ref-pack.md)
### [push](reference/cli-reference/cli-ref-push.md)
### [restore](reference/cli-reference/cli-ref-restore.md)
### [search](reference/cli-reference/cli-ref-search.md)
### [setapikey](reference/cli-reference/cli-ref-setapikey.md)
### [sign](reference/cli-reference/cli-ref-sign.md)
### [sources](reference/cli-reference/cli-ref-sources.md)
### [spec](reference/cli-reference/cli-ref-spec.md)
### [update](reference/cli-reference/cli-ref-update.md)
### [verify](reference/cli-reference/cli-ref-verify.md)
### [trusted-signers](reference/cli-reference/cli-ref-trusted-signers.md)
### [Zmienne środowiskowe](reference/cli-reference/cli-ref-environment-variables.md)
### [Obsługa długich ścieżek](reference/cli-reference/cli-ref-long-path.md)
## [Dokumentacja programu PowerShell](reference/powershell-reference.md)
### [Add-BindingRedirect](reference/ps-reference/ps-ref-add-bindingredirect.md)
### [Find-Package](reference/ps-reference/ps-ref-find-package.md)
### [Get-Package](reference/ps-reference/ps-ref-get-package.md)
### [Get-Project](reference/ps-reference/ps-ref-get-project.md)
### [Install-Package](reference/ps-reference/ps-ref-install-package.md)
### [Open-PackagePage](reference/ps-reference/ps-ref-open-packagepage.md)
### [Sync-Package](reference/ps-reference/ps-ref-sync-package.md)
### [Uninstall-Package](reference/ps-reference/ps-ref-uninstall-package.md)
### [Update-Package](reference/ps-reference/ps-ref-update-package.md)
## Interfejs API serwera NuGet
### [Omówienie](api/overview.md)
### Resources
#### [Autouzupełnianie](api/search-autocomplete-service-resource.md)
#### [Wykaz](api/catalog-resource.md)
#### [Zawartość pakietu](api/package-base-address-resource.md)
#### [Adres URL szczegółów pakietu](api/package-details-template-resource.md)
#### [Metadane pakietu](api/registration-base-url-resource.md)
#### [Wypychanie i usuwanie](api/package-publish-resource.md)
#### [Wypychanie pakietów symboli](api/symbol-package-publish-resource.md)
#### [Adres URL do zgłaszania nadużyć](api/report-abuse-resource.md)
#### [Podpisy repozytorium](api/repository-signatures-resource.md)
#### [Wyszukiwanie](api/search-query-service-resource.md)
#### [Indeks usług](api/service-index.md)
### [Instrukcje: Wykonywanie zapytania o wszystkie pakiety za pomocą interfejsu API](guides/api/query-for-all-published-packages.md)
### [Limit szybkości](api/rate-limits.md)
### [Protokoły nuget.org](api/nuget-protocols.md)
### [tools.json](api/tools-json.md)
## [Zestaw SDK klienta programu NuGet](reference/nuget-client-sdk.md)
## [Błędy i ostrzeżenia](reference/Errors-and-Warnings.md)
### [NU1000](reference/errors-and-warnings/NU1000.md)
### [NU1001](reference/errors-and-warnings/NU1001.md)
### [NU1002](reference/errors-and-warnings/NU1002.md)
### [NU1003](reference/errors-and-warnings/NU1003.md)
### [NU1100](reference/errors-and-warnings/NU1100.md)
### [NU1101](reference/errors-and-warnings/NU1101.md)
### [NU1102](reference/errors-and-warnings/NU1102.md)
### [NU1103](reference/errors-and-warnings/NU1103.md)
### [NU1104](reference/errors-and-warnings/NU1104.md)
### [NU1105](reference/errors-and-warnings/NU1105.md)
### [NU1106](reference/errors-and-warnings/NU1106.md)
### [NU1107](reference/errors-and-warnings/NU1107.md)
### [NU1108](reference/errors-and-warnings/NU1108.md)
### [NU1201](reference/errors-and-warnings/NU1201.md)
### [NU1202](reference/errors-and-warnings/NU1202.md)
### [NU1203](reference/errors-and-warnings/NU1203.md)
### [NU1401](reference/errors-and-warnings/NU1401.md)
### [NU1500](reference/errors-and-warnings/NU1500.md)
### [NU1501](reference/errors-and-warnings/NU1501.md)
### [NU1502](reference/errors-and-warnings/NU1502.md)
### [NU1503](reference/errors-and-warnings/NU1503.md)
### [NU1601](reference/errors-and-warnings/NU1601.md)
### [NU1602](reference/errors-and-warnings/NU1602.md)
### [NU1603](reference/errors-and-warnings/NU1603.md)
### [NU1604](reference/errors-and-warnings/NU1604.md)
### [NU1605](reference/errors-and-warnings/NU1605.md)
### [NU1608](reference/errors-and-warnings/NU1608.md)
### [NU1701](reference/errors-and-warnings/NU1701.md)
### [NU1703](reference/errors-and-warnings/NU1703.md)
### [NU1801](reference/errors-and-warnings/NU1801.md)
### [NU3000](reference/errors-and-warnings/NU3000.md)
### [NU3001](reference/errors-and-warnings/NU3001.md)
### [NU3002](reference/errors-and-warnings/NU3002.md)
### [NU3003](reference/errors-and-warnings/NU3003.md)
### [NU3004](reference/errors-and-warnings/NU3004.md)
### [NU3005](reference/errors-and-warnings/NU3005.md)
### [NU3006](reference/errors-and-warnings/NU3006.md)
### [NU3007](reference/errors-and-warnings/NU3007.md)
### [NU3008](reference/errors-and-warnings/NU3008.md)
### [NU3009](reference/errors-and-warnings/NU3009.md)
### [NU3010](reference/errors-and-warnings/NU3010.md)
### [NU3011](reference/errors-and-warnings/NU3011.md)
### [NU3012](reference/errors-and-warnings/NU3012.md)
### [NU3013](reference/errors-and-warnings/NU3013.md)
### [NU3014](reference/errors-and-warnings/NU3014.md)
### [NU3015](reference/errors-and-warnings/NU3015.md)
### [NU3016](reference/errors-and-warnings/NU3016.md)
### [NU3017](reference/errors-and-warnings/NU3017.md)
### [NU3018](reference/errors-and-warnings/NU3018.md)
### [NU3019](reference/errors-and-warnings/NU3019.md)
### [NU3020](reference/errors-and-warnings/NU3020.md)
### [NU3021](reference/errors-and-warnings/NU3021.md)
### [NU3022](reference/errors-and-warnings/NU3022.md)
### [NU3023](reference/errors-and-warnings/NU3023.md)
### [NU3024](reference/errors-and-warnings/NU3024.md)
### [NU3025](reference/errors-and-warnings/NU3025.md)
### [NU3026](reference/errors-and-warnings/NU3026.md)
### [NU3027](reference/errors-and-warnings/NU3027.md)
### [NU3028](reference/errors-and-warnings/NU3028.md)
### [NU3029](reference/errors-and-warnings/NU3029.md)
### [NU3030](reference/errors-and-warnings/NU3030.md)
### [NU3031](reference/errors-and-warnings/NU3031.md)
### [NU3032](reference/errors-and-warnings/NU3032.md)
### [NU3033](reference/errors-and-warnings/NU3033.md)
### [NU3034](reference/errors-and-warnings/NU3034.md)
### [NU3035](reference/errors-and-warnings/NU3035.md)
### [NU3036](reference/errors-and-warnings/NU3036.md)
### [NU3037](reference/errors-and-warnings/NU3037.md)
### [NU3038](reference/errors-and-warnings/NU3038.md)
### [NU3040](reference/errors-and-warnings/NU3040.md)
### [NU5000](reference/errors-and-warnings/NU5000.md)
### [NU5001](reference/errors-and-warnings/NU5001.md)
### [NU5002](reference/errors-and-warnings/NU5002.md)
### [NU5003](reference/errors-and-warnings/NU5003.md)
### [NU5004](reference/errors-and-warnings/NU5004.md)
### [NU5005](reference/errors-and-warnings/NU5005.md)
### [NU5007](reference/errors-and-warnings/NU5007.md)
### [NU5008](reference/errors-and-warnings/NU5008.md)
### [NU5009](reference/errors-and-warnings/NU5009.md)
### [NU5010](reference/errors-and-warnings/NU5010.md)
### [NU5011](reference/errors-and-warnings/NU5011.md)
### [NU5012](reference/errors-and-warnings/NU5012.md)
### [NU5013](reference/errors-and-warnings/NU5013.md)
### [NU5014](reference/errors-and-warnings/NU5014.md)
### [NU5015](reference/errors-and-warnings/NU5015.md)
### [NU5016](reference/errors-and-warnings/NU5016.md)
### [NU5017](reference/errors-and-warnings/NU5017.md)
### [NU5018](reference/errors-and-warnings/NU5018.md)
### [NU5019](reference/errors-and-warnings/NU5019.md)
### [NU5020](reference/errors-and-warnings/NU5020.md)
### [NU5021](reference/errors-and-warnings/NU5021.md)
### [NU5022](reference/errors-and-warnings/NU5022.md)
### [NU5023](reference/errors-and-warnings/NU5023.md)
### [NU5024](reference/errors-and-warnings/NU5024.md)
### [NU5025](reference/errors-and-warnings/NU5025.md)
### [NU5026](reference/errors-and-warnings/NU5026.md)
### [NU5027](reference/errors-and-warnings/NU5027.md)
### [NU5028](reference/errors-and-warnings/NU5028.md)
### [NU5029](reference/errors-and-warnings/NU5029.md)
### [NU5030](reference/errors-and-warnings/NU5030.md)
### [NU5031](reference/errors-and-warnings/NU5031.md)
### [NU5032](reference/errors-and-warnings/NU5032.md)
### [NU5033](reference/errors-and-warnings/NU5033.md)
### [NU5034](reference/errors-and-warnings/NU5034.md)
### [NU5035](reference/errors-and-warnings/NU5035.md)
### [NU5036](reference/errors-and-warnings/NU5036.md)
### [NU5037](reference/errors-and-warnings/NU5037.md)
### [NU5046](reference/errors-and-warnings/NU5046.md)
### [NU5047](reference/errors-and-warnings/NU5047.md)
### [NU5048](reference/errors-and-warnings/NU5048.md)
### [NU5100](reference/errors-and-warnings/NU5100.md)
### [NU5101](reference/errors-and-warnings/NU5101.md)
### [NU5102](reference/errors-and-warnings/NU5102.md)
### [NU5103](reference/errors-and-warnings/NU5103.md)
### [NU5104](reference/errors-and-warnings/NU5104.md)
### [NU5105](reference/errors-and-warnings/NU5105.md)
### [NU5106](reference/errors-and-warnings/NU5106.md)
### [NU5107](reference/errors-and-warnings/NU5107.md)
### [NU5108](reference/errors-and-warnings/NU5108.md)
### [NU5109](reference/errors-and-warnings/NU5109.md)
### [NU5110](reference/errors-and-warnings/NU5110.md)
### [NU5111](reference/errors-and-warnings/NU5111.md)
### [NU5112](reference/errors-and-warnings/NU5112.md)
### [NU5114](reference/errors-and-warnings/NU5114.md)
### [NU5115](reference/errors-and-warnings/NU5115.md)
### [NU5116](reference/errors-and-warnings/NU5116.md)
### [NU5117](reference/errors-and-warnings/NU5117.md)
### [NU5118](reference/errors-and-warnings/NU5118.md)
### [NU5119](reference/errors-and-warnings/NU5119.md)
### [NU5120](reference/errors-and-warnings/NU5120.md)
### [NU5121](reference/errors-and-warnings/NU5121.md)
### [NU5122](reference/errors-and-warnings/NU5122.md)
### [NU5123](reference/errors-and-warnings/NU5123.md)
### [NU5124](reference/errors-and-warnings/NU5124.md)
### [NU5125](reference/errors-and-warnings/NU5125.md)
### [NU5127](reference/errors-and-warnings/NU5127.md)
### [NU5128](reference/errors-and-warnings/NU5128.md)
### [NU5129](reference/errors-and-warnings/NU5129.md)
### [NU5130](reference/errors-and-warnings/NU5130.md)
### [NU5131](reference/errors-and-warnings/NU5131.md)
### [NU5500](reference/errors-and-warnings/NU5500.md)
## Zawartość zarchiwizowana
### [Format zarządzania project.json](archive/project-json.md)
### [Plik project.json i platforma UWP](archive/project-json-and-uwp.md)
### [Wpływ pliku project.json](archive/project-json-impact.md)
# Rozszerzalność
## Rozszerzalność — wtyczki narzędzia NuGet
### [Wtyczki narzędzia NuGet dla wielu platform](reference/extensibility/NuGet-Cross-Platform-Plugins.md)
### [Wtyczka uwierzytelniania NuGet dla wielu platform](reference/extensibility/nuget-cross-platform-authentication-plugin.md)
### [Dostawcy poświadczeń programu NuGet dla programu Visual Studio](reference/extensibility/nuget-credential-providers-for-visual-studio.md)
### [Dostawcy poświadczeń programu nuget.exe](reference/extensibility/nuget-exe-credential-providers.md)
## Rozszerzalność programu Visual Studio
### [Interfejs API programu NuGet w programie Visual Studio](visual-studio-extensibility/nuget-api-in-visual-studio.md)
### [Obsługa systemów projektów](visual-studio-extensibility/project-system-support.md)
### [Szablony programu Visual Studio](visual-studio-extensibility/visual-studio-templates.md)
# Resources
## Zasady
### [Nadzór](policies/governance.md)
### [Ekosystem](policies/ecosystem.md)
### [Zasady witryny NuGet.org](nuget-org/policies/data-requests.md)
## Uwagi do wersji
### [Znane problemy](release-notes/known-issues.md)
### NuGet 5.x
#### [NuGet 5.11](release-notes/NuGet-5.11.md)
#### [NuGet 5.10](release-notes/NuGet-5.10.md)
#### [NuGet 5.9](release-notes/NuGet-5.9.md)
#### [NuGet 5.8](release-notes/NuGet-5.8.md)
#### [NuGet 5.7](release-notes/NuGet-5.7.md)
#### [NuGet 5.6](release-notes/NuGet-5.6.md)
#### [NuGet 5.5](release-notes/NuGet-5.5.md)
#### [NuGet 5.4](release-notes/NuGet-5.4.md)
#### [NuGet 5.3](release-notes/NuGet-5.3.md)
#### [NuGet 5.2](release-notes/NuGet-5.2-RTM.md)
#### [NuGet 5.1](release-notes/NuGet-5.1-RTM.md)
#### [NuGet 5.0](release-notes/NuGet-5.0-RTM.md)
### NuGet 4.x
#### [NuGet 4.9 RTM](release-notes/NuGet-4.9-RTM.md)
#### [NuGet 4.8 RTM](release-notes/NuGet-4.8-RTM.md)
#### [NuGet 4.7 RTM](release-notes/NuGet-4.7-RTM.md)
#### [NuGet 4.6 RTM](release-notes/NuGet-4.6-RTM.md)
#### [NuGet 4.5 RTM](release-notes/NuGet-4.5-RTM.md)
#### [NuGet 4.4 RTM](release-notes/NuGet-4.4-RTM.md)
#### [NuGet 4.3 RTM](release-notes/NuGet-4.3-RTM.md)
#### [NuGet 4.0 RTM](release-notes/NuGet-4.0-RTM.md)
#### [NuGet 4.0 RC](release-notes/NuGet-4.0-RC.md)
### NuGet 3.x
#### [NuGet 3.5 RTM](release-notes/NuGet-3.5-RTM.md)
#### [NuGet 3.5 RC](release-notes/NuGet-3.5-RC.md)
#### [NuGet 3.5 Beta2](release-notes/NuGet-3.5-Beta2.md)
#### [NuGet 3.5 Beta](release-notes/NuGet-3.5-Beta.md)
#### [NuGet 3.4.4](release-notes/NuGet-3.4.4.md)
#### [NuGet 3.4.3](release-notes/NuGet-3.4.3.md)
#### [NuGet 3.4.2](release-notes/NuGet-3.4.2.md)
#### [NuGet 3.4.1](release-notes/NuGet-3.4.1.md)
#### [NuGet 3.4](release-notes/NuGet-3.4.md)
#### [NuGet 3.4 RC](release-notes/NuGet-3.4-RC.md)
#### [NuGet 3.3](release-notes/NuGet-3.3.md)
#### [NuGet 3.2.1](release-notes/NuGet-3.2.1.md)
#### [NuGet 3.2](release-notes/NuGet-3.2.md)
#### [NuGet 3.2 RC](release-notes/NuGet-3.2-RC.md)
#### [NuGet 3.1.1](release-notes/NuGet-3.1.1.md)
#### [NuGet 3.1](release-notes/NuGet-3.1.md)
#### [NuGet 3.0.0](release-notes/NuGet-3.0.0.md)
#### [NuGet 3.0 RC2](release-notes/NuGet-3.0-RC2.md)
#### [NuGet 3.0 RC](release-notes/NuGet-3.0-RC.md)
#### [NuGet 3.0 Beta](release-notes/NuGet-3.0-Beta.md)
#### [NuGet 3.0 (wersja zapoznawcza)](release-notes/NuGet-3.0-Preview.md)
### NuGet 2.x
#### [NuGet 2.12](release-notes/NuGet-2.12.md)
#### [NuGet 2.12 RC](release-notes/NuGet-2.12-RC.md)
#### [NuGet 2.9 RC](release-notes/NuGet-2.9-RC.md)
#### [NuGet 2.8.7](release-notes/NuGet-2.8.7.md)
#### [NuGet 2.8.6](release-notes/NuGet-2.8.6.md)
#### [NuGet 2.8.5](release-notes/NuGet-2.8.5.md)
#### [NuGet 2.8.3](release-notes/NuGet-2.8.3.md)
#### [NuGet 2.8.2](release-notes/NuGet-2.8.2.md)
#### [NuGet 2.8.1](release-notes/NuGet-2.8.1.md)
#### [NuGet 2.8](release-notes/NuGet-2.8.md)
#### [NuGet 2.7.2](release-notes/NuGet-2.7.2.md)
#### [NuGet 2.7.1](release-notes/NuGet-2.7.1.md)
#### [NuGet 2.7](release-notes/NuGet-2.7.md)
#### [NuGet 2.6.1-for-WebMatrix](release-notes/NuGet-2.6.1-for-WebMatrix.md)
#### [NuGet 2.6](release-notes/NuGet-2.6.md)
#### [NuGet 2.5](release-notes/NuGet-2.5.md)
#### [NuGet 2.2.1](release-notes/NuGet-2.2.1.md)
#### [NuGet 2.2](release-notes/NuGet-2.2.md)
#### [NuGet 2.1](release-notes/NuGet-2.1.md)
#### [NuGet 2.0](release-notes/NuGet-2.0.md)
### NuGet 1.x
#### [NuGet 1.8](release-notes/NuGet-1.8.md)
#### [NuGet 1.7](release-notes/NuGet-1.7.md)
#### [NuGet 1.6](release-notes/NuGet-1.6.md)
#### [NuGet 1.5](release-notes/NuGet-1.5.md)
#### [NuGet 1.4](release-notes/NuGet-1.4.md)
#### [NuGet 1.3](release-notes/NuGet-1.3.md)
#### [NuGet 1.2](release-notes/NuGet-1.2.md)
#### [NuGet 1.1](release-notes/NuGet-1.1.md)
## [Często zadawane pytania](resources/nuget-faq.yml)
## [Format projektu](resources/check-project-format.md)
# [NuGet.org](nuget-org/overview-nuget-org.md)
