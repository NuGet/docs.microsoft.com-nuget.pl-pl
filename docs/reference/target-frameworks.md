---
title: Dokumentacja platform docelowych dla programu NuGet
description: Platforma docelowa programu NuGet odwołuje się do identyfikowania i izolowania składników zależnych od struktury pakietu.
author: karann-msft
ms.author: karann
ms.date: 12/11/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: caa1509fd996c54f7de17e86559ea62ef67f749f
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380480"
---
# <a name="target-frameworks"></a>Platformy docelowe

Pakiet NuGet używa odwołań platformy docelowej w różnych miejscach, aby identyfikować i izolować składniki zależne od platformy:

- [plik projektu](../create-packages/multiple-target-frameworks-project-file.md): dla projektów w stylu zestawu SDK element *. csproj* zawiera odwołania do platformy docelowej.
- [manifest. nuspec](../reference/nuspec.md): pakiet może wskazywać różne pakiety do uwzględnienia w projekcie w zależności od platformy docelowej projektu.
- [Nazwa folderu. nupkg](../create-packages/creating-a-package.md#from-a-convention-based-working-directory): foldery w folderze `lib` pakietu mogą być nazwane zgodnie z platformą docelową, z których każdy zawiera biblioteki DLL i inną zawartość odpowiednią dla tej struktury.
- [Packages. config](../reference/packages-config.md): atrybut `targetframework` zależności określa wariant pakietu do zainstalowania.

> [!Note]
> Kod źródłowy klienta NuGet, który oblicza poniższe tabele, znajduje się w następujących lokalizacjach:
> - Obsługiwane nazwy struktur: [FrameworkConstants.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/FrameworkConstants.cs)
> - Pierwszeństwo i mapowanie struktury: [DefaultFrameworkMappings.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/DefaultFrameworkMappings.cs)

## <a name="supported-frameworks"></a>Obsługiwane struktury

Struktura jest zwykle przywoływana przez krótką moniker struktury docelowej lub TFM. W .NET Standard jest to również uogólnione *TxM* , aby umożliwić pojedyncze odwołanie do wielu struktur.

Klienci NuGet obsługują struktury w poniższej tabeli. Równoważne są wyświetlane w nawiasach kwadratowych []. Należy pamiętać, że niektóre narzędzia, takie jak `dotnet`, mogą używać odmian kanonicznych TFMs w niektórych plikach. Na przykład `dotnet pack` używa `.NETCoreApp2.0` w pliku `.nuspec`, a nie `netcoreapp2.0`. Różne narzędzia klienta NuGet odpowiednio obsługują te odmiany, ale w przypadku bezpośredniej edycji plików należy zawsze używać kanonicznej TFMs.

| Nazwa | Jednostek | TFMs/TxMs |
| ------------- | ------------ | --------- |
|.NET Framework | Waga | net11 |
| | | net20 |
| | | net35 |
| | | net40 |
| | | net403 |
| | | net45 |
| | | net451 |
| | | net452 |
| | | net46 |
| | | net461 |
| | | net462 |
| | | net47 |
| | | net471 |
| | | net472 |
| | | net48 |
|Microsoft Store (Sklep Windows) | netcore | Rdzeń [netcore45] |
| | | netcore45 [win, Win8] |
| | | netcore451 [Win81] |
| | | netcore50 |
|Platforma .NET | netmf | netmf |
|Windows | kupione | win [Win8, netcore45] |
| | | Win8 [netcore45, win] |
| | | Win81 [netcore451] |
| | | Win10 (nieobsługiwane przez platformę Windows 10) |
Silverlight | SL | sl4 |
| | | sl5 |
Windows Phone (SL) | dokumenty | WP [WP7] |
| | | wp7 |
| | | wp75 |
| | | WP8 |
| | | wp81 |
Windows Phone (platformy UWP) | | wpa81 |
Platforma uniwersalna systemu Windows | UAP | UAP [UAP 10.0] |
| | | UAP 10.0 |
| | | UAP 10.0. xxxxx (gdzie 10.0. xxxxx to minimalna wersja platformy docelowej zużywanej aplikacji) |
.NET Standard | netstandard | Standard 1.0 |
| | | Standard 1.1 |
| | | Standard 1.2 |
| | | Standard 1.3 |
| | | Standardowa 1.4 |
| | | Standard 1.5 |
| | | Standard 1.6 |
| | | Standard 2.0 |
Aplikacja .NET Core | netcoreapp | netcoreapp 1.0 |
| | | netcoreapp 1.1 |
| | | netcoreapp 2.0 |
| | | netcoreapp 2.1 |
| | | netcoreapp 2.2 |
| | | netcoreapp 3.0 |
Tizen | tizen | tizen3 |
| | | tizen4 |

## <a name="deprecated-frameworks"></a>Przestarzałe struktury

Następujące struktury są przestarzałe. Pakiety ukierunkowane na te struktury powinny być migrowane do wskazanych elementów zastępczych.

| Przestarzałe środowisko | Zastępc
| --- | ---
| aspnet50 | netcoreapp |
| aspnetcore50 |
| dnxcore50 |
| środowiska DNX |
| dnx45 |
| dnx451 |
| dnx452 |
| dotnet | netstandard |
| dotnet50 | |
| dotnet51 | |
| dotnet52 | |
| dotnet53 | |
| dotnet54 | |
| dotnet55 | |
| dotnet56 | |
| środowiska | kupione |

## <a name="precedence"></a>Pierwszeństwo

Niektóre struktury są powiązane z i zgodne ze sobą, ale niekoniecznie są równoważne:

| Framework | Może używać |
| -- | --- |
| UAP (platforma uniwersalna systemu Windows) | Win81 |
| | wpa81 |
| | netcore50 |
| win (Microsoft Store) | środowiska |
| | |

## <a name="net-standard"></a>Standard .NET

[.NET Standard](/dotnet/standard/net-standard) upraszcza odwołania między strukturami zgodnymi z binarnym, umożliwiając pojedynczej platformie docelowej odwołujące się do kombinacji innych. (Aby uzyskać ogólne, zobacz [.NET](/dotnet/articles/standard/index).)

[Narzędzie do pobierania najbliższej struktury programu NuGet](https://aka.ms/s2m3th) symuluje, co używa NuGet, aby wybrać jedną strukturę spośród wielu dostępnych zasobów platformy w pakiecie w oparciu o strukturę projektu.

Seria `dotnet` monikerów powinna być używana w programie NuGet 3,3 i starszych wersjach. Składnia monikera `netstandard` powinna być używana w wersji 3.4 i nowszych.

## <a name="portable-class-libraries"></a>Przenośne biblioteki klas

> [!Warning]
> **PCLs nie są zalecane**. Chociaż PCLs są obsługiwane, autorzy pakietów powinni obsługiwać standard. .NET Platform Standard to ewolucja PCLs i reprezentuje binarny port na wielu platformach przy użyciu jednego monikera, który nie jest powiązany z biblioteką statyczną, taką jak *Portable-a + b +* krótkie monikery.

Aby zdefiniować platformę docelową, która odwołuje się do wielu struktur obiektów podrzędnych-Target, użyj słowa kluczowego `portable` użytego do prefiksu listy struktur, do których istnieją odwołania. Unikaj sztucznego uwzględniania dodatkowych platform, które nie są bezpośrednio kompilowane, ponieważ może to prowadzić do niezamierzonych efektów ubocznych w tych strukturach.

Dodatkowe struktury zdefiniowane przez strony trzecie zapewniają zgodność z innymi środowiskami, które są dostępne w ten sposób. Ponadto istnieją skrócone numery profilów, które są dostępne w odniesieniu do tych kombinacji powiązanych struktur jako `Profile#`, ale nie jest to zalecane rozwiązanie do używania tych liczb, ponieważ zmniejsza czytelność folderów i `.nuspec`.

| Profilu # | Struktury | Pełna nazwa | .NET Standard |
 --- | --- | --- | ---
 Profile2 | . NETFramework 4,0 | przenośne-net40 + Win8 + SL4 + WP7 |
 | | System Windows 8,0 | |
 | | Program Silverlight 4,0 |
 | | WindowsPhone 7,0|
 Profile3 | . NETFramework 4,0 | przenośne-net40 + SL4
 | | Program Silverlight 4,0 |
 Profile4 | . NETFramework 4,5 | przenośne-net45 + SL4 + Win8 + WP7
 | | Program Silverlight 4,0 |
 | | System Windows 8,0 |
 | | WindowsPhone 7,0 |
 Profile5 | . NETFramework 4,0 | przenośne-net40 + Win8
 | | System Windows 8,0 |
 Profile6 | . NETFramework 4.0.3 | przenośne-net403 + Win8
 | | System Windows 8,0 |
 Profile7 | . NETFramework 4,5 | przenośne-net45 + Win8 | Standard 1.1
 | | System Windows 8,0 |
 Profile14 | . NETFramework 4,0 | przenośne-net40 + SL5
 | | Program Silverlight 5,0 |
 Profile18 | . NETFramework 4.0.3 | przenośne-net403 + SL4
 | | Program Silverlight 4,0 |
 Profile19 | . NETFramework 4.0.3 | przenośne-net403 + SL5
 | | Program Silverlight 5,0 |
 Profile23 | . NETFramework 4,5 | przenośne-net45 + SL4
 | | Program Silverlight 4,0 |
 Profile24 | . NETFramework 4,5 | przenośne-net45 + SL5
 | | Program Silverlight 5,0 |
 Profile31 | Windows 8.1 | przenośne-Win81 + WP81 | Standard 1.0
 | | WindowsPhone 8,1 (SL) |
 Profile32 | Windows 8.1 | przenośne-Win81 + wpa81 | Standard 1.2
 | | WindowsPhone 8,1 (platformy UWP) |
 Profile36 | . NETFramework 4,0 | przenośne-net40 + SL4 + Win8 + WP8
 | | Program Silverlight 4,0 |
 | | System Windows 8,0 |
 | | WindowsPhone 8,0 (SL) |
 Profile37 | . NETFramework 4,0 | przenośne-net40 + SL5 + Win8
 | | Program Silverlight 5,0 |
 | | System Windows 8,0 |
 Profile41 | . NETFramework 4.0.3 | przenośne-net403 + SL4 + Win8
 | | Program Silverlight 4,0 |
 | | System Windows 8,0 |
 Profile42 | . NETFramework 4.0.3 | przenośne-net403 + SL5 + Win8
 | | Program Silverlight 5,0 |
 | | System Windows 8,0 |
 Profile44 | . NETFramework 4.5.1 | przenośne-net451 + Win81 | Standard 1.2
 | | Windows 8.1 |
 Profile46 | . NETFramework 4,5 | przenośne-net45 + SL4 + Win8
 | | Program Silverlight 4,0 |
 | | System Windows 8,0 |
 Profile47 | . NETFramework 4,5 | przenośne-net45 + SL5 + Win8
 | | Program Silverlight 5,0 |
 | | System Windows 8,0 |
 Profile49 | . NETFramework 4,5 | przenośne-net45 + WP8 | Standard 1.0
 | | WindowsPhone 8,0 (SL) |
 Profile78 | . NETFramework 4,5 | przenośne-net45 + Win8 + WP8 | Standard 1.0
 | | System Windows 8,0 |
 | | WindowsPhone 8,0 (SL) |
 Profile84 | WindowsPhone 8,1 | przenośne-WP81 + wpa81 | Standard 1.0
 | | WindowsPhone 8,1 (platformy UWP) |
 Profile88 | . NETFramework 4,0 | przenośne-net40 + SL4 + Win8 + wp75
 | | Program Silverlight 4,0 |
 | | System Windows 8,0 |
 | | WindowsPhone 7,5 |
 Profile92 | . NETFramework 4,0 | przenośne-net40 + Win8 + wpa81
 | | System Windows 8,0 |
 | | WindowsPhone 8,1 (platformy UWP) |
 Profile95 | . NETFramework 4.0.3 | przenośne-net403 + SL4 + Win8 + WP7
 | | Program Silverlight 4,0 |
 | | System Windows 8,0 |
 | | WindowsPhone 7,0 |
 Profile96 | . NETFramework 4.0.3 | przenośne-net403 + SL4 + Win8 + wp75
 | | Program Silverlight 4,0 |
 | | System Windows 8,0 |
 | | WindowsPhone 7,5 |
 Profile102 | . NETFramework 4.0.3 | przenośne-net403 + Win8 + wpa81
 | | System Windows 8,0 |
 | | WindowsPhone 8,1 (platformy UWP) |
 Profile104 | . NETFramework 4,5 | przenośne-net45 + SL4 + Win8 + wp75
 | | Program Silverlight 4,0 |
 | | System Windows 8,0 |
 | | WindowsPhone 7,5 |
 Profile111 | . NETFramework 4,5 | przenośne-net45 + Win8 + wpa81 | Standard 1.1
 | | System Windows 8,0 |
 | | WindowsPhone 8,1 (platformy UWP) |
 Profile136 | . NETFramework 4,0 | przenośne-net40 + SL5 + Win8 + WP8
 | | Program Silverlight 5,0 |
 | | System Windows 8,0 |
 | | WindowsPhone 8,0 (SL) |
 Profile143 | . NETFramework 4.0.3 | przenośne-net403 + SL4 + Win8 + WP8
 | | Program Silverlight 4,0 |
 | | System Windows 8,0 |
 | | WindowsPhone 8,0 (SL) |
 Profile147 | . NETFramework 4.0.3 | przenośne-net403 + SL5 + Win8 + WP8
 | | Program Silverlight 5,0 |
 | | System Windows 8,0 |
 | | WindowsPhone 8,0 (SL) |
 Profile151 | NETFramework 4.5.1 | przenośne-net451 + Win81 + wpa81 | Standard 1.2
 | | Windows 8.1 |
 | | WindowsPhone 8,1 (platformy UWP) |
 Profile154 | . NETFramework 4,5 | przenośne-net45 + SL4 + Win8 + WP8
 | | Program Silverlight 4,0 |
 | | System Windows 8,0 |
 | | WindowsPhone 8,0 (SL) |
 Profile157 | Windows 8.1 | przenośne-Win81 + WP81 + wpa81 | Standard 1.0
 | | WindowsPhone 8,1 (SL) |
 | | WindowsPhone 8,1 (platformy UWP) |
 Profile158 | . NETFramework 4,5 | przenośne-net45 + SL5 + Win8 + WP8
 | | Program Silverlight 5,0 |
 | | System Windows 8,0 |
 | | WindowsPhone 8,0 (SL) |
 Profile225 | . NETFramework 4,0 | przenośne-net40 + SL5 + Win8 + wpa81
 | | Program Silverlight 5,0 |
 | | System Windows 8,0 |
 | | WindowsPhone 8,1 (platformy UWP) |
 Profile240 | . NETFramework 4.0.3 | przenośne-net403 + SL5 + Win8 + wpa8
 | | Program Silverlight 5,0 |
 | | System Windows 8,0 |
 | | WindowsPhone 8,1 (platformy UWP) |
 Profile255 | . NETFramework 4,5 | przenośne-net45 + SL5 + Win8 + wpa81
 | | Program Silverlight 5,0 |
 | | System Windows 8,0 |
 | | WindowsPhone 8,1 (platformy UWP) |
 Profile259 | . NETFramework 4,5 | przenośne-net45 + Win8 + wpa81 + WP8 | Standard 1.0
 | | System Windows 8,0 |
 | | WindowsPhone 8,1 (platformy UWP) |
 | | WindowsPhone 8,0 (SL) |
 Profile328 | . NETFramework 4,0 | Portable-net40 + SL5 + Win8 + wpa81 + WP8
 | | Program Silverlight 5,0 |
 | | System Windows 8,0 |
 | | WindowsPhone 8,1 (platformy UWP) |
 | | WindowsPhone 8,0 (SL) |
 Profile336 | . NETFramework 4.0.3 | Portable-net403 + SL5 + Win8 + wpa81 + WP8
 | | Program Silverlight 5,0 |
 | | System Windows 8,0 |
 | | WindowsPhone 8,1 (platformy UWP) |
 | | WindowsPhone 8,0 (SL) |
 Profile344 | . NETFramework 4,5 | Portable-net45 + SL5 + Win8 + wpa81 + WP8
 | | Program Silverlight 5,0 |
 | | System Windows 8,0 |
 | | WindowsPhone 8,1 (platformy UWP) |
 | | WindowsPhone 8,0 (SL) |

Ponadto pakiety NuGet ukierunkowane na platformę Xamarin mogą używać dodatkowych struktur zdefiniowanych w programie Xamarin. Zobacz [Tworzenie pakietów NuGet dla platformy Xamarin](https://developer.xamarin.com/guides/cross-platform/advanced/nuget/).

| Nazwa | Opis | .NET Standard |
| --- | --- | ---
| system Android | Obsługa platformy mono dla systemu Android | Standardowa 1.4 |
| MonoTouch | Obsługa platformy mono dla systemu iOS | Standardowa 1.4 |
| platformy monomac | Obsługa platformy mono dla OSX | Standardowa 1.4 |
| xamarinios | Obsługa platformy Xamarin dla systemu iOS | Standardowa 1.4 |
| xamarinmac | Obsługuje program Xamarin dla komputerów Mac | Standardowa 1.4 |
| xamarinpsthree | Obsługa platformy Xamarin w systemie PlayStation 3 | Standardowa 1.4 |
| xamarinpsfour | Obsługa platformy Xamarin w systemie PlayStation 4 | Standardowa 1.4 |
| xamarinpsvita | Obsługa platformy Xamarin na platformie PS Vita | Standardowa 1.4 |
| xamarinwatchos | System operacyjny dla programu Xamarin for Watch | Standardowa 1.4 |
| xamarintvos | System operacyjny Xamarin for TV | Standardowa 1.4 |
| xamarinxboxthreesixty | Platforma Xamarin dla konsoli XBox 360 | Standardowa 1.4 |
| xamarinxboxone | Platforma Xamarin dla konsoli XBox one | Standardowa 1.4 |

> [!Note]
> Stephen wyczyścił narzędzie, które wyświetla listę obsługiwanych PCLs, które można znaleźć w [profilach post, Framework w programie .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html).
