---
ms.openlocfilehash: e8949e9964ed19d342df53f08f59bb0f89e5feb0
ms.sourcegitcommit: 5aa49478dc466c67db5c3edda7c6ce8dcd8ae033
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2019
ms.locfileid: "68817478"
---
Identyfikator pakietu i numer wersji to dwie najważniejsze wartości w projekcie, ponieważ jednoznacznie identyfikują dokładny kod zawarty w pakiecie.

**Najlepsze rozwiązania dotyczące identyfikatora pakietu:**

- **Unikatowość**: Identyfikator musi być unikatowy w obrębie nuget.org lub dowolnej galerii, w której znajduje się pakiet. Przed podjęciem decyzji o identyfikatorze Przeszukaj stosowną galerię, aby sprawdzić, czy nazwa jest już używana. Aby uniknąć konfliktów, dobrym wzorcem jest użycie nazwy firmy jako pierwszej części identyfikatora, na przykład `Contoso.`.
- **Nazwy podobne do nazw**: Postępuj zgodnie ze wzorcem podobnym do przestrzeni nazw w programie .NET przy użyciu notacji kropkowej zamiast łączników. Na przykład użyj `Contoso.Utility.UsefulStuff` `Contoso-Utility-UsefulStuff` zamiast lub `Contoso_Utility_UsefulStuff`. Konsumenci są również pomocne, gdy identyfikator pakietu jest zgodny z przestrzeniami nazw używanymi w kodzie.
- **Przykładowe pakiety**: Jeśli utworzysz pakiet przykładowego kodu, który pokazuje, jak używać innego pakietu, Dołącz `.Sample` jako sufiks do identyfikatora, jak w. `Contoso.Utility.UsefulStuff.Sample` (Przykładowy pakiet jest oczywiście zależny od innego pakietu). Podczas tworzenia przykładowego pakietu Użyj `contentFiles` wartości w. `<IncludeAssets>` W folderze Rozmieść przykładowy kod w folderze o nazwie `\Samples\<identifier>` w `\Samples\Contoso.Utility.UsefulStuff.Sample`. `content`

**Najlepsze rozwiązania dotyczące wersji pakietu:**

- Ogólnie rzecz biorąc Ustaw wersję pakietu na zgodną z projektem (lub zestawem), ale nie jest to ściśle wymagane. Jest to prosta kwestia w przypadku ograniczenia pakietu do jednego zestawu. Ogólnie, pamiętaj, że sam pakiet NuGet zajmuje się wersjami pakietu podczas rozpoznawania zależności, a nie wersji zestawu.
- W przypadku korzystania ze schematu wersji niestandardowej należy wziąć pod uwagę reguły obsługi wersji NuGet zgodnie z opisem w temacie [wersja pakietu](../../reference/package-versioning.md). Pakiet NuGet jest w większości [semver 2 zgodny](../../reference/package-versioning.md#semantic-versioning-200).

> Aby uzyskać informacje dotyczące rozpoznawania zależności, zobacz [rozpoznawanie zależności z PackageReference](../../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference). Aby poznać starsze informacje, które mogą być przydatne do lepszego zrozumienia wersji, zobacz tę serię wpisów w blogu.
>
> - [Część 1. Pobieranie na Hell DLL](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Część 2. Podstawowy algorytm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Część 3: Ujednolicenie za pomocą przekierowań powiązań](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)