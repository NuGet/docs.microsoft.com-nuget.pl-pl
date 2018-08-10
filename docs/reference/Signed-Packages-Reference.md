---
title: Podpisanych pakietów
description: Wymagania dotyczące podpisywania pakietu NuGet.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 992097281e21cd8cf37edf67fb1968b70c2b359b
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020521"
---
# <a name="signed-packages"></a>Podpisanych pakietów

*NuGet 4.6.0+ i Visual Studio 2017 w wersji 15.6 i nowszych*

Pakiety NuGet może zawierać podpis cyfrowy, który zapewnia ochronę przed zmodyfikowany zawartości. Ta sygnatura jest generowany z certyfikat X.509, który dodaje również autentyczności dowody do rzeczywistego źródła pakietu.

Podpisanych pakietów zapewnia najsilniejszą weryfikacji end-to-end. Istnieją dwa różne typy podpisów NuGet:
- **Tworzenie sygnatury**. Autor podpis gwarantuje, że pakiet nie został zmodyfikowany od czasu Autor podpisania pakietu, niezależnie od którego repozytorium lub co transportu metody jest dostarczany w pakiecie. Ponadto podpisane przez autora pakietów zapewniają mechanizm uwierzytelniania dodatkowego do potoku publikowania w witrynie nuget.org, ponieważ certyfikatu podpisywania musi być zarejestrowany wcześniej. Aby uzyskać więcej informacji, zobacz [rejestrowanie certyfikatów](#register-certificate-on-nugetorg).
- **Podpis repozytorium**. Podpisy repozytorium zapewniają gwarancji spójności dla **wszystkich** pakietów w repozytorium, czy są one podpisane lub nie, autor, nawet wtedy, gdy te pakiety są uzyskiwane z innej lokalizacji niż oryginalny repozytorium, gdzie znajdowały się podpisany.   

Aby uzyskać szczegółowe informacje na temat tworzenia pakietu podpisem autora, zobacz [podpisywanie pakietów](../create-packages/Sign-a-package.md) i [polecenie logowania nuget](../tools/cli-ref-sign.md).

> [!Important]
> Podpisywanie pakietów jest obecnie obsługiwana tylko wtedy, gdy za pomocą nuget.exe na Windows. Weryfikacja podpisanych pakietów jest obecnie obsługiwana tylko wtedy, gdy za pomocą nuget.exe lub Visual Studio na Windows.

## <a name="certificate-requirements"></a>Wymagania certyfikatu

Podpisywanie pakietów wymaga podpisywania certyfikatu, który to specjalny typ certyfikatu, który nadaje się do kodu `id-kp-codeSigning` cel [[RFC 5280 sekcji 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Ponadto certyfikat musi mieć publicznego długość klucza RSA 2048 bitów lub nowszej.

## <a name="get-a-code-signing-certificate"></a>Uzyskaj certyfikat podpisywania kodu

Prawidłowe certyfikaty mogą być uzyskane z publicznego urzędu certyfikacji takich jak:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Globalne logowania](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

Pełną listę urzędy certyfikacji używane przez Windows można uzyskać z [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Utwórz certyfikat testowy

Można użyć własnym wystawionych certyfikatów do celów testowych. Aby utworzyć własny wystawionego certyfikatu, użyj [polecenia PowerShell New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate.md).

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
> nuget.org nie akceptuje pakietów podpisany przy użyciu własnym wystawionych certyfikatów.

## <a name="timestamp-requirements"></a>Wymagania dotyczące znacznik czasu:

Podpisanych pakietów powinien zawierać znacznik czasu RFC 3161 w celu zapewnienia walidacji podpisu poza podpisywania okresu ważności certyfikatu pakietu. Certyfikat używany do podpisywania to sygnatura czasowa muszą być prawidłowe dla `id-kp-timeStamping` cel [[RFC 5280 sekcji 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Ponadto certyfikat musi mieć publicznego długość klucza RSA 2048 bitów lub nowszej.

Dodatkowe szczegóły techniczne można znaleźć w [specyfikacje techniczne podpisu pakietu](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Wymagania dotyczące podpisu w witrynie nuget.org

nuget.org ma dodatkowe wymagania dotyczące zaakceptowanie podpisanych pakietów:

- Podpis podstawowy musi mieć podpis autora.
- Podpis podstawowy musi mieć pojedynczy prawidłową sygnaturę czasową.
- Certyfikaty X.509 dla podpisu autora i jeho signatura sygnatura czasowa:
  - Musi mieć klucz publiczny RSA 2048 bitów lub nowszej.
  - Musi być w okresie ważności na bieżący czas UTC, podczas weryfikacji pakietu w witrynie nuget.org.
  - Muszą być powiązane z zaufanego głównego urzędu certyfikacji, który jest zaufany domyślnie w systemie Windows. Pakiety podpisany przy użyciu własnym wystawionych certyfikatów są odrzucane.
  - Musi być ważny przez jej przeznaczenie: 
    - Tworzenie certyfikatu podpisywania musi być prawidłowy do podpisywania kodu.
    - Znacznik czasu: musi to być nieprawidłowy dla użycia.
  - Nie musi zostać cofnięta podczas podpisywania czasu. (To nie będzie knowable w chwili przesyłania, więc nuget.org okresowo sprawdza ponownie stanu odwołania).

## <a name="register-certificate-on-nugetorg"></a>Zarejestruj certyfikat w witrynie nuget.org

Aby przesłać pakiet podpisem, należy zarejestrować certyfikat za pomocą nuget.org. Wymagany certyfikat jako `.cer` pliku w formacie binarnym DER. Możesz wyeksportować istniejący certyfikat na format binarny DER, za pomocą Kreatora eksportu certyfikatów.

![Kreator eksportu certyfikatów](media/CertificateExportWizard.png)

Zaawansowani użytkownicy można wyeksportować certyfikatu za pomocą [polecenia PowerShell eksportu certyfikatu](/powershell/module/pkiclient/export-certificate.md).

Aby zarejestrować certyfikat za pomocą nuget.org, przejdź do `Certificates` sekcji na `Account settings` stronie (lub na stronie Ustawienia w organizacji) i wybierz `Register new certificate`.

![Certyfikaty zarejestrowane](media/registered-certs.png)

> [!Tip]
> Jeden użytkownik może przesłać ten sam certyfikat i wielu certyfikatów, które mogą być rejestrowane przez wielu użytkowników.

Po użytkownik ma zarejestrowane certyfikatu, wszystkie przyszłe pakietu przesłania **musi** być podpisane przy użyciu jednego z certyfikatów.

Użytkownicy mogą również usuwać certyfikat zarejestrowany z konta. Po usunięciu certyfikatu na przesłanie się nie powieść pakietów podpisane przy użyciu tego certyfikatu. Nie ma wpływu na istniejące pakiety.

## <a name="configure-package-signing-requirements"></a>Skonfiguruj wymagania dotyczące podpisywania pakietu

Jeśli jesteś jedynym właścicielem pakietu, jest to wymagane osoby podpisującej. Oznacza to, że umożliwia dowolny zarejestrowane certyfikaty podpisywania pakietów i przekazywania na stronie nuget.org.

Jeżeli pakiet zawiera wiele właścicieli, domyślnie, certyfikaty "Dowolna" właściciel może służyć do podpisania pakietu. Jako współwłaściciela pakietu można zastąpić "Dowolne", przy użyciu samodzielnie lub wszelkie inne współwłaścicielem jako wymagane osoby podpisującej. W przypadku wprowadzenia właściciela, który nie ma żadnych certyfikatów zarejestrowanych pakietów niepodpisane będą dozwolone. 

Podobnie, jeśli wartość domyślna "Dowolna" opcja jest zaznaczona dla pakietu, w której jeden właściciel ma certyfikat zarejestrowany i innego właściciela nie ma żadnych certyfikatów zarejestrowanych, następnie nuget.org akceptuje podpisanych pakietów za pomocą podpisu zarejestrowany za pomocą jednej z jego właścicieli lub Niepodpisany pakietu (ponieważ jest to jeden z właścicieli nie ma żadnych certyfikatów zarejestrowanych).

![Konfigurowanie pakietów, które podpisały](media/configure-package-signers.png)
