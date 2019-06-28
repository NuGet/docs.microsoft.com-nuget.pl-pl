---
title: Informacje o wersji 1.2 NuGet
description: Informacje o wersji programu NuGet 1.2, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5d10d6bf27614980a144c30c3af6f9892a109061
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426186"
---
# <a name="nuget-12-release-notes"></a>Informacje o wersji 1.2 NuGet

[1.0 i 1.1 informacjach o wersji NuGet](../release-notes/nuget-1.1.md) | [informacjach o wersji NuGet 1.3](../release-notes/nuget-1.3.md)

NuGet 1.2 został wydany 30 marca 2011 r.

## <a name="new-features"></a>Nowe funkcje

### <a name="framework-profile-support"></a>Obsługa profilu Framework

Od samego początku obsługiwane o NuGet biblioteki docelowych różnych środowisk. Ale teraz pakietów może zawierać zestawów, przeznaczone dla konkretnych profilów, takich jak profil Windows Phone. Pod kątem określonego profilu strukturę, Dołącz kreską następuje skrót nazwy profilu. Na przykład pod kątem programu SilverLight, systemem Windows Phone (zwane również Windows Phone 7), zestawu można umieścić w folderze systemu wp sl3, jak pokazano na poniższym zrzucie ekranu.

![Framework profilu folderu układu](./media/framework-profile-support.png)

Może poprosić, dlaczego firma Microsoft nie tylko chce użyć "wp7" jako moniker. W części firma Microsoft jest przewidywanie czy Windows Phone 7 mogą zostać uruchomione nowszą wersję programu Silverlight w przyszłości, w którym to przypadku konieczne może być dokładniej, o które środowisko profilu, możesz teraz odwołujących.

### <a name="automatically-add-binding-redirects"></a>Automatycznie dodać przekierowania powiązań

Podczas instalowania pakietu za pomocą silnych nazwanych zestawów, NuGet może teraz wykrywać przypadki, w którym projekt wymaga przekierowania, które mają zostać dodane do pliku konfiguracji, aby projekt, aby skompilować i dodać je automatycznie powiązań. Część 3 David Ebbo serię wpisów w blogu wpis w wersji NuGet prawo "[ujednolicenie za pośrednictwem powiązania przekierowuje](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" obejmuje celem tej funkcji, które bardziej szczegółowo.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Określanie Framework odwołania do zestawów (GAC)

W niektórych przypadkach pakietu może zależeć od zestawu, który znajduje się w programie .NET Framework. Ściśle rzecz ujmując nie zawsze jest to konieczne, czy konsument pakietu odwołują się do zestawu struktury. Ale w niektórych przypadkach jest istotne, np. gdy deweloper potrzebuje kodu typów, w tym zestawie, aby można było używać pakietu. Nowy `frameworkAssemblies` elementu, element podrzędny elementu metadanych pozwala określić zbiór `frameworkAssembly` elementy wskazujący zestaw Framework w GAC. Należy pamiętać, z uwzględnieniem zestawu struktury.
Te zestawy nie są uwzględnione w pakiecie, zgodnie z ich są zakłada się, że na każdym komputerze w ramach programu .NET Framework. W poniższej tabeli przedstawiono atrybuty `frameworkAssembly` elementu.


|Atrybut |Opis|
|----------------|-----------|
|**assemblyName**|*Wymagane*. Nazwa zestawu, takie jak `System.Net`.|
|**targetFramework**|*Opcjonalnie*. Umożliwia określenie nazwy framework i profil (lub alias), ten zestaw framework dotyczy takich jak "net40" lub "sl4". Używa tego samego formatu opisanego w [obsługi wielu platform docelowych](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>teraz nuget.exe jest można przechowywać poświadczenia klucza interfejsu API

Podczas korzystania z narzędzia wiersza polecenia nuget.exe, możesz teraz używać polecenia SetApiKey przechowywać swój klucz interfejsu API. Dzięki temu nie trzeba je określić w każdym wypchnięciu pakietu. Aby uzyskać szczegółowe informacje na temat zapisywania swój klucz interfejsu API z nuget.exe [zapoznaj się z dokumentacją na temat publikowania pakietu](../nuget-org/publish-a-package.md).

### <a name="package-explorer"></a>Eksplorator pakietów
Eksplorator pakietów został zaktualizowany do obsługi NuGet 1.2. Aby uzyskać więcej informacji, zapoznaj się z [informacje o wersji w narzędziu Package Explorer](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Inne funkcje/poprawki

Poprzedniej liście były najbardziej zauważalne w wielu funkcji, które wprowadziliśmy i usterek, którą usunięto. Rzecz biorąc, zaimplementowane/naprawiliśmy [elementów roboczych 59](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) w tej wersji.

## <a name="known-issues"></a>Znane problemy

* **1.2, pakiet niezgodności**: Pakiety skompilowane przy użyciu najnowszej wersji narzędzia wiersza polecenia, nuget.exe (> 1.2) nie będzie działać z poprzednimi wersjami dodatku programu NuGet VS (na przykład 1.1). Jeśli napotkasz komunikat coś o schemacie niezgodne zostały przekroczone tego błędu. Zaktualizuj NuGet do najnowszej wersji.
* **Niezgodność NuGet.Server**: Jeśli przechowujesz NuGet wewnętrznego źródła danych za pomocą programu NuGet.Server project, należy zaktualizować tego projektu z najnowszą wersją NuGet.Server.
* **Błąd niezgodność podpisu**: Jeśli napotkasz błąd podczas uaktualniania z komunikatem o niezgodność podpisu, należy najpierw odinstalować NuGet, a następnie zainstaluj go. To znajduje się w naszym [strony znane problemy](../release-notes/known-issues.md) który zawiera bardziej szczegółowe informacje. Ten problem ma wpływ na komputery z systemem Visual Studio 2010 z dodatkiem SP1 i tylko w wersji 1.0 NuGet zainstalowane, który został niepoprawnie podpisany. Ta wersja tylko podjęto dostępne w witrynie CodePlex przez pewien okres, więc ten problem nie powinien wpływać na zbyt wiele osób.