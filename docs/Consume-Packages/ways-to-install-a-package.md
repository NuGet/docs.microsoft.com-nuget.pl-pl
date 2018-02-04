---
title: "Sposoby można zainstalować pakietów NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/30/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "W tym artykule opisano proces instalowania pakietów NuGet do projektu, w tym, co się dzieje na dysku oraz pliki dotyczy projektu."
keywords: "instalowania NuGet użycia pakietu NuGet, instalowanie pakietów NuGet, odwołania do pakietu NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9e48bbe813168e773bc46b7fe25af29785ff75df
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/01/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>Różne sposoby, można zainstalować pakietu NuGet

Pakiety NuGet zostaną pobrane i zainstalowane przy użyciu dowolnej z następujących metod (zobacz [NuGet zainstalować narzędzia klienta](../install-nuget-client-tools.md) Jeśli nie są już zainstalowane):

| Metoda | Opis |
| --- | --- |
| DotNet.exe interfejsu wiersza polecenia<br/>`dotnet install <package_name>` | (Wszystkie platformy) Pobiera pakiet identyfikowane przez \<nazwa_pakietu\>rozszerza jego zawartość do folderu w bieżącym katalogu i dodaje odwołanie do pliku projektu. Również pobiera i instaluje zależności.<ul><li>[Zainstalować i używać pakietu (dotnet CLI)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[polecenia DotNet](../tools/dotnet-commands.md)</li></ul> |
| Interfejs użytkownika Menedżera pakietów (Visual Studio) | (System Windows i Mac) Udostępnia interfejs, za pomocą którego można wybrać, wybierz i zainstaluj pakietów oraz ich zależności w projekcie. Dodaje odwołania do zainstalowanych pakietów do pliku projektu.<ul><li>[Zainstalować i używać pakietu (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Informacje o interfejsie użytkownika Menedżera pakietów (system Windows)](../tools/package-manager-ui.md)</li><li>[W tym pakietu NuGet w projekcie (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Konsola Menedżera pakietów (Visual Studio)<br/>`Install-Package <package_name>` | (Tylko system Windows) Pobiera i instaluje pakiet identyfikowane przez \<nazwa_pakietu\> do określonego projektu w rozwiązaniu, a następnie dodaje odwołanie do pliku projektu. Również pobiera i instaluje zależności.<ul><li>[Zainstalować i używać pakietu (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Przewodnik Konsola Menedżera pakietów](../tools/package-manager-console.md)</li></ul> |
| nuget.exe interfejsu wiersza polecenia<br/>`nuget install <package_name>` | (Wszystkie platformy) Pobiera pakiet identyfikowane przez \<nazwa_pakietu\> i rozwija jego zawartość do folderu w bieżącym katalogu; można również pobrać wszystkie pakiety wymienione w `packages.config` pliku. Również pobiera i instaluje zależności, ale nie zmienia plików projektu.<ul><li>[polecenie instalacji](../tools/cli-ref-install.md)</li></ul> |

## <a name="general-install-process"></a>Proces instalacji ogólne

Ogólnie rzecz biorąc NuGet wykonuje następujące pytanie, aby zainstalować pakiet:

1. Pobieranie pakietu:
    - Sprawdź, czy żądany pakiet już istnieje w pamięci podręcznej (zobacz [Zarządzanie pamięci podręcznej NuGet](managing-the-nuget-cache.md)).
    - Jeśli pakiet nie jest w pamięci podręcznej, spróbuj pobrać pakiet ze źródeł wymienionych w plikach konfiguracji, rozpoczynając od pierwszego na liście. Umożliwia to zachowanie, przy użyciu źródła pakietu prywatnej przed szuka pakietu w nuget.org (zobacz [NuGet Konfigurowanie zachowania](configuring-nuget-behavior.md)).
    - Jeśli pakiet jest pomyślnie uzyskano z jednego ze źródeł, NuGet dodaje go do pamięci podręcznej. W przeciwnym razie instalacja nie powiedzie się.

1. Rozwiń pakiet w projekcie.
    - Rozszerzanie oznacza rozpakować zawartość pakietu do odpowiedniego podfolderu. Kopię `.nupkg` również znajduje się w podfolderze.
    - Jeśli pakiet jest instalowany do projektu programu Visual Studio lub .NET Core, tylko te pliki, które są odpowiednie do platformy docelowej projektu zostaną rozwinięte. Podczas instalacji przy użyciu wiersza polecenia nuget.exe zostaną rozwinięte wszystkie zestawy.

1. Jeśli pakiet jest zainstalowany w programie Visual Studio lub platformy dotnet interfejsu wiersza polecenia, odwołanie zostanie dodany do pliku odpowiedni projekt (lub `packages.config` dla niektórych typów projektów programu Visual Studio).

## <a name="related-topics"></a>Tematy pokrewne

- [Omówienie i przepływ pracy zużycia pakietu](../consume-packages/overview-and-workflow.md)
- [Wyszukiwanie i Wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md)
- [Konfigurowanie zachowania NuGet](../consume-packages/configuring-nuget-behavior.md)
- [Zarządzanie pamięcią podręczną NuGet](managing-the-nuget-cache.md)
