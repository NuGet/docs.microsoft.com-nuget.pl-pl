---
title: polecenia NuGet DotNet
description: Krótkie odwołanie poleceń związanych z NuGet przy użyciu interfejsu wiersza polecenia platformy dotnet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: fe49274af339c987d5e090c99edd78f62f59ce47
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/27/2018
---
# <a name="dotnet-commands"></a>polecenia DotNet

`dotnet` Interfejsu wiersza polecenia, co jest uruchomiony na systemu Windows, Mac OS X i Linux, zawiera pewną liczbę poleceń podstawowych nuget.exe wymienione poniżej. Jeśli dotnet odpowiada potrzebom użytkownika, nie jest konieczne użycie `nuget.exe`.

Aby uzyskać pełne informacje na `dotnet`, zobacz [narzędzi interfejsu wiersza polecenia (CLI) platformy .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Użycie pakietu

- [**DotNet Dodaj pakiet**](/dotnet/core/tools/dotnet-add-package): Dodaje odwołanie pakietu do pliku projektu, a następnie uruchamia `dotnet restore` do zainstalowania pakietu.
- [**DotNet usunąć pakiet**](/dotnet/core/tools/dotnet-remove-package): Usuwa odwołanie do pakietu z pliku projektu.
- [**Przywracanie DotNet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): przywraca zależności i narzędzia do projektu. Począwszy od NuGet 4.0 uruchomienie tego samego kodu jako `nuget restore`.
- [**Zmienne lokalne nuget DotNet**](/dotnet/core/tools/dotnet-nuget-locals): Wyświetla lokalizacje *globalne pakiety*, *pamięci podręcznej http*, i *temp* folderów i czyści zawartość te foldery.

## <a name="package-creation"></a>Tworzenie pakietu

- [**Pakiet DotNet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): pakiety kodu do pakietu NuGet. Począwszy od NuGet 4.0 uruchomienie tego samego kodu jako `nuget pack`.
- [**wypychania nuget DotNet**](/dotnet/core/tools/dotnet-nuget-push): wypchnięcia pakietu na serwerze i publikuje ją dotyczy nuget.org, Visual Studio Team Services i serwery NuGet innych firm.
- [**Usuń DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): usuwa lub unlists pakietu z hosta i mające zastosowanie do nuget.org, Visual Studio Team Services i serwery NuGet innych firm.
