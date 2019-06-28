---
title: polecenia NuGet interfejsu wiersza polecenia platformy DotNet
description: Krótkie odniesienie do polecenia związane z NuGet, za pomocą interfejsu wiersza polecenia dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: cc99b327c0edb4aeb573dfa8c2f9b9dba7b8cc38
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426001"
---
# <a name="dotnet-cli-commands"></a>polecenia interfejsu wiersza polecenia platformy DotNet

`dotnet` Interfejsu wiersza polecenia (CLI), która jest uruchamiana w Windows, Mac OS X i Linux, oferuje pewną liczbę podstawowych poleceń, takich jak instalowanie, przywracania i publikowania pakietów. Jeśli dotnet odpowiada potrzebom użytkownika, nie jest konieczne użycie `nuget.exe`.

Przykłady użycia tych poleceń, aby korzystanie z pakietów, zobacz [instalowania i zarządzania pakietami przy użyciu interfejsu wiersza polecenia platformy dotnet](../consume-packages/install-use-packages-dotnet-cli.md). Przykłady korzystania z tych poleceń do tworzenia pakietów, zobacz [tworzenie i publikowanie pakietu przy użyciu interfejsu wiersza polecenia platformy dotnet]... / quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Pełne polecenie odwołania na `dotnet` interfejsu wiersza polecenia, zobacz [narzędzi interfejsu wiersza polecenia (CLI) platformy .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Użycie pakietu

- [**polecenia DotNet Dodaj pakiet**](/dotnet/core/tools/dotnet-add-package): Dodaje odwołania do pakietu do pliku projektu, a następnie uruchamia `dotnet restore` do zainstalowania pakietu.
- [**polecenia DotNet, usuń pakiet**](/dotnet/core/tools/dotnet-remove-package): Usuwa odwołanie do pakietu z pliku projektu.
- [**DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Przywraca zależności i narzędzia do projektu. Począwszy od NuGet 4.0, spowoduje to uruchomienie tego samego kodu jako `nuget restore`.
- [**Zmienne lokalne nuget DotNet**](/dotnet/core/tools/dotnet-nuget-locals): Wyświetla lokalizacje *globalnymi pakietami*, *pamięci podręcznej http*, i *temp* foldery i czyści zawartość tych folderów.

## <a name="package-creation"></a>Tworzenie pakietu

- [**pakietu DotNet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Pakiety kodu do pakietu NuGet. Począwszy od NuGet 4.0, spowoduje to uruchomienie tego samego kodu jako `nuget pack`.
- [**wypychane nuget DotNet**](/dotnet/core/tools/dotnet-nuget-push): Wypycha pakietu do serwera i publikuje go dotyczy nuget.org, Visual Studio Team Services i innych firm serwery NuGet.
- [**Usuń DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): Usuwa lub unlists pakietu z hosta dotyczy nuget.org, Visual Studio Team Services i innych firm serwery NuGet.
