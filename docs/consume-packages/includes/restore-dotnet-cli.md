---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825172"
---
Użyj polecenia [przywracania dotnet,](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) które przywraca pakiety wymienione w pliku projektu (patrz [PackageReference](../../consume-packages/package-references-in-project-files.md)). Z .NET Core 2.0 i nowsze, przywracanie odbywa się automatycznie z `dotnet build` i `dotnet run`. Od nuget 4.0, to działa `nuget restore`ten sam kod jako .

Podobnie jak `dotnet` w przypadku innych poleceń interfejsu wiersza polecenia, najpierw otwórz wiersz polecenia i przełącz się do katalogu zawierającego plik projektu.

Aby przywrócić pakiet `dotnet restore`przy użyciu:

```dotnetcli
dotnet restore 
```