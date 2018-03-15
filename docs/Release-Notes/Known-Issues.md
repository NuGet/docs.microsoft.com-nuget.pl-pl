---
title: NuGet znane problemy | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Znane problemy związane z tym instalacji pakietu aktualizacji, uwierzytelniania i narzędzia NuGet."
keywords: "Znane problemy i problemów NuGet NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ac00e3f11c54290a31319e7f2946fd965a0a9288
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/15/2018
---
# <a name="known-issues-with-nuget"></a><span data-ttu-id="d3a7e-104">Znane problemy dotyczące programu NuGet</span><span class="sxs-lookup"><span data-stu-id="d3a7e-104">Known Issues with NuGet</span></span>

<span data-ttu-id="d3a7e-105">Są to najczęściej znane problemy z programem NuGet wielokrotnie są zgłaszane.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-105">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="d3a7e-106">Jeśli występują problemy dotyczące instalowania NuGet lub Poświęć zarządzania pakietami, przejrzyj następujące znane problemy i ich rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-106">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="d3a7e-107">Począwszy od NuGet 4.0, znanych problemów są częścią odpowiednie informacje o wersji.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-107">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="d3a7e-108">Problemy z uwierzytelnianiem nuget źródeł w programu VSTS z nuget.exe v3.4.3</span><span class="sxs-lookup"><span data-stu-id="d3a7e-108">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="d3a7e-109">**Problem:**</span><span class="sxs-lookup"><span data-stu-id="d3a7e-109">**Problem:**</span></span>

<span data-ttu-id="d3a7e-110">Możemy użyć następującego polecenia do przechowywania poświadczeń, możemy zakończyć się dwa razy szyfrowania osobisty Token dostępu.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-110">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="d3a7e-111">$PAT = "Twoje osobisty token dostępu" $Feed = "url".\nuget.exe źródeł add - nazwa testu — $UserName $Feed źródła - UserName-$PAT hasła</span><span class="sxs-lookup"><span data-stu-id="d3a7e-111">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="d3a7e-112">**Obejście problemu:**</span><span class="sxs-lookup"><span data-stu-id="d3a7e-112">**Workaround:**</span></span>

<span data-ttu-id="d3a7e-113">Przechowywania haseł w postaci zwykłego tekstu przy użyciu [- StorePasswordInClearText](../tools/cli-ref-sources.md) opcji.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-113">Store passwords in clear text using the [-StorePasswordInClearText](../tools/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="d3a7e-114">Błąd podczas instalowania pakietów z NuGet 3.4 3.4.1</span><span class="sxs-lookup"><span data-stu-id="d3a7e-114">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="d3a7e-115">**Problem:**</span><span class="sxs-lookup"><span data-stu-id="d3a7e-115">**Problem:**</span></span>

<span data-ttu-id="d3a7e-116">W NuGet 3.4 i 3.4.1 używając dodatku NuGet żadnych źródeł są zgłaszane jako dostępne i nie można dodać nowego źródła w oknie Konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-116">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="d3a7e-117">Wynik jest podobny do obraz poniżej:</span><span class="sxs-lookup"><span data-stu-id="d3a7e-117">The result is similar to the image below:</span></span>

![Konfiguracja NuGet z żadnymi źródłami](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="d3a7e-119">`NuGet.Config` Plików w sieci `%AppData%\NuGet\` (system Windows) lub `~/.nuget/` przypadkowo został opróżniony folder (system Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="d3a7e-119">The `NuGet.Config` file in your `%AppData%\NuGet\` (Windows) or `~/.nuget/` (Mac/Linux) folder has accidentally been emptied.</span></span> <span data-ttu-id="d3a7e-120">Aby rozwiązać ten problem: Zamknij program Visual Studio (w systemie Windows, jeśli ma to zastosowanie), Usuń `NuGet.Config` plik i spróbuj ponownie wykonać operację.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-120">To fix this: close Visual Studio (on Windows, if applicable), delete the `NuGet.Config` file, and try the operation again.</span></span> <span data-ttu-id="d3a7e-121">NuGet wygenerował nowy `NuGet.Config` i powinno być możliwe kontynuować.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-121">NuGet generated a new `NuGet.Config` and you should be able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="d3a7e-122">Błąd podczas instalowania pakietów z NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="d3a7e-122">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="d3a7e-123">**Problem:**</span><span class="sxs-lookup"><span data-stu-id="d3a7e-123">**Problem:**</span></span>

<span data-ttu-id="d3a7e-124">NuGet 2.7 lub powyżej, podczas próby zainstalowania dowolnego pakietu, który zawiera odwołania do zestawów, może zostać wyświetlony komunikat o błędzie **"ciąg wejściowy nie był w poprawnym formacie."** , tak jak poniżej:</span><span class="sxs-lookup"><span data-stu-id="d3a7e-124">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

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

<span data-ttu-id="d3a7e-125">Jest to spowodowane biblioteki typów dla `VSLangProj.dll` składnika modelu COM wyrejestrowywany w tym systemie.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-125">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="d3a7e-126">Może się to zdarzyć, na przykład, jeśli masz dwie wersje programu Visual Studio zainstalowany side-by-side, a następnie odinstaluj starszą wersję.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-126">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="d3a7e-127">W ten sposób mogą przypadkowo wyrejestrować powyżej biblioteki COM.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-127">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="d3a7e-128">**Rozwiązanie:**:</span><span class="sxs-lookup"><span data-stu-id="d3a7e-128">**Solution:**:</span></span>

<span data-ttu-id="d3a7e-129">Uruchom to polecenie z **podniesionego wiersza** Aby ponownie zarejestrować biblioteki typów `VSLangProj.dll`</span><span class="sxs-lookup"><span data-stu-id="d3a7e-129">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="d3a7e-130">Jeśli polecenie nie powiedzie się, sprawdź, czy plik istnieje w tej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-130">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="d3a7e-131">Aby uzyskać więcej informacji na temat tego błędu, zobacz [elementu roboczego](https://nuget.codeplex.com/workitem/3609 "elementu roboczego 3609").</span><span class="sxs-lookup"><span data-stu-id="d3a7e-131">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="d3a7e-132">Niepowodzenie kompilacji, po zainstalowaniu pakietu aktualizacji w wersji programu VS 2012</span><span class="sxs-lookup"><span data-stu-id="d3a7e-132">Build failure after package update in VS 2012</span></span>

<span data-ttu-id="d3a7e-133">Problem: w przypadku korzystania z wersji programu VS 2012 RTM.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-133">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="d3a7e-134">Podczas aktualizowania pakietów NuGet, ten komunikat: "nie można ukończyć co najmniej jednego pakietu odinstalowane."</span><span class="sxs-lookup"><span data-stu-id="d3a7e-134">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="d3a7e-135">i zostanie wyświetlony monit o ponowne uruchomienie programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-135">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="d3a7e-136">Po ponownym uruchomieniu programu VS, występują błędy kompilacji nieco dziwne.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-136">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="d3a7e-137">Przyczyną jest to, że niektóre pliki w pakietach starego jest zablokowany przez tła procesu programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-137">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span> <span data-ttu-id="d3a7e-138">Nawet w przypadku, po ponownym uruchomieniu programu VS, tło procesu programu MSBuild nadal używa plików w starym pakietów powodujące błędy kompilacji.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-138">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="d3a7e-139">Poprawka jest aktualizacji VS 2012, np. VS 2012 Update 2.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-139">The fix is to install VS 2012 Update, e.g. VS 2012 Update 2.</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="d3a7e-140">Uaktualnianie do najnowszej NuGet ze starszej wersji powoduje błąd weryfikacji podpisu</span><span class="sxs-lookup"><span data-stu-id="d3a7e-140">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="d3a7e-141">Jeśli korzystasz z VS 2010 z dodatkiem SP1, możesz napotkać komunikat o błędzie podczas próby uaktualnienia NuGet, jeśli masz starszą wersję zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-141">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Instalator rozszerzenia programu Visual Studio](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="d3a7e-143">Podczas wyświetlania dzienniki, można napotkać informację o `SignatureMismatchException`.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-143">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="d3a7e-144">Aby temu zapobiec, jest [poprawki programu Visual Studio 2010 z dodatkiem SP1](http://bit.ly/vsixcertfix) można zainstalować.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-144">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="d3a7e-145">Alternatywnie obejściem jest po prostu Odinstaluj NuGet (podczas uruchamiania programu Visual Studio jako Administrator), a następnie zainstalować go z galerii rozszerzeń programu VS.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-145">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="d3a7e-146">Zobacz [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-146">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="d3a7e-147">Konsola Menedżera pakietów zgłasza wyjątek, gdy reflektora Visual Studio dodatek jest również instalowany.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-147">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="d3a7e-148">Podczas uruchamiania konsoli Menedżera pakietów, może wystąpić następujący komunikat o wyjątku Jeśli masz dodatku VS reflektora zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-148">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="d3a7e-149">lub</span><span class="sxs-lookup"><span data-stu-id="d3a7e-149">or</span></span>

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

<span data-ttu-id="d3a7e-150">Zostały możemy skontaktować się z autorem dodatku w nadziei pracy się, że rozdzielczość.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-150">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="d3a7e-151">Aktualizacja: Firma Microsoft zweryfikowano czy najnowsza wersja reflektor, 6.5, już nie powoduje, że tego wyjątku w konsoli.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-151">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="d3a7e-152">Konsola Menedżera pakietów otwierania zakończy się niepowodzeniem z wyjątkiem niepoprawny</span><span class="sxs-lookup"><span data-stu-id="d3a7e-152">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="d3a7e-153">Te błędy napotkać podczas próby otwarcia konsoli Menedżera pakietów:</span><span class="sxs-lookup"><span data-stu-id="d3a7e-153">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="d3a7e-154">Jeśli tak, postępuj zgodnie z rozwiązania [omówione w witrynie StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) rozwiązywania tych problemów.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-154">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="d3a7e-155">Okno dialogowe Dodaj odwołanie do biblioteki pakietu zgłasza wyjątek, jeśli rozwiązanie zawiera InstallShield Limited Edition projektu</span><span class="sxs-lookup"><span data-stu-id="d3a7e-155">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project</span></span>

<span data-ttu-id="d3a7e-156">Ma określiliśmy, że jeśli rozwiązanie zawiera co najmniej jeden projekt InstallShield Limited Edition, **Dodaj odwołanie do biblioteki pakietu** okna dialogowego spowoduje zgłoszenie wyjątku po otwarciu.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-156">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="d3a7e-157">Nie istnieje obecnie obejście jeszcze z wyjątkiem usuwanie projektów InstallShield albo zwalnianie je.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-157">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="d3a7e-158">Odinstaluj przycisk nieaktywna?</span><span class="sxs-lookup"><span data-stu-id="d3a7e-158">Uninstall Button Greyed out?</span></span> <span data-ttu-id="d3a7e-159">NuGet wymaga uprawnień administratora do instalacji/dezinstalacji</span><span class="sxs-lookup"><span data-stu-id="d3a7e-159">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="d3a7e-160">Jeśli użytkownik próbuje odinstalować NuGet Menedżera rozszerzenia za pomocą programu Visual Studio, mogą pojawić się wyłączeniu przycisk Odinstaluj.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-160">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span> <span data-ttu-id="d3a7e-161">NuGet wymaga dostępu administracyjnego do instalowania i odinstalowywania.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-161">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="d3a7e-162">Uruchom ponownie program Visual Studio jako administrator, aby odinstalować rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-162">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span> <span data-ttu-id="d3a7e-163">NuGet nie wymaga dostępu administracyjnego z niego korzystać.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-163">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="d3a7e-164">Konsola Menedżera pakietów ulega awarii podczas otwierania go w systemie Windows XP.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-164">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="d3a7e-165">Co jest nie tak?</span><span class="sxs-lookup"><span data-stu-id="d3a7e-165">What's wrong?</span></span>

<span data-ttu-id="d3a7e-166">NuGet wymaga środowiska uruchomieniowego programu Powershell 2.0.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-166">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="d3a7e-167">Windows XP, domyślnie nie ma programu Powershell 2.0.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-167">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="d3a7e-168">Możesz pobrać środowiska uruchomieniowego programu Powershell 2.0 z [ http://support.microsoft.com/kb/968929 ](http://support.microsoft.com/kb/968929).</span><span class="sxs-lookup"><span data-stu-id="d3a7e-168">You can download the Powershell 2.0 runtime from [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span></span> <span data-ttu-id="d3a7e-169">Po jej zainstalowaniu, uruchom ponownie program Visual Studio i powinno być możliwe otworzyć konsolę Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-169">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="d3a7e-170">Visual Studio 2010 z dodatkiem SP1 Beta ulega awarii przy zamykaniu, jeśli konsola Menedżera pakietów jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-170">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="d3a7e-171">Po zainstalowaniu programu Visual Studio 2010 z dodatkiem SP1 Beta, możesz zauważyć, że pozostaw otwarte konsoli Menedżera pakietów, zamknij program Visual Studio go ulegnie awarii.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-171">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="d3a7e-172">Jest to znany problem programu Visual Studio i zostanie rozwiązany w wersji RTM SP1 wersji.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-172">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span> <span data-ttu-id="d3a7e-173">Teraz po prostu Ignoruj awarii lub odinstalować z dodatkiem SP1 Beta, jeśli to możliwe.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-173">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="d3a7e-174">Element "metadanych"... ma nieprawidłowy element wyjątek występuje</span><span class="sxs-lookup"><span data-stu-id="d3a7e-174">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="d3a7e-175">Jeśli zainstalowano pakiety z wersji wstępnej programu NuGet, może wystąpić komunikat o błędzie "element"metadanych"w przestrzeni nazw"schemas.microsoft.com/packaging/2010/07/nuspec.xsd"ma nieprawidłowy element podrzędny" podczas uruchamiania RTM wersja programu NuGet z tego projektu.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-175">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="d3a7e-176">Należy odinstalować i ponownie zainstalować każdego pakietu NuGet w wersji RTM.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-176">You need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a><span data-ttu-id="d3a7e-177">Próby zainstalowania lub odinstalowania powoduje błąd "Nie można utworzyć pliku, ten plik już istnieje."</span><span class="sxs-lookup"><span data-stu-id="d3a7e-177">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists."</span></span>

<span data-ttu-id="d3a7e-178">Niektóre przyczyny rozszerzeń programu Visual Studio można uzyskać w stanie nieco dziwne, gdzie został odinstalowany rozszerzenie VSIX, ale niektóre pliki zostały pozostawione.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-178">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="d3a7e-179">Aby obejść ten problem:</span><span class="sxs-lookup"><span data-stu-id="d3a7e-179">To work around this issue:</span></span>

1. <span data-ttu-id="d3a7e-180">Zamknij program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d3a7e-180">Exit Visual Studio</span></span>
1. <span data-ttu-id="d3a7e-181">Otwórz następujący folder (może to być na innym dysku na tym komputerze)</span><span class="sxs-lookup"><span data-stu-id="d3a7e-181">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="d3a7e-182">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span><span class="sxs-lookup"><span data-stu-id="d3a7e-182">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span></span>

1. <span data-ttu-id="d3a7e-183">Usuń wszystkie pliki z *.deleteme* rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-183">Delete all the files with the *.deleteme* extensions.</span></span>
1. <span data-ttu-id="d3a7e-184">Otwórz ponownie program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d3a7e-184">Re-open Visual Studio</span></span>

<span data-ttu-id="d3a7e-185">Po wykonaniu tych kroków, można kontynuować.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-185">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="d3a7e-186">W rzadkich przypadkach kompilowania za pomocą analizy kodu włączona powoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-186">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="d3a7e-187">Może pobrać następujący błąd, jeśli instaluje FluentNHibernate z konsoli Menedżera pakietów, a następnie Skompiluj projekt z "Kod — analiza" włączone.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-187">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="d3a7e-188">Domyślnie FluentNHibernate wymaga NHibernate 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-188">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="d3a7e-189">Jednak zgodnie z założeniami NuGet zainstaluje NHibernate 3.0.0.4000 w projekcie i dodaj odpowiednie powiązanie przekierowuje, dzięki czemu będzie ona działać.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-189">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="d3a7e-190">Możesz projekt zostanie skompilowany świetnie, jeśli nie włączono analizy kodu.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-190">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="d3a7e-191">W przeciwieństwie do kompilatora narzędzie do analizy kodu nie będzie poprawnie zgodna przekierowania powiązania do użycia zamiast 3.0.0.2001 3.0.0.4000.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-191">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="d3a7e-192">Można obejść ten problem przez albo instalowania NHibernate 3.0.0.2001 lub poproś narzędzie do analizy kodu do działają tak samo, jak kompilator w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d3a7e-192">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="d3a7e-193">Przejdź do *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span><span class="sxs-lookup"><span data-stu-id="d3a7e-193">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="d3a7e-194">Otwórz FxCopCmd.exe.config i zmień `AssemblyReferenceResolveMode` z `StrongName` do `StrongNameIgnoringVersion`.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-194">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="d3a7e-195">Zapisz zmiany i ponownie skompiluj projekt.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-195">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="d3a7e-196">Błąd zapisu polecenie nie działa wewnątrz install.ps1/uninstall.ps1/init.ps1</span><span class="sxs-lookup"><span data-stu-id="d3a7e-196">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="d3a7e-197">Jest to znany problem.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-197">This is a known issue.</span></span> <span data-ttu-id="d3a7e-198">Zamiast wywoływania Write-Error, spróbuj wywołać throw.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-198">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="d3a7e-199">Instalowania NuGet z ograniczonym dostępem w systemie Windows 2003 można awarię programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d3a7e-199">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>

<span data-ttu-id="d3a7e-200">Podczas próby zainstalowania NuGet za pomocą Menedżera rozszerzenia programu Visual Studio i nie jest uruchomiona jako administrator, &#8220;Uruchom jako&#8221; z pola wyboru zostanie wyświetlone okno dialogowe &#8220;uruchomienia tego programu z ograniczonym dostępem&#8221; sprawdzana przez domyślne.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-200">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![Uruchom jako ograniczeniami okna dialogowego](./media/RunAsRestricted.png)

<span data-ttu-id="d3a7e-202">Kliknięcie przycisku OK z sprawdzanym ulega awarii programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-202">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="d3a7e-203">Upewnij się, usuń zaznaczenie tej opcji, przed zainstalowaniem NuGet.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-203">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="d3a7e-204">Nie można odinstalować NuGet dla narzędzia Windows Phone</span><span class="sxs-lookup"><span data-stu-id="d3a7e-204">Cannot uninstall NuGet for Windows Phone Tools</span></span>

<span data-ttu-id="d3a7e-205">Narzędzia Windows Phone nie ma obsługi Menedżera rozszerzeń dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-205">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="d3a7e-206">Aby odinstalować program NuGet, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-206">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="d3a7e-207">Zmiana wielkości liter identyfikatorów pakietów NuGet dzieli przywracania pakietu</span><span class="sxs-lookup"><span data-stu-id="d3a7e-207">Changing the capitalization of NuGet package IDs breaks package restore</span></span>

<span data-ttu-id="d3a7e-208">Zgodnie z opisem długości na [ten problem GitHub](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), zmiana wielkości liter pakietów NuGet może odbywać się przy pomocy technicznej NuGet, ale komplikacji powoduje, że podczas przywracania pakietu dla użytkowników, którzy mają istniejących, inaczej — z uwzględnieniem wielkości liter, pakiety w ich lokalną pamięć podręczną pakietów.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-208">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their local package cache.</span></span> <span data-ttu-id="d3a7e-209">Zaleca się tylko żądania zmiany wielkości, jeśli masz sposób komunikowania się z istniejących użytkowników do pakietu o przerwie, który może wystąpić, aby przywrócić ich czas kompilacji pakietu.</span><span class="sxs-lookup"><span data-stu-id="d3a7e-209">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="d3a7e-210">Zgłaszanie problemów</span><span class="sxs-lookup"><span data-stu-id="d3a7e-210">Reporting issues</span></span>

<span data-ttu-id="d3a7e-211">Aby zgłosić problemy NuGet, odwiedź stronę [ https://github.com/nuget/home/issues ](https://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="d3a7e-211">To report NuGet issues, visit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span></span>
