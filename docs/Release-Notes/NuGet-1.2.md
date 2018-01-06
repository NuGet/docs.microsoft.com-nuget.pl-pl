---
title: Informacje o wersji NuGet 1.2 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 48f23141-b2ad-4cdf-8d81-7bb6b9419aa6
description: "Informacje o wersji NuGet 1.2 tym znanych problemów, poprawki, dodatkowe funkcje i dcr."
keywords: Wersji NuGet 1.2 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 79e82f19d2be96fee3832eeb24ebb443aebc2b64
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-12-release-notes"></a>Informacje o wersji 1.2 NuGet

[Wersji 1.0 i 1.1 NuGet](../release-notes/nuget-1.1.md) | [NuGet 1.3 informacje o wersji](../release-notes/nuget-1.3.md)

Wersji NuGet 1.2 wydanej w dniu 30 marca 2011.

## <a name="new-features"></a>Nowe funkcje

### <a name="framework-profile-support"></a>Obsługa profilu Framework

Od początku, NuGet obsługiwane o różnych platform docelowych bibliotek. Ale teraz opakowania mogą zawierać zestawy przeznaczonych dla określonych profilów, takie jak profil Windows Phone. Pod kątem określonego profilu RAM, Dołącz łącznikiem następuje skrót profilu. Na przykład pod kątem SilverLight systemem Windows Phone (alias Windows Phone 7), możesz umieścić zestaw w folderze sl3 wp, jak pokazano na poniższym zrzucie ekranu.

![Framework profilu folderu układu](./media/framework-profile-support.png)

Może poprosić o dlaczego właśnie nie został wybrany do użycia jako moniker "wp7". W części firma Microsoft jest przewidywanie czy Windows Phone 7 mogą zostać uruchomione nowszej wersji Silverlight w przyszłości, dotyczących w takim przypadku konieczne może być bardziej szczegółowe informacje w ramach których profil, możesz w przypadku.

### <a name="automatically-add-binding-redirects"></a>Automatycznie Dodaj przekierowania powiązania

Podczas instalowania pakietu z silną nazwane zestawy, NuGet może teraz wykrywać przypadków, gdy projekt wymaga przekierowania do dodania do pliku konfiguracji, aby projekt, aby skompilować i automatyczne dodawanie powiązań. Część 3 serii post na blogu Ebbo Dominik w wersji NuGet pod tytułem "[ujednolicenie za pośrednictwem powiązania przekierowuje](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" obejmuje celem tej funkcji w bardziej szczegółowe informacje.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Określanie Framework odwołania do zestawów (GAC)

W niektórych przypadkach pakietu może zależeć od zestawu, który znajduje się w programie .NET Framework. Mówiąc ściślej nie zawsze jest konieczne, że konsumenta pakietu odwoływać się do zestawu framework. Jednak w niektórych przypadkach jest ważne, na przykład gdy dewelopera potrzebuje kodu dla typów w tym zestawie, aby można było używać pakietu. Nowy `frameworkAssemblies` elementu i elementem podrzędnym elementu metadanych służy do określenia zestawu `frameworkAssembly` elementy wskazujący zestawem struktury w pamięci GAC. Należy pamiętać, z uwzględnieniem zestawu struktury.
Te zestawy nie znajdują się w pakiecie zgodnie z ich są rozpatrywane na każdym komputerze w ramach programu .NET Framework. W poniższej tabeli przedstawiono atrybuty `frameworkAssembly` elementu.


|Atrybut |Opis|
|----------------|-----------|
|**assemblyName**|*Wymagane*. Nazwa zestawu, takich jak `System.Net`.|
|**targetFramework**|*Opcjonalne*. Umożliwia określenie nazwy framework i profilu (lub alias) stosowanym przez ten zestaw framework do takich jak "net40" lub "sl4". Używa tego samego formatu opisanego w [obsługi wielu platform docelowych](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>teraz nuget.exe jest możliwość przechowywania poświadczeń klucz interfejsu API

Korzystając z narzędzia wiersza polecenia nuget.exe, można teraz używać polecenia SetApiKey do przechowywania klucza interfejsu API. W ten sposób, nie należy określić go za każdym razem, gdy push pakietu. Aby uzyskać więcej informacji o zapisywaniu klucza interfejsu API z nuget.exe [przeczytaj dokumentację dotyczącą publikowania pakietu](../create-packages/publish-a-package.md).

### <a name="package-explorer"></a>Pakiet Eksploratora
Pakiet Eksploratora została zaktualizowana do obsługi wersji NuGet 1.2. Aby uzyskać więcej informacji, zapoznaj się z [Explorer pakietu wersji](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Funkcji i poprawek

Najłatwiej zauważyć wiele funkcji, które wprowadziliśmy i usterki, które usunięto zostały poprzedniej liście. Ogólnie biorąc, zaimplementowana/usunięto [elementy robocze 59](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) w tej wersji.

## <a name="known-issues"></a>Znane problemy

* **1.2 pakietu niezgodności**: pakiety skompilowanej za pomocą najnowszej wersji narzędzia wiersza polecenia, nuget.exe (> 1.2) nie będzie działać ze starszymi wersjami programu NuGet VS dodatek (na przykład 1.1). Jeśli napotkasz komunikat coś o schemacie niezgodne używasz do tego błędu. Zaktualizuj NuGet do najnowszej wersji.
* **Niezgodność NuGet.Server**: Jeśli przechowujesz NuGet wewnętrznego źródła danych za pomocą programu NuGet.Server project, musisz zaktualizować tego projektu do najnowszej wersji NuGet.Server.
* **Błąd niezgodność podpisu**: Jeśli napotkasz błąd podczas uaktualniania z następującym komunikatem o niezgodność podpisu, musisz najpierw odinstalować NuGet, a następnie zainstaluj go. Jest to wymienione w naszym [strony znane problemy](../release-notes/Known-Issues.md) zapewniające więcej szczegółów. Problem ma wpływ tylko uruchomione Visual Studio 2010 z dodatkiem SP1 i zainstalowana wersja 1.0 NuGet zainstalowane, który został podpisany niepoprawnie. Ta wersja została tylko udostępniona w witrynie CodePlex przez krótki czas, ten problem nie ma wpływu na zbyt wiele osób.