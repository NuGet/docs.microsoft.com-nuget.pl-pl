---
title: "Rozwiązywanie problemów z pakietu NuGet przywracania w programie Visual Studio | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: b70326a0-5bfc-4b7c-881d-7a7d5ebeeed5
description: "Opis wspólnej NuGet Przywracanie błędy w Visual Studio i sposoby ich rozwiązywania."
keywords: "Przywracanie pakietu NuGet, przywracanie pakietów, rozwiązywania problemów, rozwiązywanie problemów"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c23a9ed2b7cffbf904018a089ccde000adaa517f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a><span data-ttu-id="555a5-104">Rozwiązywanie problemów z błędami przywracania pakietu w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="555a5-104">Troubleshooting package restore errors in Visual Studio</span></span>

> [!Note]
> <span data-ttu-id="555a5-105">Ta strona dotyczy przede wszystkim typowe błędy podczas przywracania pakietów w Visual Studio i kroki, aby je rozwiązać.</span><span class="sxs-lookup"><span data-stu-id="555a5-105">This page focuses on common errors when restoring packages in Visual Studio and steps to resolve them.</span></span> <span data-ttu-id="555a5-106">Przywrócić pakietów, jak to zrobić, zobacz [Przywracanie pakietu](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="555a5-106">For how-to restore packages, see [Package restore](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="555a5-107">Domyślnie wówczas skompilowanie projektu w programie Visual Studio automatycznie przywraca pakietów NuGet, do którego odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="555a5-107">By default, building a project in Visual Studio automatically restores NuGet packages referenced in the project.</span></span> <span data-ttu-id="555a5-108">Jednak kompilacji zakończy się niepowodzeniem po wyłączeniu Przywracanie pakietu w **Narzędzia > Opcje > Menedżera pakietów NuGet > Przywracanie pakietów** ustawienia i wymaganych pakietów nie są dostępne na komputerze.</span><span class="sxs-lookup"><span data-stu-id="555a5-108">However, builds will fail if package restore is disabled in the **Tools > Options > NuGet Package Manager > Package Restore** settings and the necessary packages are not available on your computer.</span></span> <span data-ttu-id="555a5-109">W takich przypadkach mogą zostać wyświetlone następujące błędy:</span><span class="sxs-lookup"><span data-stu-id="555a5-109">In these cases you may see the following errors:</span></span>

```
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

```
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name} 
```

<span data-ttu-id="555a5-110">Aby włączyć Przywracanie pakietu, otwórz **Narzędzia > Opcje > Menedżera pakietów NuGet** i wybierz polecenie Opcje **Zezwalaj narzędziu NuGet na pobieranie brakujących pakietów** i **automatycznie czy nie brakuje pakietów podczas kompilacji w programie Visual Studio**:</span><span class="sxs-lookup"><span data-stu-id="555a5-110">To enable package restore, open **Tools > Options > NuGet Package Manager** and select the options for **Allow NuGet to download missing packages** and **Automatically check for missing packages during build in Visual Studio**:</span></span>

![Włącz Przywracanie pakietu NuGet w narzędzia/Opcje](../Consume-Packages/media/restore-01-autorestoreoptions.png)

