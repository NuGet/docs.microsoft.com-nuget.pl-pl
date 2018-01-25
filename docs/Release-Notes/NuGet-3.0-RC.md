---
title: Informacje o wersji RC NuGet 3.0 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o wersji programu NuGet 3.0 RC tym znanych problemów, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 3.0 informacje o wersji RC, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4693fd8884283e01d3c0a8ad74e0692c1ca00659
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-30-rc-release-notes"></a>Informacje o wersji RC NuGet 3.0

[Informacje o wersji Beta NuGet 3.0](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 informacje o wersji](../release-notes/nuget-3.0-RC2.md)

Począwszy od wersji programu Visual Studio 2015 RC z NuGet 3.0 RC został wydany 29 kwietnia 2015 r. Ta wersja zawiera szereg ważnych poprawek, wydajności i aktualizacji do obsługi nowej struktury.  Jest on dostępny tylko dla programu Visual Studio 2015.

### <a name="continued-focus-on-performance"></a>Kontynuacja fokus na wydajność

Stabilność i wydajność kwerend NuGet nadal będą dostępne na temat dynamicznej.  W tej wersji należy zacząć wyświetlić operacje bardzo szybkiego wyszukiwania w NuGet interfejsu użytkownika i witryny sieci Web.  Firma Microsoft jest monitorowanie usługi i sposobie korzystania z usługi tak, aby móc dalej dostosować te operacje.

## <a name="significant-issues-resolved"></a>Istotne problemy rozwiązane

Aby ustabilizowania klientów NuGet, możemy rozpoznać wiele problemów w ramach tej wersji.  Poniżej przedstawiono tylko krótki listę niektórych ważniejsze rozwiązaniu problemów:

* W ramach zmiany nazwy K framework dla platformy ASP.NET 5, monikerów framework zostały zaktualizowane do obsługi środowiska dnx i dnxcore [łącza](https://github.com/NuGet/Home/issues/215)
* Dodane w dokumentacji pomocy z łącza w interfejsie użytkownika programu Visual Studio [łącza](https://github.com/NuGet/Home/issues/232)
* Lepszą obsługę złożonych odwołań w `.nuspec` z odwołaniami rozdzielana przecinkami framework [łącza](https://github.com/NuGet/Home/issues/276)
* Stałe obsługę japońskiego kultur [łącza](https://github.com/NuGet/Home/issues/253)
* Zaktualizowanego klienta umożliwiają projektów ASP.NET 5 nowe punkty końcowe v3 [łącza](https://github.com/NuGet/Home/issues/219)
* Zaktualizowano w celu lepszej obsługi pakietów folder z kontrolą źródła [łącza](https://github.com/NuGet/Home/issues/56)
* Stałe obsługi pakietów satelity [łącza](https://github.com/NuGet/Home/issues/17)
* Poprawiona obsługa plików zawartości określonej struktury [łącza](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>Naprawy głównej obecności GitHub

Wprowadziliśmy pewne zmiany do naszej [źródła repozytoria kodu w witrynie GitHub](http://github.com/nuget/home).  Jeśli masz problemy z klienta NuGet programu Visual Studio, poleceń programu Powershell lub wiersza polecenia pliku wykonywalnego możesz zalogować tych problemów i monitorować ich postęp na naszych [listę problemów repozytorium GitHub głównej](http://github.com/nuget/home/issues).  Śledzimy problemy z galerii w naszym [repozytorium GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Wkrótce

Można śledzić na [naszym blogu](http://blog.nuget.org) więcej i powiadomień dla NuGet 3.0!