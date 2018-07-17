---
title: Obsługa długich ścieżek interfejs wiersza polecenia NuGet
description: Dokumentacja dotycząca pomocy technicznej z długą ścieżką nuget.exe
author: zhili1208
ms.author: lzhi
manager: rob
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 0119be3fd8fd6c2e06e0135de5e498e0730bb0cc
ms.sourcegitcommit: a76ecc58f41c2c5b3536ff4a3f3fcbdf5258177c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/17/2018
ms.locfileid: "39072746"
---
# <a name="long-path-support-nuget-cli"></a>Obsługa długich ścieżek (interfejs wiersza polecenia NuGet)

**Dotyczy:** wszystkich &bullet; **obsługiwane wersje:** 4.8 +

NuGet.exe pomocy technicznej lub nowszy 4,8 długich ścieżek plików i katalogów w scenariuszach, takich jak pakiet, przywracanie, instalacji i większości scenariuszy, które wymagają ścieżki do plików.

## <a name="required-operating-system"></a>Wymagany System operacyjny

-   Windows 10 (wersja 1607 lub nowszej)
-   Windows 10 (lipiec 2015 r. lub używana wersja 1511) .NET Framework w przypadku uaktualnienia do wersji 4.6.2 lub nowszy.
-   System Windows Server 2016 (wszystkie wersje)

## <a name="enable-win32-long-paths-group-policy"></a>Włączanie zasad grupy "Długich ścieżek systemu Win32"

Należy włączyć obsługę długich ścieżek w tych systemach przez ustawienie zasad grupy.

Kroki:
1. Uruchom **Edytor zasad grupy** — wpisz "Edytuj zasady grupy" na pasku wyszukiwania rozpoczęcia lub uruchomić "gpedit.msc" z polecenia Uruchom (Windows-R).
2. W **Edytora lokalnych zasad grupy**, włącz "lokalnego komputera zasad i komputera Konfiguracja/administracyjne szablony/wszystkich długich ścieżek ustawienia/Włącz Win32".

![Zasady długie ścieżki](media/LongPathPolicy.png)


> [!Note]
> Inne narzędzia NuGet, do obsługi długich ścieżek
>
> -   Interfejsu wiersza polecenia DotNet obsługuje długich ścieżek niezależnie od systemu operacyjnego i wersji.
> -   Visual Studio lub program msbuild /t:restore jeszcze nie obsługuje długich ścieżek.
> -   Oprogramowanie, które korzysta z bibliotek usługi NuGet do wykonania przywracania i innych poleceń będzie obsługiwać długich ścieżek na tych samych systemach NuGet.exe działające w, również ustawić longPathAware w ich systemie windows manifestu i skonfigurować UseLegacyPathHandling na wartość false, za pomocą pliku App.Config [ Zobacz więcej informacji](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

