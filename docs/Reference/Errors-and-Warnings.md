---
title: NuGet błędy i ostrzeżenia odwołania
description: Pełną dokumentację dla ostrzeżeń i błędów wystawiony na podstawie NuGet podczas różne operacje NuGet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: anangaur
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: dcff20e35adc0a3dbcc7bef482f81a937cf059c5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="errors-and-warnings"></a>Błędy i ostrzeżenia

W 4.3.0+ NuGet błędy i ostrzeżenia są numerowane zgodnie z opisem w tym temacie i zawierają szczegółowe informacje pozwalające rozwiązać problemy związane z.

Błędy i ostrzeżenia wymienione w tym miejscu są dostępne tylko w przypadku [na podstawie PackageReference](../consume-packages/package-references-in-project-files.md) projektów i NuGet 4.3.0+. NuGet honoruje także właściwości programu MSBuild tłumienie ostrzeżeń lub podniesienie ich poziomu błędy. Aby uzyskać więcej informacji, zobacz [porady: pomijanie ostrzeżeń kompilatora](/visualstudio/ide/how-to-suppress-compiler-warnings) w dokumentacji programu Visual Studio.

**Błędy**

| Grupa | Błąd liczby |
| --- | --- |
| [Nieprawidłowy błędów na wejściu](#invalid-input-errors) | [NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003) |
| [Brak błędów pakietu i projektu](#missing-package-and-project-errors) | [NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (wcześniej NU1607) [NU1108](#nu1108) (wcześniej NU1606) |
| [Błędy zgodności](#compatibility-errors) | [NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401) |

**Ostrzeżenia**

| Grupa | Numery ostrzeżeń |
| --- | --- |
| [Nieprawidłowy wejściowy ostrzeżenia](#invalid-input-warnings) | [NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503) |
| [Nieoczekiwany pakietu wersji ostrzeżenia](#unexpected-package-version-warnings) | [NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605) |
| [Mechanizm rozpoznawania konfliktu ostrzeżenia](#resolver-conflict-warnings) | [NU1608](#nu1608) |
| [Ostrzeżenia rezerwowy pakietu](#package-fallback-warnings) | [NU1701](#nu1701) |
| [Źródła danych ostrzeżenia](#feed-warnings) | [NU1801](#nu1801) |
| [NuGet wewnętrzne błędy i ostrzeżenia](#nuget-internal-errors-and-warnings) | [NU1000](#nu1000), [NU1500](#nu1500) |
| [Podpisanych pakietów (tworzenia i weryfikacji)](#signed-packages-creation-and-verification)| [NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028) |

## <a name="invalid-input-errors"></a>Nieprawidłowy błędów na wejściu

[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)

### <a name="nu1001"></a>NU1001

| | |
| --- | --- |
| **Problem** | Projekt nie zawiera co najmniej jeden struktury. |
| **Przykładowy komunikat** | *ProjA projektu nie określa żadnych docelowych platform w c:\tmp\projA.csproj* |
| **Rozwiązanie** | Dodaj `TargetFramework` lub `TargetFrameworks` właściwości do pliku określonego projektu. |

### <a name="nu1002"></a>NU1002

| | |
| --- | --- |
| **Problem** | Nieprawidłowa kombinacja danych wejściowych oraz wyczyść — słowo kluczowe. |
| **Przykładowy komunikat** | *"CLEAR" nie można używać w połączeniu z innymi wartości* |
| **Rozwiązanie** | Użyj wyczyść samodzielnie i pominąć wszystkie inne dane wejściowe. |

### <a name="nu1003"></a>NU1003

| | |
| --- | --- |
| **Problem** | `PackageTargetFallback` i `AssetTargetFallback` Podaj inaczej wybierania zasobów i nie mogą być używane razem. |
| **Przykładowy komunikat** | *PackageTargetFallback i AssetTargetFallback nie mogą być używane razem. Usuń odwołania PackageTargetFallback(deprecated) ze środowiska projektu.* |
| **Rozwiązanie** | Usuń przestarzałe `PackageTargetFallback` elementu z projektu. |

## <a name="missing-package-and-project-errors"></a>Brak błędów pakietu i projektu

[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)

### <a name="nu1100"></a>NU1100

| | |
| --- | --- |
| **Problem** | Grupa zależności nie można rozpoznać. Jest to problem rodzajowy dla typów, które nie są pakiety lub projektów. |
| **Przykładowy komunikat** | *Nie można rozpoznać System.Missing dla net45* |
| **Rozwiązanie** | Otwórz plik projektu i sprawdź, czy lista jego zależności. Sprawdź, czy poszczególne zależności istnieje na źródła pakietów, którego używasz, i że pakiet obsługuje platforma docelowa projektu. |

### <a name="nu1101"></a>NU1101

| | |
| --- | --- |
| **Problem** | Nie można odnaleźć pakietu na wszystkich źródeł. |
| **Przykładowy komunikat** | *Nie można odnaleźć pakietu System.Missing. Żadne pakiety nie istnieje z tym identyfikatorem w źródłach: dotnet core, dotnet roslyn, nuget.org* |
| **Rozwiązanie** | Sprawdź, czy zależności projektu w programie Visual Studio należy upewnić się, że używasz pakietu poprawny identyfikator i numer wersji. Sprawdź także, czy [Konfiguracja nuget projektu](../consume-packages/Configuring-NuGet-Behavior.md) identyfikuje źródła pakietów w sieci spodziewać się przy użyciu. Jeśli używasz pakiety, które mają [Wersjonowania semantycznego 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), upewnij się, że używasz [V3 źródła](https://api.nuget.org/v3/index.json) w [Konfiguracja nuget projektu](../consume-packages/Configuring-NuGet-Behavior.md). |

### <a name="nu1102"></a>NU1102

| | |
| --- | --- |
| **Problem** | Identyfikator pakietu został znaleziony, lecz nie można odnaleźć wersji w zakresie określonym zależności na żadnym z źródeł. Pakiet, a użytkownik nie może być określony zakres. |
| **Przykładowy komunikat** | *Nie można odnaleźć pakietu NuGet.Versioning z wersją (> = 9.0.1)<br/> — wersje 30 znalezione w usłudze nuget.org [najbliższej wersji: 4.0.0]<br/> — wersje znaleziono 10 w dotnet buildtools [najbliższej wersji: 4.0.0-rc-2129]<br/> -znaleziono 9 wersje w NuGetVolatile [najbliższej wersji: 3.0.0-beta-00032]<br/> -znaleziono wersje 0 w podstawowej platformy dotnet<br/> -znaleziono wersje 0 w dotnet roslyn* |
| **Rozwiązanie** | Edytuj plik projektu, aby poprawić wersji pakietu. Sprawdź także, czy [Konfiguracja nuget projektu](../consume-packages/Configuring-NuGet-Behavior.md) identyfikuje źródła pakietów w sieci spodziewać się przy użyciu. Konieczne może być zmiana wersji requeted, jeśli ten pakiet jest bezpośrednio wywoływany przez projekt. |

### <a name="nu1103"></a>NU1103

| | |
| --- | --- |
| **Problem** | Projekt określony stabilną wersję dla zakresu zależności, ale w zakresie nie znaleziono żadnych wersji stabilnej. Wersje wstępne znaleziono, ale nie są dozwolone. |
| **Przykładowy komunikat** | *Nie można odnaleźć pakietu stabilna NuGet.Versioning z wersją (> = 3.0.0)<br/> — wersje znaleziono 10 w dotnet buildtools [najbliższej wersji: 4.0.0-rc-2129]<br/> -znaleziono 9 wersje w NuGetVolatile [najbliższej wersji: 3.0.0-beta-00032] <br/> -Znaleziono wersje 0 w podstawowej platformy dotnet<br/> -znaleziono wersje 0 w dotnet roslyn* |
| **Rozwiązanie** |  Edytuj zakres wersji w pliku projektu, aby uwzględnić wersje wstępne. Zobacz [wersji pakietu](../reference/Package-Versioning.md). |

### <a name="nu1104"></a>NU1104

| | |
| --- | --- |
| **Problem** | Wskazuje element ProjectReference do pliku, który nie istnieje. |
| **Przykładowy komunikat** | *Odwołanie do projektu nie istnieje "c:\a.csproj". Sprawdź, czy odwołanie do projektu jest prawidłowa i czy istnieje plik projektu.* |
| **Rozwiązanie** | Edytuj plik projektu albo poprawną ścieżkę do przywoływanego projektu lub Usuń odwołanie całkowicie, jeśli nie jest już potrzebne. |

### <a name="nu1105"></a>NU1105

| | |
| --- | --- |
| **Problem** | Plik projektu istnieje, ale go nie dostarczono żadnych informacji przywracania. |
| **Przykładowy komunikat** | *Nie można odczytać informacji o projekcie dla "c:\a.csproj". Plik projektu może być nieprawidłowe lub brakujące elementy docelowe, wymaganych do przywrócenia.* |
| **Rozwiązanie** | W programie Visual Studio błąd może oznaczać, że projekt jest zwolniony, w którym to przypadku ponownie Załaduj projekt. W wierszu polecenia może to oznaczać, że plik jest uszkodzony lub nie zawiera niestandardowego "po imports" potrzebne do odzyskiwania do odczytu do projektu docelowego. Sprawdź, czy plik projektu jest prawidłowa i czy zawiera element docelowy "po imports". |

### <a name="nu1106"></a>NU1106

| | |
| --- | --- |
| **Problem** | Nie można rozpoznać zależności ograniczenia. |
| **Przykładowy komunikat** | *Nie można zrealizować żądań będących w konflikcie dla {id}: {konflikt path} Framework: {docelowy wykres}* |
| **Rozwiązanie** | Edytuj plik projektu, aby określić bardziej uniwersalnym zakresy dla zależności, a nie dokładnej wersji. |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a>NU1107 (wcześniej NU1607)

| | |
| --- | --- |
| **Problem** | Nie można rozpoznać ograniczenia zależności między pakietami. |
| **Przykładowy komunikat** | *Konflikt wersji dla NuGet.Versioning wykryte. Pakiet odwoływać się bezpośrednio z projektu, aby rozwiązać ten problem.<br/>  NuGet.Versioning (= 3.5.0) -> NuGet.Packaging 3.5.0<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)* |
| **Rozwiązanie** | Pakiety z ograniczeniami zależności na dokładną wersję nie zezwalają na inne pakiety w razie potrzeby zwiększyć wersji. Dodaj odwołanie do projektu bezpośrednio (w pliku projektu) na dokładną wersję wymaganą. |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a>NU1108 (wcześniej NU1606)

| | |
| --- | --- |
| **Problem** | Wykryto zależność cykliczną. |
| **Przykładowy komunikat** | *Wykryto cykl: A -> B -> A* |
| **Rozwiązanie** | Pakiet jest w pełni autoryzowane; Skontaktuj się z właścicielem pakietu, aby naprawić ten błąd. |

## <a name="compatibility-errors"></a>Błędy zgodności

[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)

### <a name="nu1201"></a>NU1201

| | |
| --- | --- |
| **Problem** | Zależności projektu nie zawiera struktury zgodne z bieżącego projektu. Zazwyczaj platformę docelową projektu jest wyższą wersję niż odbierającą projektu. |
| **Przykładowy komunikat** | *ServerWeb projektu nie jest zgodny z netstandard1.3 (. Krótkich nazw NETStandard, Version = w wersji 1.3). Projekt obsługuje ServerWeb:<br/> -netstandard1.6 (. Krótkich nazw NETStandard, Version = w wersji 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = 1.0)* |
| **Rozwiązanie** | Zmień platformę docelową projektu na wersję równa lub mniejsza niż odbierającą projektu. |

### <a name="nu1202"></a>NU1202

| | |
| --- | --- |
| **Problem** | Pakiet zależności nie zawiera żadnych zasobów, które są zgodne z projektem. |
| **Przykładowy komunikat** | *Pakiet System.ComponentModel.EventBasedAsync 4.0.11 nie jest zgodny z netstandard1.3 (. Krótkich nazw NETStandard, Version = w wersji 1.3). Pakiet obsługuje System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, wersja = 1.0)<br/> -monotouch10 (MonoTouch, wersja = 1.0)<br/> -net45 (. NETFramework, Version = 4.5)<br/> -netcore50 (. NETCore, Version = v5.0)<br/> -netstandard1.0 (. Krótkich nazw NETStandard, Version = 1.0)<br/> -przenośny net45 + win8 + wp8 + wpa81 (. NETPortable, wersja = v0.0, profil = Profile259)<br/> — Windows 8 (Windows, wersja = w wersji 8.0)<br/> -wp8 (WindowsPhone, wersja = w wersji 8.0)<br/> -wpa81 (WindowsPhoneApp, wersja = v8.1)<br/> — xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*|
| **Rozwiązanie** | Zmień platformę docelową projektu na taki, który obsługuje pakietu. |

### <a name="nu1203"></a>NU1203

| | |
| --- | --- |
| **Problem** | Pakiet nie obsługuje projektu `RuntimeIdentifier`. |
| **Przykładowy komunikat** | *System.Example 1.0.0 udostępnia zestaw odwołania czasu kompilowania dla a.dll na net461, ale nie nie zgodny zestaw czasu wykonywania.* |
| **Rozwiązanie** | Zmień `RuntimeIdentifier` wartości użyte w projekcie, zgodnie z potrzebami. |

### <a name="nu1401"></a>NU1401

| | |
| --- | --- |
| **Problem** | Pakiet wymaga funkcji lub struktur nie są obecnie obsługiwane przez zainstalowaną wersję programu NuGet. |
| **Przykładowy komunikat** | *Pakiet "NuGet.Versioning" wymaga wersji klienta "5.0.0" NuGet lub nowszej, ale bieżąca wersja NuGet to "4.3.0".* |
| **Rozwiązanie** | Zainstaluj nowszą wersję programu NuGet. Zobacz [narzędzia klienta instalowania NuGet](../install-nuget-client-tools.md). |

## <a name="invalid-input-warnings"></a>Nieprawidłowy wejściowy ostrzeżenia

[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)

### <a name="nu1501"></a>NU1501

| | |
| --- | --- |
| **Problem** | Przywracanie projektu próbuje działać na nie został znaleziony. |
| **Przykładowy komunikat** | *Folder "c:\projects\a" nie zawiera projektu do przywrócenia.* |
| **Rozwiązanie** | Uruchamianie przywracania nuget w folderze, który zawiera projekt. |

### <a name="nu1502"></a>NU1502

| | |
| --- | --- |
| **Problem** | `RuntimeSupports` zawiera nieprawidłowy profil. Zazwyczaj obsługuje profil nie został znaleziony w `runtime.json` plik z bieżącego zależności pakietów.|
| **Przykładowy komunikat** | *Profil zgodności nieznany: aaa* |
| **Rozwiązanie** | Sprawdź `RuntimeSupports` wartość w projekcie. |

### <a name="nu1503"></a>NU1503

| | |
| --- | --- |
| **Problem** | Zależności projektu nie importuje obiekty docelowe przywracania NuGet. Ten jest podobny do NU1105, ale w tym miejscu projektu zostanie pominięty i zignorowany zamiast powoduje wszystkie przywracania się niepowodzeniem. W złożonych rozwiązań są często innych typów projektów, które mogą nie obsługiwać przywracania. |
| **Przykładowy komunikat** | *Pomijanie przywracania dla projektu "c:\a.csproj". Plik projektu może być nieprawidłowe lub brakujące elementy docelowe, wymaganych do przywrócenia.* |
| **Rozwiązanie** | Może to nastąpić dla projektów, które nie należy importować wspólne właściwości/cele, które są automatycznie importowane przywracania. Jeśli projekt nie trzeba przywrócić możesz go zignorować. W przeciwnym razie edytować dotyczy projektu, aby dodać elementy docelowe przywracania. |

## <a name="unexpected-package-version-warnings"></a>Nieoczekiwany pakietu wersji ostrzeżenia

[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)

### <a name="nu1601"></a>NU1601

| | |
| --- | --- |
| **Problem** | Zależności bezpośrednich projektu był upadku na wyższą wersję niż określonego projektu. |
| **Przykładowy komunikat** | *Określoną zależnością było NuGet.Versioning (> = 3.5.0), ale ostatecznie otrzymano NuGet.Versioning 4.0.0.* |
| **Rozwiązanie** | Zaktualizuj zależności w projekcie do odpowiedniej wersji. |

### <a name="nu1602"></a>NU1602

| | |
| --- | --- |
| **Problem** | Zależność pakietu brak dolnej granicy. To nie zezwala na przywracania znaleźć *najlepszego dopasowania*. Każdy przywracania będzie przestawiany dół próby znalezienia starszej wersji, który może być używany. Oznacza to, że przywracanie przejdzie do trybu online, aby sprawdzić wszystkie źródła zawsze zamiast pakietów, które już istnieją w folderze pakietów użytkowników. |
| **Przykładowy komunikat** | *NuGet.Packaging 4.0.0 nie zapewnia włącznie dolna granica dla zależności NuGet.Versioning (> 3.5.0). Przybliżony najlepsze dopasowanie 3.6.0 został rozwiązany.* |
| **Rozwiązanie** | Jest to zazwyczaj błąd tworzenia pakietu. Skontaktuj się z autorem pakietu, aby rozwiązać ten problem. |

### <a name="nu1603"></a>NU1603

| | |
| --- | --- |
| **Problem** | Zależność pakietu określonej wersji, którego nie można odnaleźć. Zazwyczaj źródła pakietu nie zawierają wersja oczekiwana dolnej granicy. Nowsza wersja użyto zamiast tego, który różni się od pakietu opracowania przed.<br/><br/>Oznacza to, że przywracanie nie znalazł *najlepszego dopasowania*. Każdy przywracania będzie przestawiany dół próby znalezienia starszej wersji, który może być używany. Oznacza to, że przywracanie przejdzie do trybu online, aby sprawdzić wszystkie źródła zawsze zamiast pakietów, które już istnieją w folderze pakietów użytkowników. |
| **Przykładowy komunikat** | NuGet.Packaging 4.0.0 zależy od NuGet.Versioning (> = 4.0.0), ale nie można odnaleźć 4.0.0. Przybliżony najlepsze dopasowanie 5.0.0 został rozwiązany. |
| **Rozwiązanie** | Jeśli nie zostało zwolnione pakietu oczekiwano może to być błąd tworzenia pakietu. Skontaktuj się z autorem pakietu, aby rozwiązać ten problem. Jeśli pakiet został zwolniony, sprawdź, czy plik jest dostępny na źródła pakietów, którego używasz. Jeśli przy użyciu prywatnych źródła, może być konieczne zaktualizowanie pakietu w tego źródła. |

### <a name="nu1604"></a>NU1604

| | |
| --- | --- |
| **Problem** | Zależności projektu nie definiuje dolną granicą.<br/><br/>Oznacza to, że przywracanie nie znalazł *najlepszego dopasowania*. Każdy przywracania będzie przestawiany dół próby znalezienia starszej wersji, który może być używany. Oznacza to, że przywracanie przejdzie do trybu online, aby sprawdzić wszystkie źródła zawsze zamiast pakietów, które już istnieją w folderze pakietów użytkowników. |
| **Przykładowy komunikat** | *Projekt zależności NuGet.Versioning (< = od 9.0.0) Nowak zawiera włącznie dolnej granicy. Dolna granica należy uwzględnić w wersji zależności, aby zapewnić wyniki przywracania na poziomie.* |
| **Rozwiązanie** | Aktualizowanie projektu `PackageReference` `Version` atrybutu uwzględnienie dolną granicą. |

### <a name="nu1605"></a>NU1605

| | |
| --- | --- |
| **Problem** | Pakiet zależności określić ograniczenia wersji za pomocą nowszej wersji pakietu niż przywracania ostatecznie rozwiązane. Oznacza to z powodu "najbliższej wins" reguła podczas rozpoznawania pakietów, bliżej położonego pakietu na wykresie mogą mieć zastąpione odległymi pakiet. |
| **Przykładowy komunikat** | *Wykryto starszą wersję pakietu: NuGet.Versioning z 4.0.0 do 3.5.0. Odwoływać się bezpośrednio z projektu, aby wybrać inną wersję pakietu.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0* |
| **Rozwiązanie** | Dodaj bezpośrednie odwołanie do projektu do nowszej wersji pakietu, który ma być używany. |

## <a name="resolver-conflict-warnings"></a>Mechanizm rozpoznawania konfliktu ostrzeżenia

### <a name="nu1608"></a>NU1608

| | |
| --- | --- |
| **Problem** | Rozwiązany pakietu jest większa niż umożliwia ograniczenie zależności. Oznacza to, że pakiet bezpośrednio odwołuje się projekt zastępuje ograniczenia zależności z innymi pakietami.|
| **Przykładowy komunikat** | *Wersja pakietu wykrytych poza ograniczenia zależności: x 1.0.0 wymaga y (= 1.0.0), ale wersja y 2.0.0 został rozwiązany.* |
| **Rozwiązanie** | W niektórych przypadkach jest to zamierzone i można pominąć to ostrzeżenie. W przeciwnym razie Zmień odwołanie projektu do pakietu, aby zwiększyć swoje ograniczenia wersji. |

## <a name="package-fallback-warnings"></a>Ostrzeżenia rezerwowy pakietu

### <a name="nu1701"></a>NU1701

| | |
| --- | --- |
| **Problem** | `PackageTargetFallback` / `AssetTargetFallback` użyto Wybierz zasoby z pakietem. Ostrzeżenie powiadomić użytkowników, że zasoby nie mogą być 100% zgodny. |
| **Przykładowy komunikat** | *Pakiet "NuGet.Versioning" został przywrócony przy użyciu "portable net45 + win8" zamiast platformy docelowej projektu "netstandard1.5". Ten pakiet nie może być całkowicie zgodne z projektem.* |
| **Rozwiązanie** | Zmień platformę docelową projektu na taki, który obsługuje pakietu. |

## <a name="feed-warnings"></a>Źródła danych ostrzeżenia

### <a name="nu1801"></a>NU1801

| | |
| --- | --- |
| **Problem** | Wystąpił błąd podczas odczytywania źródła po `IgnoreFailedSources` jest ustawiona na wartość true, konwersją niekrytyczny ostrzeżenie. To może zawierać żadnych komunikatów i jest rodzajowy. |
| **Przykładowy komunikat** | n/d |
| **Rozwiązanie** | Edytuj konfigurację, aby określić prawidłową źródła. |

## <a name="nuget-internal-errors-and-warnings"></a>NuGet wewnętrzne błędy i ostrzeżenia

[NU1000](#nu1000) | [NU1500](#nu1500)

### <a name="nu1000"></a>NU1000

| | |
| --- | --- |
| **Problem** | Nieokreślony błąd wewnętrzny z pakietu NuGet. |
| **Rozwiązanie** | Sprawdź dzienniki, aby uzyskać więcej informacji |

### <a name="nu1500"></a>NU1500

| | |
| --- | --- |
| **Problem** | Nieokreślony ostrzeżenie wewnętrzny z pakietu NuGet. |
| **Rozwiązanie** | Sprawdź dzienniki, aby uzyskać więcej informacji |

## <a name="signed-packages-creation-and-verification"></a>Podpisanych pakietów (tworzenia i weryfikacji)

*NuGet 4.6.0+*

[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)

### <a name="nu3000"></a>NU3000

| | |
| --- | --- |
| **Problem** | Ogólny błąd odnoszące się do podpisywania pakietu i podpisany weryfikacji pakietu. |
| **Rozwiązanie** | Sprawdź dzienniki, aby uzyskać więcej informacji. |

### <a name="nu3001"></a>NU3001

| | |
| --- | --- |
| **Problem** | Nieprawidłowe argumenty albo [zarejestrować polecenia](../tools/cli-ref-sign.md) lub [Sprawdź polecenie](../tools/cli-ref-verify.md). |
| **Rozwiązanie** | Sprawdź i popraw na podstawie podanych argumentów. |

### <a name="nu3002"></a>NU3002

| | |
| --- | --- |
| **Problem** | `-Timestamper` Nie określono opcję z [polecenia nuget znak](../tools/cli-ref-sign.md). |
| **Przykładowy komunikat** | *"-Timestamper" nie określono opcji. Podpisanego pakietu nie jest oznaczony znacznikiem czasowym.* |
| **Rozwiązanie** | Określ `-Timestamper` opcję z `nuget sign`. |

### <a name="nu3004"></a>NU3004

| | |
| --- | --- |
| **Problem** | Dostarczono niepodpisanego pakietu [nuget Sprawdź polecenie](../tools/cli-ref-verify.md). |
| **Rozwiązanie** | Uruchom `nuget verify` przy użyciu podpisanego pakietu. Zobacz [podpisywania pakietu](../create-packages/Sign-a-Package.md). |

### <a name="nu3008"></a>NU3008

| | |
| --- | --- |
| **Problem** | Nie można sprawdzić integralność pakietu, co oznacza, że pakiet podpisany został zmodyfikowany od czasu podpisania. |
| **Rozwiązanie** | Skanowanie komputera za pomocą oprogramowania antywirusowego. Następnie usuń pakiet z komputera, zainstaluj go ponownie i spróbuj ponownie wykonać operację. Jeśli problem będzie się powtarzać, skontaktuj się z właścicielem źródła pakietu i właściciela pakietu. |

### <a name="nu3018"></a>NU3018

| | |
| --- | --- |
| **Problem** | Tworzenie łańcucha certyfikatów nie powiodło się dla podpisu podstawowego. Podstawowy certyfikat podpisywania nie jest zaufane, odwołany, lub informacji o odwołaniu dla certyfikatu jest niedostępny. |
| **Przykładowy komunikat** | *Ostrzeżenie: NU3018: funkcja odwołania nie może sprawdzić odwołania certyfikatu.* |
| **Rozwiązanie** | Użyj zaufanego, ważny certyfikat. Sprawdź łączność z Internetem. |

### <a name="nu3028"></a>NU3028

| | |
| --- | --- |
| **Problem** | Tworzenie łańcucha certyfikatów nie powiodło się dla podpisu sygnatury czasowej. Certyfikat podpisywania sygnatury czasowej nie jest zaufane, odwołany, lub informacji o odwołaniu dla certyfikatu jest niedostępny. |
| **Przykładowy komunikat** | *Ostrzeżenie: NU3028: funkcja odwołania nie może sprawdzić odwołania certyfikatu.* |
| **Rozwiązanie** | Użyj zaufanego, ważny certyfikat. Sprawdź łączność z Internetem. |
