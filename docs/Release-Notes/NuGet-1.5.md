---
title: Informacje o wersji 1.5 NuGet
description: Informacje o wersji dla tym znanych problemów, poprawki, dodatkowe funkcje i dcr NuGet w wersji 1.5.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1f2f7ebe718ce943faa31b7e19395eead8726648
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-15-release-notes"></a>Informacje o wersji 1.5 NuGet

[Informacje o wersji NuGet 1.4](../release-notes/nuget-1.4.md) | [NuGet w wersji 1.6 informacje o wersji](../release-notes/nuget-1.6.md)

NuGet w wersji 1.5 został wydany 30 sierpnia 2011.

## <a name="features"></a>Funkcje

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Szablony projektu z pakietami NuGet preinstalowane
Podczas tworzenia nowego szablonu projektu programu ASP.NET MVC 3, biblioteki skryptów jQuery zawarty w projekcie faktycznie umieszczone w nim przez instalowanie pakietów NuGet.

Szablon projektu programu ASP.NET MVC 3 zawiera zestaw pakietów NuGet, które zainstalowane po wywołaniu szablonu projektu. Ta możliwość uwzględnienia pakietów NuGet z szablonem projektu jest teraz funkcją NuGet który _żadnych_ szablonu projektu można teraz korzystać z.

Aby uzyskać więcej informacji na temat tej funkcji przeczytaj [wpis w blogu przez dewelopera funkcji](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Odwołania do zestawów jawne

Dodano nową `<references />` element używany do określenia jawnie zestawy, które w pakiecie ma być utworzone odwołanie.

Jeśli na przykład dodaj następujący kod:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Następnie tylko `xunit.dll` i `xunit.extensions.dll` zostanie dodane odwołanie z wykorzystaniem odpowiedniej [podfolder, w ramach profilu](../reference/nuspec.md#explicit-assembly-references) z `lib` folderu, nawet jeśli istnieją innych zestawów w folderze.

Jeśli ten element zostanie pominięty, a następnie stosuje zwykłe zachowanie, czyli odwołać się do każdego zestawu w `lib` folderu.

__Do czego służy ta funkcja?__

Ta funkcja obsługuje tylko zestawy czasu projektowania. Na przykład używając kontraktów kodu zestawów kontraktu musi być obok zestawy środowiska wykonawczego, do których one rozszerzyć, aby można je znaleźć Visual Studio, ale zestawów kontraktu powinien nie faktycznie można odwołuje się projekt i nie powinny być kopiowane do `bin` folderu.

Podobnie funkcja może być używana do dla platform testów jednostkowych, takich jak XUnit, którą musi jego zestawów narzędzia znajdujące się obok zestawy środowiska wykonawczego, ale wyłączone z odwołań do projektu.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Dodano możliwość Wyklucz pliki zawarte w .nuspec
`<file>` w elemencie `.nuspec` plików może służyć do uwzględnienia określonego pliku lub zestawu plików przy użyciu symboli wieloznacznych. Podczas korzystania z symbolem wieloznacznym, nie istnieje sposób wykluczenia konkretnego podzestawu dołączonych plików. Na przykład załóżmy, że chcesz, aby wszystkie pliki tekstowe, w folderze z wyjątkiem określonych.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

Użyj średników do określenia wielu plików.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

Lub użyj symbolu wieloznacznego, aby wykluczyć zestaw plików, na przykład wszystkie pliki kopii zapasowej

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>Usuwanie pakietów, korzystając z okna dialogowego monituje o usunięcie zależności
Podczas odinstalowywania pakietu z zależnościami, wyświetli NuGet, co pozwala na usunięcie zależności pakietów wraz z pakietem.

![Usuwanie pakietów zależnych](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` polecenie poprawy
`Get-Package` Polecenia obsługuje teraz `-ProjectName` parametru. To polecenie

    Get-Package –ProjectName A

Wyświetla wszystkie pakiety zainstalowane w projekcie A.

### <a name="support-for-proxies-that-require-authentication"></a>Obsługa serwerów proxy, które wymagają uwierzytelniania
Gdy używasz serwera proxy wymagającego uwierzytelniania przy użyciu narzędzia NuGet, NuGet teraz wyświetli monit o podanie poświadczeń serwera proxy. Wprowadzanie poświadczeń umożliwia NuGet do nawiązania połączenia ze zdalnego repozytorium.

### <a name="support-for-repositories-that-require-authentication"></a>Obsługa repozytoriów, które wymagają uwierzytelniania
NuGet obsługuje teraz nawiązywania [prywatne repozytoria](../hosting-packages/local-feeds.md) wymagające basic lub uwierzytelniania NTLM.

Obsługa do uwierzytelnienia szyfrowanego zostanie dodana w przyszłej wersji.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Ulepszenia wydajności umożliwiające repozytorium nuget.org
Poprawiono kilka wydajności do galerii nuget.org, aby utworzyć pakiet wyświetlania i szybsze wyszukiwanie.

### <a name="solution-dialog-project-filtering"></a>Filtrowanie projektu okna dialogowego rozwiązania
W oknie rozwiązanie na poziomie monitując o jakie projekty do zainstalowania możemy Pokaż tylko projekty, które są zgodne z wybranego pakietu.

### <a name="package-release-notes"></a>Informacje o wersji pakietu
Pakiety NuGet teraz obejmuje obsługę wersji. Informacje o wersji Pokazuj tylko się podczas wyświetlania _aktualizacje_ dla pakietu, więc go nie ma sensu je dodać do Twojego pierwszego wydania.

![Informacje o wersji w karcie Aktualizacje](./media/manage-nuget-packages-release-notes.png)

Aby dodać informacje o wersji do pakietu, należy użyć nowego `<releaseNotes />` metadane elementu w pliku NuSpec.

### <a name="nuspec-ltfiles-gt-improvement"></a>.nuspec & ltfiles /&gt; poprawy jakości
`.nuspec` Pliku umożliwia teraz pusty `<files />` element, który informuje nuget.exe pozwalające nie zawiera plików w pakiecie.

## <a name="bug-fixes"></a>Poprawki błędów
NuGet w wersji 1.5 było łącznie 107 stałej elementów roboczych. 103 tych zostały oznaczone jako usterki.

Pełną listę prac elementów usunięto w wersji NuGet w wersji 1.5, sprawdź widok [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Warto zauważyć, poprawki:

* [Problem 1273](http://nuget.codeplex.com/workitem/1273): wprowadzone `packages.config` przyjazną alfabetycznie sortowanie pakietów i usunięcia spacji dodatkowe więcej kontroli wersji.
* [Problem 844](http://nuget.codeplex.com/workitem/844): numery wersji są teraz znormalizowany, aby `Install-Package 1.0` działa na pakiet z wersją `1.0.0`.
* [Problem 1060](http://nuget.codeplex.com/workitem/1060): podczas tworzenia pakietu przy użyciu nuget.exe, `-Version` Flaga zastąpienia `<version />` elementu.
