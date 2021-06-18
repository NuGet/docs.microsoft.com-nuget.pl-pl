---
title: Polecenie zaufanych podpisujących interfejs wiersza polecenia nuGet
description: Odwołanie do polecenia nuget.exe zaufanych podpisujących
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: a5f3564af8b96dfa673d2252aea2e77a79c184a4
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323593"
---
# <a name="trusted-signers-command-nuget-cli"></a>Polecenie trusted-signers (interfejs wiersza polecenia NuGet)

**Dotyczy: zużycie** pakietu &bullet; **Obsługiwane wersje:** 4.9.1+

Pobiera lub ustawia zaufanych podpisujących do konfiguracji NuGet. Aby uzyskać dodatkowe informacje o użyciu, zobacz [Typowe konfiguracje NuGet.](../../consume-packages/configuring-nuget-behavior.md) Aby uzyskać szczegółowe informacje na temat nuget.config schematu, zapoznaj się z odwołaniem do pliku [konfiguracji NuGet](../nuget-config-file.md).

## <a name="usage"></a>Użycie

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Jeśli żadna z `list|add|remove|sync` wartości nie zostanie określona, polecenie domyślnie będzie mieć wartość `list` .

## <a name="nuget-trusted-signers-list"></a>Lista zaufanych podpisujących nuget

Wyświetla listę wszystkich zaufanych osób podpisujących w konfiguracji. Ta opcja obejmuje wszystkie certyfikaty (z algorytmem odcisku palca i odcisku palca) posiadane przez każdego podpiszcę. Jeśli certyfikat ma poprzednią `[U]` wartość , oznacza to, że wpis certyfikatu został `allowUntrustedRoot` ustawiony jako `true` .

Poniżej przedstawiono przykładowe dane wyjściowe tego polecenia:

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D
        SHA256 - 5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>NuGet — zaufani podpisujący dodają [opcje]

Dodaje zaufanego podpiszącego o podanej nazwie do konfiguracji. Ta opcja ma różne gesty dodawania zaufanego autora lub repozytorium.

## <a name="options-for-add-based-on-a-package"></a>Opcje dodawania na podstawie pakietu

```cli
nuget trusted-signers add <package> -Name <name> [options]
```

gdzie `<package>` to jeden podpisany `.nupkg` plik.

- **`-Author`**

  Określa, że podpis autora podpisanego pakietu powinien być zaufany.

- **`-AllowUntrustedRoot`**

  Określa, czy certyfikat zaufanego podpiszącego powinien mieć możliwość podpisania łańcucha do niezaufanego katalogu głównego.

- **`-Owners`**

  Rozdzielana średnikami lista zaufanych właścicieli w celu dalszego ograniczenia zaufania repozytorium. Prawidłowy tylko w przypadku korzystania z `-Repository` opcji .

- **`-Repository`**

  Określa, że podpis repozytorium lub countersignature podpisanego pakietu powinny być zaufane.

Zarówno, `-Author` jak i w tym samym `-Repository` czasie, nie są obsługiwane.

## <a name="options-for-add-based-on-a-service-index"></a>Opcje dodawania na podstawie indeksu usługi

```cli
nuget trusted-signers add -Name <name> [options]
```

_Uwaga:_ ta opcja spowoduje dodanie tylko zaufanych repozytoriów. 

- **`-AllowUntrustedRoot`**

  Określa, czy certyfikat zaufanego podpiszącego powinien mieć możliwość podpisania łańcucha do niezaufanego katalogu głównego.

- **`-Owners`**

  Rozdzielana średnikami lista zaufanych właścicieli w celu dalszego ograniczenia zaufania repozytorium.

- **`-ServiceIndex`**

  Określa indeks usługi w wersji 3 repozytorium, który ma być zaufany. To repozytorium musi obsługiwać zasób sygnatur repozytorium. Jeśli nie zostanie podany, polecenie będzie szukać źródła pakietu z tym samym i `-Name` pobrać indeks usługi z tego źródła.

## <a name="options-for-add-based-on-the-certificate-information"></a>Opcje dodawania na podstawie informacji o certyfikacie

```cli
nuget trusted-signers add -Name <name> [options]
```

_Uwaga:_ jeśli zaufany podpiszator o podanej nazwie już istnieje, element certyfikatu zostanie dodany do tego osoby podpiszącego. W przeciwnym razie zostanie utworzony zaufany autor z elementem certyfikatu z informacji o certyfikacie.


- **`-AllowUntrustedRoot`**

  Określa, czy certyfikat zaufanego podpiszącego powinien mieć możliwość podpisania łańcucha do niezaufanego katalogu głównego.

- **`-CertificateFingerprint`**

  Określa odciski palców certyfikatu, za pomocą którego muszą być podpisane podpisane pakiety. Odcisk palca certyfikatu jest skrótem certyfikatu. W opcji należy określić algorytm wyznaczania wartości skrótu używany do obliczania tego `FingerprintAlgorithm` skrótu.

- **`-FingerprintAlgorithm`**

  Określa algorytm wyznaczania wartości skrótu używany do obliczania odcisku palca certyfikatu. Wartość domyślna to `SHA256` . Obsługiwane wartości to `SHA256` , `SHA384` i `SHA512` .

## <a name="nuget-trusted-signers-remove--name-name"></a>Zaufani podpisujący nuget usuwają -Name \<name\>

Usuwa wszystkich zaufanych podpisujących, które pasują do podanej nazwy.

## <a name="nuget-trusted-signers-sync--name-name"></a>Nuget trusted-signers sync -Name \<name\>

Żąda najnowszej listy certyfikatów używanych w aktualnie zaufanym repozytorium w celu zaktualizowania istniejącej listy certyfikatów na zaufanym podpisie.

_Uwaga:_ ten gest spowoduje usunięcie bieżącej listy certyfikatów i zastąpienie ich aktualną listą z repozytorium.

## <a name="options"></a>Opcje

- **`-ConfigFile`**

  Plik konfiguracji NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.

- **`-ForceEnglishOutput`**

  Wymusza nuget.exe uruchamiania przy użyciu niezmiennej kultury opartej na języku angielskim.

- **`-?|-help`**

  Wyświetla informacje pomocy dotyczące polecenia.

- **`-Name`**

  Nazwa zaufanego podpisatora.

- **`-NonInteractive`**

  Pomija monity o wprowadzenie danych przez użytkownika lub potwierdzenia.

- **`-Verbosity [normal|quiet|detailed]`**

  Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (ustawienie domyślne), `quiet` lub `detailed` .


## <a name="examples"></a>Przykłady

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget trusted-signers Remove -Name TrustedRepo

nuget trusted-signers Sync -Name TrustedRepo
```
