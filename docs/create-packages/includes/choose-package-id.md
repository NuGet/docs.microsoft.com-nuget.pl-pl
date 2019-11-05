---
ms.openlocfilehash: c92f6e0c34347ee8555d416140d95ea2df5a3fbb
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610548"
---
Identyfikator pakietu i numer wersji to dwie najważniejsze wartości w projekcie, ponieważ jednoznacznie identyfikują dokładny kod zawarty w pakiecie.

**Najlepsze rozwiązania dotyczące identyfikatora pakietu:**

- **Unikatowość**: Identyfikator musi być unikatowy w obrębie NuGet.org lub dowolnej galerii, w której znajduje się pakiet. Przed podjęciem decyzji o identyfikatorze Przeszukaj stosowną galerię, aby sprawdzić, czy nazwa jest już używana. Aby uniknąć konfliktów, dobrym wzorcem jest użycie nazwy firmy jako pierwszej części identyfikatora, takiej jak `Contoso.`.
- **Nazwy podobne do nazw**: Postępuj zgodnie ze wzorcem podobnym do przestrzeni nazw w programie .NET przy użyciu notacji kropkowej zamiast łączników. Na przykład użyj `Contoso.Utility.UsefulStuff`, a nie `Contoso-Utility-UsefulStuff` lub `Contoso_Utility_UsefulStuff`. Konsumenci są również pomocne, gdy identyfikator pakietu jest zgodny z przestrzeniami nazw używanymi w kodzie.
- **Przykładowe pakiety**: w przypadku tworzenia pakietu przykładowego kodu, który demonstruje sposób użycia innego pakietu, należy dołączyć `.Sample` jako sufiks do identyfikatora, jak w `Contoso.Utility.UsefulStuff.Sample`. (Przykładowy pakiet jest oczywiście zależny od innego pakietu). Podczas tworzenia przykładowego pakietu Użyj wartości `contentFiles` w `<IncludeAssets>`. W folderze `content` Rozmieść przykładowy kod w folderze o nazwie `\Samples\<identifier>` jako `\Samples\Contoso.Utility.UsefulStuff.Sample`.

**Najlepsze rozwiązania dotyczące wersji pakietu:**

- Ogólnie rzecz biorąc Ustaw wersję pakietu na zgodną z projektem (lub zestawem), ale nie jest to ściśle wymagane. Jest to prosta kwestia w przypadku ograniczenia pakietu do jednego zestawu. Ogólnie, pamiętaj, że sam pakiet NuGet zajmuje się wersjami pakietu podczas rozpoznawania zależności, a nie wersji zestawu.
- W przypadku korzystania ze schematu wersji niestandardowej należy wziąć pod uwagę reguły obsługi wersji NuGet zgodnie z opisem w temacie [wersja pakietu](../../concepts/package-versioning.md). Pakiet NuGet jest w większości [semver 2 zgodny](../../concepts/package-versioning.md#semantic-versioning-200).

> Aby uzyskać informacje dotyczące rozpoznawania zależności, zobacz [rozpoznawanie zależności z PackageReference](../../concepts/dependency-resolution.md#dependency-resolution-with-packagereference). Aby poznać starsze informacje, które mogą być przydatne do lepszego zrozumienia wersji, zobacz tę serię wpisów w blogu.
>
> - [Część 1: pobieranie biblioteki DLL Hell](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Część 2: podstawowy algorytm](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Część 3: ujednolicenie za pośrednictwem przekierowań powiązań](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)
