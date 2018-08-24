---
title: Dokumentacja platformy docelowej dla NuGet
description: Odwołania struktury docelowej NuGet zidentyfikować i izolowania składników zależny od struktury pakietu.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/11/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: c9267945b8055b536cf35911c36a066981ef67b6
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/21/2018
ms.locfileid: "42793605"
---
# <a name="target-frameworks"></a>Platformy docelowe

NuGet używa odwołania struktury docelowej w różnych miejscach specjalnie zidentyfikować i izolowania składników zależny od struktury pakietu:

- [.nuspec manifest](../reference/nuspec.md): pakiet może wskazywać różnych pakietów do uwzględnienia w projekcie, w zależności od platformy docelowej projektu.
- [Nazwa folderu .nupkg](../create-packages/creating-a-package.md#from-a-convention-based-working-directory): foldery wewnątrz pakietu `lib` folder może być nazwany według platformy docelowej, z których każdy zawiera biblioteki dll i innej zawartości, które są odpowiednie dla tej struktury.
- [Packages.config](../reference/packages-config.md): `targetframework` atrybut zależności określa wariant pakiet do zainstalowania.

> [!Note]
> Kod źródłowy NuGet klienta, który oblicza w poniższej tabeli znajduje się w następujących lokalizacjach:
> - Obsługiwane framework nazwy: [FrameworkConstants.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/FrameworkConstants.cs)
> - Pierwszeństwo Framework i mapowania: [DefaultFrameworkMappings.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/DefaultFrameworkMappings.cs)

## <a name="supported-frameworks"></a>Obsługiwane platformy

Struktura zazwyczaj odwołuje się moniker platformy docelowej krótki lub TFM. W programie .NET Standard to samo jest uogólniony, aby *TxM* umożliwia jedno odwołanie do wielu platform.

Klienci NuGet obsługują struktury w poniższej tabeli. Odpowiedniki są wyświetlane w nawiasach kwadratowych []. Należy pamiętać, że niektóre narzędzia, takie jak `dotnet`, mogą używać odmiany canonical krótkich nazw w niektórych plików. Na przykład `dotnet pack` używa `.NETCoreApp2.0` w `.nuspec` pliku zamiast `netcoreapp2.0`. Różne narzędzia klienta programu NuGet prawidłowo obsługiwać te zmiany, ale należy zawsze używać canonical krótkich nazw podczas edytowania plików bezpośrednio.

| Nazwa | Skrót | Krótkich nazw/TxMs |
| ------------- | ------------ | --------- |
|.NET Framework | NET | net11 |
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
|Microsoft Store (Windows Store) | netcore | netcore [netcore45] |
| | | netcore45 [win win8] |
| | | netcore451 [win81] |
| | | netcore50 |
|MicroFramework platformy .NET | netmf | netmf |
|Windows | Wygraj | win [win8, netcore45] |
| | | win8 [netcore45, wygrać] |
| | | win81 [netcore451] |
| | | Windows 10 (nieobsługiwane przez system Windows 10 platformy) |
Silverlight | sl | sl4 |
| | | sl5 |
Windows Phone (SL) | WP | WP [wp7] |
| | | wp7 |
| | | wp75 |
| | | wp8 |
| | | wp81 |
Windows Phone (UWP) | | wpa81 |
Platforma uniwersalna systemu Windows | uap | uap [uap10.0] |
| | | uap10.0 |
.NET standard | netstandard | netstandard1.0 |
| | | netstandard1.1 |
| | | netstandard1.2 |
| | | netstandard1.3 |
| | | netstandard1.4 |
| | | netstandard1.5 |
| | | netstandard1.6 |
| | | netstandard2.0 |
Aplikacja programu .NET core | Element netcoreapp | netcoreapp1.0 |
| | | netcoreapp1.1 |
| | | netcoreapp2.0 |
| | | netcoreapp2.1 |
Tizen | Tizen | tizen3 |
| | | tizen4 |

## <a name="deprecated-frameworks"></a>Przestarzałe struktur

Następujące struktury są przestarzałe. Pakiety przeznaczone dla tych platform należy migrować do wskazanego zamiany.

| Przestarzałe framework | Zastępczy
| --- | ---
| aspnet50 | Element netcoreapp |
| aspnetcore50 |
| dnxcore50 |
| dnx |
| dnx45 |
| dnx451 |
| dnx452 |
| polecenia DotNet | netstandard |
| dotnet50 | |
| dotnet51 | |
| dotnet52 | |
| dotnet53 | |
| dotnet54 | |
| dotnet55 | |
| dotnet56 | |
| winrt | Wygraj |

## <a name="precedence"></a>Pierwszeństwo

Wiele struktur są powiązane z i zgodność ze sobą, ale nie zawsze jest równoważne:

| Framework | Można użyć |
| -- | --- |
| uap (Universal Windows Platform) | win81 |
| | wpa81 |
| | netcore50 |
| Wygraj (Microsoft Store) | winrt |
| | |

## <a name="net-platform-standard"></a>Platformy NET Standard

[Platformy .NET Standard](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/net-platform-standard.md) upraszcza odwołania między struktur zgodne dane binarne, dzięki czemu platforma pojedynczy element docelowy odwoływać się do innych kombinacji. (Aby uzyskać ogólne, zobacz [Elementarz .NET](/dotnet/articles/standard/index).)

[NuGet Pobierz najbliższą narzędzia Framework](https://aka.ms/s2m3th) symuluje NuGet używa do wybrania jednej struktury z wielu zasobów framework dostępne w pakiecie oparty na framework projektu.

`dotnet` Serii monikerów powinny być używane w rozszerzenia NuGet 3.3 i starszych; `netstandard` składni moniker należy używać w wersji 3.4 i nowszych wersjach.

## <a name="portable-class-libraries"></a>Biblioteki klas przenośnych

> [!Warning]
> **Nie zaleca się PCLs**. Choć PCLs są obsługiwane, autorom pakietów powinien obsługiwać netstandard zamiast tego. Platformy .NET Standard jest unowocześnienia PCLs i reprezentuje możliwości binarnego przenoszenia na wielu platformach za pomocą pojedynczego monikera, która nie jest powiązany z biblioteki statycznej, takich jak *przenośne-+ b + c* monikerów.

Aby zdefiniować platformę docelową, która odwołuje się do wielu podrzędnych —-platform docelowych, `portable` użyj słowa kluczowego używana jako prefiks lista platform do którego istnieje odwołanie. Należy unikać sztucznie tym dodatkowe struktury, które nie są bezpośrednio kompilowane przed ponieważ może to prowadzić do niezamierzone efekty uboczne w tych środowisk.

Dodatkowe struktury zdefiniowany przez strony trzecie zapewniają zgodność z innych środowisk, które są dostępne w ten sposób. Ponadto istnieją numery profilu skrótu, które są dostępne te kombinacje pokrewne struktury jako odwołanie do `Profile#`, ale nie jest to zalecana praktyka do użycia tych numerów, ponieważ zmniejsza to czytelność folderów i `.nuspec`.

| Profil # | Struktury | Imię i nazwisko | .NET standard |
 --- | --- | --- | ---
 Profile2 | .NETFramework 4.0 | portable-net40+win8+sl4+wp7 |
 | | Windows 8.0 | |
 | | Silverlight 4.0 |
 | | WindowsPhone 7.0|
 Profile3 | .NETFramework 4.0 | portable-net40+sl4
 | | Silverlight 4.0 |
 Profile4 | .NETFramework 4.5 | portable-net45+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile5 | .NETFramework 4.0 | portable-net40+win8
 | | Windows 8.0 |
 Profile6 | .NETFramework 4.0.3 | portable-net403+win8
 | | Windows 8.0 |
 Profile7 | .NETFramework 4.5 | portable-net45+win8 | netstandard1.1
 | | Windows 8.0 |
 Profile14 | .NETFramework 4.0 | portable-net40+sl5
 | | Silverlight 5.0 |
 Profile18 | .NETFramework 4.0.3 | portable-net403+sl4
 | | Silverlight 4.0 |
 Profile19 | .NETFramework 4.0.3 | portable-net403+sl5
 | | Silverlight 5.0 |
 Profile23 | .NETFramework 4.5 | portable-net45+sl4
 | | Silverlight 4.0 |
 Profile24 | .NETFramework 4.5 | portable-net45+sl5
 | | Silverlight 5.0 |
 Profile31 | Windows 8.1 | portable-win81+wp81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 Profile32 | Windows 8.1 | portable-win81+wpa81 | netstandard1.2
 | | WindowsPhone 8.1 (systemu Windows UWP) |
 Profile36 | .NETFramework 4.0 | portable-net40+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile37 | .NETFramework 4.0 | portable-net40+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile41 | .NETFramework 4.0.3 | portable-net403+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile42 | .NETFramework 4.0.3 | portable-net403+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile44 | .NETFramework 4.5.1 | portable-net451+win81 | netstandard1.2
 | | Windows 8.1 |
 Profile46 | .NETFramework 4.5 | portable-net45+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile47 | .NETFramework 4.5 | portable-net45+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile49 | .NETFramework 4.5 | portable-net45+wp8 | netstandard1.0
 | | WindowsPhone 8.0 (SL) |
 Profile78 | .NETFramework 4.5 | portable-net45+win8+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile84 | WindowsPhone 8.1 | portable-wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (systemu Windows UWP) |
 Profile88 | .NETFramework 4.0 | portable-net40+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile92 | .NETFramework 4.0 | portable-net40+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (systemu Windows UWP) |
 Profile95 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile96 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile102 | .NETFramework 4.0.3 | portable-net403+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (systemu Windows UWP) |
 Profile104 | .NETFramework 4.5 | portable-net45+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile111 | .NETFramework 4.5 | portable-net45+win8+wpa81 | netstandard1.1
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (systemu Windows UWP) |
 Profile136 | .NETFramework 4.0 | portable-net40+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile143 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile147 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile151 | NETFramework 4.5.1 | portable-net451+win81+wpa81 | netstandard1.2
 | | Windows 8.1 |
 | | WindowsPhone 8.1 (systemu Windows UWP) |
 Profile154 | .NETFramework 4.5 | portable-net45+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile157 | Windows 8.1 | portable-win81+wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 | | WindowsPhone 8.1 (systemu Windows UWP) |
 Profile158 | .NETFramework 4.5 | portable-net45+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile225 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (systemu Windows UWP) |
 Profile240 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (systemu Windows UWP) |
 Profile255 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (systemu Windows UWP) |
 Profile259 | .NETFramework 4.5 | portable-net45+win8+wpa81+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (systemu Windows UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile328 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (systemu Windows UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile336 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (systemu Windows UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile344 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (systemu Windows UWP) |
 | | WindowsPhone 8.0 (SL) |

Ponadto pakiety NuGet określanie wartości docelowej platformy Xamarin można użyć dodatkowe struktury zdefiniowane w środowisku Xamarin. Zobacz [NuGet tworzenie pakietów dla platformy Xamarin](https://developer.xamarin.com/guides/cross-platform/advanced/nuget/).

| Nazwa | Opis | .NET standard |
| --- | --- | ---
| monoandroid | Obsługa środowiska mono dla systemu operacyjnego Android | netstandard1.4 |
| monotouch | Mono dla systemu iOS | netstandard1.4 |
| platformy monomac | Obsługa środowiska mono dla systemu OSX | netstandard1.4 |
| xamarinios | Obsługa platformy Xamarin dla systemu iOS | netstandard1.4 |
| xamarinmac | Obsługuje dla platformy Xamarin dla komputerów Mac | netstandard1.4 |
| xamarinpsthree | Obsługa platformy Xamarin na Playstation 3 | netstandard1.4 |
| xamarinpsfour | Obsługa platformy Xamarin na Playstation 4 | netstandard1.4 |
| xamarinpsvita | Obsługa platformy Xamarin na PS Vita | netstandard1.4 |
| xamarinwatchos | Platforma Xamarin dla całkowicie Obejrzyj systemu operacyjnego | netstandard1.4 |
| xamarintvos | Platforma Xamarin dla całkowicie system TV OS | netstandard1.4 |
| xamarinxboxthreesixty | Platforma Xamarin dla konsoli XBox 360 | netstandard1.4 |
| xamarinxboxone | Platforma Xamarin dla całkowicie XBox One | netstandard1.4 |

> [!Note]
> Autor: Stephen wyraźnie utworzył to narzędzie, które wyświetla listę obsługiwanych PCLs, które można znaleźć na jego wpis, [profile Framework na platformie .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html).
