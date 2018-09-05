---
title: Znane problemy
description: Znane problemy związane z tym instalacji pakietu aktualizacji, uwierzytelniania i narzędzia NuGet.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fc338ba3810a125f638a937cf14456bf519a24a8
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548477"
---
# <a name="known-issues-with-nuget"></a>Znane problemy z NuGet

Są to najczęściej znane problemy z NuGet, które często są zgłaszane. Jeśli występują problemy z zainstalowaniem NuGet lub zarządzania pakietami, zapoznaj się za pośrednictwem tych znane problemy i ich rozwiązania.

> [!Note]
> Począwszy od NuGet 4.0, znane problemy są częścią odpowiedniej wersji.

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>Problemy z uwierzytelnianiem za pomocą NuGet źródeł danych w usłudze VSTS za pomocą nuget.exe v3.4.3

**Problem:**

Gdy obsługujemy za pomocą następującego polecenia do przechowywania poświadczeń, firma Microsoft znajdą się podwójnego szyfrowania osobisty Token dostępu.

$PAT = "Twój osobisty token dostępu" $Feed = "url".\nuget.exe źródeł add - nazwa testu-$UserName $Feed źródła - UserName-$PAT hasła

**Obejście:**

Store hasła w postaci zwykłego tekstu przy użyciu [- StorePasswordInClearText](../tools/cli-ref-sources.md) opcji.

## <a name="error-installing-packages-with-nuget-34-341"></a>Błąd podczas instalowania pakietów z NuGet 3.4 3.4.1

**Problem:**

NuGet 3.4 i 3.4.1 korzystając z dodatku programu NuGet, żadnych źródeł są zgłaszane jako dostępne i nie można dodać nowe źródła w oknie konfiguracji. Wynik jest podobna do poniższej ilustracji:

![Config NuGet za pomocą żadnych źródeł](./media/knownIssue-34-NoSources.PNG)

`NuGet.Config` Plików w Twojej `%AppData%\NuGet\` (Windows) lub `~/.nuget/` przypadkowo został opróżniony folder (Mac/Linux). Aby rozwiązać ten problem: Zamknij program Visual Studio (w Windows, jeśli ma to zastosowanie), Usuń `NuGet.Config` pliku i spróbuj ponownie wykonać operację. NuGet wygenerował nowy `NuGet.Config` i powinno być możliwe kontynuować.

## <a name="error-installing-packages-with-nuget-27"></a>Błąd podczas instalowania pakietów z NuGet w wersji 2.7

**Problem:**

W NuGet w wersji 2.7 lub powyżej, gdy spróbujesz zainstalować dowolny pakiet, który zawiera odwołania do zestawów, otrzymasz komunikat o błędzie **"ciąg wejściowy nie jest w poprawnym formacie."** , tak jak poniżej:

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

Jest to spowodowane przez biblioteki typów dla `VSLangProj.dll` składnika COM wyrejestrowywany w Twoim systemie. Może się to zdarzyć, na przykład, jeśli masz dwie wersje programu Visual Studio zainstalowane side-by-side i następnie odinstaluj starszą wersję. Ten sposób może przypadkowo wyrejestrować powyżej biblioteki COM.

**Rozwiązanie:**:

Uruchom następujące polecenie z **wiersz** ponownie zarejestrować biblioteki typów `VSLangProj.dll`

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

Jeśli polecenie zakończy się niepowodzeniem, sprawdź, czy plik istnieje w tej lokalizacji.

Aby uzyskać więcej informacji na temat tego błędu, zobacz ten [elementu roboczego](https://nuget.codeplex.com/workitem/3609 "elementu roboczego 3609").

## <a name="build-failure-after-package-update-in-vs-2012"></a>Błąd kompilacji, po zainstalowaniu pakietu aktualizacji w programie VS 2012

Problem: w przypadku korzystania z programu VS 2012 RTM. Podczas aktualizowania pakietów NuGet, zostanie wyświetlony ten komunikat: "nie można wykonać jeden lub więcej pakietów odinstalowane." i zostanie wyświetlony monit o ponowne uruchomienie programu Visual Studio. Po ponownym uruchomieniu programu VS, pojawiają się błędy nieco dziwne kompilacji.

Przyczyną jest to, że niektórych plików w starym pakiety są zablokowane przez tła procesu programu MSBuild. Nawet w przypadku, po ponownym uruchomieniu programu VS, tło procesu programu MSBuild nadal używa plików w starym pakietów, powodując błędy kompilacji.

Obejście polega na zainstalowaniu programu VS 2012 Update, np. programu VS 2012 Update 2.

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>Uaktualnienie do najnowszego rozwiązania NuGet ze starszej wersji powoduje, że błąd weryfikacji podpisu

Jeśli używasz programu VS 2010 z dodatkiem SP1, możesz napotkać komunikat o błędzie podczas próby uaktualnienia NuGet, jeśli masz starszą wersję zainstalowane.

![Instalator rozszerzenia programu Visual Studio](./media/Visual-Studio-Extension-Installer.png)

Podczas wyświetlania dziennika, może wyświetlić informację o `SignatureMismatchException`.

Aby temu zapobiec, jest [poprawki programu Visual Studio 2010 SP1](http://bit.ly/vsixcertfix) można zainstalować.
Alternatywnie obejściem jest po prostu Odinstaluj NuGet (podczas uruchamiania programu Visual Studio jako Administrator), a następnie zainstalować go z galerii rozszerzeń programu VS.  Zobacz [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Aby uzyskać więcej informacji.

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>Konsola Menedżera pakietów zgłasza wyjątek, gdy odblaskowego Visual Studio dodatek programu jest również instalowany.

Podczas uruchamiania konsoli Menedżera pakietów, może wystąpić następujący komunikat o wyjątku w przypadku dodatek VS odblaskowego zainstalowane.

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

Kontaktujemy się z autorem dodatku w nadziei pracy na poziomie rozwiązania.

<p class="info">Aktualizacja: Firma Microsoft została zweryfikowana czy najnowszą wersję odblaskowego, 6.5, nie powoduje już tego wyjątku w konsoli programu.</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>Konsola Menedżera pakietów otwierania zakończy się niepowodzeniem z wyjątkiem niepoprawny

Możesz zobaczyć te błędy podczas próby otwarcia konsoli Menedżera pakietów:

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

Jeśli tak, postępuj zgodnie z rozwiązania [opisem na stronie StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) rozwiązywania tych problemów.

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>Okno dialogowe Dodaj odwołanie do pakietu biblioteki zgłasza wyjątek, jeśli rozwiązanie zawiera projekt InstallShield Limited Edition

Firma Microsoft ma ustaliła, że jeśli Twoje rozwiązanie zawiera co najmniej jeden projekt InstallShield Limited Edition, **Dodaj odwołanie do pakietu biblioteki** okna dialogowego spowoduje zgłoszenie wyjątku po otwarciu. Obecnie nie ma sposobu obejścia jeszcze z wyjątkiem usuwanie projektów InstallShield lub zwalnianie je.

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>Odinstaluj wyszarzone przycisku? NuGet wymaga uprawnień administratora do instalacji/dezinstalacji

Jeśli zostanie podjęta próba odinstalowania NuGet za pomocą programu Visual Studio Extension Manager, można zauważyć, że przycisk Odinstaluj jest wyłączona. NuGet wymaga dostępu administratora do instalowania i odinstalowywania. Uruchom ponownie program Visual Studio jako administrator, aby odinstalować rozszerzenie. NuGet nie wymaga dostępu administratora z niego korzystać.

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>Konsola Menedżera pakietów ulega awarii podczas otwierania go w Windows XP. Co jest nie tak?

NuGet wymaga środowiska uruchomieniowego programu Powershell w wersji 2.0. Windows XP, domyślnie nie ma programu Powershell w wersji 2.0. Możesz pobrać program Powershell 2.0 środowisko uruchomieniowe z [ http://support.microsoft.com/kb/968929 ](http://support.microsoft.com/kb/968929). Po jego zainstalowaniu, uruchom ponownie program Visual Studio, a powinien mieć możliwość otwarcia konsoli Menedżera pakietów.

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>Visual Studio 2010 z dodatkiem SP1 Beta ulega awarii przy zamykaniu, jeśli konsola Menedżera pakietów jest otwarty.

Po zainstalowaniu programu Visual Studio 2010 z dodatkiem SP1 Beta można zauważyć, że jeśli zamykaj konsoli Menedżera pakietów, a następnie zamknij program Visual Studio, jego ulegnie awarii. Jest to znany problem programu Visual Studio i zostanie rozwiązany w wersji z dodatkiem SP1 RTM wydania. Teraz po prostu Ignoruj awarii lub odinstalować z dodatkiem SP1 Beta, jeżeli jest to możliwe.

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>Element "metadata"... ma nieprawidłowy element wyjątek występuje

Jeśli zainstalowano pakiety skompilowane przy użyciu wersji wstępnej programu NuGet, może wystąpić komunikat o błędzie z informacją "elementem"metadata"w przestrzeni nazw"schemas.microsoft.com/packaging/2010/07/nuspec.xsd"ma nieprawidłowy element podrzędny" podczas uruchamiania RTM Wersja pakietu nuget za pomocą tego projektu. Należy odinstalować i ponownie zainstalować każdego pakietu NuGet w wersji RTM.

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a>Próby zainstalowania lub odinstalowania powoduje błąd "Nie można utworzyć pliku, ten plik już istnieje."

Jakiegoś powodu rozszerzeń programu Visual Studio można uzyskać w stanie nieco dziwne, gdzie zostały odinstalowane rozszerzenia VSIX, ale niektóre pliki zostały pozostawione. Aby obejść ten problem:

1. Zamknij program Visual Studio
1. Otwórz następujący folder (może to być na innym dysku na komputerze)

    C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\

1. Usuń wszystkie pliki z *.deleteme* rozszerzenia.
1. Otwórz ponownie program Visual Studio

Po wykonaniu tych kroków, można kontynuować.

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>W rzadkich przypadkach kompilowanie za pomocą analizy kodu włączona, powoduje błąd.

Może być występuje następujący błąd, jeśli zainstaluje FluentNHibernate za pomocą konsoli Menedżera pakietów, a następnie Skompiluj projekt za pomocą "Analizy kodu" włączona.

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

Domyślnie FluentNHibernate wymaga NHibernate 3.0.0.2001. Jednak zgodnie z projektem NuGet zainstalujesz NHibernate 3.0.0.4000 w projekcie i dodaj odpowiednie powiązanie przekierowuje, dzięki czemu będzie ona działać. Projekt zostanie skompilowany świetnie Jeśli nie włączono analizy kodu. W przeciwieństwie do kompilatora narzędzie do analizy kodu nie prawidłowo wykonaj przekierowania powiązań do używania 3.0.0.4000 zamiast 3.0.0.2001. Można obejść ten problem, albo instalowanie NHibernate 3.0.0.2001 lub poproś narzędzie do analizy kodu do działa tak samo jak kompilator, wykonując następujące czynności:

1. Przejdź do *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static analizy Tools\FxCop*
1. Otwórz FxCopCmd.exe.config i zmień `AssemblyReferenceResolveMode` z `StrongName` do `StrongNameIgnoringVersion`.
1. Zapisz zmiany i ponownie skompiluj projekt.

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>Błąd zapisu polecenie nie działa wewnątrz install.ps1/uninstall.ps1/init.ps1

Jest to znany problem. Zamiast wywoływania błąd zapisu, spróbuj wywoływania throw.

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>Instalowanie NuGet z ograniczonym dostępem w systemie Windows 2003 można awarię programu Visual Studio

Podczas próby zainstalowania NuGet za pomocą Menedżera rozszerzeń programu Visual Studio, a nie jest uruchomione jako administrator, &#8220;Uruchom jako&#8221; za pomocą pola wyboru zostanie wyświetlone okno dialogowe &#8220;uruchamiaj ten program z ograniczonym dostępem&#8221; sprawdzana przez Domyślnie.

![Uruchom jako ograniczeniami okna dialogowego](./media/RunAsRestricted.png)

Kliknięcie przycisku OK, korzystając z niego zaznaczone awarie programu Visual Studio. Upewnij się, usuń zaznaczenie tej opcji, przed zainstalowaniem programu NuGet.

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>Nie można odinstalować programu NuGet dla narzędzi Windows Phone

Narzędzia Windows Phone nie ma obsługi Menedżera rozszerzeń dla programu Visual Studio. Aby odinstalować NuGet, uruchom następujące polecenie.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>Zmiana wielkości liter, identyfikatory pakietu NuGet przerywa Przywracanie pakietu

Zgodnie z opisem szeroko na [problem w usłudze GitHub](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), zmiana wielkości liter pakietów NuGet może odbywać się przez obsługę pakietów NuGet, ale kompilacji powoduje, że podczas przywracania pakietu dla użytkowników, którzy mają istniejące, inaczej — z uwzględnieniem wielkości liter, pakiety w ich *globalnymi pakietami* folderu. Firma Microsoft zaleca tylko żądania zmiany wielkości liter, gdy masz sposób do komunikowania się z istniejącym użytkownikom pakietu o przerwania, który może wystąpić, aby ich przywracania pakietów w czasie kompilacji.

## <a name="reporting-issues"></a>Raportowanie problemów

Aby zgłosić problemy z NuGet, odwiedź stronę [ https://github.com/nuget/home/issues ](https://github.com/nuget/home/issues).
