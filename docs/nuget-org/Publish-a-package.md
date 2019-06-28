---
title: Jak opublikować pakiet NuGet
description: Szczegółowe instrukcje dotyczące sposobu opublikowania pakietu NuGet nuget.org lub źródła danych prywatnych i zarządzanie własność pakietu w witrynie nuget.org.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 6d183100a8319b517347567f34d276e94eb4e15d
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427573"
---
# <a name="publishing-packages"></a>Publikowanie pakietów

Gdy utworzono pakiet i mają swoje `.nupkg` plików w kasie, jest to prosty proces, aby udostępnić go innym deweloperom publiczną lub prywatną:

- Publicznych pakietów są udostępniane wszystkim deweloperom globalnie za pomocą [nuget.org](https://www.nuget.org/packages/manage/upload) zgodnie z opisem w tym artykule (wymaga NuGet 4.1.0+).
- Prywatne pakiety są dostępne dla zespołu lub organizacji, udostępniając je albo udziału plików, prywatny serwer NuGet, [artefaktów Azure](https://www.visualstudio.com/docs/package/nuget/publish), lub repozytorium innych firm, takich jak myget ProGet, Nexus repozytorium i Artifactory. Aby uzyskać więcej informacji, zobacz [hostingu — Omówienie pakietów](../hosting-packages/overview.md).

W tym artykule opisano publikowania w witrynie nuget.org; do publikowania artefaktów platformy Azure, zobacz [zarządzania pakietami](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Publikowanie w witrynie nuget.org

Nuget.org musisz zalogować się przy użyciu konta Microsoft, z którym użytkownik zostanie zapytany zarejestrować konto z repozytorium nuget.org. Możesz też zarejestrować się przy użyciu konta nuget.org, utworzony za pomocą starszej wersji portalu.

![Znak NuGet w lokalizacji](media/publish_NuGetSignIn.png)

Następnie można albo przekaż pakiet za pośrednictwem portalu sieci web w witrynie nuget.org, Wypchnij do repozytorium nuget.org z wiersza polecenia (wymaga `nuget.exe` 4.1.0+), lub Opublikuj jako część procesu ciągłej integracji/ciągłego wdrażania za pośrednictwem usługi DevOps platformy Azure, zgodnie z opisem w poniższych sekcjach.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Portal sieci Web: Użyj karty przekazywania pakietu w witrynie nuget.org

1. Wybierz **przekazywanie** w menu u góry nuget.org i przejdź do lokalizacji pakietu.

    ![Przekaż pakiet w witrynie nuget.org](media/publish_UploadYourPackage.PNG)

1. nuget.org informuje, czy nazwa pakietu jest dostępna. Zmiana nie jest identyfikator pakietu w projekcie, ponownie skompilować, a następnie ponów próbę przekazania.

1. Jeśli nazwa pakietu jest dostępny, zostanie otwarty nuget.org **Sprawdź** sekcji, w którym można przejrzeć metadane z manifestu pakietu. Aby zmienić dowolne z metadanych, należy edytować projektu (plik projektu lub `.nuspec` pliku), ponownie skompilować, ponowne utworzenie pakietu, a następnie przekaż ponownie.

1. W obszarze **dokumentacji importu** możesz wkleić języka znaczników Markdown, wskaż swoje dokumenty z adresem URL lub Przekaż plik dokumentacji.

1. Gdy wszystkie informacje są gotowe, wybierz pozycję **przesyłania** przycisku

### <a name="command-line"></a>Wiersz polecenia

Do wypychania pakietów nuget.org, należy użyć [nuget.exe verze 4.1.0 lub nowszej](https://www.nuget.org/downloads), który implementuje wymagane [protokołów NuGet](../api/nuget-protocols.md). Musisz mieć również klucz interfejsu API, który jest tworzony w witrynie nuget.org.

#### <a name="create-api-keys"></a>Tworzenie kluczy interfejsu API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>Publikowanie za pomocą polecenia dotnet nuget wypychania

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>Publikowanie za pomocą wypychania nuget

1. W wierszu polecenia Uruchom następujące polecenie, zastępując `<your_API_key>` przy użyciu klucza uzyskane z repozytorium nuget.org:

    ```cli
    nuget setApiKey <your_API_key>
    ```

    To polecenie przechowuje klucz interfejsu API w konfiguracji NuGet, dzięki czemu należy powtórzyć ten krok ponownie na tym samym komputerze.

1. Wypchnij pakietu do galerii pakietów NuGet, używając następującego polecenia:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a>Publikowanie podpisanych pakietów

Aby przesłać podpisanych pakietów, musisz najpierw [zarejestrować certyfikat](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) używany do podpisywania pakietów. 

> [!Warning]
> nuget.org odrzuci pakiety, które nie spełniają [podpisany wymagań dotyczących pakietu](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).

### <a name="package-validation-and-indexing"></a>Sprawdzanie poprawności pakietu i indeksowania

Pakiety wypchnięty do repozytorium nuget.org uczestniczenia w kilku operacji sprawdzania poprawności, takich jak sprawdzanie przed wirusami. (Wszystkie pakiety w witrynie nuget.org są okresowo skanowane.)

Gdy pakiet został przekazany wszystkie testy sprawdzania poprawności, może potrwać chwilę, aby mogła być indeksowane i wyświetlane w wynikach wyszukiwania. Po zakończeniu indeksowania, otrzymasz wiadomość e-mail, potwierdzenia, że pakiet został pomyślnie opublikowany. Jeśli pakiet nie powiodło się sprawdzenie poprawności, na stronie szczegółów pakietu zostanie zaktualizowana, aby wyświetlić skojarzony błąd i otrzymasz wiadomość e-mail z powiadomieniem o nim.

Sprawdzanie poprawności pakietu i indeksowanie zwykle trwa mniej niż 15 minut. Publikowanie pakietu trwa dłużej niż oczekiwano, odwiedź stronę [status.nuget.org](https://status.nuget.org/) do sprawdzenia, jeśli nuget.org występuje przerw. Jeśli pakiet nie został pomyślnie opublikowany w ciągu godziny są wszystkie systemy operacyjne, zaloguj się na stronie nuget.org i skontaktuj się z nami przy użyciu linku skontaktuj się z działem pomocy technicznej na stronie pakiet.

Aby wyświetlić stan pakietu, wybierz **Zarządzanie pakietami** pod nazwą Twojego konta w witrynie nuget.org. Otrzymasz wiadomość e-mail z potwierdzeniem, gdy sprawdzanie poprawności zostało ukończone.

Należy zwrócić uwagę na to, że może upłynąć trochę czasu pakiet indeksowane i wyświetlane w wynikach wyszukiwania, gdzie inne osoby mogą ją znaleźć, w tym czasie zostanie wyświetlony następujący komunikat na stronie pakiet:

![Komunikat wskazujący, że pakiet nie został jeszcze opublikowany.](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a>Usługi Azure DevOps (CI/CD)

Jeśli pakiety są wypychane na stronie nuget.org przy użyciu usługi DevOps platformy Azure jako część procesu ciągłej integracji/ciągłego wdrażania, należy użyć `nuget.exe` 4.1 lub nowszym w zadaniach NuGet. Szczegółowe informacje można znaleźć na [przy użyciu najnowszego rozwiązania NuGet w kompilacji](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blog Microsoft DevOps).

## <a name="managing-package-owners-on-nugetorg"></a>Zarządzanie właścicielami pakietu w witrynie nuget.org

Mimo że każdy pakiet NuGet `.nuspec` plik definiuje autorom pakietów, galerii nuget.org nie używa tych metadanych do definiowania własności. Zamiast tego nuget.org przypisuje początkowej prawa własności do osoby, która publikuje pakiet. Jest to zalogowanego użytkownika, który pakiet za pośrednictwem interfejsu użytkownika w witrynie nuget.org, lub użytkowników, których klucz interfejsu API została użyta z `nuget SetApiKey` lub `nuget push`.

Wszyscy właściciele pakietu mają pełne uprawnienia do pakietu, w tym dodawanie i usuwanie innych właścicieli i publikowanie aktualizacji.

Aby zmienić własność pakietu, wykonaj następujące czynności:

1. Zaloguj się w witrynie nuget.org, przy użyciu konta, który jest bieżącym właścicielem pakietu.
1. Wybierz nazwę swojego konta, wybierz pozycję **Zarządzanie pakietami**i rozwiń **opublikowane pakiety**.
1. Wybierz pakiet, którym chcesz zarządzać, a następnie po prawej stronie wybierz **zarządzenie właścicielami**.

W tym miejscu masz kilka opcji:

1. Usuń wszelkie właściciela na liście **bieżącego właścicieli**.
1. Dodaj właściciela w obszarze **dodać właściciela** , wprowadzając odpowiednią nazwę użytkownika, komunikat i wybierając **Dodaj**. Ta akcja spowoduje wysłanie wiadomości e-mail do tego nowego właściciela współpracujących z linkiem umożliwiającym potwierdzenia. Po potwierdzeniu, osoba ta ma pełne uprawnienia do dodawania i usuwania właścicieli. (Do czasu potwierdzenia, **bieżącego właścicieli** sekcji wskazuje na zatwierdzenie dla tej osoby.)
1. Aby przenieść własność (jako podczas zmiany prawa własności lub pakietu została opublikowana na koncie problem), Dodaj nowego właściciela, a po ich zostało potwierdzone własność one należy usunąć z listy.

Aby przypisać własność firmy lub grupy, Utwórz konto nuget.org, za pomocą aliasu adresu e-mail, który jest przekazywany do członków zespołu odpowiednie. Na przykład różne pakiety Microsoft ASP.NET wspólnie są własnością [microsoft](http://nuget.org/profiles/microsoft) i [aspnet](http://nuget.org/profiles/aspnet) konta, które po prostu takie aliasy.

### <a name="recovering-package-ownership"></a>Odzyskiwanie własność pakietu

Od czasu do czasu pakietu nie może mieć aktywne właściciela. Na przykład pierwotnego właściciela mogą być przechowywane w firmie, która tworzy pakiet, nuget.org poświadczenia zostaną utracone lub wcześniejsze błędy w galerii left ownerless pakietu.

Jeśli są prawowitego właściciela pakietu i trzeba odzyskać własności, użyj [formularz kontaktowy](https://www.nuget.org/policies/Contact) w witrynie nuget.org, aby wyjaśnić sytuacji zespołowi NuGet. Firma Microsoft następnie postępuj zgodnie z procesem na zweryfikowanie Twojej własności pakietu, w tym próbuje zlokalizować istniejący właściciel za pośrednictwem adresu URL projektu pakietu, Twitter, wiadomości e-mail lub w inny sposób. Ale jeśli wszystko inne nie powiedzie się, możemy wysłać nowe zaproszenie, aby stać się właścicielem.
