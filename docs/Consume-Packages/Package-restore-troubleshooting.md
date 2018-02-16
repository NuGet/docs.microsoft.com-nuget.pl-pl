---
title: "Rozwiązywanie problemów z pakietu NuGet przywracania w programie Visual Studio | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Opis wspólnej NuGet Przywracanie błędy w Visual Studio i sposoby ich rozwiązywania."
keywords: "Przywracanie pakietu NuGet, przywracanie pakietów, rozwiązywania problemów, rozwiązywanie problemów"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c0993e2585452e3c64da28d14bb1bbe1bea27768
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/14/2018
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a><span data-ttu-id="6340c-104">Rozwiązywanie problemów z błędami przywracania pakietu w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6340c-104">Troubleshooting package restore errors in Visual Studio</span></span>

> [!Note]
> <span data-ttu-id="6340c-105">Ta strona dotyczy przede wszystkim typowe błędy podczas przywracania pakietów w Visual Studio i kroki, aby je rozwiązać.</span><span class="sxs-lookup"><span data-stu-id="6340c-105">This page focuses on common errors when restoring packages in Visual Studio and steps to resolve them.</span></span> <span data-ttu-id="6340c-106">Przywrócić pakietów, jak to zrobić, zobacz [Przywracanie pakietu](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="6340c-106">For how-to restore packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="6340c-107">Domyślnie wówczas skompilowanie projektu w programie Visual Studio automatycznie przywraca pakietów NuGet, do którego odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="6340c-107">By default, building a project in Visual Studio automatically restores NuGet packages referenced in the project.</span></span> <span data-ttu-id="6340c-108">Jednak kompilacji zakończy się niepowodzeniem po wyłączeniu Przywracanie pakietu w **Narzędzia > Opcje > Menedżera pakietów NuGet > Przywracanie pakietów** ustawienia i wymaganych pakietów nie są dostępne na komputerze.</span><span class="sxs-lookup"><span data-stu-id="6340c-108">However, builds will fail if package restore is disabled in the **Tools > Options > NuGet Package Manager > Package Restore** settings and the necessary packages are not available on your computer.</span></span> <span data-ttu-id="6340c-109">W takich przypadkach mogą zostać wyświetlone następujące błędy:</span><span class="sxs-lookup"><span data-stu-id="6340c-109">In these cases you may see the following errors:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name} 
```

<span data-ttu-id="6340c-110">Aby włączyć Przywracanie pakietu, otwórz **Narzędzia > Opcje > Menedżera pakietów NuGet** i wybierz polecenie Opcje **Zezwalaj narzędziu NuGet na pobieranie brakujących pakietów** i **automatycznie czy nie brakuje pakietów podczas kompilacji w programie Visual Studio**:</span><span class="sxs-lookup"><span data-stu-id="6340c-110">To enable package restore, open **Tools > Options > NuGet Package Manager** and select the options for **Allow NuGet to download missing packages** and **Automatically check for missing packages during build in Visual Studio**:</span></span>

![Włącz Przywracanie pakietu NuGet w narzędzia/Opcje](../consume-packages/media/restore-01-autorestoreoptions.png)
