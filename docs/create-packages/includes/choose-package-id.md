---
ms.openlocfilehash: c92f6e0c34347ee8555d416140d95ea2df5a3fbb
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610548"
---
Identyfikator pakietu i numer wersji są dwie najważniejsze wartości w projekcie, ponieważ jednoznacznie zidentyfikować dokładny kod, który jest zawarty w pakiecie.

**Najważniejsze wskazówki dotyczące identyfikatora pakietu:**

- **Unikatowość:** identyfikator musi być unikatowy w nuget.org lub dowolnej galerii hostuje pakiet. Przed podjęciem decyzji o identyfikatorze przeszukaj odpowiednią galerię, aby sprawdzić, czy nazwa jest już używana. Aby uniknąć konfliktów, dobrym wzorcem jest użycie nazwy firmy jako pierwszej `Contoso.`części identyfikatora, takiej jak .
- Nazwy podobne do **przestrzeni nazw:** Postępuj zgodnie ze wzorcem podobnym do obszarów nazw w domenie .NET, używając notacji kropkowej zamiast łączników. Na przykład `Contoso.Utility.UsefulStuff` użyj, `Contoso-Utility-UsefulStuff` `Contoso_Utility_UsefulStuff`a nie lub . Konsumenci również znaleźć przydatne, gdy identyfikator pakietu pasuje do obszarów nazw używanych w kodzie.
- **Przykładowe pakiety:** Jeśli tworzysz pakiet przykładowego kodu, który `.Sample` pokazuje, jak używać innego pakietu, `Contoso.Utility.UsefulStuff.Sample`dołącz jako sufiks do identyfikatora, jak w . (Przykładowy pakiet będzie oczywiście zależny od innego pakietu.) Podczas tworzenia przykładowego pakietu `contentFiles` użyj `<IncludeAssets>`wartości w pliku . W `content` folderze rozmieść przykładowy `\Samples\<identifier>` kod `\Samples\Contoso.Utility.UsefulStuff.Sample`w folderze o nazwie w pliku .

**Najważniejsze wskazówki dotyczące wersji pakietu:**

- Ogólnie rzecz biorąc ustaw wersję pakietu, aby dopasować projekt (lub zestaw), chociaż nie jest to ściśle wymagane. Jest to prosta sprawa, gdy ograniczysz pakiet do pojedynczego zestawu. Ogólnie rzecz biorąc, należy pamiętać, że NuGet sam zajmuje się wersjami pakietów podczas rozpoznawania zależności, a nie wersji zestawu.
- Korzystając z niestandardowego schematu wersji, należy wziąć pod uwagę reguły wersji NuGet, jak wyjaśniono w [wersji pakietu.](../../concepts/package-versioning.md) NuGet jest w większości [zgodny z semver 2](../../concepts/package-versioning.md#semantic-versioning-200).

> Aby uzyskać informacje na temat rozpoznawania zależności, zobacz [Rozpoznawanie zależności za pomocą packagereference](../../concepts/dependency-resolution.md#dependency-resolution-with-packagereference). Aby uzyskać starsze informacje, które mogą być również pomocne w lepszym zrozumieniu przechowywania wersji, zobacz tę serię wpisów w blogu.
>
> - [Część 1: Biorąc na DLL Hell](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Część 2: Podstawowy algorytm](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Część 3: Ujednolicenie za pomocą przekierowań wiążących](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)
