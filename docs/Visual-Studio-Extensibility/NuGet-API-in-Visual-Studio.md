---
title: NuGet interfejsu API w programie Visual Studio | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 31f88cf0-d40a-42ee-974e-07910bb0771c
description: "Dokumentacja interfejsu API NuGet eksportuje za pośrednictwem Managed Extensibility Framework w programie Visual Studio"
keywords: "Interfejs API NuGet, NuGet w programie Visual Studio, interfejsów programowania NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1d5c4cba1474f4215c6cc83497e347b2145f21ef
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-api-in-visual-studio"></a><span data-ttu-id="9d231-104">NuGet interfejsu API w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9d231-104">NuGet API in Visual Studio</span></span>

<span data-ttu-id="9d231-105">Oprócz konsoli w programie Visual Studio i interfejs użytkownika Menedżera pakietów NuGet Eksportuje również niektóre usługi za pośrednictwem [Managed Extensibility Framework (MEF)](http://msdn.microsoft.com/library/dd460648.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d231-105">In addition to the Package Manager UI and Console in Visual Studio, NuGet also exports some useful services through the [Managed Extensibility Framework (MEF)](http://msdn.microsoft.com/library/dd460648.aspx).</span></span> <span data-ttu-id="9d231-106">Ten interfejs umożliwia innych składników w programie Visual Studio do interakcji z NuGet, która może służyć do instalowania i odinstalowywania pakietów oraz w celu uzyskania informacji na temat zainstalowanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="9d231-106">This interface allows other components in Visual Studio to interact with NuGet, which can be used to install and uninstall packages, and to obtain information about installed packages.</span></span>

<span data-ttu-id="9d231-107">Począwszy od NuGet 3.3 + NuGet eksportuje następujących usług, które znajdują się w `NuGet.VisualStudio` przestrzeni nazw w `NuGet.VisualStudio.dll` zestawu:</span><span class="sxs-lookup"><span data-stu-id="9d231-107">As of NuGet 3.3+, NuGet exports the following services all of which reside in the `NuGet.VisualStudio` namespace in the `NuGet.VisualStudio.dll` assembly:</span></span>

- <span data-ttu-id="9d231-108">[`IRegistryKey`](#iregistrykey-interface): Metody do pobierania wartości z podklucza rejestru.</span><span class="sxs-lookup"><span data-stu-id="9d231-108">[`IRegistryKey`](#iregistrykey-interface): Method to retrieve a value from a registry subkey.</span></span>
- <span data-ttu-id="9d231-109">[`IVsPackageInstaller`](#ivspackageinstaller-interface): Metody można zainstalować pakietów NuGet w projektach.</span><span class="sxs-lookup"><span data-stu-id="9d231-109">[`IVsPackageInstaller`](#ivspackageinstaller-interface): Methods to install NuGet packages into projects.</span></span>
- <span data-ttu-id="9d231-110">[`IVsPackageInstallerEvents`](#ivspackageinstallerevents-interface): Zdarzenia dla Instalowanie/Odinstalowywanie pakietu.</span><span class="sxs-lookup"><span data-stu-id="9d231-110">[`IVsPackageInstallerEvents`](#ivspackageinstallerevents-interface): Events for package install/uninstall.</span></span>
- <span data-ttu-id="9d231-111">[`IVsPackageInstallerProjectEvents`](#ivspackageinstallerprojectevents-interface): Zdarzenia partii Instalowanie/Odinstalowywanie pakietu.</span><span class="sxs-lookup"><span data-stu-id="9d231-111">[`IVsPackageInstallerProjectEvents`](#ivspackageinstallerprojectevents-interface): Batch events for package install/uninstall.</span></span>
- <span data-ttu-id="9d231-112">[`IVsPackageInstallerServices`](#ivspackageinstallerservices-interface): Metody, aby pobrać zainstalowanych pakietów w bieżącym rozwiązaniu i sprawdź, czy dany pakiet jest zainstalowany w projekcie.</span><span class="sxs-lookup"><span data-stu-id="9d231-112">[`IVsPackageInstallerServices`](#ivspackageinstallerservices-interface): Methods to retrieve installed packages in the current solution and to check whether a given package is installed in a project.</span></span>
- <span data-ttu-id="9d231-113">[`IVsPackageManagerProvider`](#ivspackagemanagerprovider-interface): Metody w celu zapewnienia alternatywnej Menedżera pakietów sugestie dotyczące pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="9d231-113">[`IVsPackageManagerProvider`](#ivspackagemanagerprovider-interface): Methods to provide alternative Package Manager suggestions for a NuGet package.</span></span>
- <span data-ttu-id="9d231-114">[`IVsPackageMetadata`](#ivspackagemetadata-interface); Metody do pobierania informacji o zainstalowanym pakietem.</span><span class="sxs-lookup"><span data-stu-id="9d231-114">[`IVsPackageMetadata`](#ivspackagemetadata-interface); Methods to retrieve information about an installed package.</span></span>
- <span data-ttu-id="9d231-115">[`IVsPackageProjectMetadata`](#ivspackageprojectmetadata-interface); Metody do pobierania informacji o projekcie, w którym NuGet akcje są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="9d231-115">[`IVsPackageProjectMetadata`](#ivspackageprojectmetadata-interface); Methods to retrieve information about a project where NuGet actions are being executed.</span></span>
- <span data-ttu-id="9d231-116">[`IVsPackageRestorer`](#ivspackagerestorer-interface): Metody, aby przywrócić pakiety zainstalowane w projekcie.</span><span class="sxs-lookup"><span data-stu-id="9d231-116">[`IVsPackageRestorer`](#ivspackagerestorer-interface): Methods to restore packages installed in a project.</span></span>
- <span data-ttu-id="9d231-117">[`IVsPackageSourceProvider`](#ivspackagesourceprovider-interface): Metody, aby pobrać listę NuGet pakietu źródeł.</span><span class="sxs-lookup"><span data-stu-id="9d231-117">[`IVsPackageSourceProvider`](#ivspackagesourceprovider-interface): Methods to retrieve a list of NuGet package sources.</span></span>
- <span data-ttu-id="9d231-118">[`IVsPackageUninstaller`](#ivspackageuninstaller-interface): Metody do odinstalowania pakietów NuGet z projektów.</span><span class="sxs-lookup"><span data-stu-id="9d231-118">[`IVsPackageUninstaller`](#ivspackageuninstaller-interface): Methods to uninstall NuGet packages from projects.</span></span>
- <span data-ttu-id="9d231-119">[`IVsTemplateWizard`](#ivstemplatewizard-interface): Przeznaczony dla szablonów projektu/elementu uwzględnić wstępnie zainstalowane pakiety; Ten interfejs jest *nie* ma być wywoływany z kodu i nie ma żadnych metod publicznych.</span><span class="sxs-lookup"><span data-stu-id="9d231-119">[`IVsTemplateWizard`](#ivstemplatewizard-interface): Designed for project/item templates to include pre-installed packages; this interface is *not* meant to be invoked from code and has no public methods.</span></span>

## <a name="using-nuget-services"></a><span data-ttu-id="9d231-120">Przy użyciu usług NuGet</span><span class="sxs-lookup"><span data-stu-id="9d231-120">Using NuGet services</span></span>

1. <span data-ttu-id="9d231-121">Zainstaluj [ `NuGet.VisualStudio` ](https://www.nuget.org/packages/NuGet.VisualStudio) pakietu do projektu, który zawiera `NuGet.VisualStudio.dll` zestawu.</span><span class="sxs-lookup"><span data-stu-id="9d231-121">Install the [`NuGet.VisualStudio`](https://www.nuget.org/packages/NuGet.VisualStudio) package into your project, which contains the `NuGet.VisualStudio.dll` assembly.</span></span>

    <span data-ttu-id="9d231-122">Po zainstalowaniu pakietu automatycznie ustawia **Osadź typy międzyoperacyjne** właściwości odwołania zestawu do **True**.</span><span class="sxs-lookup"><span data-stu-id="9d231-122">When installed, the package automatically sets the **Embed Interop Types** property of the assembly reference to **True**.</span></span> <span data-ttu-id="9d231-123">Dzięki temu kodu odporne na zmiany wersji, gdy użytkownicy zaktualizować do nowszej wersji programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="9d231-123">This makes your code  resilient against version changes when users update to newer versions of NuGet.</span></span>

> [!Warning]
> <span data-ttu-id="9d231-124">Nie należy używać innych typów poza interfejsów publicznych w kodzie, a nie odwołuj się do żadnych innych NuGet zestawów, w tym `NuGet.Core.dll`.</span><span class="sxs-lookup"><span data-stu-id="9d231-124">Do not use any other types besides the public interfaces in your code, and do not reference any other NuGet assemblies, including `NuGet.Core.dll`.</span></span>

1. <span data-ttu-id="9d231-125">Aby korzystać z usługi, zaimportuj go za pośrednictwem [zaimportować MEF atrybutu](https://msdn.microsoft.com/library/dd460648.aspx#Imports%20and%20Exports%20with%20Attributes), lub za pomocą [usługi IComponentModel](http://msdn.microsoft.com/library/microsoft.visualstudio.componentmodelhost.icomponentmodel.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d231-125">To use a service, import it through the [MEF Import attribute](https://msdn.microsoft.com/library/dd460648.aspx#Imports%20and%20Exports%20with%20Attributes), or through the [IComponentModel service](http://msdn.microsoft.com/library/microsoft.visualstudio.componentmodelhost.icomponentmodel.aspx).</span></span>

    ```cs
    //Using the Import attribute
    [Import(typeof(IVsPackageInstaller2))]
    public IVsPackageInstaller2 packageInstaller;
    packageInstaller.InstallLatestPackage(null, currentProject,
        "Newtonsoft.Json", false, false);

    //Using the IComponentModel service
    var componentModel = (IComponentModel)GetService(typeof(SComponentModel));
    IVsPackageInstallerServices installerServices =
        componentModel.GetService<IVsPackageInstallerServices>();

    var installedPackages = installerServices.GetInstalledPackages();
    ```

<span data-ttu-id="9d231-126">Odwołania, zawarty w kodzie źródłowym nuget.VisualStudio [repozytorium NuGet.Clients](https://github.com/NuGet/NuGet.Client/tree/dev/src/NuGet.Clients/NuGet.VisualStudio).</span><span class="sxs-lookup"><span data-stu-id="9d231-126">For reference, the source code for NuGet.VisualStudio is contained within the [NuGet.Clients repository](https://github.com/NuGet/NuGet.Client/tree/dev/src/NuGet.Clients/NuGet.VisualStudio).</span></span>

## <a name="iregistrykey-interface"></a><span data-ttu-id="9d231-127">Interfejs IRegistryKey</span><span class="sxs-lookup"><span data-stu-id="9d231-127">IRegistryKey interface</span></span>

```cs
/// <summary>
/// Specifies methods for manipulating a key in the Windows registry.
/// </summary>
public interface IRegistryKey
    {
    /// <summary>
    /// Retrieves the specified subkey for read or read/write access.
    /// </summary>
    /// <param name="name">The name or path of the subkey to create or open.</param>
    /// <returns>The subkey requested, or null if the operation failed.</returns>
    IRegistryKey OpenSubKey(string name);


    /// <summary>
    /// Retrieves the value associated with the specified name.
    /// </summary>
    /// <param name="name">The name of the value to retrieve. This string is not case-sensitive.</param>
    /// <returns>The value associated with name, or null if name is not found.</returns>
    object GetValue(string name);


    /// <summary>
    /// Closes the key and flushes it to disk if its contents have been modified.
    /// </summary>
    void Close();
}
```

## <a name="ivspackageinstaller-interface"></a><span data-ttu-id="9d231-128">Interfejs IVsPackageInstaller</span><span class="sxs-lookup"><span data-stu-id="9d231-128">IVsPackageInstaller interface</span></span>

```cs
public interface IVsPackageInstaller
{
    /// <summary>
    /// Installs a single package from the specified package source.
    /// </summary>
    /// <param name="source">
    /// The package source to install the package from. This value can be <c>null</c>
    /// to indicate that the user's configured sources should be used. Otherwise,
    /// this should be the source path as a string. If the user has credentials
    /// configured for a source, this value must exactly match the configured source
    /// value.
    /// </param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageId">The package ID of the package to install.</param>
    /// <param name="version">
    /// The version of the package to install. <c>null</c> can be provided to
    /// install the latest version of the package.
    /// </param>
    /// <param name="ignoreDependencies">
    /// A boolean indicating whether or not to ignore the package's dependencies
    /// during installation.
    /// </param>
    void InstallPackage(string source, Project project, string packageId, Version version, bool ignoreDependencies);

    /// <summary>
    /// Installs a single package from the specified package source.
    /// </summary>
    /// <param name="source">
    /// The package source to install the package from. This value can be <c>null</c>
    /// to indicate that the user's configured sources should be used. Otherwise,
    /// this should be the source path as a string. If the user has credentials
    /// configured for a source, this value must exactly match the configured source
    /// value.
    /// </param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageId">The package ID of the package to install.</param>
    /// <param name="version">
    /// The version of the package to install. <c>null</c> can be provided to
    /// install the latest version of the package.
    /// </param>
    /// <param name="ignoreDependencies">
    /// A boolean indicating whether or not to ignore the package's dependencies
    /// during installation.
    /// </param>
    void InstallPackage(string source, Project project, string packageId, string version, bool ignoreDependencies);

    /// <summary>
    /// Installs a single package from the specified package source.
    /// </summary>
    /// <param name="repository">The package repository to install the package from.</param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageId">The package id of the package to install.</param>
    /// <param name="version">
    /// The version of the package to install. <c>null</c> can be provided to
    /// install the latest version of the package.
    /// </param>
    /// <param name="ignoreDependencies">
    /// A boolean indicating whether or not to ignore the package's dependencies
    /// during installation.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating if assembly references from the package should be
    /// skipped.
    /// </param>
    void InstallPackage(IPackageRepository repository, Project project, string packageId, string version, bool ignoreDependencies, bool skipAssemblyReferences);

    /// <summary>
    /// Installs one or more packages that exist on disk in a folder defined in the registry.
    /// </summary>
    /// <param name="keyName">
    /// The registry key name (under NuGet's repository key) that defines the folder on disk
    /// containing the packages.
    /// </param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// <para>
    /// Dependencies are always ignored.
    /// </para>
    /// </remarks>
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    /// <summary>
    /// Installs one or more packages that exist on disk in a folder defined in the registry.
    /// </summary>
    /// <param name="keyName">
    /// The registry key name (under NuGet's repository key) that defines the folder on disk
    /// containing the packages.
    /// </param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="ignoreDependencies">A boolean indicating whether the package's dependencies should be ignored</param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// </remarks>
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, bool ignoreDependencies, Project project, IDictionary<string, string> packageVersions);

    /// <summary>
    /// Installs one or more packages that are embedded in a Visual Studio Extension Package.
    /// </summary>
    /// <param name="extensionId">The Id of the Visual Studio Extension Package.</param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="project">The target project for package installation</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// <para>
    /// Dependencies are always ignored.
    /// </para>
    /// </remarks>
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    /// <summary>
    /// Installs one or more packages that are embedded in a Visual Studio Extension Package.
    /// </summary>
    /// <param name="extensionId">The Id of the Visual Studio Extension Package.</param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="ignoreDependencies">A boolean indicating whether the package's dependencies should be ignored</param>
    /// <param name="project">The target project for package installation</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// </remarks>
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, bool ignoreDependencies, Project project, IDictionary<string, string> packageVersions);
}
```

## <a name="ivspackageinstallerevents-interface"></a><span data-ttu-id="9d231-129">Interfejs IVsPackageInstallerEvents</span><span class="sxs-lookup"><span data-stu-id="9d231-129">IVsPackageInstallerEvents interface</span></span>

```cs
public interface IVsPackageInstallerEvents
{
    /// <summary>
    /// Raised when a package is about to be installed into the current solution.
    /// </summary>
    event VsPackageEventHandler PackageInstalling;

    /// <summary>
    /// Raised after a package has been installed into the current solution.
    /// </summary>
    event VsPackageEventHandler PackageInstalled;

    /// <summary>
    /// Raised when a package is about to be uninstalled from the current solution.
    /// </summary>
    event VsPackageEventHandler PackageUninstalling;

    /// <summary>
    /// Raised after a package has been uninstalled from the current solution.
    /// </summary>
    event VsPackageEventHandler PackageUninstalled;

    /// <summary>
    /// Raised after a package has been installed into a project within the current solution.
    /// </summary>
    event VsPackageEventHandler PackageReferenceAdded;

    /// <summary>
    /// Raised after a package has been uninstalled from a project within the current solution.
    /// </summary>
    event VsPackageEventHandler PackageReferenceRemoved;
}
```

## <a name="ivspackageinstallerprojectevents-interface"></a><span data-ttu-id="9d231-130">Interfejs IVsPackageInstallerProjectEvents</span><span class="sxs-lookup"><span data-stu-id="9d231-130">IVsPackageInstallerProjectEvents interface</span></span>

```cs
public interface IVsPackageInstallerProjectEvents
{
    /// <summary>
    /// Raised before any IVsPackageInstallerEvents events are raised for a project.
    /// </summary>
    event VsPackageProjectEventHandler BatchStart;

    /// <summary>
    /// Raised after all IVsPackageInstallerEvents events are raised for a project.
    /// </summary>
    event VsPackageProjectEventHandler BatchEnd;
}
```

## <a name="ivspackageinstallerservices-interface"></a><span data-ttu-id="9d231-131">Interfejs IVsPackageInstallerServices</span><span class="sxs-lookup"><span data-stu-id="9d231-131">IVsPackageInstallerServices interface</span></span>

```cs
public interface IVsPackageInstallerServices
{
    // IMPORTANT: do NOT rearrange the methods here. The order is important to maintain
    // backwards compatibility with clients that were compiled against old versions of NuGet.

    /// <summary>
    /// Get the list of NuGet packages installed in the current solution.
    /// </summary>
    IEnumerable<IVsPackageMetadata> GetInstalledPackages();

    /// <summary>
    /// Checks if a NuGet package with the specified Id is installed in the specified project.
    /// </summary>
    /// <param name="project">The project to check for NuGet package.</param>
    /// <param name="id">The id of the package to check.</param>
    /// <returns><c>true</c> if the package is install. <c>false</c> otherwise.</returns>
    bool IsPackageInstalled(Project project, string id);

    /// <summary>
    /// Checks if a NuGet package with the specified Id and version is installed in the specified project.
    /// </summary>
    /// <param name="project">The project to check for NuGet package.</param>
    /// <param name="id">The id of the package to check.</param>
    /// <param name="version">The version of the package to check.</param>
    /// <returns><c>true</c> if the package is install. <c>false</c> otherwise.</returns>
    bool IsPackageInstalled(Project project, string id, SemanticVersion version);

    /// <summary>
    /// Checks if a NuGet package with the specified Id and version is installed in the specified project.
    /// </summary>
    /// <param name="project">The project to check for NuGet package.</param>
    /// <param name="id">The id of the package to check.</param>
    /// <param name="versionString">The version of the package to check.</param>
    /// <returns><c>true</c> if the package is install. <c>false</c> otherwise.</returns>
    /// <remarks>
    /// The reason this method is named IsPackageInstalledEx, instead of IsPackageInstalled, is that
    /// when client project compiles against this assembly, the compiler would attempt to bind against
    /// the other overload which accepts SemanticVersion and would require client project to reference NuGet.Core.
    /// </remarks>
    bool IsPackageInstalledEx(Project project, string id, string versionString);

    /// <summary>
    /// Get the list of NuGet packages installed in the specified project.
    /// </summary>
    /// <param name="project">The project to get NuGet packages from.</param>
    IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
}
```

## <a name="ivspackagemanagerprovider-interface"></a><span data-ttu-id="9d231-132">Interfejs IVsPackageManagerProvider</span><span class="sxs-lookup"><span data-stu-id="9d231-132">IVsPackageManagerProvider interface</span></span>

```cs
public interface IVsPackageManagerProvider
{
    /// <summary>
    /// Localized display package manager name.
    /// </summary>
    string PackageManagerName { get; }

    /// <summary>
    /// Package manager unique id.
    /// </summary>
    string PackageManagerId { get; }

    /// <summary>
    /// The tool tip description for the package
    /// </summary>
    string Description { get; }

    /// <summary>
    /// Check if a recommendation should be surfaced for an alternate package manager.
    /// This code should not rely on slow network calls, and should return rapidly.
    /// </summary>
    /// <param name="packageId">Current package id</param>
    /// <param name="projectName">Unique project name for finding the project through VS dte</param>
    /// <param name="token">Cancellation Token</param>
    /// <returns>return true if need to direct to integrated package manager for this package</returns>
    Task<bool> CheckForPackageAsync(string packageId, string projectName, CancellationToken token);

    /// <summary>
    /// This Action should take the user to the other package manager.
    /// </summary>
    /// <param name="packageId">Current package id</param>
    /// <param name="projectName">Unique project name for finding the project through VS dte</param>
    void GoToPackage(string packageId, string projectName);
}
```

## <a name="ivspackagemetadata-interface"></a><span data-ttu-id="9d231-133">Interfejs IVsPackageMetadata</span><span class="sxs-lookup"><span data-stu-id="9d231-133">IVsPackageMetadata interface</span></span>

```cs
public interface IVsPackageMetadata
{
    /// <summary>
    /// Id of the package.
    /// </summary>
    string Id { get; }

    /// <summary>
    /// Version of the package.
    /// </summary>
    /// <remarks>
    /// Do not use this property because it will require referencing NuGet.Core.dll assembly. Use the VersionString
    /// property instead.
    /// </remarks>
    [Obsolete("Do not use this property because it will require referencing NuGet.Core.dll assembly. Use the VersionString property instead.")]
    NuGet.SemanticVersion Version { get; }

    /// <summary>
    /// Title of the package.
    /// </summary>
    string Title { get; }

    /// <summary>
    /// Description of the package.
    /// </summary>
    string Description { get; }

    /// <summary>
    /// The authors of the package.
    /// </summary>
    IEnumerable<string> Authors { get; }

    /// <summary>
    /// The location where the package is installed on disk.
    /// </summary>
    string InstallPath { get; }

    // IMPORTANT: This property must come LAST, because it was added in 2.5. Having it declared
    // LAST will avoid breaking components that compiled against earlier versions which doesn't
    // have this property.
    /// <summary>
    /// The version of the package.
    /// </summary>
    /// <remarks>
    /// Use this property instead of the Version property becase with the type string,
    /// it doesn't require referencing NuGet.Core.dll assembly.
    /// </remarks>
    string VersionString { get; }
}
```

## <a name="ivspackageprojectmetadata-interface"></a><span data-ttu-id="9d231-134">Interfejs IVsPackageProjectMetadata</span><span class="sxs-lookup"><span data-stu-id="9d231-134">IVsPackageProjectMetadata interface</span></span>

```cs
public interface IVsPackageProjectMetadata
{
    /// <summary>
    /// Unique batch id for batch start/end events of the project.
    /// </summary>
    string BatchId { get; }

    /// <summary>
    /// Name of the project.
    /// </summary>
    string ProjectName { get; }
}
```

## <a name="ivspackagerestorer-interface"></a><span data-ttu-id="9d231-135">Interfejs IVsPackageRestorer</span><span class="sxs-lookup"><span data-stu-id="9d231-135">IVsPackageRestorer interface</span></span>

```cs
public interface IVsPackageRestorer
{
    /// <summary>
    /// Returns a value indicating whether the user consent to download NuGet packages
    /// has been granted.
    /// </summary>
    /// <returns>true if the user consent has been granted; otherwise, false.</returns>
    bool IsUserConsentGranted();

    /// <summary>
    /// Restores NuGet packages installed in the given project within the current solution.
    /// </summary>
    /// <param name="project">The project whose NuGet packages to restore.</param>
    void RestorePackages(Project project);
}
```

## <a name="ivspackagesourceprovider-interface"></a><span data-ttu-id="9d231-136">Interfejs IVsPackageSourceProvider</span><span class="sxs-lookup"><span data-stu-id="9d231-136">IVsPackageSourceProvider interface</span></span>

```cs
public interface IVsPackageSourceProvider
{
    /// <summary>
    /// Provides the list of package sources.
    /// </summary>
    /// <param name="includeUnOfficial">Unofficial sources will be included in the results</param>
    /// <param name="includeDisabled">Disabled sources will be included in the results</param>
    /// <returns>Key: source name Value: source URI</returns>
    IEnumerable<KeyValuePair<string, string>> GetSources(bool includeUnOfficial, bool includeDisabled);

    /// <summary>
    /// Raised when sources are added, removed, disabled, or modified.
    /// </summary>
    event EventHandler SourcesChanged;
}
```

## <a name="ivspackageuninstaller-interface"></a><span data-ttu-id="9d231-137">Interfejs IVsPackageUninstaller</span><span class="sxs-lookup"><span data-stu-id="9d231-137">IVsPackageUninstaller interface</span></span>

```cs
public interface IVsPackageUninstaller
{
    /// <summary>
    /// Uninstall the specified package from a project and specify whether to uninstall its dependency packages
    /// too.
    /// </summary>
    /// <param name="project">The project from which the package is uninstalled.</param>
    /// <param name="packageId">The package to be uninstalled</param>
    /// <param name="removeDependencies">
    /// A boolean to indicate whether the dependency packages should be
    /// uninstalled too.
    /// </param>
    void UninstallPackage(Project project, string packageId, bool removeDependencies);
}
```

## <a name="ivstemplatewizard-interface"></a><span data-ttu-id="9d231-138">Interfejs IVsTemplateWizard</span><span class="sxs-lookup"><span data-stu-id="9d231-138">IVsTemplateWizard interface</span></span>

```cs
/// <summary>
/// Defines the logic for a template wizard extension.
/// </summary>

public interface IVsTemplateWizard : IWizard
{
}
```
