---
title: Obsługa długiej ścieżki interfejsu wiersza polecenia NuGet
description: Informacje o pomocy technicznej dotyczącej długiej ścieżki nuget.exe
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 1143da911c80125a9d60e4b98798b11871e9988a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238195"
---
# <a name="long-path-support-nuget-cli"></a>Obsługa długich ścieżek (interfejs wiersza polecenia NuGet)

**Dotyczy:** wszystkie &bullet; **obsługiwane wersje:** 4.8 +

NuGet.exe 4,8 i nowsze obsługują długie ścieżki dla plików i katalogów dla scenariuszy takich jak pakowanie, przywracanie, Instalowanie i większość innych scenariuszy, które wymagają ścieżek plików.

## <a name="required-operating-system"></a>Wymagany system operacyjny

-   Windows 10 (wersja 1607 lub nowsza)
-   Windows 10 (wydanie z lipca 2015 lub wersja 1511) w przypadku uaktualnienia .NET Framework do wersji 4.6.2 lub nowszej.
-   Windows Server 2016 (wszystkie wersje)

## <a name="enable-win32-long-paths-group-policy"></a>Włącz "długie ścieżki Win32" zasady grupy

Należy włączyć obsługę długich ścieżek w tych systemach przez ustawienie zasad grupy.

Kroki:
1. Uruchom **zasady grupy Edytor** -wpisz "Edytuj zasady grupy" na Start paska wyszukiwania lub uruchom polecenie "gpedit. msc" z polecenia Run (Windows-R).
2. W **Edytor lokalnych zasad grupy** Włącz ustawienie "zasady komputera lokalnego/Konfiguracja komputera/Szablony administracyjne/wszystkie ustawienia/Włącz długie ścieżki Win32".

![Zasady dotyczące długiej ścieżki](media/LongPathPolicy.png)


> [!Note]
> Włączanie obsługi długich ścieżek przez inne narzędzia NuGet
>
> -   Interfejs wiersza polecenia dotnet obsługuje długie ścieżki niezależnie od systemu operacyjnego lub wersji.
> -   Program Visual Studio lub nie `msbuild -t:restore` obsługuje jeszcze długich ścieżek.
> -   Oprogramowanie, które korzysta z bibliotek NuGet do wykonywania przywracania i innych poleceń, będzie obsługiwać długie ścieżki w tych samych systemach, w których NuGet.exe działa, jeśli również zostały ustawione `longPathAware` w manifeście systemu Windows i skonfigurować `UseLegacyPathHandling` do `false` za pomocą App.Config [Zobacz więcej informacji](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)