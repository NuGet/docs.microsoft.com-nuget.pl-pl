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
# <a name="known-issues-with-nuget"></a><span data-ttu-id="52b3d-103">Znane problemy z NuGet</span><span class="sxs-lookup"><span data-stu-id="52b3d-103">Known Issues with NuGet</span></span>

<span data-ttu-id="52b3d-104">Są to najczęściej znane problemy z NuGet, które często są zgłaszane.</span><span class="sxs-lookup"><span data-stu-id="52b3d-104">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="52b3d-105">Jeśli występują problemy z zainstalowaniem NuGet lub zarządzania pakietami, zapoznaj się za pośrednictwem tych znane problemy i ich rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="52b3d-105">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="52b3d-106">Począwszy od NuGet 4.0, znane problemy są częścią odpowiedniej wersji.</span><span class="sxs-lookup"><span data-stu-id="52b3d-106">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="52b3d-107">Problemy z uwierzytelnianiem za pomocą NuGet źródeł danych w usłudze VSTS za pomocą nuget.exe v3.4.3</span><span class="sxs-lookup"><span data-stu-id="52b3d-107">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="52b3d-108">**Problem:**</span><span class="sxs-lookup"><span data-stu-id="52b3d-108">**Problem:**</span></span>

<span data-ttu-id="52b3d-109">Gdy obsługujemy za pomocą następującego polecenia do przechowywania poświadczeń, firma Microsoft znajdą się podwójnego szyfrowania osobisty Token dostępu.</span><span class="sxs-lookup"><span data-stu-id="52b3d-109">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="52b3d-110">$PAT = "Twój osobisty token dostępu" $Feed = "url".\nuget.exe źródeł add - nazwa testu-$UserName $Feed źródła - UserName-$PAT hasła</span><span class="sxs-lookup"><span data-stu-id="52b3d-110">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="52b3d-111">**Obejście:**</span><span class="sxs-lookup"><span data-stu-id="52b3d-111">**Workaround:**</span></span>

<span data-ttu-id="52b3d-112">Store hasła w postaci zwykłego tekstu przy użyciu [- StorePasswordInClearText](../tools/cli-ref-sources.md) opcji.</span><span class="sxs-lookup"><span data-stu-id="52b3d-112">Store passwords in clear text using the [-StorePasswordInClearText](../tools/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="52b3d-113">Błąd podczas instalowania pakietów z NuGet 3.4 3.4.1</span><span class="sxs-lookup"><span data-stu-id="52b3d-113">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="52b3d-114">**Problem:**</span><span class="sxs-lookup"><span data-stu-id="52b3d-114">**Problem:**</span></span>

<span data-ttu-id="52b3d-115">NuGet 3.4 i 3.4.1 korzystając z dodatku programu NuGet, żadnych źródeł są zgłaszane jako dostępne i nie można dodać nowe źródła w oknie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="52b3d-115">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="52b3d-116">Wynik jest podobna do poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="52b3d-116">The result is similar to the image below:</span></span>

![Config NuGet za pomocą żadnych źródeł](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="52b3d-118">`NuGet.Config` Plików w Twojej `%AppData%\NuGet\` (Windows) lub `~/.nuget/` przypadkowo został opróżniony folder (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="52b3d-118">The `NuGet.Config` file in your `%AppData%\NuGet\` (Windows) or `~/.nuget/` (Mac/Linux) folder has accidentally been emptied.</span></span> <span data-ttu-id="52b3d-119">Aby rozwiązać ten problem: Zamknij program Visual Studio (w Windows, jeśli ma to zastosowanie), Usuń `NuGet.Config` pliku i spróbuj ponownie wykonać operację.</span><span class="sxs-lookup"><span data-stu-id="52b3d-119">To fix this: close Visual Studio (on Windows, if applicable), delete the `NuGet.Config` file, and try the operation again.</span></span> <span data-ttu-id="52b3d-120">NuGet wygenerował nowy `NuGet.Config` i powinno być możliwe kontynuować.</span><span class="sxs-lookup"><span data-stu-id="52b3d-120">NuGet generated a new `NuGet.Config` and you should be able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="52b3d-121">Błąd podczas instalowania pakietów z NuGet w wersji 2.7</span><span class="sxs-lookup"><span data-stu-id="52b3d-121">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="52b3d-122">**Problem:**</span><span class="sxs-lookup"><span data-stu-id="52b3d-122">**Problem:**</span></span>

<span data-ttu-id="52b3d-123">W NuGet w wersji 2.7 lub powyżej, gdy spróbujesz zainstalować dowolny pakiet, który zawiera odwołania do zestawów, otrzymasz komunikat o błędzie **"ciąg wejściowy nie jest w poprawnym formacie."** , tak jak poniżej:</span><span class="sxs-lookup"><span data-stu-id="52b3d-123">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

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

<span data-ttu-id="52b3d-124">Jest to spowodowane przez biblioteki typów dla `VSLangProj.dll` składnika COM wyrejestrowywany w Twoim systemie.</span><span class="sxs-lookup"><span data-stu-id="52b3d-124">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="52b3d-125">Może się to zdarzyć, na przykład, jeśli masz dwie wersje programu Visual Studio zainstalowane side-by-side i następnie odinstaluj starszą wersję.</span><span class="sxs-lookup"><span data-stu-id="52b3d-125">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="52b3d-126">Ten sposób może przypadkowo wyrejestrować powyżej biblioteki COM.</span><span class="sxs-lookup"><span data-stu-id="52b3d-126">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="52b3d-127">**Rozwiązanie:**:</span><span class="sxs-lookup"><span data-stu-id="52b3d-127">**Solution:**:</span></span>

<span data-ttu-id="52b3d-128">Uruchom następujące polecenie z **wiersz** ponownie zarejestrować biblioteki typów `VSLangProj.dll`</span><span class="sxs-lookup"><span data-stu-id="52b3d-128">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="52b3d-129">Jeśli polecenie zakończy się niepowodzeniem, sprawdź, czy plik istnieje w tej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="52b3d-129">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="52b3d-130">Aby uzyskać więcej informacji na temat tego błędu, zobacz ten [elementu roboczego](https://nuget.codeplex.com/workitem/3609 "elementu roboczego 3609").</span><span class="sxs-lookup"><span data-stu-id="52b3d-130">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="52b3d-131">Błąd kompilacji, po zainstalowaniu pakietu aktualizacji w programie VS 2012</span><span class="sxs-lookup"><span data-stu-id="52b3d-131">Build failure after package update in VS 2012</span></span>

<span data-ttu-id="52b3d-132">Problem: w przypadku korzystania z programu VS 2012 RTM.</span><span class="sxs-lookup"><span data-stu-id="52b3d-132">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="52b3d-133">Podczas aktualizowania pakietów NuGet, zostanie wyświetlony ten komunikat: "nie można wykonać jeden lub więcej pakietów odinstalowane."</span><span class="sxs-lookup"><span data-stu-id="52b3d-133">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="52b3d-134">i zostanie wyświetlony monit o ponowne uruchomienie programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52b3d-134">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="52b3d-135">Po ponownym uruchomieniu programu VS, pojawiają się błędy nieco dziwne kompilacji.</span><span class="sxs-lookup"><span data-stu-id="52b3d-135">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="52b3d-136">Przyczyną jest to, że niektórych plików w starym pakiety są zablokowane przez tła procesu programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="52b3d-136">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span> <span data-ttu-id="52b3d-137">Nawet w przypadku, po ponownym uruchomieniu programu VS, tło procesu programu MSBuild nadal używa plików w starym pakietów, powodując błędy kompilacji.</span><span class="sxs-lookup"><span data-stu-id="52b3d-137">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="52b3d-138">Obejście polega na zainstalowaniu programu VS 2012 Update, np. programu VS 2012 Update 2.</span><span class="sxs-lookup"><span data-stu-id="52b3d-138">The fix is to install VS 2012 Update, e.g. VS 2012 Update 2.</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="52b3d-139">Uaktualnienie do najnowszego rozwiązania NuGet ze starszej wersji powoduje, że błąd weryfikacji podpisu</span><span class="sxs-lookup"><span data-stu-id="52b3d-139">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="52b3d-140">Jeśli używasz programu VS 2010 z dodatkiem SP1, możesz napotkać komunikat o błędzie podczas próby uaktualnienia NuGet, jeśli masz starszą wersję zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="52b3d-140">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Instalator rozszerzenia programu Visual Studio](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="52b3d-142">Podczas wyświetlania dziennika, może wyświetlić informację o `SignatureMismatchException`.</span><span class="sxs-lookup"><span data-stu-id="52b3d-142">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="52b3d-143">Aby temu zapobiec, jest [poprawki programu Visual Studio 2010 SP1](http://bit.ly/vsixcertfix) można zainstalować.</span><span class="sxs-lookup"><span data-stu-id="52b3d-143">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="52b3d-144">Alternatywnie obejściem jest po prostu Odinstaluj NuGet (podczas uruchamiania programu Visual Studio jako Administrator), a następnie zainstalować go z galerii rozszerzeń programu VS.</span><span class="sxs-lookup"><span data-stu-id="52b3d-144">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="52b3d-145">Zobacz [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="52b3d-145">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="52b3d-146">Konsola Menedżera pakietów zgłasza wyjątek, gdy odblaskowego Visual Studio dodatek programu jest również instalowany.</span><span class="sxs-lookup"><span data-stu-id="52b3d-146">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="52b3d-147">Podczas uruchamiania konsoli Menedżera pakietów, może wystąpić następujący komunikat o wyjątku w przypadku dodatek VS odblaskowego zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="52b3d-147">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="52b3d-148">lub</span><span class="sxs-lookup"><span data-stu-id="52b3d-148">or</span></span>

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

<span data-ttu-id="52b3d-149">Kontaktujemy się z autorem dodatku w nadziei pracy na poziomie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="52b3d-149">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="52b3d-150">Aktualizacja: Firma Microsoft została zweryfikowana czy najnowszą wersję odblaskowego, 6.5, nie powoduje już tego wyjątku w konsoli programu.</span><span class="sxs-lookup"><span data-stu-id="52b3d-150">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="52b3d-151">Konsola Menedżera pakietów otwierania zakończy się niepowodzeniem z wyjątkiem niepoprawny</span><span class="sxs-lookup"><span data-stu-id="52b3d-151">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="52b3d-152">Możesz zobaczyć te błędy podczas próby otwarcia konsoli Menedżera pakietów:</span><span class="sxs-lookup"><span data-stu-id="52b3d-152">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="52b3d-153">Jeśli tak, postępuj zgodnie z rozwiązania [opisem na stronie StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) rozwiązywania tych problemów.</span><span class="sxs-lookup"><span data-stu-id="52b3d-153">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="52b3d-154">Okno dialogowe Dodaj odwołanie do pakietu biblioteki zgłasza wyjątek, jeśli rozwiązanie zawiera projekt InstallShield Limited Edition</span><span class="sxs-lookup"><span data-stu-id="52b3d-154">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project</span></span>

<span data-ttu-id="52b3d-155">Firma Microsoft ma ustaliła, że jeśli Twoje rozwiązanie zawiera co najmniej jeden projekt InstallShield Limited Edition, **Dodaj odwołanie do pakietu biblioteki** okna dialogowego spowoduje zgłoszenie wyjątku po otwarciu.</span><span class="sxs-lookup"><span data-stu-id="52b3d-155">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="52b3d-156">Obecnie nie ma sposobu obejścia jeszcze z wyjątkiem usuwanie projektów InstallShield lub zwalnianie je.</span><span class="sxs-lookup"><span data-stu-id="52b3d-156">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="52b3d-157">Odinstaluj wyszarzone przycisku?</span><span class="sxs-lookup"><span data-stu-id="52b3d-157">Uninstall Button Greyed out?</span></span> <span data-ttu-id="52b3d-158">NuGet wymaga uprawnień administratora do instalacji/dezinstalacji</span><span class="sxs-lookup"><span data-stu-id="52b3d-158">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="52b3d-159">Jeśli zostanie podjęta próba odinstalowania NuGet za pomocą programu Visual Studio Extension Manager, można zauważyć, że przycisk Odinstaluj jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="52b3d-159">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span> <span data-ttu-id="52b3d-160">NuGet wymaga dostępu administratora do instalowania i odinstalowywania.</span><span class="sxs-lookup"><span data-stu-id="52b3d-160">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="52b3d-161">Uruchom ponownie program Visual Studio jako administrator, aby odinstalować rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="52b3d-161">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span> <span data-ttu-id="52b3d-162">NuGet nie wymaga dostępu administratora z niego korzystać.</span><span class="sxs-lookup"><span data-stu-id="52b3d-162">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="52b3d-163">Konsola Menedżera pakietów ulega awarii podczas otwierania go w Windows XP.</span><span class="sxs-lookup"><span data-stu-id="52b3d-163">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="52b3d-164">Co jest nie tak?</span><span class="sxs-lookup"><span data-stu-id="52b3d-164">What's wrong?</span></span>

<span data-ttu-id="52b3d-165">NuGet wymaga środowiska uruchomieniowego programu Powershell w wersji 2.0.</span><span class="sxs-lookup"><span data-stu-id="52b3d-165">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="52b3d-166">Windows XP, domyślnie nie ma programu Powershell w wersji 2.0.</span><span class="sxs-lookup"><span data-stu-id="52b3d-166">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="52b3d-167">Możesz pobrać program Powershell 2.0 środowisko uruchomieniowe z [ http://support.microsoft.com/kb/968929 ](http://support.microsoft.com/kb/968929).</span><span class="sxs-lookup"><span data-stu-id="52b3d-167">You can download the Powershell 2.0 runtime from [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span></span> <span data-ttu-id="52b3d-168">Po jego zainstalowaniu, uruchom ponownie program Visual Studio, a powinien mieć możliwość otwarcia konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="52b3d-168">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="52b3d-169">Visual Studio 2010 z dodatkiem SP1 Beta ulega awarii przy zamykaniu, jeśli konsola Menedżera pakietów jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="52b3d-169">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="52b3d-170">Po zainstalowaniu programu Visual Studio 2010 z dodatkiem SP1 Beta można zauważyć, że jeśli zamykaj konsoli Menedżera pakietów, a następnie zamknij program Visual Studio, jego ulegnie awarii.</span><span class="sxs-lookup"><span data-stu-id="52b3d-170">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="52b3d-171">Jest to znany problem programu Visual Studio i zostanie rozwiązany w wersji z dodatkiem SP1 RTM wydania.</span><span class="sxs-lookup"><span data-stu-id="52b3d-171">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span> <span data-ttu-id="52b3d-172">Teraz po prostu Ignoruj awarii lub odinstalować z dodatkiem SP1 Beta, jeżeli jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="52b3d-172">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="52b3d-173">Element "metadata"... ma nieprawidłowy element wyjątek występuje</span><span class="sxs-lookup"><span data-stu-id="52b3d-173">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="52b3d-174">Jeśli zainstalowano pakiety skompilowane przy użyciu wersji wstępnej programu NuGet, może wystąpić komunikat o błędzie z informacją "elementem"metadata"w przestrzeni nazw"schemas.microsoft.com/packaging/2010/07/nuspec.xsd"ma nieprawidłowy element podrzędny" podczas uruchamiania RTM Wersja pakietu nuget za pomocą tego projektu.</span><span class="sxs-lookup"><span data-stu-id="52b3d-174">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="52b3d-175">Należy odinstalować i ponownie zainstalować każdego pakietu NuGet w wersji RTM.</span><span class="sxs-lookup"><span data-stu-id="52b3d-175">You need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a><span data-ttu-id="52b3d-176">Próby zainstalowania lub odinstalowania powoduje błąd "Nie można utworzyć pliku, ten plik już istnieje."</span><span class="sxs-lookup"><span data-stu-id="52b3d-176">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists."</span></span>

<span data-ttu-id="52b3d-177">Jakiegoś powodu rozszerzeń programu Visual Studio można uzyskać w stanie nieco dziwne, gdzie zostały odinstalowane rozszerzenia VSIX, ale niektóre pliki zostały pozostawione.</span><span class="sxs-lookup"><span data-stu-id="52b3d-177">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="52b3d-178">Aby obejść ten problem:</span><span class="sxs-lookup"><span data-stu-id="52b3d-178">To work around this issue:</span></span>

1. <span data-ttu-id="52b3d-179">Zamknij program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="52b3d-179">Exit Visual Studio</span></span>
1. <span data-ttu-id="52b3d-180">Otwórz następujący folder (może to być na innym dysku na komputerze)</span><span class="sxs-lookup"><span data-stu-id="52b3d-180">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="52b3d-181">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span><span class="sxs-lookup"><span data-stu-id="52b3d-181">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span></span>

1. <span data-ttu-id="52b3d-182">Usuń wszystkie pliki z *.deleteme* rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="52b3d-182">Delete all the files with the *.deleteme* extensions.</span></span>
1. <span data-ttu-id="52b3d-183">Otwórz ponownie program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="52b3d-183">Re-open Visual Studio</span></span>

<span data-ttu-id="52b3d-184">Po wykonaniu tych kroków, można kontynuować.</span><span class="sxs-lookup"><span data-stu-id="52b3d-184">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="52b3d-185">W rzadkich przypadkach kompilowanie za pomocą analizy kodu włączona, powoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="52b3d-185">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="52b3d-186">Może być występuje następujący błąd, jeśli zainstaluje FluentNHibernate za pomocą konsoli Menedżera pakietów, a następnie Skompiluj projekt za pomocą "Analizy kodu" włączona.</span><span class="sxs-lookup"><span data-stu-id="52b3d-186">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="52b3d-187">Domyślnie FluentNHibernate wymaga NHibernate 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="52b3d-187">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="52b3d-188">Jednak zgodnie z projektem NuGet zainstalujesz NHibernate 3.0.0.4000 w projekcie i dodaj odpowiednie powiązanie przekierowuje, dzięki czemu będzie ona działać.</span><span class="sxs-lookup"><span data-stu-id="52b3d-188">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="52b3d-189">Projekt zostanie skompilowany świetnie Jeśli nie włączono analizy kodu.</span><span class="sxs-lookup"><span data-stu-id="52b3d-189">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="52b3d-190">W przeciwieństwie do kompilatora narzędzie do analizy kodu nie prawidłowo wykonaj przekierowania powiązań do używania 3.0.0.4000 zamiast 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="52b3d-190">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="52b3d-191">Można obejść ten problem, albo instalowanie NHibernate 3.0.0.2001 lub poproś narzędzie do analizy kodu do działa tak samo jak kompilator, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="52b3d-191">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="52b3d-192">Przejdź do *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static analizy Tools\FxCop*</span><span class="sxs-lookup"><span data-stu-id="52b3d-192">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="52b3d-193">Otwórz FxCopCmd.exe.config i zmień `AssemblyReferenceResolveMode` z `StrongName` do `StrongNameIgnoringVersion`.</span><span class="sxs-lookup"><span data-stu-id="52b3d-193">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="52b3d-194">Zapisz zmiany i ponownie skompiluj projekt.</span><span class="sxs-lookup"><span data-stu-id="52b3d-194">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="52b3d-195">Błąd zapisu polecenie nie działa wewnątrz install.ps1/uninstall.ps1/init.ps1</span><span class="sxs-lookup"><span data-stu-id="52b3d-195">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="52b3d-196">Jest to znany problem.</span><span class="sxs-lookup"><span data-stu-id="52b3d-196">This is a known issue.</span></span> <span data-ttu-id="52b3d-197">Zamiast wywoływania błąd zapisu, spróbuj wywoływania throw.</span><span class="sxs-lookup"><span data-stu-id="52b3d-197">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="52b3d-198">Instalowanie NuGet z ograniczonym dostępem w systemie Windows 2003 można awarię programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="52b3d-198">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>

<span data-ttu-id="52b3d-199">Podczas próby zainstalowania NuGet za pomocą Menedżera rozszerzeń programu Visual Studio, a nie jest uruchomione jako administrator, &#8220;Uruchom jako&#8221; za pomocą pola wyboru zostanie wyświetlone okno dialogowe &#8220;uruchamiaj ten program z ograniczonym dostępem&#8221; sprawdzana przez Domyślnie.</span><span class="sxs-lookup"><span data-stu-id="52b3d-199">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![Uruchom jako ograniczeniami okna dialogowego](./media/RunAsRestricted.png)

<span data-ttu-id="52b3d-201">Kliknięcie przycisku OK, korzystając z niego zaznaczone awarie programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52b3d-201">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="52b3d-202">Upewnij się, usuń zaznaczenie tej opcji, przed zainstalowaniem programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="52b3d-202">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="52b3d-203">Nie można odinstalować programu NuGet dla narzędzi Windows Phone</span><span class="sxs-lookup"><span data-stu-id="52b3d-203">Cannot uninstall NuGet for Windows Phone Tools</span></span>

<span data-ttu-id="52b3d-204">Narzędzia Windows Phone nie ma obsługi Menedżera rozszerzeń dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52b3d-204">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="52b3d-205">Aby odinstalować NuGet, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="52b3d-205">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="52b3d-206">Zmiana wielkości liter, identyfikatory pakietu NuGet przerywa Przywracanie pakietu</span><span class="sxs-lookup"><span data-stu-id="52b3d-206">Changing the capitalization of NuGet package IDs breaks package restore</span></span>

<span data-ttu-id="52b3d-207">Zgodnie z opisem szeroko na [problem w usłudze GitHub](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), zmiana wielkości liter pakietów NuGet może odbywać się przez obsługę pakietów NuGet, ale kompilacji powoduje, że podczas przywracania pakietu dla użytkowników, którzy mają istniejące, inaczej — z uwzględnieniem wielkości liter, pakiety w ich *globalnymi pakietami* folderu.</span><span class="sxs-lookup"><span data-stu-id="52b3d-207">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their *global-packages* folder.</span></span> <span data-ttu-id="52b3d-208">Firma Microsoft zaleca tylko żądania zmiany wielkości liter, gdy masz sposób do komunikowania się z istniejącym użytkownikom pakietu o przerwania, który może wystąpić, aby ich przywracania pakietów w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="52b3d-208">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="52b3d-209">Raportowanie problemów</span><span class="sxs-lookup"><span data-stu-id="52b3d-209">Reporting issues</span></span>

<span data-ttu-id="52b3d-210">Aby zgłosić problemy z NuGet, odwiedź stronę [ https://github.com/nuget/home/issues ](https://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="52b3d-210">To report NuGet issues, visit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span></span>
