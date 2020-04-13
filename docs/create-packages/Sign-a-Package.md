---
title: Podpisywanie pakietów NuGet
description: W tym artykule wyjaśniono, jak podpisane pakiety mogą służyć do włączania weryfikacji integralności zawartości.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 00fe1d5fa81132b5d6826203a0d26e56aa8d4755
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429004"
---
# <a name="signing-nuget-packages"></a>Podpisywanie pakietów NuGet

Podpisane pakiety umożliwiają sprawdzanie integralności zawartości, co zapewnia ochronę przed manipulowaniem zawartością. Podpis pakietu służy również jako jedno źródło prawdy o rzeczywistym pochodzeniu pakietu i wzmacnia autentyczność pakietu dla konsumenta. W tym przewodniku założono, że pakiet został już [utworzony.](creating-a-package.md)

## <a name="get-a-code-signing-certificate"></a>Uzyskaj certyfikat podpisywania kodu

Ważne certyfikaty mogą być uzyskane z publicznego urzędu certyfikacji, takiego jak [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)itp. Pełną listę urzędów certyfikacji zaufanych [http://aka.ms/trustcertpartners](https://aka.ms/trustcertpartners)przez system Windows można uzyskać z programu .

Do celów testowych można używać certyfikatów wystawionych samodzielnie. Jednak pakiety podpisane przy użyciu certyfikatów wystawionych samodzielnie nie są akceptowane przez NuGet.org. Dowiedz się więcej o [tworzeniu certyfikatu testowego](#create-a-test-certificate)

## <a name="export-the-certificate-file"></a>Eksportowanie pliku certyfikatu

* Istniejący certyfikat można wyeksportować do binarnego formatu DER za pomocą Kreatora eksportu certyfikatów.

  ![Kreator eksportu certyfikatów](../reference/media/CertificateExportWizard.png)

* Certyfikat można również wyeksportować za pomocą [polecenia Programu PowerShell certyfikat eksportu](/powershell/module/pkiclient/export-certificate).

## <a name="sign-the-package"></a>Podpisz paczkę

> [!note]
> Wymaga nuget.exe 4.6.0 lub nowszego. dotnet.exe wsparcie już wkrótce - [#7939](https://github.com/NuGet/Home/issues/7939)

Podpisz pakiet za pomocą [znaku nuget:](../reference/cli-reference/cli-ref-sign.md)

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> Dostawca certyfikatów często udostępnia również adres URL serwera sygnatury czasowej, którego można użyć w przypadku opcjonalnego argumentu `Timestamper` wyświetlenia powyżej. Zapoznaj się z dokumentacją dostawcy i/lub pomocą techniczną dotyczącą tego adresu URL usługi.

* Można użyć certyfikatu dostępnego w magazynie certyfikatów lub użyć certyfikatu z pliku. Zobacz odwołanie do interfejsu wiersza polecenia dla [znaku nuget](../reference/cli-reference/cli-ref-sign.md).
* Podpisane pakiety powinny zawierać sygnaturę czasową, aby upewnić się, że podpis pozostaje ważny po wygaśnięciu certyfikatu podpisywania. W przeciwnym razie operacja znaku spowoduje [ostrzeżenie](../reference/errors-and-warnings/NU3002.md).
* Możesz zobaczyć szczegóły podpisu danego pakietu za pomocą [nuget verify](../reference/cli-reference/cli-ref-verify.md).

## <a name="register-the-certificate-on-nugetorg"></a>Zarejestruj certyfikat na NuGet.org

Aby opublikować podpisany pakiet, należy najpierw zarejestrować certyfikat w NuGet.org. Certyfikat jest potrzebny `.cer` jako plik w binarnym formacie DER.

1. [Zaloguj się,](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) aby NuGet.org.
1. Przejdź `Account settings` do `Manage Organization` **>** `Edit Organziation` (lub jeśli chcesz zarejestrować certyfikat na koncie organizacji).
1. Rozwiń `Certificates` sekcję `Register new`i wybierz opcję .
1. Przeglądaj i wybierz plik certficate, który został wyeksportowany wcześniej.
  ![Zarejestrowane certyfikaty](../reference/media/registered-certs.png)

**Uwaga**
* Jeden użytkownik może przesłać wiele certyfikatów, a ten sam certyfikat może być zarejestrowany przez wielu użytkowników.
* Gdy użytkownik ma zarejestrowany certyfikat, wszystkie przyszłe zgłoszenia pakietów **muszą** być podpisane za pomocą jednego z certyfikatów. Zobacz [Zarządzanie wymaganiami dotyczącymi podpisywania pakietu na NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)
* Użytkownicy mogą również usunąć zarejestrowany certyfikat z konta. Po usunięciu certyfikatu nowe pakiety podpisane za pomocą tego certyfikatu nie powiedzie się podczas przesyłania. Nie ma to wpływu na istniejące pakiety.

## <a name="publish-the-package"></a>Publikowanie pakietu

Teraz możesz opublikować pakiet, aby NuGet.org. Zobacz [Publikowanie pakietów](../nuget-org/Publish-a-package.md).

## <a name="create-a-test-certificate"></a>Tworzenie certyfikatu testowego

Do celów testowych można używać certyfikatów wystawionych samodzielnie. Aby utworzyć certyfikat wystawiony samodzielnie, należy użyć [polecenia New-SelfSignedCertificate PowerShell](/powershell/module/pkiclient/new-selfsignedcertificate).

```ps
New-SelfSignedCertificate -Subject "CN=NuGet Test Developer, OU=Use for testing purposes ONLY" `
                          -FriendlyName "NuGetTestDeveloper" `
                          -Type CodeSigning `
                          -KeyUsage DigitalSignature `
                          -KeyLength 2048 `
                          -KeyAlgorithm RSA `
                          -HashAlgorithm SHA256 `
                          -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
                          -CertStoreLocation "Cert:\CurrentUser\My" 
```

To polecenie tworzy certyfikat testowania dostępny w magazynie certyfikatów osobistych bieżącego użytkownika. Magazyn certyfikatów można otworzyć, uruchamiając `certmgr.msc` nowo utworzony certyfikat.

> [!Warning]
> NuGet.org nie akceptuje pakietów podpisanych certyfikatami wystawionymi samodzielnie.

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a>Zarządzanie wymaganiami dotyczącymi podpisywania pakietu na NuGet.org
1. [Zaloguj się,](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) aby NuGet.org.

1. Przejdź `Manage Packages`  
    ![do konfigurowania sygnatariuszy pakietu](../reference/media/configure-package-signers.png)

* Jeśli jesteś jedynym właścicielem pakietu, jesteś wymaganym sygnatariuszem, czyli możesz użyć dowolnego z zarejestrowanych certyfikatów do podpisania i opublikowania swoich paczek, aby NuGet.org.

* Jeśli pakiet ma wielu właścicieli, domyślnie certyfikaty właściciela "Dowolna" mogą być używane do podpisywania pakietu. Jako współwłaściciel pakietu możesz zastąpić "Dowolny" ze sobą lub innym współwłaścicielem, aby być wymaganym sygnatariuszem. Jeśli zrobisz właściciela, który nie ma żadnego certyfikatu zarejestrowanego, niepodpisane pakiety będą dozwolone. 

* Podobnie, jeśli domyślna opcja "Dowolna" jest zaznaczona dla pakietu, w którym jeden właściciel ma zarejestrowany certyfikat, a inny właściciel nie ma zarejestrowanego certyfikatu, NuGet.org akceptuje podpisany pakiet z podpisem zarejestrowanym przez jednego z jego właścicieli lub niepodpisany pakiet (ponieważ jeden z właścicieli nie ma żadnego certyfikatu zarejestrowanego).

## <a name="related-articles"></a>Pokrewne artykuły:

- [Zarządzanie granicami zaufania pakietów](../consume-packages/installing-signed-packages.md)
- [Odwołanie do pakietów podpisanych](../reference/Signed-Packages-Reference.md)
