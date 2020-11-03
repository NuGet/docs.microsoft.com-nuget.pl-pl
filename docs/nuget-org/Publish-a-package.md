---
title: Jak opublikować pakiet NuGet
description: Szczegółowe instrukcje dotyczące publikowania pakietu NuGet w nuget.org lub prywatnych źródłach oraz zarządzania własnością pakietu na nuget.org.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: fe5625247dca51c10d82fffe82022c40a4716069
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237935"
---
# <a name="publishing-packages"></a>Publikowanie pakietów

Po utworzeniu pakietu i udostępnieniu `.nupkg` pliku jest to prosty proces udostępniania go innym deweloperom — publicznie lub prywatnie:

- Pakiety publiczne są udostępniane wszystkim deweloperom globalnie przez [NuGet.org](https://www.nuget.org/packages/manage/upload) zgodnie z opisem w tym artykule (wymaga NuGet 4.1.0 +).
- Pakiety prywatne są dostępne tylko dla zespołu lub organizacji, udostępniając im udział plików, prywatny serwer NuGet, [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish)lub repozytorium innych firm, takie jak MyGet, ProGet, Nexus Repository i Artifactory. Aby uzyskać więcej informacji, zobacz [Omówienie pakietów hostingu](../hosting-packages/overview.md).

W tym artykule opisano publikowanie w usłudze nuget.org; Aby opublikować Azure Artifacts, zobacz [Zarządzanie pakietami](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Publikowanie w usłudze nuget.org

W przypadku nuget.org należy zalogować się przy użyciu konto Microsoft, z którym zostanie wyświetlony monit o zarejestrowanie konta w usłudze nuget.org.

![Lokalizacja logowania NuGet](media/publish_NuGetSignIn.png)

Następnie można przekazać pakiet za pośrednictwem portalu sieci Web nuget.org, wypchnąć do nuget.org z wiersza polecenia (wymaga `nuget.exe` 4.1.0 +) lub opublikować jako część procesu ciągłej integracji/ciągłego wdrażania za pomocą Azure DevOps Services, zgodnie z opisem w poniższych sekcjach.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Portal sieci Web: korzystanie z karty przekazywanie pakietu w witrynie nuget.org

1. Wybierz pozycję **Przekaż** w górnym menu NuGet.org i przejdź do lokalizacji pakietu.

    ![Przekaż pakiet na nuget.org](media/publish_UploadYourPackage.PNG)

1. nuget.org informuje o tym, czy nazwa pakietu jest dostępna. Jeśli tak nie jest, należy zmienić identyfikator pakietu w projekcie, ponownie skompilować i ponowić próbę przekazania.

1. Jeśli nazwa pakietu jest dostępna, nuget.org otwiera sekcję **Weryfikuj** , w której można przejrzeć metadane z manifestu pakietu. Aby zmienić dowolne metadane, Edytuj projekt (plik projektu lub `.nuspec` plik), Skompiluj ponownie, ponownie utwórz pakiet i przekaż go ponownie.

1. W obszarze **Importuj dokumentację** możesz wkleić do promocji, wskazać swój dokument z adresem URL lub przekazać plik dokumentacji.

1. Gdy wszystkie informacje są gotowe, wybierz przycisk **Prześlij**

### <a name="command-line"></a>Wiersz polecenia

Aby wypchnąć pakiety do nuget.org, należy najpierw dysponować kluczem interfejsu API utworzonym w nuget.org. Musisz użyć obu dotnet.exe (.NET Core) lub nuget.exe v 4.1.0 lub nowszych, które implementują wymagane protokoły NuGet.
Aby uzyskać więcej informacji, zobacz Protokoły [.NET Core](/dotnet/core/install/), [nuget.exe](https://www.nuget.org/downloads)i [NuGet](../api/nuget-protocols.md).

#### <a name="create-api-keys"></a>Utwórz klucze interfejsu API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>Publikowanie przy użyciu wypychania NuGet programu dotnet

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>Publikowanie przy użyciu wypychania NuGet

1. W wierszu polecenia Uruchom następujące polecenie, zastępując `<your_API_key>` klucz uzyskany od NuGet.org:

    ```cli
    nuget setApiKey <your_API_key>
    ```

    To polecenie zapisuje klucz interfejsu API w konfiguracji NuGet, dzięki czemu nie trzeba ponownie powtarzać tego kroku na tym samym komputerze.

    > [!NOTE]
    > Klucz interfejsu API nie jest używany do uwierzytelniania w prywatnym źródle danych. Zapoznaj się z [ `nuget sources` poleceniem](../reference/cli-reference/cli-ref-sources.md) , aby zarządzać poświadczeniami do uwierzytelniania ze źródłem.
    > Klucze interfejsu API można uzyskać z poszczególnych serwerów NuGet. Aby utworzyć i manange APIKeys dla nuget.org, zobacz [Tworzenie kluczy interfejsu API](#create-api-keys).

1. Wypchnij pakiet do galerii NuGet przy użyciu następującego polecenia:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a>Publikuj podpisane pakiety

Aby przesłać podpisane pakiety, należy najpierw [zarejestrować certyfikat](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) używany do podpisywania pakietów. 

> [!Warning]
> nuget.org odrzuca pakiety, które nie spełniają [wymagań podpisanego pakietu](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).

### <a name="package-validation-and-indexing"></a>Sprawdzanie poprawności pakietu i indeksowanie

Pakiety wypychane do nuget.org zostały poddane kilku walidacji, takich jak sprawdzanie wirusów. (Wszystkie pakiety na nuget.org są okresowo skanowane).

Gdy pakiet przeszedł wszystkie testy sprawdzania poprawności, może upłynąć trochę czasu, aby można było indeksować go i wyświetlać w wynikach wyszukiwania. Po zakończeniu indeksowania otrzymasz wiadomość e-mail z potwierdzeniem, że pakiet został pomyślnie opublikowany. Jeśli pakiet nie zostanie zweryfikowany, Strona szczegóły pakietu zostanie zaktualizowana w celu wyświetlenia powiązanego błędu i otrzymasz wiadomość e-mail z powiadomieniem o tym fakcie.

Sprawdzanie poprawności pakietu i indeksowania zazwyczaj trwa 15 minut. Jeśli publikowanie pakietu trwa dłużej niż oczekiwano, odwiedź stronę [status.NuGet.org](https://status.nuget.org/) , aby sprawdzić, czy w NuGet.org występują jakiekolwiek przerwy. Jeśli wszystkie systemy działają, a pakiet nie został pomyślnie opublikowany w ciągu godziny, zaloguj się do nuget.org i skontaktuj się z nami za pomocą linku skontaktuj się z pomocą techniczną na stronie pakietu.

Aby wyświetlić stan pakietu, wybierz pozycję **Zarządzaj pakietami** w polu Nazwa konta w witrynie NuGet.org. Po zakończeniu walidacji otrzymasz wiadomość e-mail z potwierdzeniem.

Należy pamiętać, że może upłynąć trochę czasu, zanim pakiet będzie indeksowany i pojawia się w wynikach wyszukiwania, gdzie inne osoby mogą go znaleźć, podczas gdy na stronie pakietu zostanie wyświetlony następujący komunikat:

![Komunikat informujący o tym, że pakiet nie został jeszcze opublikowany](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a>Azure DevOps Services (CI/CD)

W przypadku wypychania pakietów do nuget.org przy użyciu Azure DevOps Services w ramach procesu ciągłej integracji/wdrażania należy użyć `nuget.exe` 4,1 lub więcej w zadaniach NuGet. Szczegółowe informacje znajdują się w temacie [Korzystanie z najnowszego pakietu NuGet w kompilacji](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blog Microsoft DevOps).

## <a name="managing-package-owners-on-nugetorg"></a>Zarządzanie właścicielami pakietów w witrynie nuget.org

Mimo że każdy plik pakietu NuGet `.nuspec` definiuje autorów pakietu, galeria NuGet.org nie używa tych metadanych do definiowania własności. Zamiast tego nuget.org przypisuje wstępną własność do osoby, która publikuje pakiet. Jest to zalogowany użytkownik, który przekazał pakiet za pomocą interfejsu użytkownika nuget.org, lub użytkowników, których klucz interfejsu API był używany z systemem `nuget SetApiKey` lub `nuget push` .

Wszyscy właściciele pakietu mają pełne uprawnienia do pakietu, w tym dodawanie i usuwanie innych właścicieli oraz publikowanie aktualizacji.

Aby zmienić własność pakietu, wykonaj następujące czynności:

1. Zaloguj się do nuget.org przy użyciu konta, które jest bieżącym właścicielem pakietu.
1. Wybierz nazwę swojego konta, wybierz pozycję **Zarządzaj pakietami** i rozwiń węzeł **opublikowane pakiety** .
1. Wybierz pakiet, którym chcesz zarządzać, a następnie po prawej stronie wybierz pozycję **Zarządzaj właścicielami** .

W tym miejscu masz kilka opcji:

1. Usuń wszystkich właścicieli wymienionych w obszarze **bieżący właściciele** .
1. Dodaj właściciela w obszarze **Dodaj właściciela** , wprowadzając jego nazwę użytkownika, komunikat i wybierając pozycję **Dodaj** . Ta akcja spowoduje wysłanie wiadomości e-mail do tego nowego współwłaściciela z linkiem potwierdzającym. Po potwierdzeniu osoba ta ma pełne uprawnienia do dodawania i usuwania właścicieli. (Do momentu potwierdzenia **Bieżąca sekcja właściciele** wskazuje, że oczekuje na zatwierdzenie przez tę osobę).
1. Aby przenieść własność (jak w przypadku zmiany własności lub opublikowania pakietu na niewłaściwym koncie), Dodaj nowego właściciela, a po potwierdzeniu prawa własności można usunąć użytkownika z listy.

Aby przypisać własność do firmy lub grupy, Utwórz konto usługi nuget.org przy użyciu aliasu e-mail, który jest przekazywany do odpowiednich członków zespołu. Na przykład różne pakiety Microsoft ASP.NET są współwłasnością kont [Microsoft](https://nuget.org/profiles/microsoft) i [ASPNET](https://nuget.org/profiles/aspnet) , które po prostu takie aliasy.

### <a name="recovering-package-ownership"></a>Odzyskiwanie własności pakietu

Czasami pakiet może nie mieć aktywnego właściciela. Na przykład oryginalny właściciel może pozostać w firmie, która produkuje pakiet, nuget.org poświadczenia są tracone lub wcześniejsze usterki w galerii pozostawiają bez właściciela pakietu.

Jeśli jesteś właścicielem pakietu i chcesz odzyskać własność, użyj [formularza kontaktu](https://www.nuget.org/policies/Contact) w witrynie NuGet.org, aby wyjaśnić swoją sytuację do zespołu NuGet. Następnie postępuj zgodnie z procesem weryfikacji własności pakietu, w tym przy próbie zlokalizowania istniejącego właściciela za pośrednictwem adresu URL projektu pakietu, serwisu Twitter, poczty e-mail lub innych metod. Jeśli jednak wszystkie inne opcje zakończą się niepowodzeniem, możemy wysłać nowe zaproszenie, aby stał się właścicielem.
