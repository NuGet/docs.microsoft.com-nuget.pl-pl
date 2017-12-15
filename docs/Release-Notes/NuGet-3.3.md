---
title: Informacje o wersji NuGet 3.3 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 4110a36a-cffe-4038-8da4-e841bce6e94b
description: "Informacje o wersji dla tym znanych problemów, poprawki, dodatkowe funkcje i dcr 3.3 NuGet."
keywords: NuGet 3.3 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f35f7621db324957b0af8329cf9faa11493835e2
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-33-release-notes"></a>Informacje o wersji 3.3 NuGet

[Informacje o wersji NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC informacje o wersji](../release-notes/nuget-3.4-RC.md)

NuGet 3.3 został wydany 30 listopada 2015 z znaczących aktualizacje interfejsu użytkownika i funkcje wiersza polecenia, a także kolekcję przydatne poprawek klientom NuGet.

## <a name="new-features"></a>Nowe funkcje

* Dostawcy poświadczeń zostały wprowadzone zezwalające klientom wiersza polecenia NuGet można było współpracuje z uwierzytelnionego źródła danych. [Instrukcje dotyczące instalowania programu Visual Studio Team Services poświadczeń dostawcy ](../API/nuget-exe-Credential-Providers.md) i skonfigurować NuGet klientom na używanie go są dostępne na NuGet Docs.

## <a name="new-user-interface-features"></a>Nowe funkcje interfejsu użytkownika

* Oddzielne karty przeglądania, zainstalowane i dostępne aktualizacje
* Aktualizacje dostępne wskaźnika wskazującą liczbę pakietów o dostępności aktualizacji
* Identyfikatory pakietów na liście pakietów, aby wskazać, czy pakiet jest zainstalowany, czy dostępna jest aktualizacja
* Pobierz liczbę i autora dodane do listy pakietów
* Największa liczba dostępnych wersji i numer obecnie zainstalowanej wersji na liście pakietu
* Przyciski akcji umożliwia szybkiej instalacji aktualizacji i odinstalować z listy pakietów
* Jaśniejszy przycisków akcji w panelu szczegółów pakietu
* Data aktualizacji pakietu w panelu szczegółów pakietu
* Konsolidacja panelu w widoku Solution
* Sortowanie siatki projektów i numery wersji zainstalowanej w widoku rozwiązania

## <a name="new-command-line-features"></a>Nowe funkcje wiersza polecenia

W tej wersji wprowadzono `add` i `init` polecenia, aby zainicjować na podstawie folderu repozytoria zgodnie z opisem w [odwołania nuget.exe](../tools/nuget-exe-cli-reference.md). Repozytoria, które są konstruowane i z tego folderu struktury będzie [dostarczania korzystny wydajności](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) w sposób opisany w naszym blogu.

## <a name="contentfiles"></a>Pliki

Zawartość jest teraz obsługiwana w `project.json` zarządzane za pomocą nowej `contentFiles` folderu i `.nuspec` `contentFiles` element notation.  Ta zawartość można określić więcej bezpośrednio przez autora pakietu w celu interakcji z systemami projektu.  Więcej informacji na temat sposobu konfigurowania pliki w `.nuspec` można znaleźć w dokumencie [.nuspec odwołania](../schema/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Zmienne lokalne NuGet pamięci podręcznej zarządzania

Wiersza polecenia NuGet została zaktualizowana w celu uwzględnienia informacji o sposobie zarządzania lokalnej pamięci podręcznej na stacji roboczej.  Więcej informacji o poleceniu zmiennych lokalnych jest dostępna w [wiersza polecenia NuGet](../tools/cli-ref-locals.md).

## <a name="fixed-issues"></a>Rozwiązane problemy

**Godne uwagi problemy**

* Pakiety NuGet przywrócone za pomocą wiersza polecenia przywracania z pliku rozwiązania na Mono - [1543](https://github.com/NuGet/Home/issues/1543)

Pełną listę problemów, które zostały opisane w 3.3 wersji można znaleźć w witrynie GitHub pod [3.3 punkt kontrolny](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

Lista problemów rozwiązanych w 3.3 wersji wiersza polecenia są rejestrowane w [3.3 wiersza polecenia punkt kontrolny](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Znane problemy

W dalszym ciągu do śledzenia problemów w naszej listy problemów GitHub, który znajduje się w temacie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)