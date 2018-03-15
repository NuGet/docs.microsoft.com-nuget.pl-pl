---
title: "Jak opublikować pakietu NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/05/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Szczegółowe instrukcje dotyczące sposobu publikowania pakietu NuGet nuget.org lub prywatnej źródeł danych i jak zarządzać własność pakietu na nuget.org."
keywords: "Publikowanie pakietu NuGet, publikowania pakietu NuGet, własność pakietu NuGet, publikować nuget.org, prywatnego źródeł danych NuGet"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6cb582c036392ae2792f2fa4d307370e91c4f961
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/15/2018
---
# <a name="publishing-packages"></a>Publikowanie pakietów

Gdy utworzono pakiet i mieć Twojej `.nukpg` w pliku, jest prosty proces, aby udostępnić ją innym producentom publiczną lub prywatną:

- Pakiety publicznego były dostępne dla wszystkich deweloperów globalnie za pomocą [nuget.org](https://www.nuget.org/packages/manage/upload) zgodnie z opisem w tym temacie.
- Pakietów prywatnych są dostępne dla tylko zespół lub organizacja, umieszczając je albo udziału plików, serwer prywatnej NuGet [Visual Studio Team Services pakietu zarządzania](https://www.visualstudio.com/docs/package/nuget/publish), lub repozytorium innych firm, takich jak myget, ProGet, węzła Repozytorium i Artifactory. Aby uzyskać więcej informacji, zobacz [Hosting Omówienie pakietów](../hosting-packages/overview.md).

W tym temacie omówiono publikowanie nuget.org; do publikowania w Visual Studio Team Services, zobacz [zarządzania pakietami](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Publikowanie nuget.org

Dla nuget.org, należy najpierw [zarejestrować bezpłatne konto](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) lub zaloguj się, jeśli jest już zarejestrowany:

![Rejestracja NuGet i zalogować się w lokalizacji](media/publish_NuGetSignIn.png)

Następnie można albo przekaż pakiet w portalu sieci web nuget.org, wypychać do nuget.org za pomocą wiersza polecenia (wymaga `nuget.exe` 4.1.0+), lub Opublikuj jako część procesu CI/CD za pomocą programu Visual Studio Team Services, zgodnie z opisem w poniższych sekcjach.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Portal sieci Web: karta przekaż pakiet na nuget.org

![Przekaż pakiet z Menedżera pakietów NuGet](media/publish_UploadYourPackage.PNG)

### <a name="command-line"></a>Wiersz polecenia

> [!Important]
> Pakiety wypychania do nuget.org musi używać [nuget.exe v4.1.0 lub nowszej](https://www.nuget.org/downloads), który implementuje wymaganych [protokołów NuGet](../api/nuget-protocols.md).

1. Kliknij nazwę użytkownika, aby przejść do ustawień konta.
1. W obszarze **klucz interfejsu API**, kliknij przycisk **Kopiuj do Schowka** można pobrać dostępu do klucza należy w interfejsu wiersza polecenia:

    ![Kopiowanie klucza interfejsu API z ustawienia konta](media/publish_APIKey.png)

1. W wierszu polecenia Uruchom następujące polecenie:

    ```cli
    nuget setApiKey Your-API-Key
    ```

    Klucz interfejsu API to przechowuje na komputerze, dzięki czemu nie muszą wykonać ten krok ponownie na tym samym komputerze.

1. Wypychanie do pakietu do galerii NuGet za pomocą polecenia:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

1. Przed upubliczniona są wszystkie pakiety przekazane do nuget.org są skanowany w poszukiwaniu wirusów i odrzucone w przypadku znalezienia wirusów. Wszystkie pakiety wymienione na nuget.org również są skanowane okresowo.

1. Na koncie nuget.org, kliknij przycisk **Moje pakiety zarządzania** aby zobaczyć ten właśnie opublikowane; otrzymasz wiadomość e-mail z potwierdzeniem. Należy pamiętać, że może upłynąć trochę czasu pakietu indeksowane i wyświetlane w wynikach wyszukiwania, gdy inne można znaleźć go w tym czasie zostanie wyświetlony następujący komunikat na stronie pakiet:

    ![Komunikat wskazujący, że pakiet nie jest jeszcze indeksowanym.](media/publish_NotYetIndexed.png)

### <a name="package-validation-and-indexing"></a>Sprawdzanie poprawności pakietu i indeksowania

Pakiety do nuget.org przechodzą kilku operacji sprawdzania poprawności. Po upływie wszystkie testy sprawdzania poprawności pakietu może upłynąć trochę czasu na jej indeksowane i wyświetlane w wynikach wyszukiwania. Po zakończeniu indeksowania otrzymasz wiadomość e-mail z potwierdzeniem, że pakiet został pomyślnie opublikowany. W przypadku niepowodzenia sprawdzenia poprawności pakietu na stronie Szczegóły pakietu zostanie zaktualizowana, aby wyświetlić skojarzony błąd i otrzymasz wiadomość e-mail powiadomienia użytkownika o nim.

Sprawdzanie poprawności pakietu i indeksowania zazwyczaj trwa poniżej 15 minut. Publikowanie pakietu trwa dłużej niż oczekiwano, odwiedź stronę [status.nuget.org](https://status.nuget.org/) do sprawdzenia, czy nuget.org występują żadnych przerw w działaniu. Jeśli pakiet nie został pomyślnie opublikowany w ciągu godziny są wszystkie systemy operacyjne, zaloguj się do nuget.org i skontaktuj się z nami za pomocą łącza Skontaktuj się z pomocą techniczną na stronie pakiet.

### <a name="visual-studio-team-services-cicd"></a>Visual Studio Team Services (CI/CD)

Jeśli pakiety są Wypychanie do nuget.org jako część procesu ciągłej integracji/wdrożenia przy użyciu programu Visual Studio Team Services, należy użyć `nuget.exe` 4.1 lub nowszej w zadaniach NuGet. Szczegółowe informacje można znaleźć w [za pomocą najnowszej NuGet w kompilacji](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blog DevOps firmy Microsoft).

## <a name="managing-package-owners-on-nugetorg"></a>Zarządzanie właścicielami pakietu na nuget.org

Mimo że każdy pakiet NuGet `.nuspec` pliku definiuje autorów pakietu, Galeria nuget.org nie używa tych metadanych do definiowania własności. Zamiast tego nuget.org przypisuje początkowej prawa własności do osoby, która publikuje pakiet. To jest zalogowany użytkownik, który pakiet za pomocą nuget.org interfejsu użytkownika lub użytkowników, którego klucz interfejsu API została użyta z `nuget SetApiKey` lub `nuget push`.

Wszystkie właściciele pakietu mają pełne uprawnienia do pakietu, w tym dodawanie i usuwanie właścicieli innych oraz publikowanie aktualizacji.

Aby zmienić własność pakietu, wykonaj następujące czynności:

1. Zaloguj się do nuget.org przy użyciu konta, który jest bieżącym właścicielem pakietu.
1. Kliknij swoją nazwę użytkownika, następnie **Moje pakiety zarządzania**, a następnie na pakiet, którym chcesz zarządzać.
1. Kliknij przycisk **Zarządzaj właścicielami** link po lewej stronie.

W tym miejscu masz kilka opcji:

1. Aby dodać właściciela, wprowadź nazwę konta ich NuGet, a następnie kliknij przycisk **Dodaj**. To wysyła wiadomość e-mail do tej nowej współwłaściciel Link potwierdzenia. Po potwierdzeniu, że osoba ma pełne uprawnienia do dodawania i usuwania właścicieli. (Do momentu potwierdzony, **Zarządzaj właścicielami** strony wskazuje "oczekuje na zatwierdzenie" dla tej osoby).
1. Aby usunąć właściciela, wybierz odpowiednią nazwę na **Zarządzaj właścicielami** i kliknij przycisk **Usuń**.
1. Aby przetransferować własność (jako podczas zmiany własności lub pakiet został opublikowany na koncie niewłaściwy), po prostu Dodaj nowy właściciel, a po ich zostały potwierdzone własność one należy usunąć z listy.

Aby przypisać własność firmy lub grupy, należy utworzyć konto nuget.org przy użyciu alias poczty e-mail, który jest przekazywany do członków zespołu odpowiednie. Na przykład różnych pakietów Microsoft ASP.NET umieszczone są własnością [microsoft](http://nuget.org/profiles/microsoft) i [aspnet](http://nuget.org/profiles/aspnet) kont, która po prostu takich aliasów.

### <a name="recovering-package-ownership"></a>Odzyskiwanie własność pakietu

Czasami pakietu nie mogą mieć aktywne właściciela. Na przykład pierwotny właściciel mogą być przechowywane w firmie, która tworzy pakiet, nuget.org poświadczenia zostaną utracone lub wcześniejszych błędów w galerii pozostałych ownerless pakietu.

Jeśli jesteś właścicielem prawowitego pakietu i trzeba odzyskać własność, użyj [skontaktuj się z formularza](https://www.nuget.org/policies/Contact) na nuget.org w celu ułatwienia zrozumienia potrzeb do zespołu NuGet. Firma Microsoft postępuj procesu zweryfikowanie prawa własności pakietu, w tym próby zlokalizowania istniejących właściciela przez adres URL projektu pakietu, Twitter, poczty e-mail lub w inny sposób. Ale jeśli nie wszystkie inne, abyśmy mogli podać nowe zaproszenie do staje się właścicielem.
