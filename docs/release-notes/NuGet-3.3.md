---
title: Informacje o wersji narzędzia NuGet 3,3
description: Informacje o wersji programu NuGet 3,3, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cd3f8c9c4586c608d41e7b8bfc413acfc6aff497
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776510"
---
# <a name="nuget-33-release-notes"></a>Informacje o wersji narzędzia NuGet 3,3

Informacje o wersji pakietu [NuGet 3.2.1](../release-notes/nuget-3.2.1.md)  |  Pakiet [NuGet 3,4 — Informacje o wersji RC](../release-notes/nuget-3.4-RC.md)

Pakiet NuGet 3,3 został wydane 30 listopada 2015 z znaczącą liczbą aktualizacji interfejsu użytkownika i funkcjami wiersza polecenia, a także kolekcją przydatnych poprawek do klientów programu NuGet.

## <a name="new-features"></a>Nowe funkcje

* Wprowadzono dostawców poświadczeń, dzięki którym klienci wiersza polecenia NuGet mogą bezproblemowo współpracować z uwierzytelnionym źródłem danych. [Instrukcje dotyczące sposobu instalowania dostawcy poświadczeń Visual Studio Team Services ](../reference/extensibility/nuget-exe-credential-providers.md) i konfigurowania klientów NuGet do korzystania z nich są dostępne w dokumentach programu NuGet.

## <a name="new-user-interface-features"></a>Nowe funkcje interfejsu użytkownika

* Oddziel dostępne karty przeglądania, instalacji i aktualizacji
* Dostępne aktualizacje znaczek wskazujące liczbę pakietów z dostępnymi aktualizacjami
* Identyfikatory pakietów na liście pakietów wskazujące, czy pakiet jest zainstalowany lub czy jest dostępna aktualizacja
* Liczba pobrań i autor dodana do listy pakietów
* Najwyższy dostępny numer wersji i aktualnie zainstalowany numer wersji na liście pakietów
* Przyciski akcji umożliwiające szybkie instalowanie, aktualizowanie i odinstalowywanie z listy pakietów
* Wyczyść przyciski akcji na panelu szczegółów pakietu
* Data aktualizacji pakietu na panelu szczegółów pakietu
* Konsolidowanie panelu w widoku rozwiązania
* Sortowanie siatki projektów i zainstalowanych numerów wersji w widoku rozwiązania

## <a name="new-command-line-features"></a>Nowe funkcje wiersza polecenia

W tej wersji wprowadziliśmy `add` polecenia i w `init` celu zainicjowania repozytoriów opartych na folderach zgodnie z opisem w [ dokumentacjinuget.exe](../reference/nuget-exe-cli-reference.md). Repozytoria tworzone i utrzymywane przy użyciu tej struktury folderów [zapewniają znaczący](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) wpływ na wydajność, jak opisano w naszym blogu.

## <a name="contentfiles"></a>ContentFiles

Zawartość jest teraz obsługiwana w `project.json` projektach zarządzanych za pomocą nowego `contentFiles` folderu i `.nuspec` `contentFiles` notacji elementu.  Ta zawartość może być bardziej bezpośrednio określona przez autora pakietu na potrzeby interakcji z systemami projektu.  Więcej informacji o sposobie konfigurowania contentFiles w dokumencie znajduje `.nuspec` się w [dokumentacji. nuspec](../reference/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Zarządzanie pamięcią podręczną pakietów NuGet

Wiersz polecenia NuGet został zaktualizowany w celu uwzględnienia informacji o sposobach zarządzania lokalnymi pamięciami podręcznymi na stacji roboczej.  Więcej informacji na temat polecenia locales jest dostępnych w [dokumentacji wiersza polecenia NuGet](../reference/cli-reference/cli-ref-locals.md).

## <a name="fixed-issues"></a>Rozwiązane problemy

**Istotne problemy**

* Przywrócono obsługę wiersza polecenia NuGet w celu przywrócenia pakietów z plikiem rozwiązania na platformie mono- [1543](https://github.com/NuGet/Home/issues/1543)

Pełną listę problemów, które zostały rozwiązane w wersji 3,3, można znaleźć w witrynie GitHub w punkcie [kontrolnym 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

Lista problemów rozwiązanych w wersji wiersza polecenia 3,3 jest rejestrowana w obszarze [kontrolnym 3,3 Command-Line](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Znane problemy

Będziemy nadal śledzić problemy na naszej liście problemów usługi GitHub, którą można znaleźć w witrynie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)