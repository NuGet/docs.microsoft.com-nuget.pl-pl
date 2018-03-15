---
title: "Podpisane pakiety odwołania | Dokumentacja firmy Microsoft"
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Podpisana opis funkcji pakietów."
keywords: Znak pakietu NuGet, podpisu certyfikatu
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9bf9885aaf42bedb681a5d916202fa8b26749a0c
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/15/2018
---
# <a name="signed-packages"></a>Pakiety podpisem

*NuGet 4.6.0+ i Visual Studio 2017 wersji 15.6 i nowsze*

Pakiety NuGet mogą zawierać podpis cyfrowy, który zapewnia ochronę przed zmodyfikowany zawartości. Ta sygnatura jest tworzony z certyfikatu X.509, który dodaje również dowody autentyczności do rzeczywistego źródła pakietu.

Pakiety podpisem udostępnienia najwyższy weryfikacji end-to-end. Autor podpis gwarantuje, że pakiet nie został zmodyfikowany od czasu autora podpisania pakietu, niezależnie od którego repozytorium lub co metoda jest dostarczany pakiet transportu.

Użytkowników potrzebujących środowisku zablokowany może wymagać pakiety podpisane przy użyciu certyfikatu określonego autora.

Ponadto pakiety podpisane przez autora udostępniają mechanizm uwierzytelniania dodatkowego do potoku publikowania nuget.org, ponieważ certyfikat podpisywania musi być zarejestrowana wcześniejsze.

Aby uzyskać więcej informacji na temat tworzenia podpisanego pakietu, zobacz [podpisywania pakietów](../create-packages/Sign-a-package.md) i [polecenia nuget znak](../tools/cli-ref-sign.md).

> [!Important]
> nuget.org nie akceptuje obecnie podpisanych pakietów. Możesz zarejestrować pakietów do publikowania do niestandardowych źródeł danych.

## <a name="certificate-requirements"></a>Wymagania certyfikatu

Podpisywanie pakietu wymaga podpisywania certyfikatu, który jest specjalny typ certyfikatu, który jest prawidłowy dla kodu `id-kp-codeSigning` cel [[RFC 5280 sekcji 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Ponadto certyfikat musi mieć publiczny długość klucza RSA 2048 bitów lub nowszej.

## <a name="get-a-code-signing-certificate"></a>Uzyskaj certyfikat podpisywania kodu

Prawidłowe certyfikaty mogą być uzyskane z urzędów certyfikacji publicznej, takich jak:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Globalne logowania](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

Pełna lista urzędów certyfikacji ufa systemu Windows można uzyskać z [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Tworzenie certyfikatu testowego

Wystawiony samodzielnie Certyfikaty służy do celów testowych. Aby utworzyć certyfikat wystawiony samodzielnie, użyj [SelfSignedCertificate nowy](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) polecenia programu PowerShell.

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

## <a name="timestamp-requirements"></a>Wymagania dotyczące sygnatury czasowej

Pakiety podpisem powinna zawierać znaczników czasu RFC 3161 do zapewnienia walidacji podpisu poza okres ważności certyfikatu podpisywania pakietu. Certyfikat używany do podpisywania sygnatura czasowa musi być prawidłowy dla `id-kp-timeStamping` cel [[RFC 5280 sekcji 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Ponadto certyfikat musi mieć publiczny długość klucza RSA 2048 bitów lub nowszej.

Dodatkowe szczegóły techniczne można znaleźć w [specyfikacji technicznej podpisu pakietu](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).
