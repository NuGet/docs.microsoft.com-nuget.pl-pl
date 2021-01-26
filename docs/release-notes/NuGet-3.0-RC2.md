---
title: Informacje o wersji narzędzia NuGet 3,0 RC2
description: Informacje o wersji programu NuGet 3,0 RC2, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780280"
---
# <a name="nuget-30-rc2-release-notes"></a>Informacje o wersji narzędzia NuGet 3,0 RC2

Informacje o wersji narzędzia [NuGet 3,0 RC](../release-notes/nuget-3.0-RC.md)  |  [Informacje o wersji narzędzia NuGet 3,0](../release-notes/nuget-3.0.0.md)

Pakiet NuGet 3,0 RC2 został opublikowany od 3 czerwca 2015 jako tymczasowe wydanie dostępne z galerii rozszerzeń programu Visual Studio 2015 i [CodePlex](https://nuget.codeplex.com/releases/view/615507). W tej wersji wprowadzono wiele ważnych poprawek i ulepszeń wydajności, które były ważne do wydania przed ukończeniem pełnej wersji programu Visual Studio 2015. Ta wersja rozszerzenia NuGet jest dostępna tylko dla programu Visual Studio 2015.

W sumie zostały zamknięte 158 problemów w tej wersji i można zapoznać się z [pełną listą problemów w witrynie GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).

## <a name="summary-of-top-issues-resolved"></a>Podsumowanie najważniejszych problemów rozwiązanych

* [Częste wywołania aktualizacji sieci podczas odświeżania okna Menedżera pakietów](https://github.com/NuGet/Home/issues/515)
* [Opóźnione przewijanie podczas zmiany widoku na zainstalowany w Menedżerze pakietów](https://github.com/NuGet/Home/issues/519)
* [Wywołania sieciowe powinny być uruchamiane w wątku w tle](https://github.com/NuGet/Home/issues/516)
* [Dodano pole wyboru "nie pokazuj okna podglądu"](https://github.com/NuGet/Home/issues/566)
* [Dodano ograniczanie procesów w celu zmniejszenia użycia procesora](https://github.com/NuGet/Home/issues/356)
* Ulepszona obsługa odwołań do biblioteki klas przenośnych
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [W usłudze autouzupełniania była rozróżniana wielkość liter](https://github.com/NuGet/Home/issues/198)
* [Aktualizuj, aby wprowadzić poświadczenia uwierzytelniania podstawowego](https://github.com/NuGet/Home/issues/456)
* [Ulepszone rejestrowanie błędów](https://github.com/NuGet/Home/issues/407)
* [Ulepszone komunikaty o błędach programu PowerShell podczas wywoływania polecenia Update-Package](https://github.com/NuGet/Home/issues/5)

Pobierz tę [aktualizację do rozszerzenia NuGet](https://nuget.codeplex.com/releases/view/615507) z CodePlex [, aby uzyskać więcej informacji o](http://blog.nuget.org) postępie i anonsach dla programu NuGet 3,0!.