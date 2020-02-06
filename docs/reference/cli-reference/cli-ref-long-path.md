---
title: Obsługa długiej ścieżki interfejsu wiersza polecenia NuGet
description: Dokumentacja obsługi długich ścieżek NuGet. exe
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 9b5a97d963eab7fbbde4aefae1c9b1a8bfcdeb11
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036958"
---
# <a name="long-path-support-nuget-cli"></a>Obsługa długich ścieżek (interfejs wiersza polecenia NuGet)

**Dotyczy:** wszystkie &bullet; **obsługiwane wersje:** 4.8 +

NuGet. exe 4,8 i nowsze obsługują długie ścieżki dla plików i katalogów dla scenariuszy, takich jak pakowanie, przywracanie, Instalowanie i większość innych scenariuszy, które wymagają ścieżek plików.

## <a name="required-operating-system"></a>Wymagany system operacyjny

-   Windows 10 (wersja 1607 lub nowsza)
-   Windows 10 (wydanie z lipca 2015 lub wersja 1511) w przypadku uaktualnienia .NET Framework do wersji 4.6.2 lub nowszej.
-   Windows Server 2016 (wszystkie wersje)

## <a name="enable-win32-long-paths-group-policy"></a>Włącz "długie ścieżki Win32" zasady grupy

Należy włączyć obsługę długich ścieżek w tych systemach przez ustawienie zasad grupy.

Kroki:
1. Uruchom **zasady grupy Edytor** -wpisz "Edytuj zasady grupy" na Start paska wyszukiwania lub uruchom polecenie "gpedit. msc" z polecenia Run (Windows-R).
2. W **Edytor lokalnych zasad grupy**Włącz ustawienie "zasady komputera lokalnego/Konfiguracja komputera/Szablony administracyjne/wszystkie ustawienia/Włącz długie ścieżki Win32".

![Zasady dotyczące długiej ścieżki](media/LongPathPolicy.png)


> [!Note]
> Włączanie obsługi długich ścieżek przez inne narzędzia NuGet
>
> -   Interfejs wiersza polecenia dotnet obsługuje długie ścieżki niezależnie od systemu operacyjnego lub wersji.
> -   Program Visual Studio lub `msbuild -t:restore` nie obsługuje jeszcze długich ścieżek.
> -   Oprogramowanie, które korzysta z bibliotek NuGet do wykonywania przywracania i innych poleceń, będzie obsługiwało długie ścieżki w tych samych systemach, w których działa program NuGet. exe, jeśli również ustawili `longPathAware` w ich manifeście systemu Windows i skonfiguruj `UseLegacyPathHandling` do `false` za pomocą pliku App. config [Zobacz więcej informacji](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

