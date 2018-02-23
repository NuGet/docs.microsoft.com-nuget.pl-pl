---
title: polecenia NuGet dotNet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Krótkie odwołanie poleceń związanych z NuGet przy użyciu interfejsu wiersza polecenia platformy dotnet."
keywords: polecenia NuGet DotNet dotnet, przywracania dotnet, zmienne lokalne nuget dotnet, dotnet nuget wypychania, pakowanie dotnet nuget delete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2851938cd43b35454d8e4ad595fbd93229d4dd72
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/20/2018
---
# <a name="dotnet-commands"></a>polecenia dotNet

`dotnet` Interfejsu wiersza polecenia, co jest uruchomiony na systemu Windows, Mac OS X i Linux, zawiera pewną liczbę poleceń podstawowych nuget.exe wymienione poniżej. Jeśli dotnet odpowiada potrzebom użytkownika, nie jest konieczne użycie `nuget.exe`.

Aby uzyskać pełne informacje na `dotnet`, zobacz [narzędzi interfejsu wiersza polecenia (CLI) platformy .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Użycie pakietu

- [**DotNet Dodaj pakiet**](/dotnet/core/tools/dotnet-add-package): Dodaje odwołanie pakietu do pliku projektu, a następnie uruchamia `dotnet restore` do zainstalowania pakietu.
- [**DotNet usunąć pakiet**](/dotnet/core/tools/dotnet-remove-package): Usuwa odwołanie do pakietu z pliku projektu.
- [**Przywracanie DotNet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): przywraca zależności i narzędzia do projektu. Począwszy od NuGet 4.0 uruchomienie tego samego kodu jako `nuget restore`.
- [**Zmienne lokalne nuget DotNet**](/dotnet/core/tools/dotnet-nuget-locals): usuwa lub wyświetla ich listę zasobów lokalnych NuGet pamięci podręcznej żądania http, tymczasowego pamięci podręcznej i folderu pakietów globalne dla komputera.

## <a name="package-creation"></a>Tworzenie pakietu

- [**Pakiet DotNet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): pakiety kodu do pakietu NuGet. Począwszy od NuGet 4.0 uruchomienie tego samego kodu jako `nuget pack`.
- [**wypychania nuget DotNet**](/dotnet/core/tools/dotnet-nuget-push): wypchnięcia pakietu na serwerze i publikuje ją dotyczy nuget.org, Visual Studio Team Services i serwery NuGet innych firm.
- [**Usuń DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): usuwa lub unlists pakietu z hosta i mające zastosowanie do nuget.org, Visual Studio Team Services i serwery NuGet innych firm.
