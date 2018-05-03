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
---
# <a name="known-issues-with-nuget"></a><span data-ttu-id="87be1-103">Znane problemy dotyczące programu NuGet</span><span class="sxs-lookup"><span data-stu-id="87be1-103">Known Issues with NuGet</span></span>

<span data-ttu-id="87be1-104">Są to najczęściej znane problemy z programem NuGet wielokrotnie są zgłaszane.</span><span class="sxs-lookup"><span data-stu-id="87be1-104">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="87be1-105">Jeśli występują problemy dotyczące instalowania NuGet lub Poświęć zarządzania pakietami, przejrzyj następujące znane problemy i ich rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="87be1-105">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="87be1-106">Począwszy od NuGet 4.0, znanych problemów są częścią odpowiednie informacje o wersji.</span><span class="sxs-lookup"><span data-stu-id="87be1-106">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="87be1-107">Problemy z uwierzytelnianiem nuget źródeł w programu VSTS z nuget.exe v3.4.3</span><span class="sxs-lookup"><span data-stu-id="87be1-107">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="87be1-108">**Problem:**</span><span class="sxs-lookup"><span data-stu-id="87be1-108">**Problem:**</span></span>

<span data-ttu-id="87be1-109">Możemy użyć następującego polecenia do przechowywania poświadczeń, możemy zakończyć się dwa razy szyfrowania osobisty Token dostępu.</span><span class="sxs-lookup"><span data-stu-id="87be1-109">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="87be1-110">$PAT = "Twoje osobisty token dostępu" $Feed = "url".\nuget.exe źródeł add - nazwa testu — $UserName $Feed źródła - UserName-$PAT hasła</span><span class="sxs-lookup"><span data-stu-id="87be1-110">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="87be1-111">**Obejście problemu:**</span><span class="sxs-lookup"><span data-stu-id="87be1-111">**Workaround:**</span></span>

<span data-ttu-id="87be1-112">Przechowywania haseł w postaci zwykłego tekstu przy użyciu [- StorePasswordInClearText](../tools/cli-ref-sources.md) opcji.</span><span class="sxs-lookup"><span data-stu-id="87be1-112">Store passwords in clear text using the [-StorePasswordInClearText](../tools/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="87be1-113">Błąd podczas instalowania pakietów z NuGet 3.4 3.4.1</span><span class="sxs-lookup"><span data-stu-id="87be1-113">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="87be1-114">**Problem:**</span><span class="sxs-lookup"><span data-stu-id="87be1-114">**Problem:**</span></span>

<span data-ttu-id="87be1-115">W NuGet 3.4 i 3.4.1 używając dodatku NuGet żadnych źródeł są zgłaszane jako dostępne i nie można dodać nowego źródła w oknie Konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="87be1-115">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="87be1-116">Wynik jest podobny do obraz poniżej:</span><span class="sxs-lookup"><span data-stu-id="87be1-116">The result is similar to the image below:</span></span>

![Konfiguracja NuGet z żadnymi źródłami](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="87be1-118">`NuGet.Config` Plików w sieci `%AppData%\NuGet\` (system Windows) lub `~/.nuget/` przypadkowo został opróżniony folder (system Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="87be1-118">The `NuGet.Config` file in your `%AppData%\NuGet\` (Windows) or `~/.nuget/` (Mac/Linux) folder has accidentally been emptied.</span></span> <span data-ttu-id="87be1-119">Aby rozwiązać ten problem: Zamknij program Visual Studio (w systemie Windows, jeśli ma to zastosowanie), Usuń `NuGet.Config` plik i spróbuj ponownie wykonać operację.</span><span class="sxs-lookup"><span data-stu-id="87be1-119">To fix this: close Visual Studio (on Windows, if applicable), delete the `NuGet.Config` file, and try the operation again.</span></span> <span data-ttu-id="87be1-120">NuGet wygenerował nowy `NuGet.Config` i powinno być możliwe kontynuować.</span><span class="sxs-lookup"><span data-stu-id="87be1-120">NuGet generated a new `NuGet.Config` and you should be able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="87be1-121">Błąd podczas instalowania pakietów z NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="87be1-121">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="87be1-122">**Problem:**</span><span class="sxs-lookup"><span data-stu-id="87be1-122">**Problem:**</span></span>

<span data-ttu-id="87be1-123">NuGet 2.7 lub powyżej, podczas próby zainstalowania dowolnego pakietu, który zawiera odwołania do zestawów, może zostać wyświetlony komunikat o błędzie **"ciąg wejściowy nie był w poprawnym formacie."** , tak jak poniżej:</span><span class="sxs-lookup"><span data-stu-id="87be1-123">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

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

<span data-ttu-id="87be1-124">Jest to spowodowane biblioteki typów dla `VSLangProj.dll` składnika modelu COM wyrejestrowywany w tym systemie.</span><span class="sxs-lookup"><span data-stu-id="87be1-124">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="87be1-125">Może się to zdarzyć, na przykład, jeśli masz dwie wersje programu Visual Studio zainstalowany side-by-side, a następnie odinstaluj starszą wersję.</span><span class="sxs-lookup"><span data-stu-id="87be1-125">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="87be1-126">W ten sposób mogą przypadkowo wyrejestrować powyżej biblioteki COM.</span><span class="sxs-lookup"><span data-stu-id="87be1-126">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="87be1-127">**Rozwiązanie:**:</span><span class="sxs-lookup"><span data-stu-id="87be1-127">**Solution:**:</span></span>

<span data-ttu-id="87be1-128">Uruchom to polecenie z **podniesionego wiersza** Aby ponownie zarejestrować biblioteki typów `VSLangProj.dll`</span><span class="sxs-lookup"><span data-stu-id="87be1-128">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="87be1-129">Jeśli polecenie nie powiedzie się, sprawdź, czy plik istnieje w tej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="87be1-129">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="87be1-130">Aby uzyskać więcej informacji na temat tego błędu, zobacz [elementu roboczego](https://nuget.codeplex.com/workitem/3609 "elementu roboczego 3609").</span><span class="sxs-lookup"><span data-stu-id="87be1-130">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="87be1-131">Niepowodzenie kompilacji, po zainstalowaniu pakietu aktualizacji w wersji programu VS 2012</span><span class="sxs-lookup"><span data-stu-id="87be1-131">Build failure after package update in VS 2012</span></span>

<span data-ttu-id="87be1-132">Problem: w przypadku korzystania z wersji programu VS 2012 RTM.</span><span class="sxs-lookup"><span data-stu-id="87be1-132">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="87be1-133">Podczas aktualizowania pakietów NuGet, ten komunikat: "nie można ukończyć co najmniej jednego pakietu odinstalowane."</span><span class="sxs-lookup"><span data-stu-id="87be1-133">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="87be1-134">i zostanie wyświetlony monit o ponowne uruchomienie programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="87be1-134">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="87be1-135">Po ponownym uruchomieniu programu VS, występują błędy kompilacji nieco dziwne.</span><span class="sxs-lookup"><span data-stu-id="87be1-135">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="87be1-136">Przyczyną jest to, że niektóre pliki w pakietach starego jest zablokowany przez tła procesu programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="87be1-136">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span> <span data-ttu-id="87be1-137">Nawet w przypadku, po ponownym uruchomieniu programu VS, tło procesu programu MSBuild nadal używa plików w starym pakietów powodujące błędy kompilacji.</span><span class="sxs-lookup"><span data-stu-id="87be1-137">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="87be1-138">Poprawka jest aktualizacji VS 2012, np. VS 2012 Update 2.</span><span class="sxs-lookup"><span data-stu-id="87be1-138">The fix is to install VS 2012 Update, e.g. VS 2012 Update 2.</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="87be1-139">Uaktualnianie do najnowszej NuGet ze starszej wersji powoduje błąd weryfikacji podpisu</span><span class="sxs-lookup"><span data-stu-id="87be1-139">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="87be1-140">Jeśli korzystasz z VS 2010 z dodatkiem SP1, możesz napotkać komunikat o błędzie podczas próby uaktualnienia NuGet, jeśli masz starszą wersję zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="87be1-140">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Instalator rozszerzenia programu Visual Studio](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="87be1-142">Podczas wyświetlania dzienniki, można napotkać informację o `SignatureMismatchException`.</span><span class="sxs-lookup"><span data-stu-id="87be1-142">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="87be1-143">Aby temu zapobiec, jest [poprawki programu Visual Studio 2010 z dodatkiem SP1](http://bit.ly/vsixcertfix) można zainstalować.</span><span class="sxs-lookup"><span data-stu-id="87be1-143">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="87be1-144">Alternatywnie obejściem jest po prostu Odinstaluj NuGet (podczas uruchamiania programu Visual Studio jako Administrator), a następnie zainstalować go z galerii rozszerzeń programu VS.</span><span class="sxs-lookup"><span data-stu-id="87be1-144">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="87be1-145">Zobacz [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="87be1-145">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="87be1-146">Konsola Menedżera pakietów zgłasza wyjątek, gdy reflektora Visual Studio dodatek jest również instalowany.</span><span class="sxs-lookup"><span data-stu-id="87be1-146">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="87be1-147">Podczas uruchamiania konsoli Menedżera pakietów, może wystąpić następujący komunikat o wyjątku Jeśli masz dodatku VS reflektora zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="87be1-147">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="87be1-148">lub</span><span class="sxs-lookup"><span data-stu-id="87be1-148">or</span></span>

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

<span data-ttu-id="87be1-149">Zostały możemy skontaktować się z autorem dodatku w nadziei pracy się, że rozdzielczość.</span><span class="sxs-lookup"><span data-stu-id="87be1-149">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="87be1-150">Aktualizacja: Firma Microsoft zweryfikowano czy najnowsza wersja reflektor, 6.5, już nie powoduje, że tego wyjątku w konsoli.</span><span class="sxs-lookup"><span data-stu-id="87be1-150">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="87be1-151">Konsola Menedżera pakietów otwierania zakończy się niepowodzeniem z wyjątkiem niepoprawny</span><span class="sxs-lookup"><span data-stu-id="87be1-151">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="87be1-152">Te błędy napotkać podczas próby otwarcia konsoli Menedżera pakietów:</span><span class="sxs-lookup"><span data-stu-id="87be1-152">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="87be1-153">Jeśli tak, postępuj zgodnie z rozwiązania [omówione w witrynie StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) rozwiązywania tych problemów.</span><span class="sxs-lookup"><span data-stu-id="87be1-153">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="87be1-154">Okno dialogowe Dodaj odwołanie do biblioteki pakietu zgłasza wyjątek, jeśli rozwiązanie zawiera InstallShield Limited Edition projektu</span><span class="sxs-lookup"><span data-stu-id="87be1-154">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project</span></span>

<span data-ttu-id="87be1-155">Ma określiliśmy, że jeśli rozwiązanie zawiera co najmniej jeden projekt InstallShield Limited Edition, **Dodaj odwołanie do biblioteki pakietu** okna dialogowego spowoduje zgłoszenie wyjątku po otwarciu.</span><span class="sxs-lookup"><span data-stu-id="87be1-155">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="87be1-156">Nie istnieje obecnie obejście jeszcze z wyjątkiem usuwanie projektów InstallShield albo zwalnianie je.</span><span class="sxs-lookup"><span data-stu-id="87be1-156">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="87be1-157">Odinstaluj przycisk nieaktywna?</span><span class="sxs-lookup"><span data-stu-id="87be1-157">Uninstall Button Greyed out?</span></span> <span data-ttu-id="87be1-158">NuGet wymaga uprawnień administratora do instalacji/dezinstalacji</span><span class="sxs-lookup"><span data-stu-id="87be1-158">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="87be1-159">Jeśli użytkownik próbuje odinstalować NuGet Menedżera rozszerzenia za pomocą programu Visual Studio, mogą pojawić się wyłączeniu przycisk Odinstaluj.</span><span class="sxs-lookup"><span data-stu-id="87be1-159">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span> <span data-ttu-id="87be1-160">NuGet wymaga dostępu administracyjnego do instalowania i odinstalowywania.</span><span class="sxs-lookup"><span data-stu-id="87be1-160">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="87be1-161">Uruchom ponownie program Visual Studio jako administrator, aby odinstalować rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="87be1-161">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span> <span data-ttu-id="87be1-162">NuGet nie wymaga dostępu administracyjnego z niego korzystać.</span><span class="sxs-lookup"><span data-stu-id="87be1-162">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="87be1-163">Konsola Menedżera pakietów ulega awarii podczas otwierania go w systemie Windows XP.</span><span class="sxs-lookup"><span data-stu-id="87be1-163">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="87be1-164">Co jest nie tak?</span><span class="sxs-lookup"><span data-stu-id="87be1-164">What's wrong?</span></span>

<span data-ttu-id="87be1-165">NuGet wymaga środowiska uruchomieniowego programu Powershell 2.0.</span><span class="sxs-lookup"><span data-stu-id="87be1-165">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="87be1-166">Windows XP, domyślnie nie ma programu Powershell 2.0.</span><span class="sxs-lookup"><span data-stu-id="87be1-166">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="87be1-167">Możesz pobrać środowiska uruchomieniowego programu Powershell 2.0 z [ http://support.microsoft.com/kb/968929 ](http://support.microsoft.com/kb/968929).</span><span class="sxs-lookup"><span data-stu-id="87be1-167">You can download the Powershell 2.0 runtime from [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span></span> <span data-ttu-id="87be1-168">Po jej zainstalowaniu, uruchom ponownie program Visual Studio i powinno być możliwe otworzyć konsolę Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="87be1-168">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="87be1-169">Visual Studio 2010 z dodatkiem SP1 Beta ulega awarii przy zamykaniu, jeśli konsola Menedżera pakietów jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="87be1-169">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="87be1-170">Po zainstalowaniu programu Visual Studio 2010 z dodatkiem SP1 Beta, możesz zauważyć, że pozostaw otwarte konsoli Menedżera pakietów, zamknij program Visual Studio go ulegnie awarii.</span><span class="sxs-lookup"><span data-stu-id="87be1-170">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="87be1-171">Jest to znany problem programu Visual Studio i zostanie rozwiązany w wersji RTM SP1 wersji.</span><span class="sxs-lookup"><span data-stu-id="87be1-171">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span> <span data-ttu-id="87be1-172">Teraz po prostu Ignoruj awarii lub odinstalować z dodatkiem SP1 Beta, jeśli to możliwe.</span><span class="sxs-lookup"><span data-stu-id="87be1-172">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="87be1-173">Element "metadanych"... ma nieprawidłowy element wyjątek występuje</span><span class="sxs-lookup"><span data-stu-id="87be1-173">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="87be1-174">Jeśli zainstalowano pakiety z wersji wstępnej programu NuGet, może wystąpić komunikat o błędzie "element"metadanych"w przestrzeni nazw"schemas.microsoft.com/packaging/2010/07/nuspec.xsd"ma nieprawidłowy element podrzędny" podczas uruchamiania RTM wersja programu NuGet z tego projektu.</span><span class="sxs-lookup"><span data-stu-id="87be1-174">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="87be1-175">Należy odinstalować i ponownie zainstalować każdego pakietu NuGet w wersji RTM.</span><span class="sxs-lookup"><span data-stu-id="87be1-175">You need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a><span data-ttu-id="87be1-176">Próby zainstalowania lub odinstalowania powoduje błąd "Nie można utworzyć pliku, ten plik już istnieje."</span><span class="sxs-lookup"><span data-stu-id="87be1-176">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists."</span></span>

<span data-ttu-id="87be1-177">Niektóre przyczyny rozszerzeń programu Visual Studio można uzyskać w stanie nieco dziwne, gdzie został odinstalowany rozszerzenie VSIX, ale niektóre pliki zostały pozostawione.</span><span class="sxs-lookup"><span data-stu-id="87be1-177">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="87be1-178">Aby obejść ten problem:</span><span class="sxs-lookup"><span data-stu-id="87be1-178">To work around this issue:</span></span>

1. <span data-ttu-id="87be1-179">Zamknij program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="87be1-179">Exit Visual Studio</span></span>
1. <span data-ttu-id="87be1-180">Otwórz następujący folder (może to być na innym dysku na tym komputerze)</span><span class="sxs-lookup"><span data-stu-id="87be1-180">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="87be1-181">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span><span class="sxs-lookup"><span data-stu-id="87be1-181">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span></span>

1. <span data-ttu-id="87be1-182">Usuń wszystkie pliki z *.deleteme* rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="87be1-182">Delete all the files with the *.deleteme* extensions.</span></span>
1. <span data-ttu-id="87be1-183">Otwórz ponownie program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="87be1-183">Re-open Visual Studio</span></span>

<span data-ttu-id="87be1-184">Po wykonaniu tych kroków, można kontynuować.</span><span class="sxs-lookup"><span data-stu-id="87be1-184">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="87be1-185">W rzadkich przypadkach kompilowania za pomocą analizy kodu włączona powoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="87be1-185">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="87be1-186">Może pobrać następujący błąd, jeśli instaluje FluentNHibernate z konsoli Menedżera pakietów, a następnie Skompiluj projekt z "Kod — analiza" włączone.</span><span class="sxs-lookup"><span data-stu-id="87be1-186">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="87be1-187">Domyślnie FluentNHibernate wymaga NHibernate 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="87be1-187">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="87be1-188">Jednak zgodnie z założeniami NuGet zainstaluje NHibernate 3.0.0.4000 w projekcie i dodaj odpowiednie powiązanie przekierowuje, dzięki czemu będzie ona działać.</span><span class="sxs-lookup"><span data-stu-id="87be1-188">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="87be1-189">Możesz projekt zostanie skompilowany świetnie, jeśli nie włączono analizy kodu.</span><span class="sxs-lookup"><span data-stu-id="87be1-189">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="87be1-190">W przeciwieństwie do kompilatora narzędzie do analizy kodu nie będzie poprawnie zgodna przekierowania powiązania do użycia zamiast 3.0.0.2001 3.0.0.4000.</span><span class="sxs-lookup"><span data-stu-id="87be1-190">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="87be1-191">Można obejść ten problem przez albo instalowania NHibernate 3.0.0.2001 lub poproś narzędzie do analizy kodu do działają tak samo, jak kompilator w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="87be1-191">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="87be1-192">Przejdź do *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span><span class="sxs-lookup"><span data-stu-id="87be1-192">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="87be1-193">Otwórz FxCopCmd.exe.config i zmień `AssemblyReferenceResolveMode` z `StrongName` do `StrongNameIgnoringVersion`.</span><span class="sxs-lookup"><span data-stu-id="87be1-193">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="87be1-194">Zapisz zmiany i ponownie skompiluj projekt.</span><span class="sxs-lookup"><span data-stu-id="87be1-194">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="87be1-195">Błąd zapisu polecenie nie działa wewnątrz install.ps1/uninstall.ps1/init.ps1</span><span class="sxs-lookup"><span data-stu-id="87be1-195">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="87be1-196">Jest to znany problem.</span><span class="sxs-lookup"><span data-stu-id="87be1-196">This is a known issue.</span></span> <span data-ttu-id="87be1-197">Zamiast wywoływania Write-Error, spróbuj wywołać throw.</span><span class="sxs-lookup"><span data-stu-id="87be1-197">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="87be1-198">Instalowania NuGet z ograniczonym dostępem w systemie Windows 2003 można awarię programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="87be1-198">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>

<span data-ttu-id="87be1-199">Podczas próby zainstalowania NuGet za pomocą Menedżera rozszerzenia programu Visual Studio i nie jest uruchomiona jako administrator, &#8220;Uruchom jako&#8221; z pola wyboru zostanie wyświetlone okno dialogowe &#8220;uruchomienia tego programu z ograniczonym dostępem&#8221; sprawdzana przez domyślne.</span><span class="sxs-lookup"><span data-stu-id="87be1-199">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![Uruchom jako ograniczeniami okna dialogowego](./media/RunAsRestricted.png)

<span data-ttu-id="87be1-201">Kliknięcie przycisku OK z sprawdzanym ulega awarii programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="87be1-201">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="87be1-202">Upewnij się, usuń zaznaczenie tej opcji, przed zainstalowaniem NuGet.</span><span class="sxs-lookup"><span data-stu-id="87be1-202">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="87be1-203">Nie można odinstalować NuGet dla narzędzia Windows Phone</span><span class="sxs-lookup"><span data-stu-id="87be1-203">Cannot uninstall NuGet for Windows Phone Tools</span></span>

<span data-ttu-id="87be1-204">Narzędzia Windows Phone nie ma obsługi Menedżera rozszerzeń dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="87be1-204">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="87be1-205">Aby odinstalować program NuGet, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="87be1-205">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="87be1-206">Zmiana wielkości liter identyfikatorów pakietów NuGet dzieli przywracania pakietu</span><span class="sxs-lookup"><span data-stu-id="87be1-206">Changing the capitalization of NuGet package IDs breaks package restore</span></span>

<span data-ttu-id="87be1-207">Zgodnie z opisem długości na [ten problem GitHub](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), zmiana wielkości liter pakietów NuGet może odbywać się przy pomocy technicznej NuGet, ale komplikacji powoduje, że podczas przywracania pakietu dla użytkowników, którzy mają istniejących, inaczej — z uwzględnieniem wielkości liter, pakiety w ich *globalne pakiety* folderu.</span><span class="sxs-lookup"><span data-stu-id="87be1-207">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their *global-packages* folder.</span></span> <span data-ttu-id="87be1-208">Zaleca się tylko żądania zmiany wielkości, jeśli masz sposób komunikowania się z istniejących użytkowników do pakietu o przerwie, który może wystąpić, aby przywrócić ich czas kompilacji pakietu.</span><span class="sxs-lookup"><span data-stu-id="87be1-208">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="87be1-209">Zgłaszanie problemów</span><span class="sxs-lookup"><span data-stu-id="87be1-209">Reporting issues</span></span>

<span data-ttu-id="87be1-210">Aby zgłosić problemy NuGet, odwiedź stronę [ https://github.com/nuget/home/issues ](https://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="87be1-210">To report NuGet issues, visit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span></span>
