---
title: Informacje o wersji narzędzia NuGet 1,2
description: Informacje o wersji programu NuGet 1,2, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: af2248a41800f7641be9b77d7bb72e2a94d4ce47
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777191"
---
# <a name="nuget-12-release-notes"></a>Informacje o wersji narzędzia NuGet 1,2

Informacje o wersji pakietu [NuGet 1,0 i 1,1](../release-notes/nuget-1.1.md)  |  [Informacje o wersji narzędzia NuGet 1,3](../release-notes/nuget-1.3.md)

Pakiet NuGet 1,2 został wydano 30 marca 2011.

## <a name="new-features"></a>Nowe funkcje

### <a name="framework-profile-support"></a>Obsługa profilu struktury

Z poziomu programu NuGet obsługiwane są różne struktury przeznaczone dla bibliotek. Teraz pakiety mogą zawierać zestawy, które są przeznaczone dla konkretnych profilów, takich jak profil Windows Phone. Aby określić konkretny profil struktury, należy dołączyć myślnik, po którym następuje skrót do profilu. Na przykład w celu ukierunkowania programu SilverLight działającego na Windows Phone (alias Windows Phone 7) można umieścić zestaw w folderze SL3-WP, jak pokazano na poniższym zrzucie ekranu.

![Układ folderów profilu struktury](./media/framework-profile-support.png)

Możesz zadawać, dlaczego nie tylko wybieramy jako moniker "WP7". W części oczekujemy, że Windows Phone 7 może w przyszłości uruchamiać nowszą wersję programu Silverlight. w takim przypadku może być konieczne bardziej szczegółowe informacje na temat tego, który profil platformy jest odwołujących.

### <a name="automatically-add-binding-redirects"></a>Automatycznie Dodaj przekierowania powiązań

W przypadku instalowania pakietu o silnych nazwanych zestawach NuGet może teraz wykrywać przypadki, w których projekt wymaga przekierowania powiązań, aby można je było dodać do pliku konfiguracji, aby projekt mógł zostać skompilowany i automatycznie dodany. Część 3 w blogu David Ebbo na liście wpisów w usłudze NuGet zatytułowana "[dezjednoczenie za pośrednictwem przekierowań powiązań](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" obejmuje przeznaczenie tej funkcji w bardziej szczegółowy sposób.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Określanie odwołań do zestawów struktury (GAC)

W niektórych przypadkach pakiet może zależeć od zestawu, który znajduje się w .NET Framework. Mówiąc ściślej, nie zawsze jest konieczne, aby konsument pakietu odwołuje się do zestawu struktury. Jednak w niektórych przypadkach jest to ważne, na przykład gdy Deweloper musi się zakodować względem typów w tym zestawie, aby można było korzystać z pakietu. Nowy `frameworkAssemblies` element, element podrzędny elementu metadanych, umożliwia określenie zestawu `frameworkAssembly` elementów wskazujących zestaw struktury w pamięci podręcznej GAC. Zanotuj nacisk na zestaw struktury.
Te zestawy nie są uwzględnione w pakiecie, ponieważ zakłada się, że znajdują się one na każdym komputerze w ramach .NET Framework. Poniższa tabela zawiera listę atrybutów `frameworkAssembly` elementu.


|Atrybut |Opis|
|----------------|-----------|
|**assemblyName**|*Wymagane*. Nazwa zestawu, na przykład `System.Net` .|
|**targetFramework**|*Opcjonalne*. Umożliwia określenie struktury i nazwy profilu (lub alias), do których odnosi się ten zestaw platformy, takich jak "net40" lub "SL4". Używa tego samego formatu opisanego w temacie [Obsługa wielu platform docelowych](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe teraz można przechowywać poświadczenia klucza interfejsu API

Korzystając z narzędzia wiersza polecenia nuget.exe, można teraz użyć polecenia SetApiKey w celu zapisania klucza interfejsu API. Dzięki temu nie będzie trzeba określać go przy każdym wypchnięciu pakietu. Aby uzyskać więcej informacji na temat zapisywania klucza interfejsu API za pomocą nuget.exe, [zapoznaj się z dokumentacją dotyczącą publikowania pakietu](../nuget-org/publish-a-package.md).

### <a name="package-explorer"></a>Eksplorator pakietów
Eksplorator pakietów został zaktualizowany do obsługi narzędzia NuGet 1,2. Aby uzyskać więcej informacji, zapoznaj się z informacjami o [wersji Eksploratora pakietów](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Inne funkcje/poprawki

Poprzednia lista była najbardziej zauważalna dla wielu zaimplementowanych funkcji i błędów, które zostały poprawione. Wszystko to we wszystkich implementacjach i stałych [59 elementów roboczych](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) w tej wersji.

## <a name="known-issues"></a>Znane problemy

* **niezgodność pakietów 1,2**: pakiety skompilowane przy użyciu najnowszej wersji narzędzia wiersza polecenia nuget.exe (> 1,2) nie będą działały ze starszymi wersjami dodatku NuGet vs (na przykład 1,1). Jeśli zostanie wyświetlony komunikat o błędzie z informacją o niezgodnym schemacie, wystąpi błąd. Zaktualizuj pakiet NuGet do najnowszej wersji.
* **Niezgodność programu NuGet. Server**: Jeśli przechowujesz wewnętrzne źródło danych NuGet za pomocą projektu NuGet. Server, musisz zaktualizować ten projekt przy użyciu najnowszej wersji programu NuGet. Server.
* **Błąd niezgodności podpisu**: w przypadku wystąpienia błędu podczas uaktualniania z komunikatem o niezgodności podpisów należy najpierw odinstalować pakiet NuGet, a następnie zainstalować go. Ta lista znajduje się na liście [znanych problemów](../release-notes/known-issues.md) , która zawiera więcej szczegółów. Problem dotyczy tylko tych uruchomionych programu Visual Studio 2010 z dodatkiem SP1 i ma zainstalowaną wersję programu NuGet 1,0, która została nieprawidłowo podpisana. Ta wersja była udostępniona tylko z witryny sieci Web CodePlex przez krótki okres, więc ten problem nie ma wpływu na zbyt wiele osób.