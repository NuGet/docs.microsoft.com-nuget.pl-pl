---
title: Podpisywanie pakietów NuGet
description: Wyjaśnia, w jaki sposób można używać podpisanych pakietów, aby umożliwić weryfikację integralności zawartości.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 64b28c29ae3b533bde7c8f41dd38a4ab0a5afef7
ms.sourcegitcommit: 0cc6ac680c3202d0b036c0bed7910f6709215682
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/12/2020
ms.locfileid: "94550378"
---
# <a name="signing-nuget-packages"></a>Podpisywanie pakietów NuGet

Podpisane pakiety umożliwiają sprawdzenie spójności zawartości, co zapewnia ochronę przed manipulacją zawartości. Podpis pakietu służy również jako pojedyncze Źródło prawdziwości informacji o rzeczywistym pochodzeniu pakietu i autentyczności pakietu wspomaga dla konsumenta. W tym przewodniku przyjęto założenie, że pakiet został już [utworzony](creating-a-package.md).

## <a name="get-a-code-signing-certificate"></a>Pobierz certyfikat podpisywania kodu

Prawidłowe certyfikaty można uzyskać od publicznego urzędu certyfikacji, takiego jak [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [CERTUM](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)itp. Pełną listę urzędów certyfikacji zaufanych przez system Windows można uzyskać z programu [http://aka.ms/trustcertpartners](/security/trusted-root/participants-list) .

Do celów testowych można użyć certyfikatów wystawionych przez siebie. Pakiety podpisane przy użyciu certyfikatów z podpisem własnym nie są jednak akceptowane przez NuGet.org. Dowiedz się więcej [na temat tworzenia certyfikatu testowego](#create-a-test-certificate)

## <a name="export-the-certificate-file"></a>Eksportowanie pliku certyfikatu

* Istniejący certyfikat można wyeksportować do formatu binarny DER przy użyciu Kreatora eksportu certyfikatów.

  ![Kreator eksportu certyfikatów](../reference/media/CertificateExportWizard.png)

* Certyfikat można także wyeksportować za pomocą [polecenia programu PowerShell eksportu certyfikatów](/powershell/module/pkiclient/export-certificate).

## <a name="sign-the-package"></a>Podpisz pakiet

> [!note]
> Wymaga nuget.exe 4.6.0 lub nowszego. Pomoc techniczna dotnet.exe jest dostępna wkrótce [#7939](https://github.com/NuGet/Home/issues/7939)

Podpisz pakiet przy użyciu [znaku NuGet](../reference/cli-reference/cli-ref-sign.md):

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> Dostawca certyfikatów często zawiera również adres URL serwera sygnatury czasowej, którego można użyć dla `Timestamper` opcjonalnego argumentu Pokaż powyżej. Zapoznaj się z dokumentacją dostawcy i/lub pomocą techniczną dla tego adresu URL usługi.

* Możesz użyć certyfikatu dostępnego w magazynie certyfikatów lub użyć certyfikatu z pliku. Zobacz Dokumentacja interfejsu wiersza polecenia dla [znaku NuGet](../reference/cli-reference/cli-ref-sign.md).
* Podpisane pakiety powinny zawierać sygnaturę czasową, aby upewnić się, że sygnatura jest ważna po wygaśnięciu certyfikatu podpisywania. W przeciwnym razie operacja podpisywania spowoduje wygenerowanie [ostrzeżenia](../reference/errors-and-warnings/NU3002.md).
* Możesz zobaczyć szczegóły podpisu danego pakietu przy użyciu funkcji [weryfikacji NuGet](../reference/cli-reference/cli-ref-verify.md).

## <a name="register-the-certificate-on-nugetorg"></a>Rejestrowanie certyfikatu w usłudze NuGet.org

Aby opublikować podpisany pakiet, należy najpierw zarejestrować certyfikat z NuGet.org. Certyfikat jest potrzebny jako `.cer` plik w formacie binarnym der.

1. [Zaloguj](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) się do NuGet.org.
1. Przejdź do `Account settings` (lub `Manage Organization` **>** `Edit Organization` Jeśli chcesz zarejestrować certyfikat przy użyciu konta organizacji).
1. Rozwiń `Certificates` sekcję i wybierz pozycję `Register new` .
1. Wyszukaj i wybierz plik certyfikacie, który został wyeksportowany wcześniej.
  ![Zarejestrowane certyfikaty](../reference/media/registered-certs.png)

**Uwaga**
* Jeden użytkownik może przesłać wiele certyfikatów i ten sam certyfikat może być zarejestrowany przez wielu użytkowników.
* Gdy użytkownik ma zarejestrowany certyfikat, wszystkie przyszłe przesłania pakietu **muszą** być podpisane przy użyciu jednego z certyfikatów. Zobacz [Zarządzanie wymaganiami dotyczącymi podpisywania pakietu w witrynie NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)
* Użytkownicy mogą również usunąć zarejestrowany certyfikat z konta. Po usunięciu certyfikatu nowe pakiety podpisane przy użyciu tego certyfikatu będą kończyć się niepowodzeniem podczas wysyłania. Nie ma to wpływu na istniejące pakiety.

## <a name="publish-the-package"></a>Publikowanie pakietu

Teraz można przystąpić do publikowania pakietu w NuGet.org. Zobacz [Publikowanie pakietów](../nuget-org/Publish-a-package.md).

## <a name="create-a-test-certificate"></a>Tworzenie certyfikatu testowego

Do celów testowych można użyć certyfikatów wystawionych przez siebie. Aby utworzyć certyfikat z własnym wystawiony, użyj [polecenia New-SelfSignedCertificate programu PowerShell](/powershell/module/pkiclient/new-selfsignedcertificate).

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

To polecenie umożliwia utworzenie certyfikatu testowego dostępnego w osobistym magazynie certyfikatów bieżącego użytkownika. Można otworzyć magazyn certyfikatów, uruchamiając program `certmgr.msc` w celu wyświetlenia nowo utworzonego certyfikatu.

> [!Warning]
> Usługa NuGet.org nie akceptuje pakietów podpisanych za pomocą certyfikatów z podpisem własnym.

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a>Zarządzanie wymaganiami dotyczącymi podpisywania pakietu w programie NuGet.org
1. [Zaloguj](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) się do NuGet.org.

1. Przejdź do `Manage Packages`  
    ![ konfigurowania podpisywania pakietów](../reference/media/configure-package-signers.png)

* Jeśli jesteś jedynym właścicielem pakietu, jest to wymagana osoba podpisująca. możesz użyć dowolnego z zarejestrowanych certyfikatów do podpisywania i publikowania pakietów w usłudze NuGet.org.

* Jeśli pakiet ma wielu właścicieli, domyślnie do podpisania pakietu mogą służyć "dowolny" certyfikat właściciela. Jako współwłaściciel pakietu możesz przesłonić "dowolny" samodzielnie lub innym współpracownikom jako wymaganą rejestrację. Jeśli utworzysz właściciela, który nie ma żadnego zarejestrowanego certyfikatu, niepodpisane pakiety będą dozwolone. 

* Analogicznie, jeśli wybrana jest domyślna opcja "any" dla pakietu, w którym jeden właściciel ma zarejestrowany certyfikat, a inny właściciel nie ma żadnego zarejestrowanego certyfikatu, NuGet.org akceptuje albo podpisany pakiet z podpisem zarejestrowanym przez jednego z jego właścicieli lub niepodpisanym pakietem (ponieważ jeden z właścicieli nie ma żadnego zarejestrowanego certyfikatu).

## <a name="related-articles"></a>Pokrewne artykuły:

- [Zarządzanie granicami zaufania pakietów](../consume-packages/installing-signed-packages.md)
- [Odwołanie do podpisanych pakietów](../reference/Signed-Packages-Reference.md)