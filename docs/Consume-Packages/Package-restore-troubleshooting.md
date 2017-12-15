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
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a>Rozwiązywanie problemów z błędami przywracania pakietu w programie Visual Studio

> [!Note]
> Ta strona dotyczy przede wszystkim typowe błędy podczas przywracania pakietów w Visual Studio i kroki, aby je rozwiązać. Przywrócić pakietów, jak to zrobić, zobacz [Przywracanie pakietu](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).

Domyślnie wówczas skompilowanie projektu w programie Visual Studio automatycznie przywraca pakietów NuGet, do którego odwołuje się projekt. Jednak kompilacji zakończy się niepowodzeniem po wyłączeniu Przywracanie pakietu w **Narzędzia > Opcje > Menedżera pakietów NuGet > Przywracanie pakietów** ustawienia i wymaganych pakietów nie są dostępne na komputerze. W takich przypadkach mogą zostać wyświetlone następujące błędy:

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

Aby włączyć Przywracanie pakietu, otwórz **Narzędzia > Opcje > Menedżera pakietów NuGet** i wybierz polecenie Opcje **Zezwalaj narzędziu NuGet na pobieranie brakujących pakietów** i **automatycznie czy nie brakuje pakietów podczas kompilacji w programie Visual Studio**:

![Włącz Przywracanie pakietu NuGet w narzędzia/Opcje](../Consume-Packages/media/restore-01-autorestoreoptions.png)

