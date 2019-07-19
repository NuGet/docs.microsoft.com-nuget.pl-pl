---
title: Znane problemy
description: Znane problemy związane z pakietem NuGet, w tym uwierzytelnianie, instalacja pakietu i narzędzia.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b104eb39ddeacd9ca1ea45937cf98ad57531112a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317143"
---
# <a name="known-issues-with-nuget"></a><span data-ttu-id="599de-103">Znane problemy związane z pakietem NuGet</span><span class="sxs-lookup"><span data-stu-id="599de-103">Known Issues with NuGet</span></span>

<span data-ttu-id="599de-104">Są to najczęstsze znane problemy związane z pakietem NuGet, które są wielokrotnie raportowane.</span><span class="sxs-lookup"><span data-stu-id="599de-104">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="599de-105">Jeśli masz problemy z instalowaniem NuGet lub zarządzaniem pakietami, zapoznaj się z tymi znanymi problemami i ich rozwiązaniami.</span><span class="sxs-lookup"><span data-stu-id="599de-105">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="599de-106">Począwszy od programu NuGet 4,0, znane problemy są częścią odpowiednich informacji o wersji.</span><span class="sxs-lookup"><span data-stu-id="599de-106">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="599de-107">Problemy z uwierzytelnianiem ze źródłami danych NuGet w programie VSTS z pakietem NuGet. exe v 3.4.3</span><span class="sxs-lookup"><span data-stu-id="599de-107">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="599de-108">**Problem:**</span><span class="sxs-lookup"><span data-stu-id="599de-108">**Problem:**</span></span>

<span data-ttu-id="599de-109">Gdy korzystamy z następującego polecenia do przechowywania poświadczeń, będziemy mieć podwójne szyfrowanie osobistego tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="599de-109">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="599de-110">$PAT = "osobisty token dostępu" $Feed = "Twój adres URL" .\nuget.exe Dodaj nazwę źródła test-Source $Feed-UserName $UserName-Password $PAT</span><span class="sxs-lookup"><span data-stu-id="599de-110">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="599de-111">**Poprawkę**</span><span class="sxs-lookup"><span data-stu-id="599de-111">**Workaround:**</span></span>

<span data-ttu-id="599de-112">Przechowuj hasła w postaci zwykłego tekstu przy użyciu opcji [-StorePasswordInClearText](../reference/cli-reference/cli-ref-sources.md) .</span><span class="sxs-lookup"><span data-stu-id="599de-112">Store passwords in clear text using the [-StorePasswordInClearText](../reference/cli-reference/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="599de-113">Błąd podczas instalowania pakietów z pakietem NuGet 3,4,</span><span class="sxs-lookup"><span data-stu-id="599de-113">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="599de-114">**Problem:**</span><span class="sxs-lookup"><span data-stu-id="599de-114">**Problem:**</span></span>

<span data-ttu-id="599de-115">W programie NuGet 3,4 i w przypadku korzystania z dodatku NuGet żadne źródła nie są raportowane jako dostępne i nie można dodać nowych źródeł w oknie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="599de-115">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="599de-116">Wynik jest podobny do poniższego obrazu:</span><span class="sxs-lookup"><span data-stu-id="599de-116">The result is similar to the image below:</span></span>

![Konfiguracja NuGet bez źródeł](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="599de-118">Plik w folderze (Windows`~/.nuget/` ) lub (Mac/Linux) przypadkowo został opróżniony. `%AppData%\NuGet\` `NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="599de-118">The `NuGet.Config` file in your `%AppData%\NuGet\` (Windows) or `~/.nuget/` (Mac/Linux) folder has accidentally been emptied.</span></span> <span data-ttu-id="599de-119">Aby rozwiązać ten problem: Zamknij program Visual Studio (w systemie Windows, jeśli ma to `NuGet.Config` zastosowanie), usuń plik, a następnie spróbuj ponownie wykonać operację.</span><span class="sxs-lookup"><span data-stu-id="599de-119">To fix this: close Visual Studio (on Windows, if applicable), delete the `NuGet.Config` file, and try the operation again.</span></span> <span data-ttu-id="599de-120">Pakiet NuGet wygenerował `NuGet.Config` nowe i należy mieć możliwość przejścia.</span><span class="sxs-lookup"><span data-stu-id="599de-120">NuGet generated a new `NuGet.Config` and you should be able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="599de-121">Błąd podczas instalowania pakietów przy użyciu narzędzia NuGet 2,7</span><span class="sxs-lookup"><span data-stu-id="599de-121">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="599de-122">**Problem:**</span><span class="sxs-lookup"><span data-stu-id="599de-122">**Problem:**</span></span>

<span data-ttu-id="599de-123">W programie NuGet 2,7 lub nowszym podczas próby zainstalowania dowolnego pakietu, który zawiera odwołania do zestawów, może zostać wyświetlony komunikat o błędzie **"ciąg wejściowy nie ma poprawnego formatu"** , jak poniżej:</span><span class="sxs-lookup"><span data-stu-id="599de-123">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

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

<span data-ttu-id="599de-124">Przyczyną jest to, że biblioteka `VSLangProj.dll` typów składnika com jest wyrejestrowana w systemie.</span><span class="sxs-lookup"><span data-stu-id="599de-124">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="599de-125">Taka sytuacja może wystąpić, jeśli na przykład masz dwie wersje programu Visual Studio, które zostały zainstalowane obok siebie, a następnie odinstalujesz starszą wersję.</span><span class="sxs-lookup"><span data-stu-id="599de-125">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="599de-126">Wykonanie tej czynności może przypadkowo wyrejestrować powyższą bibliotekę COM.</span><span class="sxs-lookup"><span data-stu-id="599de-126">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="599de-127">**Rozwiązanie:**</span><span class="sxs-lookup"><span data-stu-id="599de-127">**Solution:**:</span></span>

<span data-ttu-id="599de-128">Uruchom to polecenie w wierszu polecenia z **podwyższonym poziomem uprawnień** , aby ponownie zarejestrować bibliotekę typów dla`VSLangProj.dll`</span><span class="sxs-lookup"><span data-stu-id="599de-128">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="599de-129">Jeśli polecenie nie powiedzie się, sprawdź, czy plik istnieje w tej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="599de-129">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="599de-130">Aby uzyskać więcej informacji na temat tego błędu, zobacz ten element [roboczy element]roboczy(https://nuget.codeplex.com/workitem/3609 "3609").</span><span class="sxs-lookup"><span data-stu-id="599de-130">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="599de-131">Błąd kompilacji po aktualizacji pakietu w programie VS 2012</span><span class="sxs-lookup"><span data-stu-id="599de-131">Build failure after package update in VS 2012</span></span>

<span data-ttu-id="599de-132">Problem: Używasz programu VS 2012 RTM.</span><span class="sxs-lookup"><span data-stu-id="599de-132">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="599de-133">Podczas aktualizacji pakietów NuGet otrzymujesz następujący komunikat: "Nie można ukończyć odinstalowywania co najmniej jednego pakietu".</span><span class="sxs-lookup"><span data-stu-id="599de-133">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="599de-134">zostanie wyświetlony monit o ponowne uruchomienie programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="599de-134">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="599de-135">Po ponownym uruchomieniu programu VS należy uzyskać błędy kompilacji brzmienia.</span><span class="sxs-lookup"><span data-stu-id="599de-135">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="599de-136">Przyczyną jest to, że niektóre pliki w starych pakietach są blokowane przez proces MSBuild w tle.</span><span class="sxs-lookup"><span data-stu-id="599de-136">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span> <span data-ttu-id="599de-137">Nawet po ponownym uruchomieniu programu VS, proces MSBuild w tle nadal używa plików w starych pakietach, co powoduje błędy kompilacji.</span><span class="sxs-lookup"><span data-stu-id="599de-137">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="599de-138">Poprawka ma na celu zainstalowanie aktualizacji programu VS 2012, np. VS 2012 Update 2.</span><span class="sxs-lookup"><span data-stu-id="599de-138">The fix is to install VS 2012 Update, e.g. VS 2012 Update 2.</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="599de-139">Uaktualnienie do najnowszego NuGet ze starszej wersji powoduje błąd weryfikacji podpisu</span><span class="sxs-lookup"><span data-stu-id="599de-139">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="599de-140">Jeśli korzystasz z programu VS 2010 z dodatkiem SP1, możesz uruchomić następujący komunikat o błędzie, próbując uaktualnić program NuGet, jeśli masz zainstalowaną starszą wersję.</span><span class="sxs-lookup"><span data-stu-id="599de-140">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Instalator rozszerzenia programu Visual Studio](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="599de-142">Podczas przeglądania dzienników może pojawić się wzmianka `SignatureMismatchException`o.</span><span class="sxs-lookup"><span data-stu-id="599de-142">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="599de-143">Aby temu zapobiec, istnieje [poprawka programu Visual Studio 2010 z dodatkiem SP1](http://bit.ly/vsixcertfix) , którą można zainstalować.</span><span class="sxs-lookup"><span data-stu-id="599de-143">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="599de-144">Obejście polega na tym, że po prostu Odinstaluj pakiet NuGet (przy użyciu programu Visual Studio jako administrator), a następnie zainstaluj go z galerii rozszerzeń programu VS.</span><span class="sxs-lookup"><span data-stu-id="599de-144">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="599de-145">Aby [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) uzyskać więcej informacji, zobacz.</span><span class="sxs-lookup"><span data-stu-id="599de-145">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="599de-146">Konsola Menedżera pakietów zgłasza wyjątek, gdy zostanie również zainstalowany dodatek do programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="599de-146">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="599de-147">Podczas uruchamiania konsoli Menedżera pakietów można uruchomić następujący komunikat o wyjątku, jeśli zainstalowano dodatek "reflektor".</span><span class="sxs-lookup"><span data-stu-id="599de-147">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="599de-148">lub</span><span class="sxs-lookup"><span data-stu-id="599de-148">or</span></span>

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

<span data-ttu-id="599de-149">Skontaktujemy się z autorem dodatku w nadziei o rozwiązaniu problemu.</span><span class="sxs-lookup"><span data-stu-id="599de-149">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="599de-150">Update: Sprawdzono, że Najnowsza wersja reflektora 6,5 nie powoduje już wystąpienia tego wyjątku w konsoli programu.</span><span class="sxs-lookup"><span data-stu-id="599de-150">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="599de-151">Otwieranie konsoli Menedżera pakietów kończy się niepowodzeniem z powodu wyjątku ObjectSecurity</span><span class="sxs-lookup"><span data-stu-id="599de-151">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="599de-152">Te błędy mogą pojawić się podczas próby otwarcia konsoli Menedżera pakietów:</span><span class="sxs-lookup"><span data-stu-id="599de-152">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="599de-153">Jeśli tak, postępuj zgodnie z rozwiązaniem [omówionym w StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) , aby je rozwiązać.</span><span class="sxs-lookup"><span data-stu-id="599de-153">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="599de-154">Okno dialogowe Dodaj odwołanie do biblioteki pakietów zgłasza wyjątek, jeśli rozwiązanie zawiera projekt InstallShield Limited Edition</span><span class="sxs-lookup"><span data-stu-id="599de-154">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project</span></span>

<span data-ttu-id="599de-155">Zidentyfikowano, że jeśli rozwiązanie zawiera co najmniej jeden projekt InstallShield Limited Edition, w oknie dialogowym **Dodawanie odwołania do biblioteki pakietów** zostanie zgłoszony wyjątek, gdy zostanie otwarty.</span><span class="sxs-lookup"><span data-stu-id="599de-155">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="599de-156">Obecnie nie istnieje jeszcze obejście tego problemu, z wyjątkiem usuwania projektów InstallShield lub ich wyładowywania.</span><span class="sxs-lookup"><span data-stu-id="599de-156">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="599de-157">Przycisk odinstalowywania został wyszarzony?</span><span class="sxs-lookup"><span data-stu-id="599de-157">Uninstall Button Greyed out?</span></span> <span data-ttu-id="599de-158">Pakiet NuGet wymaga uprawnień administratora do zainstalowania/odinstalowania</span><span class="sxs-lookup"><span data-stu-id="599de-158">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="599de-159">Jeśli spróbujesz odinstalować pakiet NuGet za pomocą Menedżera rozszerzeń programu Visual Studio, możesz zauważyć, że przycisk Odinstaluj jest wyłączony.</span><span class="sxs-lookup"><span data-stu-id="599de-159">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span> <span data-ttu-id="599de-160">Pakiet NuGet wymaga dostępu administratora do instalacji i dezinstalacji.</span><span class="sxs-lookup"><span data-stu-id="599de-160">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="599de-161">Uruchom ponownie program Visual Studio jako administrator, aby odinstalować rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="599de-161">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span> <span data-ttu-id="599de-162">Pakiet NuGet nie wymaga dostępu administratora do korzystania z niego.</span><span class="sxs-lookup"><span data-stu-id="599de-162">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="599de-163">Konsola Menedżera pakietów ulega awarii, gdy otworzysz ją w systemie Windows XP.</span><span class="sxs-lookup"><span data-stu-id="599de-163">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="599de-164">Co jest nie tak?</span><span class="sxs-lookup"><span data-stu-id="599de-164">What's wrong?</span></span>

<span data-ttu-id="599de-165">Pakiet NuGet wymaga środowiska uruchomieniowego PowerShell 2,0.</span><span class="sxs-lookup"><span data-stu-id="599de-165">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="599de-166">Domyślnie system Windows XP nie ma programu PowerShell 2,0.</span><span class="sxs-lookup"><span data-stu-id="599de-166">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="599de-167">Środowisko uruchomieniowe programu PowerShell 2,0 można pobrać [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929)z programu.</span><span class="sxs-lookup"><span data-stu-id="599de-167">You can download the Powershell 2.0 runtime from [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span></span> <span data-ttu-id="599de-168">Po zainstalowaniu należy ponownie uruchomić program Visual Studio, aby móc otworzyć konsolę Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="599de-168">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="599de-169">Jeśli konsola Menedżera pakietów jest otwarta, program Visual Studio 2010 z dodatkiem SP1 w wersji beta jest nieoczekiwany.</span><span class="sxs-lookup"><span data-stu-id="599de-169">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="599de-170">Jeśli zainstalowano program Visual Studio 2010 z dodatkiem SP1 Beta, można zauważyć, że Jeśli opuścisz konsolę Menedżera pakietów otwartą i zamkniętą program Visual Studio, wystąpi awaria.</span><span class="sxs-lookup"><span data-stu-id="599de-170">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="599de-171">Jest to znany problem programu Visual Studio, który zostanie rozwiązany w wersji RTM programu SP1.</span><span class="sxs-lookup"><span data-stu-id="599de-171">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span> <span data-ttu-id="599de-172">Na razie po prostu zignoruj awarię lub Odinstaluj program SP1 w wersji beta, jeśli jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="599de-172">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="599de-173">Element "Metadata"... występuje nieprawidłowy wyjątek elementu podrzędnego</span><span class="sxs-lookup"><span data-stu-id="599de-173">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="599de-174">Jeśli zainstalowano pakiety skompilowane przy użyciu wersji wstępnej programu NuGet, może wystąpić komunikat o błędzie z informacją o tym, że "element" metadanych "w przestrzeni nazw" schemas.microsoft.com/packaging/2010/07/nuspec.xsd "ma nieprawidłowy element podrzędny" podczas uruchamiania programu RTM wersja programu NuGet z tym projektem.</span><span class="sxs-lookup"><span data-stu-id="599de-174">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="599de-175">Należy odinstalować, a następnie zainstalować ponownie każdy pakiet przy użyciu wersji RTM programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="599de-175">You need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a><span data-ttu-id="599de-176">Próba zainstalowania lub odinstalowania wyników spowoduje błąd "nie można utworzyć pliku, gdy ten plik już istnieje".</span><span class="sxs-lookup"><span data-stu-id="599de-176">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists."</span></span>

<span data-ttu-id="599de-177">Z jakiegoś powodu rozszerzenia programu Visual Studio mogą być w stanie brzmienia, w którym odinstalowano rozszerzenie VSIX, ale niektóre pliki zostały pozostawione w tle.</span><span class="sxs-lookup"><span data-stu-id="599de-177">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="599de-178">Aby obejść ten problem:</span><span class="sxs-lookup"><span data-stu-id="599de-178">To work around this issue:</span></span>

1. <span data-ttu-id="599de-179">Wyjdź z programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="599de-179">Exit Visual Studio</span></span>
1. <span data-ttu-id="599de-180">Otwórz następujący folder (może on znajdować się na innym dysku na komputerze)</span><span class="sxs-lookup"><span data-stu-id="599de-180">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="599de-181">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version></span><span class="sxs-lookup"><span data-stu-id="599de-181">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version></span></span>\

1. <span data-ttu-id="599de-182">Usuń wszystkie pliki z rozszerzeniami *. Deleteme* .</span><span class="sxs-lookup"><span data-stu-id="599de-182">Delete all the files with the *.deleteme* extensions.</span></span>
1. <span data-ttu-id="599de-183">Otwórz ponownie program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="599de-183">Re-open Visual Studio</span></span>

<span data-ttu-id="599de-184">Po wykonaniu tych kroków powinno być możliwe kontynuowanie.</span><span class="sxs-lookup"><span data-stu-id="599de-184">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="599de-185">W rzadkich przypadkach Kompilowanie z włączoną analizą kodu powoduje wystąpienie błędu.</span><span class="sxs-lookup"><span data-stu-id="599de-185">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="599de-186">Następujący błąd może wystąpić, Jeśli instalujesz FluentNHibernate z konsolą Menedżera pakietów, a następnie kompilujesz projekt z włączoną funkcją "Analiza kodu".</span><span class="sxs-lookup"><span data-stu-id="599de-186">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="599de-187">Domyślnie FluentNHibernate wymaga NHibernate 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="599de-187">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="599de-188">Jednak po zaprojektowaniu pakiet NuGet zainstaluje NHibernate 3.0.0.4000 w projekcie i doda odpowiednie przekierowania powiązań, aby działał.</span><span class="sxs-lookup"><span data-stu-id="599de-188">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="599de-189">Projekt zostanie skompilowany, jeśli analiza kodu nie jest włączona.</span><span class="sxs-lookup"><span data-stu-id="599de-189">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="599de-190">W przeciwieństwie do kompilatora Narzędzie analizy kodu nie jest prawidłowo zgodne z przekierowaniami powiązań, aby użyć 3.0.0.4000 zamiast 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="599de-190">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="599de-191">Problem można obejść, instalując NHibernate 3.0.0.2001 lub poinformuj Narzędzie analizy kodu, aby zachowywać się tak samo jak kompilator, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="599de-191">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="599de-192">Przejdź do pozycji *%ProgramFiles%\Microsoft Visual Studio 10.0 \ Team Tools\Static Analysis Tools\FxCop*</span><span class="sxs-lookup"><span data-stu-id="599de-192">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="599de-193">Otwórz plik plik FxCopCmd. exe. config i `AssemblyReferenceResolveMode` Zmień `StrongName` go `StrongNameIgnoringVersion`z na.</span><span class="sxs-lookup"><span data-stu-id="599de-193">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="599de-194">Zapisz zmiany i ponownie skompiluj projekt.</span><span class="sxs-lookup"><span data-stu-id="599de-194">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="599de-195">Polecenie Write-Error nie działa wewnątrz install. ps1/Uninstall. ps1/init. ps1</span><span class="sxs-lookup"><span data-stu-id="599de-195">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="599de-196">Jest to znany problem.</span><span class="sxs-lookup"><span data-stu-id="599de-196">This is a known issue.</span></span> <span data-ttu-id="599de-197">Zamiast wywołania metody Write-Error spróbuj wywołać metodę throw.</span><span class="sxs-lookup"><span data-stu-id="599de-197">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="599de-198">Instalowanie pakietu NuGet z ograniczonym dostępem w systemie Windows 2003 może spowodować awarię programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="599de-198">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>

<span data-ttu-id="599de-199">Przy próbie zainstalowania narzędzia NuGet przy użyciu Menedżera rozszerzeń programu Visual Studio i niedziałającego jako administrator zostanie &#8220;wyświetlone okno&#8221; dialogowe Uruchom jako z widocznym przyciskiem &#8220;Uruchom ten program z ograniczonym&#8221; dostępem zaznaczonym przez wartooć.</span><span class="sxs-lookup"><span data-stu-id="599de-199">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![Uruchom jako okno dialogowe z ograniczeniami](./media/RunAsRestricted.png)

<span data-ttu-id="599de-201">Kliknięcie przycisku OK powoduje awarię programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="599de-201">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="599de-202">Przed zainstalowaniem programu NuGet Usuń zaznaczenie tej opcji.</span><span class="sxs-lookup"><span data-stu-id="599de-202">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="599de-203">Nie można odinstalować programu NuGet dla narzędzi Windows Phone</span><span class="sxs-lookup"><span data-stu-id="599de-203">Cannot uninstall NuGet for Windows Phone Tools</span></span>

<span data-ttu-id="599de-204">Narzędzia Windows Phone nie obsługują Menedżera rozszerzeń programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="599de-204">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="599de-205">Aby odinstalować pakiet NuGet, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="599de-205">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="599de-206">Zmiana wielkości liter w identyfikatorach pakietów NuGet powoduje przerwanie przywracania pakietu</span><span class="sxs-lookup"><span data-stu-id="599de-206">Changing the capitalization of NuGet package IDs breaks package restore</span></span>

<span data-ttu-id="599de-207">Zgodnie z opisem w [tym problemie](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932)z usługą GitHub, zmiana wielkości liter pakietów NuGet może odbywać się przez obsługę NuGet, ale powoduje komplikacje podczas przywracania pakietów dla użytkowników, którzy mają istniejące, w różny sposób, pakiety w ich  *folder Global-Packages* .</span><span class="sxs-lookup"><span data-stu-id="599de-207">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their *global-packages* folder.</span></span> <span data-ttu-id="599de-208">Zalecamy tylko żądanie zmiany wielkości liter, gdy istnieje możliwość komunikowania się z istniejącymi użytkownikami pakietu w sprawie przerwy, która może wystąpić w przypadku przywracania pakietu w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="599de-208">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="599de-209">Raportowanie problemów</span><span class="sxs-lookup"><span data-stu-id="599de-209">Reporting issues</span></span>

<span data-ttu-id="599de-210">Aby zgłosić problemy z pakietem [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues)NuGet, odwiedź stronę.</span><span class="sxs-lookup"><span data-stu-id="599de-210">To report NuGet issues, visit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span></span>
