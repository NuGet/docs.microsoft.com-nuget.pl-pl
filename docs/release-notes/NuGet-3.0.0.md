---
title: Informacje o wersji narzędzia NuGet 3,0
description: Informacje o wersji programu NuGet 3.0.0, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776551"
---
# <a name="nuget-30-release-notes"></a>Informacje o wersji narzędzia NuGet 3,0

Informacje o wersji narzędzia [NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)  |  [Informacje o wersji narzędzia NuGet 3,1](../release-notes/nuget-3.1.md)

Pakiet NuGet 3,0 został wydano 20 lipca 2015 jako rozszerzenie pakietu do programu Visual Studio 2015. Firma Microsoft wypychamy, aby dostarczyć tę wersję za pomocą programu Visual Studio, dzięki czemu kompletne zaktualizowane środowisko NuGet 3,0 będzie dostępne dla nowych użytkowników programu Visual Studio. Ta wersja rozszerzenia NuGet jest dostępna tylko dla programu Visual Studio 2015.

Zaleca się, aby Ci deweloperzy mieli dostęp do aktualizacji galerii programu Visual Studio do najnowszej dostępnej wersji, ponieważ publikujemy aktualizację wkrótce po wydaniu programu Visual Studio 2015, który zawiera wsparcie dla rozwoju systemu Windows 10.

W sumie zostały zamknięte 240 problemów w wersji 3,0 i można zapoznać się z [pełną listą problemów w witrynie GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Znane problemy

Istniało wiele znanych problemów z tą wersją, a wszystkie te elementy zostały rozwiązane w naszym zaplanowanym 3,1 wersji, aby uzyskać zbieżność z wersją systemu Windows 10 w dniu 29 lipca.  Możesz zaktualizować rozszerzenie programu Visual Studio z galerii w tej dacie lub później, aby rozwiązać te znane problemy.

*  Nie podano tłumaczenia na etykietę "nie pokazuj ponownie" w oknie podglądu i etykiecie "autorów" w oknie opisu pakietu.
*  Podczas pracy nad projektem przy użyciu kontroli źródła TFS, NuGet nie może przedstawić interfejsu użytkownika Menedżera pakietów, jeśli plik Nuget.Config jest oznaczony jako tylko do odczytu.
   * **Obejście problemu** Wyewidencjonuj plik z TFS.
*  W przypadku korzystania z ciemnego motywu programu Visual Studio tekst w żółtym "pasku ponownego uruchamiania" w oknie programu PowerShell NuGet nie jest widoczny.
   * **Obejście problemu** Użyj motywu programu Visual Studio.


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
* [Rozwiązano link "informacje o opcjach", aby zapobiec awariom systemu Windows 10](https://github.com/NuGet/Home/issues/822)
* [Zapamiętaj ustawienie pola wyboru w wersji wstępnej](https://github.com/NuGet/Home/issues/732)
* [Ulepszone zbieranie wydajności przez buforowanie wyników między projektami w rozwiązaniu](https://github.com/NuGet/Home/issues/721)
* [Wiele pakietów może być zebranych równolegle](https://github.com/NuGet/Home/issues/713)
* [Usunięto polecenie install-package-Force](https://github.com/NuGet/Home/issues/697)

Zapoznaj się z [naszym blogiem](http://blog.nuget.org) , aby uzyskać więcej informacji o postępie i ogłoszeniach, jak jesteśmy gotowi do świadczenia pomocy technicznej dla rozwoju systemu Windows 10.