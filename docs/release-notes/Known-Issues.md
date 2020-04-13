---
title: Znane problemy
description: Znane problemy z NuGet, w tym uwierzytelnianie, instalacja pakietu i narzędzia.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8f2b33a7290301bd16db3b1979ae496eee602f55
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "75383661"
---
# <a name="known-issues-with-nuget"></a>Znane problemy z NuGet

Są to najczęściej znane problemy z NuGet, które są wielokrotnie zgłaszane. Jeśli masz problemy z instalacją NuGet lub zarządzanie pakietami, zapoznaj się z tymi znanymi problemami i ich rozwiązaniami.

> [!Note]
> Począwszy od NuGet 4.0, znane problemy są częścią odpowiednich informacji o wersji.

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>Problemy z uwierzytelnianiem z źródłami danych NuGet w programie VSTS z nuget.exe v3.4.3

**Problem:**

Gdy używamy następującego polecenia do przechowywania poświadczeń, kończy się podwójne szyfrowanie tokenu dostępu osobistego.

$PAT = "Twój osobisty token dostępu" $Feed = "Twój adres URL" .\nuget.exe źródła dodać -Name Test -Source $Feed -UserName $UserName -Password $PAT

**Obejście:**

Przechowuj hasła w postaci zwykłego tekstu za pomocą opcji [-StorePasswordInClearText.](../reference/cli-reference/cli-ref-sources.md)

## <a name="error-installing-packages-with-nuget-34-341"></a>Błąd podczas instalowania pakietów z nugetem 3.4, 3.4.1

**Problem:**

W NuGet 3.4 i 3.4.1, podczas korzystania z dodatku NuGet, żadne źródła nie są zgłaszane jako dostępne i nie można dodać nowych źródeł w oknie konfiguracji. Wynik jest podobny do poniższego obrazu:

![Konfiguracje NuGet bez źródeł](./media/knownIssue-34-NoSources.PNG)

Plik `NuGet.Config` w `%AppData%\NuGet\` folderze (Windows) lub `~/.nuget/` (Mac/Linux) został przypadkowo opróżniony. Aby rozwiązać ten problem: zamknij program Visual Studio `NuGet.Config` (w systemie Windows, jeśli dotyczy), usuń plik i spróbuj ponownie wykonać operację. NuGet wygenerował `NuGet.Config` nowy i powinieneś być w stanie kontynuować.

## <a name="error-installing-packages-with-nuget-27"></a>Błąd podczas instalowania pakietów z nugetem 2.7

**Problem:**

W NuGet 2.7 lub powyżej, podczas próby zainstalowania dowolnego pakietu, który zawiera odwołania do zestawu, może pojawić się komunikat o błędzie **"Ciąg wejściowy nie był w poprawnym formacie."**, jak poniżej:

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

Jest to spowodowane biblioteką `VSLangProj.dll` typów dla składnika COM, który jest wyrejestrowany w systemie. Może się tak zdarzyć, na przykład, gdy masz dwie wersje programu Visual Studio zainstalowane obok siebie, a następnie odinstalować starszą wersję. W ten sposób może przypadkowo wyrejestrować powyższej biblioteki COM.

**Rozwiązanie:**

Uruchom to polecenie z **monitu z podwyższonym poziomem uprawnień,** aby ponownie zarejestrować bibliotekę typów`VSLangProj.dll`

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

Jeśli polecenie nie powiedzie się, sprawdź, czy plik istnieje w tej lokalizacji.

Aby uzyskać więcej informacji na temat tego błędu, zobacz ten [element pracy](https://nuget.codeplex.com/workitem/3609 "Artykuł roboczy 3609").

## <a name="build-failure-after-package-update-in-vs-2012"></a>Awaria kompilacji po aktualizacji pakietu w programie VS 2012

Problem: Używasz VS 2012 RTM. Podczas aktualizowania pakietów NuGet, pojawi się ten komunikat: "Nie można odinstalować jednego lub więcej pakietów." i zostanie wyświetlony monit o ponowne uruchomienie programu Visual Studio. Po ponownym uruchomieniu vs, masz dziwne błędy kompilacji.

Przyczyną jest to, że niektóre pliki w starych pakietów są zablokowane przez proces MSBuild w tle. Nawet po ponownym uruchomieniu vs, w tle proces MSBuild nadal używa plików w starych pakietów, powodując błędy kompilacji.

Poprawka polega na zainstalowaniu aktualizacji programu VS 2012, np.

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>Uaktualnienie do najnowszego nuget ze starszej wersji powoduje błąd weryfikacji podpisu

Jeśli korzystasz z dodatku SP1 dla programu VS 2010, podczas próby uaktualnienia nuget może zostać wyświetlony następujący komunikat o błędzie.

![Instalator rozszerzenia programu Visual Studio](./media/Visual-Studio-Extension-Installer.png)

Podczas przeglądania dzienników może pojawić się `SignatureMismatchException`wzmianka o pliku .

Aby temu zapobiec, istnieje [poprawka dodatku SP1 programu Visual Studio 2010,](http://bit.ly/vsixcertfix) którą można zainstalować.
Alternatywnie obejście jest po prostu odinstalować NuGet (podczas uruchamiania programu Visual Studio jako administrator), a następnie zainstalować go z galerii rozszerzeń programu VS. Aby uzyskać więcej informacji, zobacz <https://support.microsoft.com/kb/2581019>.

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>Konsola Menedżera pakietów zgłasza wyjątek po zainstalowaniu dodatku Reflector Visual Studio.

Podczas uruchamiania konsoli Menedżera pakietów, można uruchomić następujący komunikat o wyjątku, jeśli masz zainstalowany dodatek Reflektor VS.

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

Skontaktowaliśmy się z autorem dodatku w nadziei na wypracowanie rozwiązania.

<p class="info">Aktualizacja: Sprawdziliśmy, że najnowsza wersja reflektora, 6.5, nie powoduje już tego wyjątku w konsoli.</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>Otwieranie konsoli Menedżera pakietów kończy się niepowodzeniem z wyjątkiem ObjectSecurity

Podczas próby otwarcia konsoli Menedżera pakietów mogą pojawić się następujące błędy:

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

Jeśli tak, postępuj zgodnie z rozwiązaniem [omówione na StackOverflow,](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) aby je naprawić.

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>Okno dialogowe Dodawanie odwołania do biblioteki pakietów zgłasza wyjątek, jeśli rozwiązanie zawiera program InstallShield Limited Edition Project

Zidentyfikowaliśmy, że jeśli rozwiązanie zawiera jeden lub więcej projektu InstallShield Limited Edition, okno dialogowe **Dodaj odwołanie do biblioteki pakietów** zgłoś wyjątek po otwarciu. Obecnie nie ma jeszcze obejścia, z wyjątkiem usuwania projektów InstallShield lub ich zwalniania.

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>Odinstaluj przycisk Wyszarzony? NuGet wymaga uprawnień administratora do zainstalowania/odinstalowania

Jeśli spróbujesz odinstalować NuGet za pośrednictwem Menedżera rozszerzeń programu Visual Studio, można zauważyć, że przycisk Odinstaluj jest wyłączony. NuGet wymaga dostępu administratora do instalacji i odinstalowania. Ponownie wykładuj program Visual Studio jako administrator, aby odinstalować rozszerzenie. NuGet nie wymaga dostępu administratora do korzystania z niego.

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>Konsola Menedżera pakietów ulega awarii po otwarciu jej w systemie Windows XP. Co jest nie tak?

NuGet wymaga środowiska uruchomieniowego programu Powershell 2.0. System Windows XP domyślnie nie ma programu Powershell 2.0. Środowisko wykonawcze programu Powershell 2.0 można pobrać z programu <https://support.microsoft.com/kb/968929>. Po zainstalowaniu go uruchom ponownie program Visual Studio i powinieneś być w stanie otworzyć konsolę Menedżera pakietów.

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>Program Visual Studio 2010 z dodatku SP1 beta ulega awarii po wyjściu, jeśli konsola Menedżera pakietów jest otwarta.

Jeśli zainstalowano program Visual Studio 2010 z dodatków SP1 Beta, można zauważyć, że jeśli pozostawisz konsolę Menedżera pakietów otwarte i zamknij visual studio, spowoduje to awarię. Jest to znany problem programu Visual Studio i zostanie rozwiązany w wersji RTM dodatku SP1. Na razie po prostu zignoruj awarię lub odinstaluj SP1 Beta, jeśli możesz.

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>Element "metadane" ... ma nieprawidłowy wyjątek elementu podrzędnego występuje

Jeśli zainstalowano pakiety utworzone przy pomocy wersji wstępnej NuGet, może wystąpić komunikat o błędzie z informacją "Element 'metadanych' w obszarze nazw "schemas.microsoft.com/packaging/2010/07/nuspec.xsd' ma nieprawidłowy element podrzędny" podczas uruchamiania wersji RTM NuGet z tym projektem. Należy odinstalować, a następnie ponownie zainstalować każdy pakiet przy użyciu wersji RTM NuGet.

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a>Próba zainstalowania lub odinstalowania powoduje błąd "Nie można utworzyć pliku, gdy ten plik już istnieje."

Z jakiegoś powodu rozszerzenia programu Visual Studio można uzyskać w dziwnym stanie, w którym odinstalowano rozszerzenie VSIX, ale niektóre pliki zostały pozostawione. Aby obejść ten problem:

1. Zamykanie programu Visual Studio
1. Otwórz następujący folder (może znajdować się na innym dysku na komputerze)

    C:\Pliki programów (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft\<Corporation\NuGet Package Manager wersja>\

1. Usuń wszystkie pliki z rozszerzeniami *.deleteme.*
1. Ponowne otwieranie programu Visual Studio

Po wykonać następujące kroki, należy być w stanie kontynuować.

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>W rzadkich przypadkach kompilacja z włączoną analizą kodu powoduje błąd.

Jeśli zainstalujesz FluentNHibernate za pomocą konsoli Menedżera pakietów, a następnie skompilujesz projekt z włączoną "Analizą kodu".

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

Domyślnie FluentNHibernate wymaga NHibernate 3.0.0.2001. Jednak zgodnie z projektem NuGet zainstaluje NHibernate 3.0.0.4000 w projekcie i dodać odpowiednie przekierowania powiązania, tak aby będzie działać. Projekt będzie kompilować dobrze, jeśli analiza kodu nie jest włączona. W przeciwieństwie do kompilatora narzędzie do analizy kodu nie należycie śledzić przekierowania powiązania do korzystania z 3.0.0.4000 zamiast 3.0.0.2001. Można obejść ten problem, instalując NHibernate 3.0.0.2001 lub powiedz narzędziu analizy kodu, aby zachowywało się tak samo jak kompilator, wykonując następujące czynności:

1. Przejdź do *pozycji %PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*
1. Otwórz fxcopcmd.exe.config `AssemblyReferenceResolveMode` i `StrongName` `StrongNameIgnoringVersion`zmień z .
1. Zapisz zmianę i odbuduj swój projekt.

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>Polecenie Write-Error nie działa wewnątrz install.ps1/uninstall.ps1/init.ps1

Jest to znany problem. Zamiast wywoływać write-error, spróbuj wywołać throw.

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>Instalowanie programu NuGet z ograniczonym dostępem w systemie Windows 2003 może ulec awarii programu Visual Studio

Podczas próby zainstalowania NuGet przy użyciu Menedżera rozszerzeń programu Visual Studio i nie działa jako administrator, &#8220;Uruchom jako&#8221; okno dialogowe jest wyświetlany z polem wyboru oznaczone &#8220;Uruchom ten program z ograniczonym dostępem&#8221; domyślnie zaznaczone.

![Uruchom jako okno dialogowe z ograniczeniami](./media/RunAsRestricted.png)

Kliknięcie przycisku OK z tym zaznaczonym awarie programu Visual Studio. Przed zainstalowaniem programu NuGet należy odznaczyć tę opcję.

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>Nie można odinstalować narzędzia NuGet dla systemu Windows Phone

Narzędzia systemu Windows Phone nie obsługują menedżera rozszerzeń programu Visual Studio. Aby odinstalować NuGet, uruchom następujące polecenie.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>Zmiana wielkich liter identyfikatorów pakietów NuGet przerywa przywracanie pakietu

Jak wspomniano w całej tej [kwestii GitHub](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), zmiana wielkości liter pakietów NuGet może być wykonana przez wsparcie NuGet, ale powoduje komplikacje podczas przywracania pakietu dla użytkowników, którzy mają istniejące, inaczej wielkości, pakiety w ich globalnym *folderze pakietów.* Firma Microsoft zaleca tylko żądanie zmiany sprawy, gdy masz sposób komunikowania się z istniejącymi użytkownikami pakietu o przerwie, która może wystąpić do ich przywracania pakietu kompilacji.

## <a name="reporting-issues"></a>Zgłaszanie problemów

Aby zgłosić problemy [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues)NuGet, odwiedź stronę .
