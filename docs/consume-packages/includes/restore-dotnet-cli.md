---
ms.openlocfilehash: 9764479d88cc8d87a9f455e64bd46ae8de15055d
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860608"
---
Użyj [dotnet Restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) polecenie, które przywraca pakiety wymienione w pliku projektu (zobacz [PackageReference](../../consume-packages/package-references-in-project-files.md)). W przypadku platformy .NET Core 2,0 i nowszych przywracanie jest wykonywane automatycznie `dotnet build` z `dotnet run`i. W przypadku programu NuGet 4,0 ten sam kod jest uruchamiany co `nuget restore`.

Podobnie jak w przypadku `dotnet` innych poleceń interfejsu wiersza polecenia, najpierw Otwórz wiersz poleceń i przejdź do katalogu, który zawiera plik projektu.

Aby przywrócić pakiet przy użyciu `dotnet restore`:

```cli
dotnet restore 
```