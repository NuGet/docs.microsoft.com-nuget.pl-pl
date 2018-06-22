---
title: Znane problemy
description: Znane problemy związane z tym instalacji pakietu aktualizacji, uwierzytelniania i narzędzia NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1f170f377a3394694e953a794f2c814388656c21
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822022"
---
# <a name="known-issues-with-nuget"></a>Znane problemy dotyczące programu NuGet

Są to najczęściej znane problemy z programem NuGet wielokrotnie są zgłaszane. Jeśli występują problemy dotyczące instalowania NuGet lub Poświęć zarządzania pakietami, przejrzyj następujące znane problemy i ich rozwiązania.

> [!Note]
> Począwszy od NuGet 4.0, znanych problemów są częścią odpowiednie informacje o wersji.

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>Problemy z uwierzytelnianiem nuget źródeł w programu VSTS z nuget.exe v3.4.3

**Problem:**

Możemy użyć następującego polecenia do przechowywania poświadczeń, możemy zakończyć się dwa razy szyfrowania osobisty Token dostępu.

$PAT = "Twoje osobisty token dostępu" $Feed = "url".\nuget.exe źródeł add - nazwa testu — $UserName $Feed źródła - UserName-$PAT hasła

**Obejście problemu:**

Przechowywania haseł w postaci zwykłego tekstu przy użyciu [- StorePasswordInClearText](../tools/cli-ref-sources.md) opcji.

## <a name="error-installing-packages-with-nuget-34-341"></a>Błąd podczas instalowania pakietów z NuGet 3.4 3.4.1

**Problem:**

W NuGet 3.4 i 3.4.1 używając dodatku NuGet żadnych źródeł są zgłaszane jako dostępne i nie można dodać nowego źródła w oknie Konfiguracja. Wynik jest podobny do obraz poniżej:

![Konfiguracja NuGet z żadnymi źródłami](./media/knownIssue-34-NoSources.PNG)

`NuGet.Config` Plików w sieci `%AppData%\NuGet\` (system Windows) lub `~/.nuget/` przypadkowo został opróżniony folder (system Mac/Linux). Aby rozwiązać ten problem: Zamknij program Visual Studio (w systemie Windows, jeśli ma to zastosowanie), Usuń `NuGet.Config` plik i spróbuj ponownie wykonać operację. NuGet wygenerował nowy `NuGet.Config` i powinno być możliwe kontynuować.

## <a name="error-installing-packages-with-nuget-27"></a>Błąd podczas instalowania pakietów z NuGet 2.7

**Problem:**

NuGet 2.7 lub powyżej, podczas próby zainstalowania dowolnego pakietu, który zawiera odwołania do zestawów, może zostać wyświetlony komunikat o błędzie **"ciąg wejściowy nie był w poprawnym formacie."** , tak jak poniżej:

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

Jest to spowodowane biblioteki typów dla `VSLangProj.dll` składnika modelu COM wyrejestrowywany w tym systemie. Może się to zdarzyć, na przykład, jeśli masz dwie wersje programu Visual Studio zainstalowany side-by-side, a następnie odinstaluj starszą wersję. W ten sposób mogą przypadkowo wyrejestrować powyżej biblioteki COM.

**Rozwiązanie:**:

Uruchom to polecenie z **podniesionego wiersza** Aby ponownie zarejestrować biblioteki typów `VSLangProj.dll`

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

Jeśli polecenie nie powiedzie się, sprawdź, czy plik istnieje w tej lokalizacji.

Aby uzyskać więcej informacji na temat tego błędu, zobacz [elementu roboczego](https://nuget.codeplex.com/workitem/3609 "elementu roboczego 3609").

## <a name="build-failure-after-package-update-in-vs-2012"></a>Niepowodzenie kompilacji, po zainstalowaniu pakietu aktualizacji w wersji programu VS 2012

Problem: w przypadku korzystania z wersji programu VS 2012 RTM. Podczas aktualizowania pakietów NuGet, ten komunikat: "nie można ukończyć co najmniej jednego pakietu odinstalowane." i zostanie wyświetlony monit o ponowne uruchomienie programu Visual Studio. Po ponownym uruchomieniu programu VS, występują błędy kompilacji nieco dziwne.

Przyczyną jest to, że niektóre pliki w pakietach starego jest zablokowany przez tła procesu programu MSBuild. Nawet w przypadku, po ponownym uruchomieniu programu VS, tło procesu programu MSBuild nadal używa plików w starym pakietów powodujące błędy kompilacji.

Poprawka jest aktualizacji VS 2012, np. VS 2012 Update 2.

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>Uaktualnianie do najnowszej NuGet ze starszej wersji powoduje błąd weryfikacji podpisu

Jeśli korzystasz z VS 2010 z dodatkiem SP1, możesz napotkać komunikat o błędzie podczas próby uaktualnienia NuGet, jeśli masz starszą wersję zainstalowane.

![Instalator rozszerzenia programu Visual Studio](./media/Visual-Studio-Extension-Installer.png)

Podczas wyświetlania dzienniki, można napotkać informację o `SignatureMismatchException`.

Aby temu zapobiec, jest [poprawki programu Visual Studio 2010 z dodatkiem SP1](http://bit.ly/vsixcertfix) można zainstalować.
Alternatywnie obejściem jest po prostu Odinstaluj NuGet (podczas uruchamiania programu Visual Studio jako Administrator), a następnie zainstalować go z galerii rozszerzeń programu VS.  Zobacz [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Aby uzyskać więcej informacji.

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>Konsola Menedżera pakietów zgłasza wyjątek, gdy reflektora Visual Studio dodatek jest również instalowany.

Podczas uruchamiania konsoli Menedżera pakietów, może wystąpić następujący komunikat o wyjątku Jeśli masz dodatku VS reflektora zainstalowane.

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

lub

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

Zostały możemy skontaktować się z autorem dodatku w nadziei pracy się, że rozdzielczość.

<p class="info">Aktualizacja: Firma Microsoft zweryfikowano czy najnowsza wersja reflektor, 6.5, już nie powoduje, że tego wyjątku w konsoli.</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>Konsola Menedżera pakietów otwierania zakończy się niepowodzeniem z wyjątkiem niepoprawny

Te błędy napotkać podczas próby otwarcia konsoli Menedżera pakietów:

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

Jeśli tak, postępuj zgodnie z rozwiązania [omówione w witrynie StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) rozwiązywania tych problemów.

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>Okno dialogowe Dodaj odwołanie do biblioteki pakietu zgłasza wyjątek, jeśli rozwiązanie zawiera InstallShield Limited Edition projektu

Ma określiliśmy, że jeśli rozwiązanie zawiera co najmniej jeden projekt InstallShield Limited Edition, **Dodaj odwołanie do biblioteki pakietu** okna dialogowego spowoduje zgłoszenie wyjątku po otwarciu. Nie istnieje obecnie obejście jeszcze z wyjątkiem usuwanie projektów InstallShield albo zwalnianie je.

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>Odinstaluj przycisk nieaktywna? NuGet wymaga uprawnień administratora do instalacji/dezinstalacji

Jeśli użytkownik próbuje odinstalować NuGet Menedżera rozszerzenia za pomocą programu Visual Studio, mogą pojawić się wyłączeniu przycisk Odinstaluj. NuGet wymaga dostępu administracyjnego do instalowania i odinstalowywania. Uruchom ponownie program Visual Studio jako administrator, aby odinstalować rozszerzenia. NuGet nie wymaga dostępu administracyjnego z niego korzystać.

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>Konsola Menedżera pakietów ulega awarii podczas otwierania go w systemie Windows XP. Co jest nie tak?

NuGet wymaga środowiska uruchomieniowego programu Powershell 2.0. Windows XP, domyślnie nie ma programu Powershell 2.0. Możesz pobrać środowiska uruchomieniowego programu Powershell 2.0 z [ http://support.microsoft.com/kb/968929 ](http://support.microsoft.com/kb/968929). Po jej zainstalowaniu, uruchom ponownie program Visual Studio i powinno być możliwe otworzyć konsolę Menedżera pakietów.

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>Visual Studio 2010 z dodatkiem SP1 Beta ulega awarii przy zamykaniu, jeśli konsola Menedżera pakietów jest otwarty.

Po zainstalowaniu programu Visual Studio 2010 z dodatkiem SP1 Beta, możesz zauważyć, że pozostaw otwarte konsoli Menedżera pakietów, zamknij program Visual Studio go ulegnie awarii. Jest to znany problem programu Visual Studio i zostanie rozwiązany w wersji RTM SP1 wersji. Teraz po prostu Ignoruj awarii lub odinstalować z dodatkiem SP1 Beta, jeśli to możliwe.

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>Element "metadanych"... ma nieprawidłowy element wyjątek występuje

Jeśli zainstalowano pakiety z wersji wstępnej programu NuGet, może wystąpić komunikat o błędzie "element"metadanych"w przestrzeni nazw"schemas.microsoft.com/packaging/2010/07/nuspec.xsd"ma nieprawidłowy element podrzędny" podczas uruchamiania RTM wersja programu NuGet z tego projektu. Należy odinstalować i ponownie zainstalować każdego pakietu NuGet w wersji RTM.

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a>Próby zainstalowania lub odinstalowania powoduje błąd "Nie można utworzyć pliku, ten plik już istnieje."

Niektóre przyczyny rozszerzeń programu Visual Studio można uzyskać w stanie nieco dziwne, gdzie został odinstalowany rozszerzenie VSIX, ale niektóre pliki zostały pozostawione. Aby obejść ten problem:

1. Zamknij program Visual Studio
1. Otwórz następujący folder (może to być na innym dysku na tym komputerze)

    C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\

1. Usuń wszystkie pliki z *.deleteme* rozszerzenia.
1. Otwórz ponownie program Visual Studio

Po wykonaniu tych kroków, można kontynuować.

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>W rzadkich przypadkach kompilowania za pomocą analizy kodu włączona powoduje błąd.

Może pobrać następujący błąd, jeśli instaluje FluentNHibernate z konsoli Menedżera pakietów, a następnie Skompiluj projekt z "Kod — analiza" włączone.

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

Domyślnie FluentNHibernate wymaga NHibernate 3.0.0.2001. Jednak zgodnie z założeniami NuGet zainstaluje NHibernate 3.0.0.4000 w projekcie i dodaj odpowiednie powiązanie przekierowuje, dzięki czemu będzie ona działać. Możesz projekt zostanie skompilowany świetnie, jeśli nie włączono analizy kodu. W przeciwieństwie do kompilatora narzędzie do analizy kodu nie będzie poprawnie zgodna przekierowania powiązania do użycia zamiast 3.0.0.2001 3.0.0.4000. Można obejść ten problem przez albo instalowania NHibernate 3.0.0.2001 lub poproś narzędzie do analizy kodu do działają tak samo, jak kompilator w następujący sposób:

1. Przejdź do *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*
1. Otwórz FxCopCmd.exe.config i zmień `AssemblyReferenceResolveMode` z `StrongName` do `StrongNameIgnoringVersion`.
1. Zapisz zmiany i ponownie skompiluj projekt.

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>Błąd zapisu polecenie nie działa wewnątrz install.ps1/uninstall.ps1/init.ps1

Jest to znany problem. Zamiast wywoływania Write-Error, spróbuj wywołać throw.

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>Instalowania NuGet z ograniczonym dostępem w systemie Windows 2003 można awarię programu Visual Studio

Podczas próby zainstalowania NuGet za pomocą Menedżera rozszerzenia programu Visual Studio i nie jest uruchomiona jako administrator, &#8220;Uruchom jako&#8221; z pola wyboru zostanie wyświetlone okno dialogowe &#8220;uruchomienia tego programu z ograniczonym dostępem&#8221; sprawdzana przez domyślne.

![Uruchom jako ograniczeniami okna dialogowego](./media/RunAsRestricted.png)

Kliknięcie przycisku OK z sprawdzanym ulega awarii programu Visual Studio. Upewnij się, usuń zaznaczenie tej opcji, przed zainstalowaniem NuGet.

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>Nie można odinstalować NuGet dla narzędzia Windows Phone

Narzędzia Windows Phone nie ma obsługi Menedżera rozszerzeń dla programu Visual Studio. Aby odinstalować program NuGet, uruchom następujące polecenie.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>Zmiana wielkości liter identyfikatorów pakietów NuGet dzieli przywracania pakietu

Zgodnie z opisem długości na [ten problem GitHub](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), zmiana wielkości liter pakietów NuGet może odbywać się przy pomocy technicznej NuGet, ale komplikacji powoduje, że podczas przywracania pakietu dla użytkowników, którzy mają istniejących, inaczej — z uwzględnieniem wielkości liter, pakiety w ich *globalne pakiety* folderu. Zaleca się tylko żądania zmiany wielkości, jeśli masz sposób komunikowania się z istniejących użytkowników do pakietu o przerwie, który może wystąpić, aby przywrócić ich czas kompilacji pakietu.

## <a name="reporting-issues"></a>Zgłaszanie problemów

Aby zgłosić problemy NuGet, odwiedź stronę [ https://github.com/nuget/home/issues ](https://github.com/nuget/home/issues).
