---
title: Podpisanych pakietów
description: Wymagania dotyczące podpisywania pakietu NuGet.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 72fb1a87c13160c53f632d2ef87a12a4e9bc02a3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/22/2018
ms.locfileid: "34449594"
---
# <a name="signed-packages"></a>Pakiety podpisem

*NuGet 4.6.0+ i Visual Studio 2017 wersji 15.6 i nowsze*

Pakiety NuGet mogą zawierać podpis cyfrowy, który zapewnia ochronę przed zmodyfikowany zawartości. Ta sygnatura jest tworzony z certyfikatu X.509, który dodaje również dowody autentyczności do rzeczywistego źródła pakietu.

Pakiety podpisem udostępnienia najwyższy weryfikacji end-to-end. Autor podpis gwarantuje, że pakiet nie został zmodyfikowany od czasu autora podpisania pakietu, niezależnie od którego repozytorium lub co metoda jest dostarczany pakiet transportu.

Ponadto pakiety podpisane przez autora udostępniają mechanizm uwierzytelniania dodatkowego do potoku publikowania nuget.org, ponieważ certyfikat podpisywania musi być zarejestrowana wcześniejsze. Aby uzyskać więcej informacji, zobacz [rejestrowanie certyfikatów](#register-certificate-on-nugetorg).

Aby uzyskać więcej informacji na temat tworzenia podpisanego pakietu, zobacz [podpisywania pakietów](../create-packages/Sign-a-package.md) i [polecenia nuget znak](../tools/cli-ref-sign.md).

> [!Important]
> Podpisywanie pakietu jest obecnie obsługiwany tylko w przypadku używania nuget.exe w systemie Windows. Weryfikacja podpisanych pakietów jest obecnie obsługiwany tylko w przypadku używania nuget.exe lub Visual Studio w systemie Windows.

## <a name="certificate-requirements"></a>Wymagania certyfikatu

Podpisywanie pakietu wymaga podpisywania certyfikatu, który jest specjalny typ certyfikatu, który jest prawidłowy dla kodu `id-kp-codeSigning` cel [[RFC 5280 sekcji 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Ponadto certyfikat musi mieć publiczny długość klucza RSA 2048 bitów lub nowszej.

## <a name="get-a-code-signing-certificate"></a>Uzyskaj certyfikat podpisywania kodu

Prawidłowe certyfikaty można uzyskać od urzędu certyfikacji publicznej, takich jak:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Globalne logowania](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

Pełna lista urzędów certyfikacji ufa systemu Windows można uzyskać z [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Tworzenie certyfikatu testowego

Wystawiony samodzielnie Certyfikaty służy do celów testowych. Aby utworzyć certyfikat wystawiony samodzielnie, użyj [polecenia New-SelfSignedCertificate PowerShell](/powershell/module/pkiclient/new-selfsignedcertificate.md).

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

To polecenie tworzy testowania dostępny certyfikat w magazynie certyfikatów osobistych bieżącego użytkownika. Można otworzyć magazynu certyfikatów, uruchamiając `certmgr.msc` wyświetlić nowo utworzony certyfikat.

> [!Warning]
> nuget.org nie akceptuje pakietów podpisane własnym wystawionych certyfikatów.

## <a name="timestamp-requirements"></a>Wymagania dotyczące sygnatury czasowej

Pakiety podpisem powinna zawierać znaczników czasu RFC 3161 do zapewnienia walidacji podpisu poza okres ważności certyfikatu podpisywania pakietu. Certyfikat używany do podpisywania sygnatura czasowa musi być prawidłowy dla `id-kp-timeStamping` cel [[RFC 5280 sekcji 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Ponadto certyfikat musi mieć publiczny długość klucza RSA 2048 bitów lub nowszej.

Dodatkowe szczegóły techniczne można znaleźć w [specyfikacji technicznej podpisu pakietu](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Wymagania dotyczące podpisu na nuget.org

nuget.org ma dodatkowe wymagania dotyczące akceptowania podpisanego pakietu:

- Podpis podstawowy musi być podpis autora.
- Podpis podstawowy musi mieć pojedynczy prawidłowy sygnatury czasowej.
- Certyfikaty X.509 dla podpisu autora i podpis sygnatura czasowa:
  - Musi mieć klucza publicznego RSA 2048 bitów lub większej.
  - Musi być w okresie ważności na bieżący czas UTC podczas sprawdzania poprawności pakietu na nuget.org.
  - Muszą być powiązane z zaufanego głównego urzędu zaufanej domyślnie w systemie Windows. Pakiety podpisane własnym wystawione certyfikaty są odrzucane.
  - Musi być prawidłową celowi: 
    - Tworzenie certyfikatu podpisywania musi być prawidłowy do podpisywania kodu.
    - Sygnatura czasowa certyfikatu musi być prawidłowy dla użycia.
  - Nie musi zostać odwołany podczas podpisywania czasu. (To nie będzie knowable podczas przesyłania, więc nuget.org okresowo sprawdza ponownie stanu odwołania).

## <a name="register-certificate-on-nugetorg"></a>Zarejestruj certyfikat na nuget.org

Aby przesłać pakiet podpisem, najpierw należy zarejestrować certyfikat z nuget.org. Wymagany jest certyfikat jako `.cer` pliku w formacie binarnym DER. Możesz wyeksportować istniejącego certyfikatu na format binarny DER przy użyciu Kreatora eksportu certyfikatów.

![Kreator eksportu certyfikatów](media/CertificateExportWizard.png)

Użytkownicy wersji Advanced można wyeksportować certyfikat przy użyciu [polecenia programu PowerShell eksportu certyfikatu](/powershell/module/pkiclient/export-certificate.md).

Aby zarejestrować certyfikat z nuget.org, przejdź do `Certificates` sekcji na `Account settings` (lub strona Ustawienia organizacji) i wybierz `Register new certificate`.

![Zarejestrowane certyfikaty](media/registered-certs.png)

> [!Tip]
> Jeden z użytkowników mogą przesyłać wiele certyfikatów i tego samego certyfikatu można zarejestrowanych przez wielu użytkowników.

Gdy użytkownik ma certyfikat zarejestrowany, wszystkie przyszłe pakietu przesłanych **musi** podpisywany z jednego z certyfikatów.

Użytkownicy mogą również usuwać zarejestrowany certyfikat z konta. Po usunięciu certyfikatu z takim podpisem pakietów się nie powieść w przesyłania. Nie ma wpływu na istniejące pakiety.

## <a name="configure-package-signing-requirements"></a>Skonfiguruj wymagania dotyczące podpisywania pakietu

Jeśli jesteś jedynym właścicielem pakietu jest wymagany podpis. Oznacza to, że służy wszelkie zarejestrowane certyfikaty do podpisywania pakietów i przedstawia nuget.org.

Jeżeli pakiet zawiera wiele właścicieli, domyślnie, "Wszystkie" właściciel certyfikaty mogą służyć do podpisania pakietu. Jako współwłaściciel pakietu można zastąpić "Dowolnego" siebie lub wszelkie inne współwłaściciel jako wymagany podpis. Jeśli wprowadzisz właściciela, który nie ma żadnych certyfikatów zarejestrowanych pakietów niepodpisane będą dozwolone. 

Podobnie, jeśli wartość domyślna "Wszystkie" zaznaczono opcję pakiet gdzie jednego właściciela ma certyfikat, który został zarejestrowany i innemu właścicielowi nie ma żadnych certyfikatów zarejestrowanych, następnie nuget.org akceptuje podpisanego pakietu za pomocą podpisu w zarejestrowany za pomocą jednej z jego właścicieli lub Niepodpisany pakiet (ponieważ jeden właścicieli nie ma żadnych certyfikatów zarejestrowanych).

![Skonfiguruj pakietów osoby podpisujące](media/configure-package-signers.png)
