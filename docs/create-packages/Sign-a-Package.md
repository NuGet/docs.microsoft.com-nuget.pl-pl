---
title: Podpisywanie pakietów NuGet
description: Wyjaśnia, w jaki sposób podpisane pakiety mogą być używane do włączania weryfikacji integralności zawartości.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: c0622520a325000d5fcb8fb884cb509ee4b641f4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901905"
---
# <a name="signing-nuget-packages"></a>Podpisywanie pakietów NuGet

Podpisane pakiety umożliwiają sprawdzanie integralności zawartości, co zapewnia ochronę przed naruszeniem zawartości. Podpis pakietu służy również jako pojedyncze źródło prawdziwych informacji o rzeczywistym pochodzeniu pakietu i wzmacnia autentyczność pakietu dla konsumenta. W tym przewodniku przyjęto założenie, [że utworzono już pakiet](creating-a-package.md).

## <a name="get-a-code-signing-certificate"></a>Uzyskiwanie certyfikatu podpisywania kodu

Prawidłowe certyfikaty można uzyskać z publicznego urzędu certyfikacji, takiego jak [DigiCert,](https://www.digicert.com/code-signing/) [Global Sign,](https://www.globalsign.com/en/code-signing-certificate/) [Comodo,](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php) [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)itp. Pełną listę urzędów certyfikacji zaufanych przez system Windows można uzyskać na stronie [http://aka.ms/trustcertpartners](/security/trusted-root/participants-list) .

Certyfikatów wystawionych samodzielnie można używać do celów testowych. Jednak pakiety podpisane przy użyciu certyfikatów wystawionych samodzielnie nie są akceptowane przez NuGet.org. Dowiedz się więcej o [tworzeniu certyfikatu testowego](#create-a-test-certificate)

## <a name="export-the-certificate-file"></a>Eksportowanie pliku certyfikatu

* Istniejący certyfikat można wyeksportować do binarnego formatu DER przy użyciu Kreatora eksportu certyfikatów.

  ![Kreator eksportu certyfikatów](../reference/media/CertificateExportWizard.png)

* Certyfikat można również wyeksportować przy użyciu [polecenia programu PowerShell Export-Certificate](/powershell/module/pkiclient/export-certificate).

## <a name="sign-the-package"></a>Podpisywanie pakietu

> [!note]
> Wymaga nuget.exe 4.6.0 lub nowszej. dotnet.exe wkrótce — #7939 [](https://github.com/NuGet/Home/issues/7939)

Podpisz pakiet przy użyciu [znaku nuget:](../reference/cli-reference/cli-ref-sign.md)

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> Dostawca certyfikatów często udostępnia również adres URL serwera ze znacznikiem czasu, którego można użyć dla `Timestamper` opcjonalnego argumentu wyświetlanego powyżej. Zapoznaj się z dokumentacją dostawcy i/lub pomocą techniczną dotyczącą tego adresu URL usługi.

* Możesz użyć certyfikatu dostępnego w magazynie certyfikatów lub certyfikatu z pliku. Zobacz cli reference for nuget sign (Informacje dotyczące [interfejsu wiersza polecenia dla znaku nuget).](../reference/cli-reference/cli-ref-sign.md)
* Podpisane pakiety powinny zawierać znacznik czasu, aby upewnić się, że podpis pozostaje ważny po wygaśnięciu certyfikatu podpisywania. W innym przypadku operacja podpisywania [spowoduje](../reference/errors-and-warnings/NU3002.md)ostrzeżenie .
* Szczegóły sygnatury danego pakietu można wyświetlić przy użyciu narzędzia [nuget verify](../reference/cli-reference/cli-ref-verify.md).

## <a name="register-the-certificate-on-nugetorg"></a>Zarejestruj certyfikat w NuGet.org

Aby opublikować podpisany pakiet, należy najpierw zarejestrować certyfikat w NuGet.org. Certyfikat jest potrzebny jako plik `.cer` w binarnym formacie DER.

1. [Zaloguj się](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) do NuGet.org.
1. Przejdź do (lub jeśli chcesz zarejestrować certyfikat `Account settings` `Manage Organization` **>** `Edit Organization` przy użyciu konta organizacji).
1. Rozwiń `Certificates` sekcję i wybierz pozycję `Register new` .
1. Przeglądaj i wybierz wyeksportowany wcześniej plik certyfikatu.
  ![Zarejestrowane certyfikaty](../reference/media/registered-certs.png)

**Uwaga**
* Jeden użytkownik może przesłać wiele certyfikatów, a ten sam certyfikat może zostać zarejestrowany przez wielu użytkowników.
* Po zarejestrowaniu certyfikatu przez użytkownika wszystkie przyszłe  przesłania pakietów muszą być podpisane przy użyciu jednego z certyfikatów. Zobacz Manage signing requirements for your package on NuGet.org (Zarządzanie wymaganiami [podpisywania dla pakietu na NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)
* Użytkownicy mogą również usunąć zarejestrowany certyfikat z konta. Po usunięciu certyfikatu nowe pakiety podpisane tym certyfikatem nie powiodą się podczas przesyłania. Nie ma to wpływu na istniejące pakiety.

## <a name="publish-the-package"></a>Publikowanie pakietu

Teraz możesz opublikować pakiet w NuGet.org. Zobacz [Publikowanie pakietów](../nuget-org/Publish-a-package.md).

## <a name="create-a-test-certificate"></a>Tworzenie certyfikatu testowego

Certyfikatów wystawionych samodzielnie można używać do celów testowych. Aby utworzyć certyfikat wystawiony samodzielnie, użyj polecenia [New-SelfSignedCertificate programu PowerShell.](/powershell/module/pkiclient/new-selfsignedcertificate)

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

To polecenie tworzy certyfikat testowania dostępny w osobistym magazynie certyfikatów bieżącego użytkownika. Możesz otworzyć magazyn certyfikatów, uruchamiając program `certmgr.msc` , aby wyświetlić nowo utworzony certyfikat.

> [!Warning]
> NuGet.org nie akceptuje pakietów podpisanych za pomocą samodzielnie wystawionych certyfikatów.

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a>Zarządzanie wymaganiami podpisywania dla pakietu na NuGet.org
1. [Zaloguj się](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) do NuGet.org.

1. Przejdź do `Manage Packages`  
    ![ konfigurowania osób podpisujących pakiety](../reference/media/configure-package-signers.png)

* Jeśli jesteś jedynym właścicielem pakietu, jesteś wymaganym podpisicielem, czyli możesz użyć dowolnego zarejestrowanego certyfikatu do podpisania i opublikowania pakietów w NuGet.org.

* Jeśli pakiet ma wielu właścicieli, do podpisania pakietu można domyślnie użyć certyfikatów właściciela "Dowolny". Jako współwłaściciel pakietu możesz zastąpić "Dowolne" swoim lub innym współwłaścicielem, aby był wymaganym podpisem. W przypadku przypisania właściciela, który nie ma zarejestrowanego certyfikatu, pakiety niepodpisane będą dozwolone. 

* Podobnie, jeśli dla pakietu, w którym jeden właściciel ma zarejestrowany certyfikat, a inny właściciel nie ma zarejestrowanego certyfikatu, wybrana jest domyślna opcja "Dowolne", program NuGet.org akceptuje podpisany pakiet z podpisem zarejestrowanym przez jednego z właścicieli lub pakiet niepodpisany (ponieważ jeden z właścicieli nie ma zarejestrowanego certyfikatu).

## <a name="related-articles"></a>Pokrewne artykuły:

- [Zarządzanie granicami zaufania pakietów](../consume-packages/installing-signed-packages.md)
- [Odwołanie do podpisanych pakietów](../reference/Signed-Packages-Reference.md)
