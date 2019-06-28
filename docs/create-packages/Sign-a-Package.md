---
title: Podpisywanie pakietów NuGet
description: Wyjaśnia, jak podpisanych pakietów może służyć do włączyć weryfikację zawartości integralności.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: abdd06642ccc652527a1a005eda2689ce97df74c
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426813"
---
# <a name="signing-nuget-packages"></a>Podpisywanie pakietów NuGet

Testy weryfikacji integralności zawartości, które zapewnia ochronę przed naruszeniem zawartości umożliwia podpisanych pakietów. Podpis pakietu również służy jako pojedyncze źródło prawdziwych informacji o rzeczywistego pochodzenia pakietu i klinowe autentyczności pakietu dla konsumentów. W tym przewodniku założono, że już [utworzył pakiet](creating-a-package.md).

## <a name="get-a-code-signing-certificate"></a>Uzyskaj certyfikat podpisywania kodu

Prawidłowe certyfikaty mogą być uzyskane z publicznego urzędu certyfikacji takich jak [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [globalnego logowania](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)itp. Pełną listę urzędy certyfikacji używane przez Windows można uzyskać z [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

Można użyć własnym wystawionych certyfikatów do celów testowych. Pakiety podpisany przy użyciu własnym wystawionych certyfikatów nie są akceptowane przez NuGet.org. Dowiedz się więcej o [tworzenia certyfikatu testowego](#create-a-test-certificate)

## <a name="export-the-certificate-file"></a>Eksportuj plik certyfikatu

* Możesz wyeksportować istniejący certyfikat na format binarny DER, za pomocą Kreatora eksportu certyfikatów.

  ![Kreator eksportu certyfikatów](../reference/media/CertificateExportWizard.png)

* Możesz też wyeksportować certyfikat przy użyciu [polecenia PowerShell eksportu certyfikatu](/powershell/module/pkiclient/export-certificate).

## <a name="sign-the-package"></a>Podpisywanie pakietu

> [!note]
> Wymaga nuget.exe 4.6.0 lub nowszej

Zaloguj się przy użyciu pakietu [logowania nuget](../tools/cli-ref-sign.md):

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> Dostawca certyfikatów często są także używane dla adresu URL serwera timestamping `Timestamper` Pokaż opcjonalny argument powyżej. Zapoznaj się z dokumentacją z dostawcą i/lub pomocy technicznej dla tego adresu URL usługi.

* Można użyć certyfikatu jest dostępny w magazynie certyfikatów lub używany certyfikat z pliku. Zobacz odwołanie do interfejsu wiersza polecenia [logowania nuget](../tools/cli-ref-sign.md).
* Podpisanych pakietów powinien zawierać sygnaturę czasową, aby upewnić się, że podpis pozostaje ważny, gdy wygasł certyfikat podpisywania. Inne dadzą operacji logowania [ostrzeżenie](../reference/errors-and-warnings/NU3002.md).
* Można wyświetlić szczegóły podpisu danego pakietu przy użyciu [Sprawdź nuget](../tools/cli-ref-verify.md).

## <a name="register-the-certificate-on-nugetorg"></a>Zarejestruj certyfikat w witrynie NuGet.org

Aby opublikować podpisanych pakietów, należy zarejestrować certyfikat za pomocą NuGet.org. Wymagany certyfikat jako `.cer` pliku w formacie binarnym DER.

1. [Zaloguj się](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) na stronie NuGet.org.
1. Przejdź do `Account settings` (lub `Manage Organization` **>** `Edit Organziation` Jeśli chcesz zarejestrować certyfikat przy użyciu konta organizacji).
1. Rozwiń `Certificates` i wybierz pozycję `Register new`.
1. Przeglądaj i wybierz wyeksportowany wcześniej plik rozszyfrować przy jego użyciu.
  ![Certyfikaty zarejestrowane](../reference/media/registered-certs.png)

**Uwaga**
* Jeden użytkownik może przesłać ten sam certyfikat i wielu certyfikatów, które mogą być rejestrowane przez wielu użytkowników.
* Po użytkownik ma zarejestrowane certyfikatu, wszystkie przyszłe pakietu przesłania **musi** być podpisane przy użyciu jednego z certyfikatów. Zobacz [Zarządzaj podpisywania wymagania dotyczące pakietu w witrynie NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)
* Użytkownicy mogą również usuwać certyfikat zarejestrowany z konta. Po usunięciu certyfikatu nie powiedzie się na przesyłanie nowe pakiety podpisany przy użyciu tego certyfikatu. Nie ma wpływu na istniejące pakiety.

## <a name="publish-the-package"></a>Publikowanie pakietu

Teraz można przystąpić do opublikowania pakietu na stronie NuGet.org. Zobacz [publikowania pakietów](../nuget-org/Publish-a-package.md).

## <a name="create-a-test-certificate"></a>Utwórz certyfikat testowy

Można użyć własnym wystawionych certyfikatów do celów testowych. Aby utworzyć własny wystawionego certyfikatu, użyj [polecenia PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate).

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

To polecenie tworzy certyfikat testowania dostępności w magazynie certyfikatów osobistych bieżącego użytkownika. Można otworzyć magazynu certyfikatów, uruchamiając `certmgr.msc` aby zobaczyć nowo utworzonego certyfikatu.

> [!Warning]
> NuGet.org nie akceptuje pakietów podpisany przy użyciu własnym wystawionych certyfikatów.

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a>Zarządzanie wymagania podpisywania pakietu w witrynie NuGet.org
1. [Zaloguj się](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) na stronie NuGet.org.

1. Przejdź do `Manage Packages`  
    ![Konfigurowanie pakietów, które podpisały](../reference/media/configure-package-signers.png)

* Jeśli jesteś jedynym właścicielem pakietu, są wymagane osoby podpisującej tj służy dowolne zarejestrowane certyfikaty do podpisywania i publikowania pakietów NuGet.org.

* Jeżeli pakiet zawiera wiele właścicieli, domyślnie, certyfikaty "Dowolna" właściciel może służyć do podpisania pakietu. Jako współwłaściciela pakietu można zastąpić "Dowolne", przy użyciu samodzielnie lub wszelkie inne współwłaścicielem jako wymagane osoby podpisującej. W przypadku wprowadzenia właściciela, który nie ma żadnych certyfikatów zarejestrowanych pakietów niepodpisane będą dozwolone. 

* Podobnie, jeśli wartość domyślna "Dowolna" opcja jest zaznaczona dla pakietu, w której jeden właściciel ma certyfikat zarejestrowany i innego właściciela nie ma żadnych certyfikatów zarejestrowanych, następnie NuGet.org akceptuje podpisanych pakietów za pomocą podpisu zarejestrowany za pomocą jednej z jego właścicieli lub Niepodpisany pakietu (ponieważ jest to jeden z właścicieli nie ma żadnych certyfikatów zarejestrowanych).

## <a name="related-articles"></a>Pokrewne artykuły:

- [Zarządzanie granicami zaufania pakietu](../consume-packages/installing-signed-packages.md)
- [Dokumentacja podpisanych pakietów](../reference/Signed-Packages-Reference.md)
