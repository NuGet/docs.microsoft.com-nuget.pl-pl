---
title: poleceń NuGet interfejsu wiersza polecenia dotnet
description: Krótkie odwołanie do poleceń związanych z pakietem NuGet przy użyciu interfejsu wiersza polecenia dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 87cb3c8153931a0917338de9f7001406b5e12dfc
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699819"
---
# <a name="dotnet-cli-commands"></a>Polecenia interfejsu wiersza polecenia DotNet

`dotnet`Interfejs wiersza polecenia (CLI), który działa w systemach Windows, Mac OS X i Linux, zawiera szereg istotnych poleceń, takich jak instalowanie, przywracanie i publikowanie pakietów. Jeśli dotnet spełnia Twoje wymagania, nie trzeba używać `nuget.exe` .

Aby zapoznać się z przykładami dotyczącymi używania tych poleceń, zobacz [Instalowanie pakietów i zarządzanie nimi za pomocą interfejsu wiersza polecenia dotnet](../consume-packages/install-use-packages-dotnet-cli.md). Przykłady użycia tych poleceń do tworzenia pakietów można znaleźć w temacie [Tworzenie i publikowanie pakietu przy użyciu interfejsu wiersza polecenia dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Aby zapoznać się z kompletnym poleceniem dotyczącym `dotnet` interfejsu wiersza polecenia, zobacz [.NET Core Command Line Interface (CLI) Tools](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Użycie pakietu

- [**Dodawanie pakietu dotnet**](/dotnet/core/tools/dotnet-add-package): dodaje odwołanie do pakietu do pliku projektu, a następnie uruchamia polecenie, `dotnet restore` Aby zainstalować pakiet.
- [**Usuwanie pakietu dotnet**](/dotnet/core/tools/dotnet-remove-package): usuwa odwołanie do pakietu z pliku projektu.
- [**dotnet Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): przywraca zależności i narzędzia projektu. W przypadku programu NuGet 4,0 ten sam kod jest uruchamiany co `nuget restore` .
- [**lokalne elementy NuGet programu dotnet**](/dotnet/core/tools/dotnet-nuget-locals): zawiera listę lokalizacji *globalnych pakietów*, *pamięci podręcznej protokołu HTTP* i folderów *tymczasowych* , a następnie czyści zawartość tych folderów.
- [**Nowy nugetconfig dotnet**](/dotnet/core/tools/dotnet-new): tworzy plik służący [`nuget.config`](../reference/nuget-config-file.md) do konfigurowania zachowania narzędzia NuGet.

## <a name="package-creation"></a>Tworzenie pakietu

- [**pakiet dotnet Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): pakuje kod do pakietu NuGet.
- [**wypychanie NuGet programu dotnet**](/dotnet/core/tools/dotnet-nuget-push): publikuje pakiet na serwerze NuGet. Dotyczy nuget.org, Azure Artifacts i [serwerów NuGet innych](../hosting-packages/overview.md)firm.
- [**usuwanie NuGet programu dotnet**](/dotnet/core/tools/dotnet-nuget-delete): usuwa pakiet z serwera NuGet lub go wystawia. Dotyczy nuget.org, Azure Artifacts i [serwerów NuGet innych](../hosting-packages/overview.md)firm.
- [**weryfikacja programu dotnet NuGet**](/dotnet/core/tools/dotnet-nuget-verify): weryfikuje podpisany pakiet NuGet.
