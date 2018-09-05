---
title: Informacje o wersji 3.3 NuGet
description: Informacje o wersji rozszerzenia NuGet 3.3 tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546650"
---
# <a name="nuget-33-release-notes"></a>Informacje o wersji 3.3 NuGet

[Informacje o wersji NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC wersji](../release-notes/nuget-3.4-RC.md)

Rozszerzenia NuGet 3.3 został wydany do 30 listopada 2015 za pomocą znaczna liczba aktualizacje interfejsu użytkownika i funkcje wiersza polecenia, a także zbiór poprawek przydatne dla klientów NuGet.

## <a name="new-features"></a>Nowe funkcje

* Wprowadzono dostawcy poświadczeń, które umożliwiają klientom wiersza polecenia NuGet można było bezproblemowej współpracy z uwierzytelnionego źródła danych. [Instrukcje dotyczące sposobu instalowania programu Visual Studio Team Services poświadczeń dostawcy ](../api/nuget-exe-credential-providers.md) i konfigurowanie pakietu NuGet klientów z niej korzystać, są dostępne w dokumentacji systemu NuGet.

## <a name="new-user-interface-features"></a>Nowe funkcje interfejsu użytkownika

* Oddzielne karty przeglądania, zainstalowane i dostępna aktualizacje
* Aktualizacje dostępne wskaźniku określającą liczbę pakietów wraz z dostępnymi aktualizacjami
* Wskaźniki pakietu na liście pakietu, aby wskazać, czy pakiet jest zainstalowany, czy dostępna jest aktualizacja
* Pobierz liczbę i autor dodane do listy pakietów
* Najwyższy numer wersji dostępnych i Liczba obecnie zainstalowanej wersji na liście pakietów
* Przyciski akcji, aby umożliwić szybkiej instalacji aktualizacji i odinstalować z listy pakietów
* Bardziej zrozumiały przyciski akcji na panelu szczegółów pakietu
* Data aktualizacji pakietu na panelu szczegółów pakietu
* Konsolidacja panelu w widoku rozwiązania
* Sortowanie siatki projektów i numery wersji zainstalowanej w widoku rozwiązania

## <a name="new-command-line-features"></a>Nowe funkcje wiersza polecenia

W tej wersji wprowadziliśmy `add` i `init` polecenia, aby zainicjować folderu repozytoriów, zgodnie z opisem w [odwołania nuget.exe](../tools/nuget-exe-cli-reference.md). Repozytoria, które są zbudowane i z tego folderu struktury będzie [dostarczać korzystny wydajności](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) zgodnie z opisem w naszym blogu.

## <a name="contentfiles"></a>Pliki

Zawartość jest teraz obsługiwana w `project.json` zarządzanych projektów za pomocą nowego `contentFiles` folder i `.nuspec` `contentFiles` element notation.  Ta zawartość można określić więcej bezpośrednio przez autora pakietu w celu interakcji z systemami projektu.  Więcej informacji na temat sposobu konfigurowania pliki w `.nuspec` można znaleźć dokumentu w [.nuspec odwołania](../reference/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Zmienne lokalne NuGet w pamięci podręcznej zarządzania

Wiersza polecenia NuGet został zaktualizowany w celu uwzględnienia informacji o sposobie zarządzania pamięciach podręcznych na stacji roboczej.  Więcej informacji o poleceniu zmiennych lokalnych jest dostępna w [wiersza polecenia NuGet](../tools/cli-ref-locals.md).

## <a name="fixed-issues"></a>Rozwiązane problemy

**Problemy godne uwagi**

* NuGet przywróconej za pomocą wiersza polecenia przywracania pakietów z plikiem rozwiązania na platformy Mono - [1543](https://github.com/NuGet/Home/issues/1543)

Pełną listę problemów, które zostały rozwiązane w wersji 3.3 można znaleźć w witrynie GitHub w ramach [3.3 punkt kontrolny](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

Lista problemów rozwiązanych w wersji 3.3 wiersza polecenia są rejestrowane w [3.3 wiersza polecenia punkt kontrolny](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Znane problemy

W dalszym ciągu śledzenia problemów na naszej liście problemów GitHub, który znajduje się w temacie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)