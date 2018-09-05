---
title: Informacje o wersji 4.6 RTM NuGet
description: Informacje o wersji programu NuGet 4.6.0 tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: anangaur
ms.author: anangaur
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: 3c71d05144aa2b92b916d4ebf319c5a4e321581f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549847"
---
# <a name="nuget-46-rtm-release-notes"></a>Informacje o wersji 4.6 RTM NuGet

[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) dołączono [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe).

## <a name="summary-whats-new-in-this-release"></a>Podsumowanie: nowości w tej wersji

* Dodaliśmy obsługę [podpisywanie pakietów](../create-packages/sign-a-package.md).
* Visual Studio 2017 i nuget.exe teraz sprawdza integralność pakietu przed instalacją, trwa przywracanie pakietów [podpisanych pakietów](../reference/signed-packages-reference.md).
* Poprawiliśmy wydajność kolejne operacje przywracania.

## <a name="known-issues"></a>Znane problemy

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemy z platformą .NET Standard 2.0 przy użyciu platformy .NET Framework i NuGet 

.NET standard i jego narzędzia zaprojektowano w taki sposób, że projekty przeznaczone dla platformy .NET Framework 4.6.1 może zużywać pakietów NuGet i projekty przeznaczone dla .NET Standard 2.0 lub wcześniejszej. [W tym dokumencie](https://github.com/dotnet/standard/issues/481) znajduje się podsumowanie problemy dotyczące tego scenariusza, planowanie adresowania, a rozwiązania można wdrożyć ze stanem współczesnych narzędzi.

## <a name="top-issues-fixed-in-this-release"></a>Najważniejsze problemy rozwiązane w tej wersji

**Poprawki wydajności**

* Nie zapisuj pliki zasobów, gdy nastąpiła żadna zmiana - [#6491](https://github.com/NuGet/Home/issues/6491)
* Przywracanie powoduje występowanie dodatkowe wersje ewaluacyjne programu MSBuild, gdy TFM projekty podrzędne nie są zgodne z nadrzędnego projektu - [#6311](https://github.com/NuGet/Home/issues/6311)
* Poprawa wydajności przywracania aktualizujący nie działa, optymalizując zależności programu graph Tworzenie specyfikacji - [#6252](https://github.com/NuGet/Home/issues/6252)

**Błędy**

* Wypychanie do lokalnego folderu pozostawia nupkg zablokowane - [#6325](https://github.com/NuGet/Home/issues/6325)
* Implementacja wtyczki NuGet: wiele problemów — [#6149](https://github.com/NuGet/Home/issues/6149)
* -Usuń zapytanie wywołania usługi od inicjowania MEF w VSSolutionManager - UIHang [#6110](https://github.com/NuGet/Home/issues/6110)
* Wyjątek dla raportowania błędów anulowane zadanie pobierania pakietu - [#6096](https://github.com/NuGet/Home/issues/6096)
* Zastępuje NuGet.exe '+' z '% 2B"w nazwie zestawu - [#5956](https://github.com/NuGet/Home/issues/5956)
* FN + F1 nie przyjmuje na stronę prawego pomocy dla interfejsu użytkownika PM i konsola — [#5912](https://github.com/NuGet/Home/issues/5912)
* NuGet do VS zapisuje ścieżki bezwzględnej do plików projektu w szczególnych okolicznościach - [#5888](https://github.com/NuGet/Home/issues/5888)
* Napraw regresji 4.3 — symbole zastępcze $product$ i $AssemblyGuid$ nie jest wymieniony w contentfile za pomocą przekształcania — [#5880](https://github.com/NuGet/Home/issues/5880)
* DotNet restore z wielu źródeł awarie - [#5817](https://github.com/NuGet/Home/issues/5817)
* Pakiet należy ponownie oceń wersji projektu, aby zezwolić na przechowywanie wersji usługi git - [#4790](https://github.com/NuGet/Home/issues/4790)
* Poprawić trudne do zrozumienia błędy podczas instalowania pakietu niezgodne - [#4555](https://github.com/NuGet/Home/issues/4555)
* TemplateWizard musi opcję, aby zainstalować pakiety jako PackageReferences - [#4549](https://github.com/NuGet/Home/issues/4549)
* Pliki dostarczane przez pakiet właściwości ignorowane podczas MSBuild.exe jest uruchamiany z poza wierszem polecenia dla deweloperów — [#4530](https://github.com/NuGet/Home/issues/4530)
* Usuń komunikat o błędzie niską podczas odwoływania się do biblioteki standardowej platformy .NET, który nie ma zastosowania do projektów — [#4423](https://github.com/NuGet/Home/issues/4423)
* DotNet Dodawanie pakietu nie powiedzie się z pakietu określania wartości docelowej profilu przenośne wskazówek - [#4349](https://github.com/NuGet/Home/issues/4349)
* pakietu DotNet - suffix wersji brakuje elementu ProjectReference - [#4337](https://github.com/NuGet/Home/issues/4337)
* Twórz błędów i awarii programu VS przy użyciu szablonu platformy .NET Core — [#3973](https://github.com/NuGet/Home/issues/3973)
* Nie można załadować indeks usługi https:* źródła - [#3681](https://github.com/NuGet/Home/issues/3681)
* nuget.exe list - allversions nie działa — [#3441](https://github.com/NuGet/Home/issues/3441)
* Mylący zależności rozpoznawania komunikat o błędzie - [#2984](https://github.com/NuGet/Home/issues/2984)
* Przywracanie nuget.exe nie generuje pliki .props i .targets .msbuildproj (Regresja podczas uaktualniania v3.3.0 3.4.4) - [#2921](https://github.com/NuGet/Home/issues/2921)
* Opóźnienie reakcji interfejsu użytkownika podczas aktualizowania pakietu NuGet XAML plik jest otwarty — [#2878](https://github.com/NuGet/Home/issues/2878)
* Projekt witryny sieci Web za pomocą programu IIS kończy się niepowodzeniem z niedozwolone znaki w ścieżce - [#2798](https://github.com/NuGet/Home/issues/2798)
* Nuget dodać zawiesza się na CentOS - [#2708](https://github.com/NuGet/Home/issues/2708)
* Przywracanie ze packagesavemode - nupkg zakończy się niepowodzeniem na składnik JSON.NET - [#2706](https://github.com/NuGet/Home/issues/2706)
* Filtr Menedżera pakietów nie jest dostępna w programie vs dane wyjściowe okna polecenie restore - [#2704](https://github.com/NuGet/Home/issues/2704)

[Lista wszystkie problemy rozwiązane w tej wersji](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
