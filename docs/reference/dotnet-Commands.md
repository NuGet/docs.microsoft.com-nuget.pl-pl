---
title: poleceń NuGet interfejsu wiersza polecenia dotnet
description: Krótkie odwołanie do poleceń związanych z pakietem NuGet przy użyciu interfejsu wiersza polecenia dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328250"
---
# <a name="dotnet-cli-commands"></a>poleceń interfejsu wiersza polecenia dotnet

Interfejs `dotnet` wiersza polecenia (CLI), który działa w systemach Windows, Mac OS X i Linux, zawiera szereg istotnych poleceń, takich jak instalowanie, przywracanie i publikowanie pakietów. Jeśli dotnet spełnia Twoje wymagania, nie trzeba używać `nuget.exe`.

Aby zapoznać się z przykładami dotyczącymi używania tych poleceń, zobacz [Instalowanie pakietów i zarządzanie nimi za pomocą interfejsu wiersza polecenia dotnet](../consume-packages/install-use-packages-dotnet-cli.md). Przykłady użycia tych poleceń do tworzenia pakietów można znaleźć w temacie [Tworzenie i publikowanie pakietu przy użyciu interfejsu wiersza polecenia dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Aby zapoznać się z kompletnym `dotnet` poleceniem dotyczącym interfejsu wiersza polecenia, zobacz [.NET Core Command Line Interface (CLI) Tools](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Użycie pakietu

- [**Dodaj pakiet dotnet**](/dotnet/core/tools/dotnet-add-package): Dodaje odwołanie do pakietu do pliku projektu, a następnie uruchamia `dotnet restore` polecenie, aby zainstalować pakiet.
- [**pakiet usuwania dotnet**](/dotnet/core/tools/dotnet-remove-package): Usuwa odwołanie do pakietu z pliku projektu.
- [**dotnet Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Przywraca zależności i narzędzia projektu. W przypadku programu NuGet 4,0 ten sam kod jest uruchamiany co `nuget restore`.
- [**Ustawienia regionalne NuGet dotnet**](/dotnet/core/tools/dotnet-nuget-locals): Wyświetla listę lokalizacji *globalnych pakietów*, *pamięci podręcznej protokołu HTTP*i folderów *tymczasowych* i czyści zawartość tych folderów.
- [**Nowy nugetconfig dotnet**](/dotnet/core/tools/dotnet-new): Tworzy plik [`nuget.config`](../reference/nuget-config-file.md) służący do konfigurowania zachowania narzędzia NuGet.

## <a name="package-creation"></a>Tworzenie pakietu

- [**pakiet dotnet Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Pakuje kod do pakietu NuGet.
- [**wypychanie NuGet narzędzia dotnet**](/dotnet/core/tools/dotnet-nuget-push): Publikuje pakiet na serwerze NuGet. Dotyczy nuget.org, Azure Artifacts i [serwerów NuGet innych](../hosting-packages/overview.md)firm.
- [**usuwanie NuGet narzędzia dotnet**](/dotnet/core/tools/dotnet-nuget-delete): Usuwa pakiet z serwera NuGet lub go wystawia. Dotyczy nuget.org, Azure Artifacts i [serwerów NuGet innych](../hosting-packages/overview.md)firm.
