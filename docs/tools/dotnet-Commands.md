---
title: polecenia NuGet DotNet
description: Krótkie odniesienie do polecenia związane z NuGet, za pomocą interfejsu wiersza polecenia dotnet.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: 88e058be674ecddc500665bfa3517f19acde0cd7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546319"
---
# <a name="dotnet-commands"></a>polecenia DotNet

`dotnet` Interfejsu wiersza polecenia, który jest uruchamiany w Windows, Mac OS X i Linux, oferuje pewną liczbę poleceń nuget.exe podstawowe, zgodnie z poniższymi. Jeśli dotnet odpowiada potrzebom użytkownika, nie jest konieczne użycie `nuget.exe`.

Aby uzyskać pełne informacje na temat `dotnet`, zobacz [narzędzi interfejsu wiersza polecenia (CLI) platformy .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Użycie pakietu

- [**polecenia DotNet Dodaj pakiet**](/dotnet/core/tools/dotnet-add-package): Dodaje odwołanie do pakietu do pliku projektu, a następnie uruchamia `dotnet restore` do zainstalowania pakietu.
- [**polecenia DotNet, usuń pakiet**](/dotnet/core/tools/dotnet-remove-package): Usuwa odwołanie do pakietu z pliku projektu.
- [**DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): przywraca zależności i narzędzia do projektu. Począwszy od NuGet 4.0, spowoduje to uruchomienie tego samego kodu jako `nuget restore`.
- [**Zmienne lokalne nuget DotNet**](/dotnet/core/tools/dotnet-nuget-locals): Wyświetla lokalizacje *globalnymi pakietami*, *pamięci podręcznej http*, i *temp* folderów i czyści zawartość te foldery.

## <a name="package-creation"></a>Tworzenie pakietu

- [**pakietu DotNet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): pakiety kodu do pakietu NuGet. Począwszy od NuGet 4.0, spowoduje to uruchomienie tego samego kodu jako `nuget pack`.
- [**wypychane nuget DotNet**](/dotnet/core/tools/dotnet-nuget-push): wypychanie pakietu do serwera i publikuje go dotyczy nuget.org, Visual Studio Team Services i innych firm serwery NuGet.
- [**Usuń DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): usuwa lub unlists pakietu z hosta dotyczy nuget.org, Visual Studio Team Services i innych firm serwery NuGet.
