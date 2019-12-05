---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825172"
---
Użyj [dotnet Restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) polecenie, które przywraca pakiety wymienione w pliku projektu (zobacz [PackageReference](../../consume-packages/package-references-in-project-files.md)). W przypadku platformy .NET Core 2,0 i nowszych przywracanie jest wykonywane automatycznie przy użyciu `dotnet build` i `dotnet run`. W przypadku programu NuGet 4,0 ten sam kod jest uruchamiany co `nuget restore`.

Podobnie jak w przypadku innych poleceń interfejsu wiersza polecenia `dotnet`, najpierw Otwórz wiersz i przejdź do katalogu, który zawiera plik projektu.

Aby przywrócić pakiet przy użyciu `dotnet restore`:

```dotnetcli
dotnet restore 
```