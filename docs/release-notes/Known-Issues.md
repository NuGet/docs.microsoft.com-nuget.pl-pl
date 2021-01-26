---
title: Znane problemy
description: Znane problemy związane z pakietem NuGet, w tym uwierzytelnianie, instalacja pakietu i narzędzia.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e6030670875192470fa47de84066281e45ac3eff
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777295"
---
# <a name="known-issues-with-nuget"></a>Znane problemy związane z pakietem NuGet

Są to najczęstsze znane problemy związane z pakietem NuGet, które są wielokrotnie raportowane. Jeśli masz problemy z instalowaniem NuGet lub zarządzaniem pakietami, zapoznaj się z tymi znanymi problemami i ich rozwiązaniami.

> [!Note]
> Począwszy od programu NuGet 4,0, znane problemy są częścią odpowiednich informacji o wersji.

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>Problemy z uwierzytelnianiem ze źródłami danych NuGet w programie VSTS z użyciem nuget.exe v 3.4.3

**Problem:**

Gdy korzystamy z następującego polecenia do przechowywania poświadczeń, będziemy mieć podwójne szyfrowanie osobistego tokenu dostępu.

$PAT = "osobisty token dostępu" $Feed = "Twój adres URL" .\nuget.exe źródła Dodaj nazwę test-Źródło $Feed-UserName $UserName-Password $PAT

**Obejście problemu:**

Przechowuj hasła w postaci zwykłego tekstu przy użyciu opcji [-StorePasswordInClearText](../reference/cli-reference/cli-ref-sources.md) .

## <a name="error-installing-packages-with-nuget-34-341"></a>Błąd podczas instalowania pakietów z pakietem NuGet 3,4,

**Problem:**

W programie NuGet 3,4 i w przypadku korzystania z dodatku NuGet żadne źródła nie są raportowane jako dostępne i nie można dodać nowych źródeł w oknie konfiguracji. Wynik jest podobny do poniższego obrazu:

![Konfiguracja NuGet bez źródeł](./media/knownIssue-34-NoSources.PNG)

`NuGet.Config`Plik w `%AppData%\NuGet\` folderze (Windows) lub `~/.nuget/` (Mac/Linux) przypadkowo został opróżniony. Aby rozwiązać ten problem: Zamknij program Visual Studio (w systemie Windows, jeśli ma to zastosowanie), Usuń `NuGet.Config` plik, a następnie spróbuj ponownie wykonać operację. Pakiet NuGet wygenerował nowe `NuGet.Config` i należy mieć możliwość przejścia.

## <a name="error-installing-packages-with-nuget-27"></a>Błąd podczas instalowania pakietów przy użyciu narzędzia NuGet 2,7

**Problem:**

W programie NuGet 2,7 lub nowszym podczas próby zainstalowania dowolnego pakietu, który zawiera odwołania do zestawów, może zostać wyświetlony komunikat o błędzie **"ciąg wejściowy nie ma poprawnego formatu"**, jak poniżej:

```ps
install-package log4net
    Installing 'log4net 2.0.0'.
    Successfully installed 'log4net 2.0.0'.
    Adding 'log4net 2.0.0' to Tyson.OperatorUpload.
    Install failed. Rolling back...
    install-package : Input string was not in a correct format.
    At line:1 char:1
        install-package log4net
        ~~~~~~~~~~~~~~~~~~~~~~~
        CategoryInfo : NotSpecified: (:) [Install-Package], FormatException
        FullyQualifiedErrorId : NuGetCmdletUnhandledException,NuGet.PowerShell.Commands.InstallPackageCommand
```

Przyczyną jest to, że biblioteka typów `VSLangProj.dll` składnika com jest wyrejestrowana w systemie. Taka sytuacja może wystąpić, jeśli na przykład masz dwie wersje programu Visual Studio, które zostały zainstalowane obok siebie, a następnie odinstalujesz starszą wersję. Wykonanie tej czynności może przypadkowo wyrejestrować powyższą bibliotekę COM.

**Rozwiązanie:**

Uruchom to polecenie w wierszu polecenia z **podwyższonym poziomem uprawnień** , aby ponownie zarejestrować bibliotekę typów dla `VSLangProj.dll`

```
regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"
```

Jeśli polecenie nie powiedzie się, sprawdź, czy plik istnieje w tej lokalizacji.

Aby uzyskać więcej informacji na temat tego błędu, zobacz ten [element roboczy](https://nuget.codeplex.com/workitem/3609 "Element roboczy 3609").

## <a name="build-failure-after-package-update-in-vs-2012"></a>Błąd kompilacji po aktualizacji pakietu w programie VS 2012

Problem: używasz programu VS 2012 RTM. Podczas aktualizacji pakietów NuGet otrzymujesz następujący komunikat: "nie można ukończyć odinstalowywania co najmniej jednego pakietu". zostanie wyświetlony monit o ponowne uruchomienie programu Visual Studio. Po ponownym uruchomieniu programu VS należy uzyskać błędy kompilacji brzmienia.

Przyczyną jest to, że niektóre pliki w starych pakietach są blokowane przez proces MSBuild w tle. Nawet po ponownym uruchomieniu programu VS, proces MSBuild w tle nadal używa plików w starych pakietach, co powoduje błędy kompilacji.

Poprawka ma na celu zainstalowanie aktualizacji programu VS 2012, np. VS 2012 Update 2.

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>Uaktualnienie do najnowszego NuGet ze starszej wersji powoduje błąd weryfikacji podpisu

Jeśli korzystasz z programu VS 2010 z dodatkiem SP1, możesz uruchomić następujący komunikat o błędzie, próbując uaktualnić program NuGet, jeśli masz zainstalowaną starszą wersję.

![Instalator rozszerzenia programu Visual Studio](./media/Visual-Studio-Extension-Installer.png)

Podczas przeglądania dzienników może pojawić się wzmianka o `SignatureMismatchException` .

Aby temu zapobiec, istnieje [poprawka programu Visual Studio 2010 z dodatkiem SP1](http://bit.ly/vsixcertfix) , którą można zainstalować.
Obejście polega na tym, że po prostu Odinstaluj pakiet NuGet (przy użyciu programu Visual Studio jako administrator), a następnie zainstaluj go z galerii rozszerzeń programu VS. Aby uzyskać więcej informacji, zobacz <https://support.microsoft.com/kb/2581019>.

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>Konsola Menedżera pakietów zgłasza wyjątek, gdy zainstalowano również Add-In reflektora programu Visual Studio.

Podczas uruchamiania konsoli Menedżera pakietów można uruchomić następujący komunikat o wyjątku, jeśli zainstalowano dodatek "reflektor".

```
The following error occurred while loading the extended type data file:
Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
Error in type "System.Security.AccessControl.ObjectSecurity":
Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
value of type "System.String" to type "System.Type".
System.Management.Automation.ActionPreferenceStopException:
Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
is set to Stop: Unable to find type
```

lub

```
System.Management.Automation.CmdletInvocationException: Could not load file or assembly 'Scripts\nuget.psm1' or one of its dependencies. <br />The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) ---&gt; System.IO.FileLoadException: Could not load file or <br />assembly 'Scripts\nuget.psm1' or one of its dependencies. The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) <br />---&gt; System.ArgumentException: Illegal characters in path.
    at System.IO.Path.CheckInvalidPathChars(String path)
    at System.IO.Path.Combine(String path1, String path2)
    at Microsoft.VisualStudio.Platform.VsAppDomainManager.<AssemblyPaths>d__1.MoveNext()
    at Microsoft.VisualStudio.Platform.VsAppDomainManager.InnerResolveHandler(String name)
    at Microsoft.VisualStudio.Platform.VsAppDomainManager.ResolveHandler(Object sender, ResolveEventArgs args)
    at System.AppDomain.OnAssemblyResolveEvent(RuntimeAssembly assembly, String assemblyFullName)
    --- End of inner exception stack trace ---
    at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadBinaryModule(Boolean trySnapInName, String moduleName, String fileName, <br />Assembly assemblyToLoad, String moduleBase, SessionState ss, String prefix, Boolean loadTypes, Boolean loadFormats, Boolean&amp; found)
    at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleNamedInManifest(String moduleName, String moduleBase, <br />Boolean searchModulePath, <br />String prefix, SessionState ss, Boolean loadTypesFiles, Boolean loadFormatFiles, Boolean&amp; found)
    at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleManifest(ExternalScriptInfo scriptInfo, ManifestProcessingFlags <br />manifestProcessingFlags, Version version)
    at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModule(String fileName, String moduleBase, String prefix, SessionState ss, <br />Boolean&amp; found)
    at Microsoft.PowerShell.Commands.ImportModuleCommand.ProcessRecord()
    at System.Management.Automation.Cmdlet.DoProcessRecord()
    at System.Management.Automation.CommandProcessor.ProcessRecord()
    --- End of inner exception stack trace ---
    at System.Management.Automation.Runspaces.PipelineBase.Invoke(IEnumerable input)
    at System.Management.Automation.Runspaces.Pipeline.Invoke()
    at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Invoke(String command, Object input, Boolean outputResults)
    at NuGetConsole.Host.PowerShell.Implementation.PowerShellHostExtensions.ImportModule(PowerShellHost host, String modulePath)
    at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.LoadStartupScripts()
    at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Initialize()
    at NuGetConsole.Implementation.Console.ConsoleDispatcher.Start()
    at NuGetConsole.Implementation.PowerConsoleToolWindow.MoveFocus(FrameworkElement consolePane)
```

Skontaktujemy się z autorem dodatku w nadziei o rozwiązaniu problemu.

<p class="info">Aktualizacja: sprawdzono, że Najnowsza wersja reflektora 6,5 nie powoduje już wystąpienia tego wyjątku w konsoli programu.</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>Otwieranie konsoli Menedżera pakietów kończy się niepowodzeniem z powodu wyjątku ObjectSecurity

Te błędy mogą pojawić się podczas próby otwarcia konsoli Menedżera pakietów:

```
The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
```

Jeśli tak, postępuj zgodnie z rozwiązaniem [omówionym w StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) , aby je rozwiązać.

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>Okno dialogowe Dodaj odwołanie do biblioteki pakietów zgłasza wyjątek, jeśli rozwiązanie zawiera projekt InstallShield Limited Edition

Zidentyfikowano, że jeśli rozwiązanie zawiera co najmniej jeden projekt InstallShield Limited Edition, w oknie dialogowym **Dodawanie odwołania do biblioteki pakietów** zostanie zgłoszony wyjątek, gdy zostanie otwarty. Obecnie nie istnieje jeszcze obejście tego problemu, z wyjątkiem usuwania projektów InstallShield lub ich wyładowywania.

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>Przycisk odinstalowywania został wyszarzony? Pakiet NuGet wymaga uprawnień administratora do zainstalowania/odinstalowania

Jeśli spróbujesz odinstalować pakiet NuGet za pomocą Menedżera rozszerzeń programu Visual Studio, możesz zauważyć, że przycisk Odinstaluj jest wyłączony. Pakiet NuGet wymaga dostępu administratora do instalacji i dezinstalacji. Uruchom ponownie program Visual Studio jako administrator, aby odinstalować rozszerzenie. Pakiet NuGet nie wymaga dostępu administratora do korzystania z niego.

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>Konsola Menedżera pakietów ulega awarii, gdy otworzysz ją w systemie Windows XP. Co jest nie tak?

Pakiet NuGet wymaga środowiska uruchomieniowego PowerShell 2,0. Domyślnie system Windows XP nie ma programu PowerShell 2,0. Środowisko uruchomieniowe programu PowerShell 2,0 można pobrać z programu <https://support.microsoft.com/kb/968929> . Po zainstalowaniu należy ponownie uruchomić program Visual Studio, aby móc otworzyć konsolę Menedżera pakietów.

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>Jeśli konsola Menedżera pakietów jest otwarta, program Visual Studio 2010 z dodatkiem SP1 w wersji beta jest nieoczekiwany.

Jeśli zainstalowano program Visual Studio 2010 z dodatkiem SP1 Beta, można zauważyć, że Jeśli opuścisz konsolę Menedżera pakietów otwartą i zamkniętą program Visual Studio, wystąpi awaria. Jest to znany problem programu Visual Studio, który zostanie rozwiązany w wersji RTM programu SP1. Na razie po prostu zignoruj awarię lub Odinstaluj program SP1 w wersji beta, jeśli jest to możliwe.

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>Element "Metadata"... występuje nieprawidłowy wyjątek elementu podrzędnego

Jeśli zainstalowano pakiety skompilowane przy użyciu wersji wstępnej programu NuGet, może wystąpić komunikat o błędzie z informacją o tym, że "element" metadanych "w przestrzeni nazw" schemas.microsoft.com/packaging/2010/07/nuspec.xsd "ma nieprawidłowy element podrzędny" podczas uruchamiania wersji RTM pakietu NuGet z tym projektem. Należy odinstalować, a następnie zainstalować ponownie każdy pakiet przy użyciu wersji RTM programu NuGet.

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a>Próba zainstalowania lub odinstalowania wyników spowoduje błąd "nie można utworzyć pliku, gdy ten plik już istnieje".

Z jakiegoś powodu rozszerzenia programu Visual Studio mogą być w stanie brzmienia, w którym odinstalowano rozszerzenie VSIX, ale niektóre pliki zostały pozostawione w tle. Aby obejść ten problem:

1. Wyjdź z programu Visual Studio
1. Otwórz następujący folder (może on znajdować się na innym dysku na komputerze)

    C:\Program Files (x86) \Microsoft Visual Studio 10.0 \ Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\

1. Usuń wszystkie pliki z rozszerzeniami *. Deleteme* .
1. Otwórz ponownie program Visual Studio

Po wykonaniu tych kroków powinno być możliwe kontynuowanie.

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>W rzadkich przypadkach Kompilowanie z włączoną analizą kodu powoduje wystąpienie błędu.

Następujący błąd może wystąpić, Jeśli instalujesz FluentNHibernate z konsolą Menedżera pakietów, a następnie kompilujesz projekt z włączoną funkcją "Analiza kodu".

```
Error 3 CA0058 : The referenced assembly
'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
could not be found. This assembly is required for analysis and was referenced by:
C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
MyProject.UnitTests
```

Domyślnie FluentNHibernate wymaga NHibernate 3.0.0.2001. Jednak po zaprojektowaniu pakiet NuGet zainstaluje NHibernate 3.0.0.4000 w projekcie i doda odpowiednie przekierowania powiązań, aby działał. Projekt zostanie skompilowany, jeśli analiza kodu nie jest włączona. W przeciwieństwie do kompilatora Narzędzie analizy kodu nie jest prawidłowo zgodne z przekierowaniami powiązań, aby użyć 3.0.0.4000 zamiast 3.0.0.2001. Problem można obejść, instalując NHibernate 3.0.0.2001 lub poinformuj Narzędzie analizy kodu, aby zachowywać się tak samo jak kompilator, wykonując następujące czynności:

1. Przejdź do pozycji *%ProgramFiles%\Microsoft Visual Studio 10.0 \ Team Tools\Static Analysis Tools\FxCop*
1. Otwórz FxCopCmd.exe.config i Zmień `AssemblyReferenceResolveMode` z `StrongName` na `StrongNameIgnoringVersion` .
1. Zapisz zmiany i ponownie skompiluj projekt.

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>Polecenie Write-Error nie działa wewnątrz install.ps1/uninstall.ps1/init.ps1

Jest to znany problem. Zamiast wywołania metody Write-Error spróbuj wywołać metodę throw.

```
throw "My error message"
```

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>Instalowanie pakietu NuGet z ograniczonym dostępem w systemie Windows 2003 może spowodować awarię programu Visual Studio

Przy próbie zainstalowania narzędzia NuGet przy użyciu Menedżera rozszerzeń programu Visual Studio i niedziałającego jako administrator zostanie wyświetlone okno dialogowe &#8220;Uruchom jako&#8221; z checkboxem z etykietą &#8220;Uruchom ten program z ograniczonym dostępem&#8221; domyślnie zaznaczone.

![Uruchom jako okno dialogowe z ograniczeniami](./media/RunAsRestricted.png)

Kliknięcie przycisku OK powoduje awarię programu Visual Studio. Przed zainstalowaniem programu NuGet Usuń zaznaczenie tej opcji.

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>Nie można odinstalować programu NuGet dla narzędzi Windows Phone

Narzędzia Windows Phone nie obsługują Menedżera rozszerzeń programu Visual Studio. Aby odinstalować pakiet NuGet, uruchom następujące polecenie.

```
vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5
```

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>Zmiana wielkości liter w identyfikatorach pakietów NuGet powoduje przerwanie przywracania pakietu

Zgodnie z opisem w [tym problemie](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932)w serwisie GitHub, zmiana wielkości liter pakietów NuGet może odbywać się przez obsługę NuGet, ale powoduje komplikacje podczas przywracania pakietów dla użytkowników, którzy mają istniejące, w różny sposób, pakiety w folderze *Global-Packages* . Zalecamy tylko żądanie zmiany wielkości liter, gdy istnieje możliwość komunikowania się z istniejącymi użytkownikami pakietu w sprawie przerwy, która może wystąpić w przypadku przywracania pakietu w czasie kompilacji.

## <a name="reporting-issues"></a>Raportowanie problemów

Aby zgłosić problemy z pakietem NuGet, odwiedź stronę [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues) .
