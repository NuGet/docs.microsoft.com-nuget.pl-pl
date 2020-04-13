---
title: Jak opublikować pakiet NuGet
description: Szczegółowe instrukcje dotyczące publikowania pakietu NuGet do nuget.org lub prywatnych kanałów informacyjnych oraz zarządzania własnością pakietu w nuget.org.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 02c6c8f3018bfd063c2d16a10381f88b54cac840
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429025"
---
# <a name="publishing-packages"></a>Publikowanie pakietów

Po utworzeniu pakietu i `.nupkg` udostępnieniu pliku w ręku jest to prosty proces, aby udostępnić go innym deweloperom, publicznie lub prywatnie:

- Pakiety publiczne są udostępniane wszystkim deweloperom na całym świecie za pośrednictwem [nuget.org](https://www.nuget.org/packages/manage/upload) zgodnie z opisem w tym artykule (wymaga NuGet 4.1.0+).
- Pakiety prywatne są dostępne tylko dla zespołu lub organizacji, hostując je albo udział plików, prywatny serwer NuGet, [artefakty platformy Azure](https://www.visualstudio.com/docs/package/nuget/publish), lub repozytorium innych firm, takich jak myget, ProGet, Repozytorium Nexus i Artifactory. Aby uzyskać dodatkowe informacje, zobacz [Omówienie pakietów hostingowych](../hosting-packages/overview.md).

Ten artykuł obejmuje publikowanie do nuget.org; aby opublikować w witrynie Azure Artifacts, zobacz [Zarządzanie pakietami](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Publikowanie w nuget.org

Aby nuget.org, musisz zalogować się za pomocą konta Microsoft, za pomocą którego zostaniesz poproszony o zarejestrowanie konta w nuget.org. Możesz również zalogować się przy użyciu konta nuget.org utworzonego przy użyciu starszych wersji portalu.

![Lokalizacja logowania NuGet](media/publish_NuGetSignIn.png)

Następnie można przekazać pakiet za pośrednictwem nuget.org portalu sieci web, wypchnąć do nuget.org z `nuget.exe` wiersza polecenia (wymaga 4.1.0+) lub opublikować jako część procesu ciągłej integracji/ciągłego wdrażania za pośrednictwem usługi Azure DevOps, zgodnie z opisem w poniższych sekcjach.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Portal sieci Web: użyj karty Przekaż pakiet na nuget.org

1. Wybierz **pozycję Przekaż** w górnym menu nuget.org i przejdź do lokalizacji pakietu.

    ![Prześlij paczkę na nuget.org](media/publish_UploadYourPackage.PNG)

1. nuget.org informuje, czy nazwa pakietu jest dostępna. Jeśli tak nie jest, zmień identyfikator pakietu w projekcie, odbuduj i spróbuj przekazać ponownie.

1. Jeśli nazwa pakietu jest dostępna, nuget.org otwiera sekcję **Sprawdź,** w której można przejrzeć metadane z manifestu pakietu. Aby zmienić dowolny z metadanych, edytuj `.nuspec` projekt (plik projektu lub plik), odbuduj, ponownie stwórz pakiet i przekaż go ponownie.

1. W obszarze **Dokumentacja importu** możesz wkleić markdown, wskazać dokumenty za pomocą adresu URL lub przekazać plik dokumentacji.

1. Gdy wszystkie informacje będą gotowe, wybierz przycisk **Prześlij**

### <a name="command-line"></a>Wiersz polecenia

Aby wypchnąć pakiety do nuget.org należy użyć [nuget.exe v4.1.0 lub wyższej](https://www.nuget.org/downloads), która implementuje wymagane [protokoły NuGet](../api/nuget-protocols.md). Potrzebny jest również klucz interfejsu API, który jest tworzony na nuget.org.

#### <a name="create-api-keys"></a>Tworzenie kluczy interfejsu API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>Publikuj z dotnet nuget push

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>Publikuj z nuget push

1. W wierszu polecenia uruchom następujące `<your_API_key>` polecenie, zastępując kluczem uzyskanym z nuget.org:

    ```cli
    nuget setApiKey <your_API_key>
    ```

    To polecenie przechowuje klucz interfejsu API w konfiguracji NuGet, dzięki czemu nie trzeba powtarzać tego kroku ponownie na tym samym komputerze.

    > [!NOTE]
    > Klucz interfejsu API nie jest używany do uwierzytelniania za pomocą prywatnego kanału informacyjnego. Zapoznaj się z [ `nuget sources` poleceniem,](../reference/cli-reference/cli-ref-sources.md) aby zarządzać poświadczeniami do uwierzytelniania ze źródłem.
    > Klucze interfejsu API można uzyskać z poszczególnych serwerów NuGet. Aby utworzyć i manange APIKeys dla nuget.org odnoszą się do [publish-api-key](../quickstart/includes/publish-api-key.md)

1. Wypchnij pakiet do Galerii NuGet za pomocą następującego polecenia:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a>Publikowanie podpisanych pakietów

Aby przesłać podpisane pakiety, należy najpierw [zarejestrować certyfikat](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) używany do podpisywania pakietów. 

> [!Warning]
> nuget.org odrzuca pakiety, które nie spełniają [wymagań podpisanego pakietu.](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg)

### <a name="package-validation-and-indexing"></a>Sprawdzanie poprawności i indeksowanie pakietów

Pakiety wypchnięte do nuget.org poddawane kilku weryfikacji, takich jak kontrole wirusów. (Wszystkie pakiety na nuget.org są okresowo skanowane).

Gdy pakiet przeszedł wszystkie sprawdzanie poprawności, może upłynąć trochę czasu, aby być indeksowane i pojawiają się w wynikach wyszukiwania. Po zakończeniu indeksowania otrzymasz wiadomość e-mail z potwierdzeniem pomyślnego opublikowania pakietu. Jeśli pakiet nie zostanie sprawdzony, strona szczegółów pakietu zostanie zaktualizowana, aby wyświetlić skojarzony błąd, a także otrzymasz wiadomość e-mail z powiadomieniem o tym.

Sprawdzanie poprawności i indeksowanie pakietów zwykle trwa mniej niż 15 minut. Jeśli publikowanie pakietu trwa dłużej niż oczekiwano, odwiedź [status.nuget.org,](https://status.nuget.org/) aby sprawdzić, czy nuget.org występują przerwy. Jeśli wszystkie systemy działają, a pakiet nie został pomyślnie opublikowany w ciągu godziny, zaloguj się do nuget.org i skontaktuj się z nami za pomocą łącza Skontaktuj się z pomocą techniczną na stronie pakietu.

Aby wyświetlić stan pakietu, wybierz pozycję **Zarządzaj pakietami** pod nazwą konta w nuget.org. Po zakończeniu sprawdzania poprawności otrzymasz wiadomość e-mail z potwierdzeniem.

Należy pamiętać, że może upłynąć trochę czasu, aby pakiet został zindeksowany i pojawił się w wynikach wyszukiwania, gdzie inni mogą go znaleźć, w tym czasie na stronie pakietu może pojawić się następujący komunikat:

![Komunikat informujący, że pakiet nie został jeszcze opublikowany](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a>Usługi DevOps platformy Azure (ci/cd)

Jeśli wypychasz pakiety do nuget.org przy użyciu usług Azure DevOps w `nuget.exe` ramach procesu ciągłej integracji/wdrażania, należy użyć 4.1 lub powyżej w zadaniach NuGet. Szczegóły można znaleźć na [korzystanie z najnowszego NuGet w kompilacji](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blogu).

## <a name="managing-package-owners-on-nugetorg"></a>Zarządzanie właścicielami pakietów na nuget.org

Mimo że `.nuspec` każdy plik pakietu NuGet definiuje autorów pakietu, nuget.org galeria nie używa tych metadanych do definiowania własności. Zamiast tego nuget.org przypisuje początkową własność osobie, która publikuje pakiet. Jest to zalogowany użytkownik, który przesłał pakiet za pośrednictwem nuget.org interfejsu użytkownika, lub użytkownicy, których klucz interfejsu API był używany z `nuget SetApiKey` lub `nuget push`.

Wszyscy właściciele pakietów mają pełne uprawnienia do pakietu, w tym dodawanie i usuwanie innych właścicieli oraz publikowanie aktualizacji.

Aby zmienić własność pakietu, wykonaj następujące czynności:

1. Zaloguj się, aby nuget.org przy tym za pomocą konta, które jest bieżącym właścicielem pakietu.
1. Wybierz nazwę swojego konta, wybierz pozycję **Zarządzaj pakietami**i rozwiń pozycję **Opublikowane pakiety**.
1. Wybierz na opakowaniu, który chcesz zarządzać, a następnie po prawej stronie wybierz pozycję **Zarządzaj właścicielami**.

W tym miejscu masz kilka opcji:

1. Usuń dowolnego właściciela wymienionego w obszarze **Bieżąci właściciele**.
1. Dodaj właściciela w obszarze **Dodaj właściciela,** wprowadzając jego nazwę użytkownika, wiadomość i wybierając **pozycję Dodaj**. Ta akcja wysyła wiadomość e-mail do tego nowego współwłaściciela z linkiem potwierdzającym. Po potwierdzeniu ta osoba ma pełne uprawnienia do dodawania i usuwania właścicieli. (Dopóki nie potwierdzono, sekcja **Obecni właściciele** wskazuje oczekujące zatwierdzenie dla tej osoby).
1. Aby przenieść własność (jak w przypadku zmiany własności lub pakiet został opublikowany na niewłaściwym koncie), dodaj nowego właściciela, a po potwierdzeniu własności mogą usunąć Cię z listy.

Aby przypisać własność do firmy lub grupy, utwórz konto nuget.org przy użyciu aliasu e-mail, który jest przekazywał do odpowiednich członków zespołu. Na przykład różne pakiety Microsoft ASP.NET są współwłasnością kont [Microsoft](https://nuget.org/profiles/microsoft) i [Aspnet,](https://nuget.org/profiles/aspnet) które po prostu takie aliasy.

### <a name="recovering-package-ownership"></a>Odzyskiwanie własności pakietu

Czasami pakiet może nie mieć aktywnego właściciela. Na przykład oryginalny właściciel może opuścić firmę, która produkuje pakiet, nuget.org poświadczenia są tracone lub wcześniejsze błędy w galerii pozostawił pakiet bez właściciela.

Jeśli jesteś prawowitym właścicielem pakietu i trzeba odzyskać własność, użyj [formularza kontaktowego](https://www.nuget.org/policies/Contact) na nuget.org, aby wyjaśnić swoją sytuację do zespołu NuGet. Następnie śledzimy proces weryfikacji własności pakietu, w tym próbuje zlokalizować istniejącego właściciela za pośrednictwem adresu URL projektu pakietu, Twitter, e-mail lub w inny sposób. Ale jeśli wszystko inne zawiedzie, możemy wysłać ci nowe zaproszenie, aby stać się właścicielem.
