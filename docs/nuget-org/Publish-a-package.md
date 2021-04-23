---
title: Jak opublikować pakiet NuGet
description: Szczegółowe instrukcje dotyczące publikowania pakietu NuGet w nuget.org lub prywatnych kanałach informacyjnych oraz zarządzania własnością pakietów na nuget.org.
author: JonDouglas
ms.author: jodou
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 05a16d8bf609d727aba3ddbc42959a3deb97b24b
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901918"
---
# <a name="publishing-packages"></a>Publikowanie pakietów

Po utworzeniu pakietu i udostępnić plikowi jest to prosty proces, aby udostępnić go innym deweloperom publicznie lub `.nupkg` prywatnie:

- Pakiety publiczne są udostępniane wszystkim deweloperom globalnie za [pośrednictwem nuget.org](https://www.nuget.org/packages/manage/upload) zgodnie z opisem w tym artykule (wymagany jest pakiet NuGet 4.1.0+).
- Pakiety prywatne są dostępne tylko dla zespołu lub organizacji przez hostowanie dla nich udziału plików, prywatnego serwera NuGet, usługi [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish)lub repozytorium innej firmy, takiego jak myget, ProGet, Nexus Repository i Artifactory. Aby uzyskać więcej informacji, zobacz [Hosting Packages Overview (Omówienie pakietów hostingu).](../hosting-packages/overview.md)

Ten artykuł dotyczy publikowania w nuget.org; Aby publikować w Azure Artifacts, zobacz [Zarządzanie pakietami](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Publikowanie w nuget.org

Na nuget.org musisz zalogować się przy użyciu konta konto Microsoft, za pomocą którego zostaniesz poproszony o zarejestrowanie konta w nuget.org.

![Lokalizacja logowania w programie NuGet](media/publish_NuGetSignIn.png)

Następnie możesz przekazać pakiet za pośrednictwem portalu internetowego usługi nuget.org, wypchnąć do usługi nuget.org z wiersza polecenia (wymaga to programu 4.1.0+) lub opublikować go w ramach procesu ci/CD za pośrednictwem usługi Azure DevOps Services, zgodnie z opisem w poniższych `nuget.exe` sekcjach.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Portal internetowy: użyj karty Upload Package (Przekaż pakiet) nuget.org

1. Wybierz **pozycję** Przekaż w górnym menu nuget.org i przejdź do lokalizacji pakietu.

    ![Przekazywanie pakietu na nuget.org](media/publish_UploadYourPackage.PNG)

1. nuget.org informuje o tym, czy nazwa pakietu jest dostępna. Jeśli tak nie jest, zmień identyfikator pakietu w projekcie, ponownie skompilować i spróbuj przekazać ponownie.

1. Jeśli nazwa pakietu jest dostępna, nuget.org **sekcję Weryfikuj,** w której można przejrzeć metadane z manifestu pakietu. Jeśli pakiet zawiera [plik readme,](/docs/nuget-org/package-readme-on-nuget-org.md) zapoznaj się z podglądem, aby upewnić się, że cała zawartość jest poprawnie renderowana. Aby zmienić dowolne metadane, edytuj projekt (plik projektu lub plik), ponownie skompilować, ponownie utworzyć `.nuspec` pakiet i przekazać go ponownie.

2. Gdy wszystkie informacje będą gotowe, wybierz przycisk **Prześlij**

### <a name="command-line"></a>Wiersz polecenia

Aby wypchnąć pakiety do nuget.org, musisz najpierw mieć klucz interfejsu API, który jest tworzony na nuget.org. Należy użyć wersji dotnet.exe (.NET Core) lub nuget.exe w wersji 4.1.0 lub powyższej, które implementują wymagane protokoły NuGet.
Aby uzyskać więcej informacji, zobacz [.NET Core](/dotnet/core/install/), [nuget.exe](https://www.nuget.org/downloads)i [Protokoły NuGet.](../api/nuget-protocols.md)

#### <a name="create-api-keys"></a>Tworzenie kluczy interfejsu API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>Publikowanie za pomocą wypychania dotnet nuget

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>Publikowanie za pomocą wypychania nuget

1. W wierszu polecenia uruchom następujące polecenie, zastępując element kluczem `<your_API_key>` uzyskanymi z nuget.org:

    ```cli
    nuget setApiKey <your_API_key>
    ```

    To polecenie przechowuje klucz interfejsu API w konfiguracji nuGet, dzięki czemu nie trzeba powtarzać tego kroku na tym samym komputerze.

    > [!NOTE]
    > Klucz interfejsu API nie jest używany do uwierzytelniania za pomocą prywatnego kanału informacyjnego. Zapoznaj się [ `nuget sources` z poleceniem](../reference/cli-reference/cli-ref-sources.md) , aby zarządzać poświadczeniami do uwierzytelniania za pomocą źródła.
    > Klucze interfejsu API można uzyskać z poszczególnych serwerów NuGet. Aby utworzyć i manange APIKeys for nuget.org, zobacz [Tworzenie kluczy interfejsu API.](#create-api-keys)

1. Wypchniesz pakiet do galerii NuGet przy użyciu następującego polecenia:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a>Publikowanie podpisanych pakietów

Aby przesłać podpisane pakiety, należy najpierw [zarejestrować certyfikat używany](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) do podpisywania pakietów. 

> [!Warning]
> nuget.org odrzuca pakiety, które nie spełniają wymagań [podpisanych pakietów.](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg)

### <a name="package-validation-and-indexing"></a>Walidacja i indeksowanie pakietów

Pakiety wypychane do nuget.org przejść kilka weryfikacji, takich jak testy wirusów. (Wszystkie pakiety na nuget.org są okresowo skanowane).

Jeśli pakiet przeszedł wszystkie testy weryfikacyjne, jego indeksowanie i pojawianie się w wynikach wyszukiwania może trochę potrwać. Po zakończeniu indeksowania otrzymasz wiadomość e-mail z potwierdzeniem pomyślnego opublikowania pakietu. Jeśli sprawdzenie poprawności pakietu zakończy się niepowodzeniem, strona szczegółów pakietu zostanie zaktualizowana w celu wyświetlenia skojarzonego błędu, a otrzymasz również wiadomość e-mail z powiadomieniem o tym.

Walidacja i indeksowanie pakietów zwykle trwa poniżej 15 minut. Jeśli publikowanie pakietów trwa dłużej niż oczekiwano, odwiedź stronę [status.nuget.org,](https://status.nuget.org/) aby sprawdzić, nuget.org występują jakieś przerwy w działaniu. Jeśli wszystkie systemy są operacyjne i pakiet nie został pomyślnie opublikowany w ciągu godziny, zaloguj się do witryny nuget.org i skontaktuj się z nami przy użyciu linku Skontaktuj się z pomocą techniczną na stronie pakietu.

Aby wyświetlić stan pakietu, wybierz pozycję Zarządzaj **pakietami** w obszarze nazwy konta na nuget.org. Po zakończeniu walidacji otrzymasz wiadomość e-mail z potwierdzeniem.

Pamiętaj, że indeksowanie pakietu i wyświetlanie go w wynikach wyszukiwania tam, gdzie inne osoby mogą go znaleźć, może trochę potrwać. W tym czasie na stronie pakietu zostanie wyświetlony następujący komunikat:

![Komunikat wskazujący, że pakiet nie został jeszcze opublikowany](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a>Azure DevOps Services (CI/CD)

W przypadku wypychania pakietów do usługi nuget.org przy użyciu Azure DevOps Services w ramach procesu ciągłej integracji/wdrażania należy użyć w zadaniach NuGet programu `nuget.exe` 4.1 lub jego więcej. Szczegółowe informacje można znaleźć na [stronie Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Korzystanie z najnowszego pakietu NuGet w kompilacji) (blog microsoft DevOps).

## <a name="managing-package-owners-on-nugetorg"></a>Zarządzanie właścicielami pakietów na nuget.org

Chociaż każdy plik pakietu NuGet definiuje autorów pakietu, galeria nuget.org nie używa tych metadanych do `.nuspec` definiowania własności. Zamiast nuget.org przypisuje początkową własność osobie, która publikuje pakiet. Jest to zalogowany użytkownik, który przesłał pakiet za pośrednictwem interfejsu nuget.org użytkownika, lub użytkownicy, których klucz interfejsu API był używany z usługą `nuget SetApiKey` lub `nuget push` .

Wszyscy właściciele pakietu mają pełne uprawnienia do pakietu, w tym dodawanie i usuwanie innych właścicieli oraz publikowanie aktualizacji.

Aby zmienić własność pakietu, wykonaj następujące czynności:

1. Zaloguj się nuget.org przy użyciu konta, które jest bieżącym właścicielem pakietu.
1. Wybierz nazwę konta, wybierz pozycję **Zarządzaj pakietami** i rozwiń pozycję **Opublikowane pakiety.**
1. Wybierz pakiet, którym chcesz zarządzać, a następnie po prawej stronie wybierz pozycję **Zarządzaj właścicielami.**

W tym miejscu masz kilka opcji:

1. Usuń wszystkich właścicieli wymienionych w obszarze **Bieżący właściciele.**
1. Dodaj właściciela w obszarze **Dodaj właściciela,** wprowadzając jego nazwę użytkownika, komunikat i wybierając pozycję **Dodaj.** Ta akcja powoduje wysłanie wiadomości e-mail do nowego współwłaściciel z linkiem potwierdzenia. Po potwierdzeniu ta osoba ma pełne uprawnienia do dodawania i usuwania właścicieli. (Do czasu potwierdzenia sekcja **Bieżący właściciele** wskazuje oczekiwanie na zatwierdzenie dla tej osoby).
1. Aby przenieść własność (tak jak w przypadku zmiany własności lub opublikowania pakietu na niewłaściwym koncie), dodaj nowego właściciela, a po potwierdzeniu własności może on usunąć Cię z listy.

Aby przypisać własność firmie lub grupie, utwórz konto nuget.org przy użyciu aliasu adresu e-mail przekazywanego do odpowiednich członków zespołu. Na przykład różne pakiety ASP.NET Microsoft są współwłasne dla [kont microsoft](https://nuget.org/profiles/microsoft) i [aspnet,](https://nuget.org/profiles/aspnet) które po prostu takie aliasy.

### <a name="recovering-package-ownership"></a>Odzyskiwanie własności pakietu

Czasami pakiet może nie mieć aktywnego właściciela. Na przykład pierwotny właściciel mógł opuścić firmę, która tworzy pakiet, nuget.org poświadczenia zostaną utracone lub wcześniejsze usterki w galerii pozostawiły pakiet bez właściciela.

Jeśli jesteś odpowiednim właścicielem pakietu i musisz odzyskać własność, użyj formularza kontaktowego na stronie nuget.org, aby wyjaśnić swoją sytuację zespołowi NuGet. [](https://www.nuget.org/policies/Contact) Następnie przechodzimy przez proces weryfikacji własności pakietu, w tym próby zlokalizowania istniejącego właściciela za pomocą adresu URL projektu pakietu, usługi Twitter, poczty e-mail lub w inny sposób. Jeśli jednak wszystkie inne zawiedzie, możemy wysłać Do Ciebie nowe zaproszenie, aby zostać właścicielem.
