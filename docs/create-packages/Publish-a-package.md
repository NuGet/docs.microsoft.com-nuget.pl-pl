---
title: Jak opublikować pakietu NuGet
description: Szczegółowe instrukcje dotyczące sposobu publikowania pakietu NuGet nuget.org lub prywatnej źródeł danych i jak zarządzać własność pakietu na nuget.org.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 806a64d2d7654e4c1bca89a13d70fd9983c12703
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/22/2018
---
# <a name="publishing-packages"></a>Publikowanie pakietów

Gdy utworzono pakiet i mieć Twojej `.nupkg` w pliku, jest prosty proces, aby udostępnić ją innym producentom publiczną lub prywatną:

- Pakiety publicznego były dostępne dla wszystkich deweloperów globalnie za pomocą [nuget.org](https://www.nuget.org/packages/manage/upload) zgodnie z opisem w tym artykule (wymaga NuGet 4.1.0+).
- Pakietów prywatnych są dostępne dla tylko zespół lub organizacja, umieszczając je albo udziału plików, serwer prywatnej NuGet [Visual Studio Team Services pakietu zarządzania](https://www.visualstudio.com/docs/package/nuget/publish), lub repozytorium innych firm, takich jak myget, ProGet, węzła Repozytorium i Artifactory. Aby uzyskać więcej informacji, zobacz [Hosting Omówienie pakietów](../hosting-packages/overview.md).

W tym artykule omówiono publikowanie nuget.org; do publikowania w Visual Studio Team Services, zobacz [zarządzania pakietami](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Publikowanie nuget.org

Dla nuget.org należy zalogować się przy użyciu konta Microsoft, z którym użytkownik zostanie zapytany zarejestrować konto z nuget.org. Możesz też zalogować się na koncie nuget.org utworzone za pomocą starszych wersji portalu.

![Lokalizacja logowania NuGet](media/publish_NuGetSignIn.png)

Następnie można albo przekaż pakiet w portalu sieci web nuget.org, wypychać do nuget.org za pomocą wiersza polecenia (wymaga `nuget.exe` 4.1.0+), lub Opublikuj jako część procesu CI/CD za pomocą programu Visual Studio Team Services, zgodnie z opisem w poniższych sekcjach.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Portal sieci Web: karta przekaż pakiet na nuget.org

1. Wybierz **przekazać** w górnym menu nuget.org i przejdź do lokalizacji pakietu.

    ![Przekaż pakiet na nuget.org](media/publish_UploadYourPackage.PNG)

1. nuget.org informuje, czy nazwa pakietu jest dostępna. Zmiana nie będzie identyfikator pakietu w projekcie, skompiluj ponownie i spróbuj ponownie przekazywania.

1. Jeśli nazwa pakietu jest dostępny, zostanie otwarty nuget.org **Sprawdź** sekcji, w którym można przejrzeć metadanych z manifestu pakietu. Aby zmienić dowolne z metadanych, należy edytować projektu (plik projektu lub `.nuspec` pliku), skompiluj ponownie ponownie utworzyć pakiet i Prześlij ponownie.

1. W obszarze **dokumentacji importu** możesz wkleić języka znaczników Markdown, wskaż polecenie swoje dokumenty przy użyciu adresu URL lub Przekaż plik dokumentacji.

1. Gdy wszystkie informacje są gotowe, wybierz **przesyłania** przycisku

### <a name="command-line"></a>Wiersz polecenia

Pakiety wypychania do nuget.org musi używać [nuget.exe v4.1.0 lub nowszej](https://www.nuget.org/downloads), który implementuje wymaganych [protokołów NuGet](../api/nuget-protocols.md). Należy również klucz interfejsu API, który jest tworzony na nuget.org.

#### <a name="create-api-keys"></a>Tworzenie kluczy interfejsu API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>Publikowanie za pomocą wypychania nuget dotnet

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>Publikowanie za pomocą wypychania nuget

1. W wierszu polecenia, uruchom następujące polecenie, zastępując `<your_API_key>` z kluczem uzyskane z nuget.org:

    ```cli
    nuget setApiKey <your_API_key>
    ```

    To polecenie zapisuje klucz interfejsu API w konfiguracji NuGet, aby należy powtórzyć ten krok ponownie na tym samym komputerze.

1. Wypychanie do pakietu do galerii NuGet przy użyciu następującego polecenia:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a>Publikowanie pakietów podpisem

Aby przesłać pakiety podpisem, należy najpierw [zarejestrować certyfikat](../reference/Signed-Packages-Reference.md#register-certificate-on-nugetorg) używany do podpisywania pakietów. 

> [!Warning]
> pakiety, które nie spełniają odrzuca nuget.org [podpisany wymagań dotyczących pakietu](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).

### <a name="package-validation-and-indexing"></a>Sprawdzanie poprawności pakietu i indeksowania

Pakiety do nuget.org przechodzą kilku operacji sprawdzania poprawności, takich jak sprawdzanie przed wirusami. (Wszystkie pakiety na nuget.org okresowo są skanowane.)

. Po upływie wszystkie testy sprawdzania poprawności pakietu może upłynąć trochę czasu na jej indeksowane i wyświetlane w wynikach wyszukiwania. Po zakończeniu indeksowania otrzymasz wiadomość e-mail z potwierdzeniem, że pakiet został pomyślnie opublikowany. W przypadku niepowodzenia sprawdzenia poprawności pakietu na stronie Szczegóły pakietu zostanie zaktualizowana, aby wyświetlić skojarzony błąd i otrzymasz wiadomość e-mail powiadomienia użytkownika o nim.

Sprawdzanie poprawności pakietu i indeksowania zazwyczaj trwa poniżej 15 minut. Publikowanie pakietu trwa dłużej niż oczekiwano, odwiedź stronę [status.nuget.org](https://status.nuget.org/) do sprawdzenia, czy nuget.org występują żadnych przerw w działaniu. Jeśli pakiet nie został pomyślnie opublikowany w ciągu godziny są wszystkie systemy operacyjne, zaloguj się do nuget.org i skontaktuj się z nami za pomocą łącza Skontaktuj się z pomocą techniczną na stronie pakiet.

Aby wyświetlić stan pakietu, wybierz **zarządzania pakietami** pod nazwą konta na nuget.org. Otrzymasz wiadomość e-mail z potwierdzeniem po zakończeniu weryfikacji.

Należy pamiętać, że może upłynąć trochę czasu pakietu indeksowane i wyświetlane w wynikach wyszukiwania, gdy inne można znaleźć go w tym czasie zostanie wyświetlony następujący komunikat na stronie pakiet:

![Komunikat wskazujący, że pakiet nie został jeszcze opublikowany.](media/publish_NotYetIndexed.png)

### <a name="visual-studio-team-services-cicd"></a>Visual Studio Team Services (CI/CD)

Jeśli pakiety są Wypychanie do nuget.org jako część procesu ciągłej integracji/wdrożenia przy użyciu programu Visual Studio Team Services, należy użyć `nuget.exe` 4.1 lub nowszej w zadaniach NuGet. Szczegółowe informacje można znaleźć w [za pomocą najnowszej NuGet w kompilacji](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blog DevOps firmy Microsoft).

## <a name="managing-package-owners-on-nugetorg"></a>Zarządzanie właścicielami pakietu na nuget.org

Mimo że każdy pakiet NuGet `.nuspec` pliku definiuje autorów pakietu, Galeria nuget.org nie używa tych metadanych do definiowania własności. Zamiast tego nuget.org przypisuje początkowej prawa własności do osoby, która publikuje pakiet. To jest zalogowany użytkownik, który pakiet za pomocą nuget.org interfejsu użytkownika lub użytkowników, którego klucz interfejsu API została użyta z `nuget SetApiKey` lub `nuget push`.

Wszystkie właściciele pakietu mają pełne uprawnienia do pakietu, w tym dodawanie i usuwanie właścicieli innych oraz publikowanie aktualizacji.

Aby zmienić własność pakietu, wykonaj następujące czynności:

1. Zaloguj się do nuget.org przy użyciu konta, który jest bieżącym właścicielem pakietu.
1. Wybierz nazwę konta, wybierz pozycję **zarządzania pakietami**i rozwiń **opublikowane pakiety**.
1. Wybierz w pakiecie, którymi chcesz zarządzać, a następnie po prawej stronie wybierz **Zarządzaj właścicielami**.

W tym miejscu masz kilka opcji:

1. Usuń wszelkie właściciela kategorii **bieżącego właścicieli**.
1. Dodaj właściciela w obszarze **dodać właściciela** wprowadzania nazwy użytkownika, wiadomości i wybierając **Dodaj**. Ta akcja wysyła wiadomość e-mail do tej nowej współwłaściciel Link potwierdzenia. Po potwierdzeniu, że osoba ma pełne uprawnienia do dodawania i usuwania właścicieli. (Do momentu potwierdzony, **bieżącego właścicieli** sekcji wskazuje oczekują na zatwierdzenie dla tej osoby.)
1. Aby przetransferować własność (jako podczas zmiany własności lub pakiet został opublikowany na koncie niewłaściwy), Dodaj nowy właściciel, a po ich zostały potwierdzone własność one należy usunąć z listy.

Aby przypisać własność firmy lub grupy, należy utworzyć konto nuget.org przy użyciu alias poczty e-mail, który jest przekazywany do członków zespołu odpowiednie. Na przykład różnych pakietów Microsoft ASP.NET umieszczone są własnością [microsoft](http://nuget.org/profiles/microsoft) i [aspnet](http://nuget.org/profiles/aspnet) kont, która po prostu takich aliasów.

### <a name="recovering-package-ownership"></a>Odzyskiwanie własność pakietu

Czasami pakietu nie mogą mieć aktywne właściciela. Na przykład pierwotny właściciel mogą być przechowywane w firmie, która tworzy pakiet, nuget.org poświadczenia zostaną utracone lub wcześniejszych błędów w galerii pozostałych ownerless pakietu.

Jeśli jesteś właścicielem prawowitego pakietu i trzeba odzyskać własność, użyj [skontaktuj się z formularza](https://www.nuget.org/policies/Contact) na nuget.org w celu ułatwienia zrozumienia potrzeb do zespołu NuGet. Firma Microsoft postępuj procesu zweryfikowanie prawa własności pakietu, w tym próby zlokalizowania istniejących właściciela przez adres URL projektu pakietu, Twitter, poczty e-mail lub w inny sposób. Ale jeśli nie wszystkie inne, abyśmy mogli podać nowe zaproszenie do staje się właścicielem.
