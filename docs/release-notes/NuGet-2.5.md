---
title: Informacje o wersji narzędzia NuGet 2,5
description: Informacje o wersji programu NuGet 2,5, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940582d5173f5a53dcd04cf1258fc02a2439af4e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237089"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="07146-103">Informacje o wersji narzędzia NuGet 2,5</span><span class="sxs-lookup"><span data-stu-id="07146-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="07146-104">Informacje o wersji pakietu [NuGet 2.2.1](../release-notes/nuget-2.2.1.md)  |  [Informacje o wersji narzędzia NuGet 2,6](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="07146-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="07146-105">Pakiet NuGet 2,5 został wydaną 25 kwietnia 2013.</span><span class="sxs-lookup"><span data-stu-id="07146-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="07146-106">Ta wersja była bardzo duża, dlatego warto pominąć wersje 2,3 i 2,4.</span><span class="sxs-lookup"><span data-stu-id="07146-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="07146-107">To jest największa wersja pakietu NuGet z ponad [160 elementami roboczymi](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) w wersji.</span><span class="sxs-lookup"><span data-stu-id="07146-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="07146-108">Podziękowania</span><span class="sxs-lookup"><span data-stu-id="07146-108">Acknowledgements</span></span>

<span data-ttu-id="07146-109">Chcemy podziękowanie następujących zewnętrznych współautorom w celu uzyskania znaczących wkładów do programu NuGet 2,5:</span><span class="sxs-lookup"><span data-stu-id="07146-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="07146-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ( [@dsplaisted](https://twitter.com/dsplaisted) )</span><span class="sxs-lookup"><span data-stu-id="07146-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="07146-111">[#2847](https://nuget.codeplex.com/workitem/2847) — Dodaj do listy znanych identyfikatorów platformy docelowej systemy Android i platformy monomac, a także opcję z nich.</span><span class="sxs-lookup"><span data-stu-id="07146-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="07146-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ( [@knocte](https://twitter.com/knocte) )</span><span class="sxs-lookup"><span data-stu-id="07146-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="07146-113">[#2865](https://nuget.codeplex.com/workitem/2865) — poprawianie pisowni `NuGet.targets` dla systemu operacyjnego uwzględniającego wielkość liter</span><span class="sxs-lookup"><span data-stu-id="07146-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="07146-114">[David Fowlera](https://www.codeplex.com/site/users/view/dfowler) ( [@davidfowl](https://twitter.com/davidfowl) )</span><span class="sxs-lookup"><span data-stu-id="07146-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="07146-115">Utwórz rozwiązanie na mono.</span><span class="sxs-lookup"><span data-stu-id="07146-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="07146-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ( [@atheken](https://twitter.com/atheken) )</span><span class="sxs-lookup"><span data-stu-id="07146-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="07146-117">Napraw testy jednostkowe zakończone niepowodzeniem na mono.</span><span class="sxs-lookup"><span data-stu-id="07146-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="07146-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ( [@OliIsCool](https://twitter.com/oliiscool) )</span><span class="sxs-lookup"><span data-stu-id="07146-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="07146-119">polecenie [#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe Pack nie propaguje właściwości do programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="07146-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="07146-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ( [@bajtos](https://twitter.com/bajtos) )</span><span class="sxs-lookup"><span data-stu-id="07146-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="07146-121">[#1511](https://nuget.codeplex.com/workitem/1511) -zmodyfikowano kod obsługi XML, aby zachować formatowanie.</span><span class="sxs-lookup"><span data-stu-id="07146-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="07146-122">[Adam pracownik2](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )</span><span class="sxs-lookup"><span data-stu-id="07146-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="07146-123">Dodano rozpoznane wyrazy do słownika niestandardowego, aby zezwolić programowi Build. cmd na pomyślne zakończenie.</span><span class="sxs-lookup"><span data-stu-id="07146-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="07146-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="07146-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="07146-125">Napraw testy jednostkowe w przypadku uruchamiania w lokalizacji zlokalizowanej i</span><span class="sxs-lookup"><span data-stu-id="07146-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="07146-126">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="07146-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="07146-127">Wyodrębniony interfejs z PackageService</span><span class="sxs-lookup"><span data-stu-id="07146-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="07146-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ( [@brugidou](https://twitter.com/brugidou) )</span><span class="sxs-lookup"><span data-stu-id="07146-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="07146-129">[#936](https://nuget.codeplex.com/workitem/936) — obsługa zależności projektu podczas pakowania</span><span class="sxs-lookup"><span data-stu-id="07146-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="07146-130">[Xavier](https://www.codeplex.com/site/users/view/XavierDecoster) ( [@XavierDecoster](https://twitter.com/xavierdecoster) )</span><span class="sxs-lookup"><span data-stu-id="07146-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="07146-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) — obsługa hasła czystego tekstu podczas zapisywania poświadczeń źródła pakietu w plikach NuGet. cofig</span><span class="sxs-lookup"><span data-stu-id="07146-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="07146-132">[Odłogi](http://www.codeplex.com/site/users/view/jmanning) ( [@manningj](https://twitter.com/manningj) )</span><span class="sxs-lookup"><span data-stu-id="07146-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="07146-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -Fix Get-Package opis pomocy</span><span class="sxs-lookup"><span data-stu-id="07146-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="07146-134">Doceniamy również następujące osoby do znajdowania usterek z pakietem NuGet 2,5 beta/RC, które zostały zatwierdzone i naprawione przed ostateczną wersją:</span><span class="sxs-lookup"><span data-stu-id="07146-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="07146-135">[Ścianka której należy Tony](https://www.codeplex.com/site/users/view/CodeChief) ( [@CodeChief](https://twitter.com/codechief) )</span><span class="sxs-lookup"><span data-stu-id="07146-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="07146-136">[#3200](https://nuget.codeplex.com/workitem/3200) -MSTest przerwany z ostatnimi kompilacjami NuGet 2,4 i 2,5</span><span class="sxs-lookup"><span data-stu-id="07146-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="07146-137">Istotne funkcje w wersji</span><span class="sxs-lookup"><span data-stu-id="07146-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="07146-138">Zezwalaj użytkownikom na zastępowanie już istniejących plików zawartości</span><span class="sxs-lookup"><span data-stu-id="07146-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="07146-139">Jedną z najbardziej pożądanych funkcji całego czasu było możliwość zastępowania plików zawartości, które już istnieją na dysku, gdy są zawarte w pakiecie NuGet.</span><span class="sxs-lookup"><span data-stu-id="07146-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="07146-140">Począwszy od programu NuGet 2,5, te konflikty są identyfikowane i zostanie wyświetlony monit o zastąpienie plików, podczas gdy wcześniej te pliki były zawsze pomijane.</span><span class="sxs-lookup"><span data-stu-id="07146-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Zastąp pliki zawartości](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="07146-142">Elementy "nuget.exe Update" i "Install-Package" teraz mają nową opcję "-FileConflictAction", aby ustawić niektóre wartości domyślne dla scenariuszy wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="07146-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="07146-143">Ustaw domyślną akcję, gdy plik z pakietu już istnieje w projekcie docelowym.</span><span class="sxs-lookup"><span data-stu-id="07146-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="07146-144">Ustaw wartość "Zastąp", aby zawsze zastępować pliki.</span><span class="sxs-lookup"><span data-stu-id="07146-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="07146-145">Ustaw na wartość "Ignoruj", aby pominąć pliki.</span><span class="sxs-lookup"><span data-stu-id="07146-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="07146-146">Jeśli nie zostanie określony, zostanie wyświetlony monit o podanie każdego pliku powodującego konflikt.</span><span class="sxs-lookup"><span data-stu-id="07146-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="07146-147">Automatyczne Importowanie elementów docelowych programu MSBuild i plików props</span><span class="sxs-lookup"><span data-stu-id="07146-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="07146-148">Nowy konwencjonalny folder został utworzony na najwyższym poziomie pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="07146-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="07146-149">Jako element równorzędny do `\lib` , `\content` , i `\tools` , możesz teraz dołączyć `\build` folder do pakietu.</span><span class="sxs-lookup"><span data-stu-id="07146-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="07146-150">W tym folderze można umieścić dwa pliki o stałych nazwach `{packageid}.targets` lub `{packageid}.props` .</span><span class="sxs-lookup"><span data-stu-id="07146-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="07146-151">Te dwa pliki mogą znajdować się bezpośrednio w folderze `build` lub w obszarze folderów specyficznych dla platformy, podobnie jak w przypadku innych folderów.</span><span class="sxs-lookup"><span data-stu-id="07146-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="07146-152">Reguła wybierania najlepszego dopasowanego folderu struktury jest dokładnie taka sama jak w przypadku tych.</span><span class="sxs-lookup"><span data-stu-id="07146-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="07146-153">Gdy narzędzie NuGet zainstaluje pakiet z plikami \Build, doda element programu MSBuild `<Import>` w pliku projektu wskazujący `.targets` `.props` pliki i.</span><span class="sxs-lookup"><span data-stu-id="07146-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="07146-154">`.props`Plik zostanie dodany u góry, natomiast `.targets` plik zostanie dodany na końcu.</span><span class="sxs-lookup"><span data-stu-id="07146-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="07146-155">Określ różne odwołania na platformę przy użyciu `<References/>` elementu</span><span class="sxs-lookup"><span data-stu-id="07146-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="07146-156">Przed 2,5, w `.nuspec` pliku, użytkownik może określić tylko pliki referencyjne, które mają być dodane do wszystkich platform.</span><span class="sxs-lookup"><span data-stu-id="07146-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="07146-157">Teraz dzięki tej nowej funkcji w 2,5, użytkownik może utworzyć `<reference/>` element dla każdej z obsługiwanych platform, na przykład:</span><span class="sxs-lookup"><span data-stu-id="07146-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

<span data-ttu-id="07146-158">Oto przepływ, dla którego NuGet dodaje odwołania do projektów opartych na `.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="07146-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="07146-159">Znajdź `lib` folder, który jest odpowiedni dla platformy docelowej, i Pobierz listę zestawów z tego folderu</span><span class="sxs-lookup"><span data-stu-id="07146-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="07146-160">Oddzielnie Znajdź grupę odwołania, która jest odpowiednia dla platformy docelowej i Pobierz listę zestawów z tej grupy.</span><span class="sxs-lookup"><span data-stu-id="07146-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="07146-161">Grupa odwołania bez określonej platformy docelowej jest grupą rezerwową.</span><span class="sxs-lookup"><span data-stu-id="07146-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="07146-162">Znajdź część wspólną dwóch list i użyj jej jako odwołań do dodania</span><span class="sxs-lookup"><span data-stu-id="07146-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="07146-163">Ta nowa funkcja umożliwi autorom pakietów używanie funkcji odwołań do stosowania podzestawów zestawów w różnych strukturach, gdy w przeciwnym razie konieczne będzie przeprowadzenie zduplikowanych zestawów w wielu `lib` folderach.</span><span class="sxs-lookup"><span data-stu-id="07146-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="07146-164">Uwaga: Aby korzystać z tej funkcji, musisz użyć pakietu nuget.exe Pack; Eksplorator pakietów NuGet jeszcze go nie obsługuje.</span><span class="sxs-lookup"><span data-stu-id="07146-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="07146-165">Przycisk Aktualizuj wszystko, aby zezwolić na jednoczesną aktualizację wszystkich pakietów</span><span class="sxs-lookup"><span data-stu-id="07146-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="07146-166">Wiele informacji na temat polecenia cmdlet programu PowerShell "Update-Package" w celu zaktualizowania wszystkich pakietów jest możliwe. Teraz można łatwo wykonać tę czynność za pomocą interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="07146-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="07146-167">Aby wypróbować tę funkcję:</span><span class="sxs-lookup"><span data-stu-id="07146-167">To try this feature out:</span></span>

1. <span data-ttu-id="07146-168">tworzenie nowej aplikacji platformy ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="07146-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="07146-169">Uruchom okno dialogowe Zarządzanie pakietami NuGet</span><span class="sxs-lookup"><span data-stu-id="07146-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="07146-170">Wybierz pozycję "aktualizacje"</span><span class="sxs-lookup"><span data-stu-id="07146-170">Select 'Updates'</span></span>
1. <span data-ttu-id="07146-171">Kliknij przycisk "Aktualizuj wszystko"</span><span class="sxs-lookup"><span data-stu-id="07146-171">Click the 'Update All' button</span></span>

![Przycisk Aktualizuj wszystko w oknie dialogowym](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="07146-173">Ulepszona obsługa odwołań projektu dla pakietu nuget.exe</span><span class="sxs-lookup"><span data-stu-id="07146-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="07146-174">Teraz nuget.exe pakiety poleceń pakietów, do których odwołują się projekty z następującymi regułami:</span><span class="sxs-lookup"><span data-stu-id="07146-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="07146-175">Jeśli przywoływany projekt ma odpowiedni `.nuspec` plik, na przykład plik o nazwie `proj1.nuspec` w tym samym folderze co `proj1.csproj` , ten projekt jest dodawany jako zależność do pakietu, przy użyciu identyfikatora i wersji Odczytaj z `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="07146-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="07146-176">W przeciwnym razie pliki projektu, do którego istnieje odwołanie, są powiązane z pakietem.</span><span class="sxs-lookup"><span data-stu-id="07146-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="07146-177">Następnie projekty, do których odwołuje się ten projekt, zostaną przetworzone cyklicznie przy użyciu tych samych reguł.</span><span class="sxs-lookup"><span data-stu-id="07146-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="07146-178">`.pdb`Dodawane są wszystkie pliki dll, i `.exe` .</span><span class="sxs-lookup"><span data-stu-id="07146-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="07146-179">Wszystkie inne pliki zawartości są dodawane.</span><span class="sxs-lookup"><span data-stu-id="07146-179">All other content files are added.</span></span>
1. <span data-ttu-id="07146-180">Wszystkie zależności są scalane.</span><span class="sxs-lookup"><span data-stu-id="07146-180">All dependencies are merged.</span></span>

<span data-ttu-id="07146-181">Dzięki temu projekt, do którego istnieje odwołanie, może być traktowany jako zależność, jeśli istnieje `.nuspec` plik, jest częścią pakietu.</span><span class="sxs-lookup"><span data-stu-id="07146-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="07146-182">Więcej szczegółów znajduje się tutaj: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="07146-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="07146-183">Dodaj właściwość "minimalna wersja NuGet" do pakietów</span><span class="sxs-lookup"><span data-stu-id="07146-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="07146-184">Nowy atrybut metadanych o nazwie "minClientVersion" może teraz wskazywać minimalną wersję klienta NuGet wymaganą do korzystania z pakietu.</span><span class="sxs-lookup"><span data-stu-id="07146-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="07146-185">Ta funkcja pomaga autorowi pakietu określić, że pakiet będzie działał tylko po określonej wersji programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="07146-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="07146-186">`.nuspec`Po dodaniu nowych funkcji programu nuget 2,5 pakiety będą mogły przejąć minimalną wersję narzędzia NuGet.</span><span class="sxs-lookup"><span data-stu-id="07146-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="07146-187">Jeśli użytkownik ma zainstalowaną program NuGet 2,5, a pakiet jest identyfikowany jako wymagający 2,6, podpowiedzi wizualne zostaną przekazane Użytkownikowi wskazującym, że pakiet nie zostanie zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="07146-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="07146-188">Użytkownik będzie następnie mógł zaktualizować swoją wersję programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="07146-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="07146-189">Poprawi to istniejące środowisko, w którym rozpocznie się instalacja pakietów, ale kończy się niepowodzeniem wskazujących, że zidentyfikowano nierozpoznaną wersję schematu.</span><span class="sxs-lookup"><span data-stu-id="07146-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="07146-190">Zależności nie są już niepotrzebne do aktualizacji podczas instalacji pakietu</span><span class="sxs-lookup"><span data-stu-id="07146-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="07146-191">Przed pakietem NuGet 2,5, podczas instalowania pakietu, który jest zależny od pakietu już zainstalowanego w projekcie, zależność zostanie zaktualizowana w ramach nowej instalacji, nawet jeśli istniejąca wersja spełnia tę zależność.</span><span class="sxs-lookup"><span data-stu-id="07146-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="07146-192">Począwszy od programu NuGet 2,5, jeśli wersja zależności jest już spełniona, zależność nie zostanie zaktualizowana podczas innych instalacji pakietu.</span><span class="sxs-lookup"><span data-stu-id="07146-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="07146-193">**Scenariusz:**</span><span class="sxs-lookup"><span data-stu-id="07146-193">**The scenario:**</span></span>

1. <span data-ttu-id="07146-194">Repozytorium źródłowe zawiera pakiet B z wersjami 1.0.0 i 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="07146-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="07146-195">Zawiera również pakiet A, który ma zależność od B (>= 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="07146-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="07146-196">Załóżmy, że bieżący projekt ma już zainstalowany pakiet B w wersji 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="07146-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="07146-197">Teraz chcesz zainstalować pakiet A.</span><span class="sxs-lookup"><span data-stu-id="07146-197">Now you want to install package A.</span></span>

<span data-ttu-id="07146-198">**W programie NuGet 2,2 i starszych:**</span><span class="sxs-lookup"><span data-stu-id="07146-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="07146-199">Podczas instalowania pakietu A pakiet NuGet aktualizuje aktualizację B do 1.0.2, nawet jeśli istniejąca wersja 1.0.0 już spełnia ograniczenie wersji zależności, czyli >= 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="07146-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="07146-200">**W programie NuGet 2,5 i nowszych:**</span><span class="sxs-lookup"><span data-stu-id="07146-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="07146-201">Pakiet NuGet nie zostanie już zaktualizowany B, ponieważ wykryje, że istniejąca wersja 1.0.0 spełnia ograniczenie wersji zależności.</span><span class="sxs-lookup"><span data-stu-id="07146-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="07146-202">Aby uzyskać więcej informacji na temat tej zmiany, przeczytaj szczegółowy [element roboczy](http://nuget.codeplex.com/workitem/1681) oraz powiązany [wątek dyskusji](http://nuget.codeplex.com/discussions/436712).</span><span class="sxs-lookup"><span data-stu-id="07146-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="07146-203">nuget.exe wyprowadza żądania HTTP z szczegółowym szczegółowośćem</span><span class="sxs-lookup"><span data-stu-id="07146-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="07146-204">W przypadku rozwiązywania problemów nuget.exe lub po prostu chcesz wiedzieć, jakie żądania HTTP są wykonywane podczas operacji, przełącznik "-verbose Szczegółowa" spowoduje teraz wyjściu wszystkie żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="07146-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Dane wyjściowe HTTP z nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="07146-206">nuget.exe push obsługuje teraz źródła UNC i folderów</span><span class="sxs-lookup"><span data-stu-id="07146-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="07146-207">Przed pakietem NuGet 2,5, Jeśli podjęto próbę uruchomienia "nuget.exe wypychania" do źródła pakietu na podstawie ścieżki UNC lub folderu lokalnego, wypchnięcie nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="07146-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="07146-208">W przypadku ostatnio dodanej funkcji konfiguracji hierarchicznej staje się ona wspólna dla nuget.exe musi być ścieżką UNC/folderem źródłowym lub galerią NuGet opartą na protokole HTTP.</span><span class="sxs-lookup"><span data-stu-id="07146-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="07146-209">Począwszy od programu NuGet 2,5, jeśli nuget.exe identyfikuje źródło UNC/folder, wykona kopię pliku do źródła.</span><span class="sxs-lookup"><span data-stu-id="07146-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="07146-210">Następujące polecenie będzie teraz działało:</span><span class="sxs-lookup"><span data-stu-id="07146-210">The following command will now work:</span></span>

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="07146-211">nuget.exe obsługuje jawnie określone pliki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="07146-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="07146-212">nuget.exe polecenia, które uzyskują dostęp do konfiguracji (wszystkie z wyjątkiem "spec" i "Pack"), teraz obsługują nową opcję "-ConfigFile", która wymusza użycie określonego pliku konfiguracji zamiast domyślnego pliku konfiguracyjnego w lokalizacji% AppData% \nuget\Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="07146-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="07146-213">Przykład:</span><span class="sxs-lookup"><span data-stu-id="07146-213">Example:</span></span>

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="07146-214">Obsługa projektów natywnych</span><span class="sxs-lookup"><span data-stu-id="07146-214">Support for Native projects</span></span>

<span data-ttu-id="07146-215">W przypadku programu NuGet 2,5 narzędzia NuGet są teraz dostępne dla natywnych projektów w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="07146-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="07146-216">Oczekujemy, że większość natywnych pakietów będzie korzystać z funkcji importów MSBuild powyżej, przy użyciu narzędzia utworzonego przez [projekt CoApp](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="07146-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="07146-217">Aby uzyskać więcej informacji, zapoznaj [się ze szczegółowymi informacjami o narzędziu](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) w witrynie coapp.org.</span><span class="sxs-lookup"><span data-stu-id="07146-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="07146-218">Nazwa platformy docelowej "native" została wprowadzona dla pakietów do dołączania plików w \Build, \Content i \Tools, gdy pakiet jest zainstalowany w projekcie natywnym.</span><span class="sxs-lookup"><span data-stu-id="07146-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="07146-219">\`Folder lib nie jest używany dla projektów natywnych.</span><span class="sxs-lookup"><span data-stu-id="07146-219">The \`lib\` folder is not used for native projects.</span></span>
