---
title: Przestarzałe pakiety na nuget.org
description: Szczegółowy opis procesu przestarzałości pakietów i sposobu, w jaki klienci pokazują te informacje
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "74096884"
---
# <a name="deprecating-packages"></a>Przestarzałe pakiety

Możesz przestarzałe pakiet, jeśli nie prowadzisz już pakietu lub jeśli chcesz zachęcić konsumentów pakietu do przejścia do innego pakietu. 

Wycofanie pakietu różni się od **nienaszacowania** pakietu, jak wyjaśniono poniżej:
* **Odsuwanie** pakietu z listy uniemożliwia jego odnajdowanie, ponieważ jest on ukryty w wynikach wyszukiwania. 
* **Przestarzałe rozwiązanie** pakietu pozwala istniejącym odbiorcom pakietu dowiedzieć się, czy mają go zainstalowany lub używany w swoich projektach. Pozwala im również znać przyczynę wycofania i alternatywny zalecany pakiet określony przez Ciebie (wydawca pakietu). Przestarzałe pakiet nie powoduje wykreślenia pakietu z listy. 

Jako wydawca możesz wybrać zarówno niepubliczne, jak i przestarzałe pakiety.

## <a name="deprecation-workflow"></a>Przepływ pracy deprecation
1. Aby przestarzałe pakiet, przejdź do **zarządzania pakietami** i wybierz **opcję Zaniechanie:**

    ![Przejdź do opcji przestarzałego pakietu](media/deprecation-select-option.png)

2. Wybierz wersję, którą chcesz przestarzałe. Jeśli chcesz przestarzałe wszystkie wersje, wybierz wybierz **wszystkie wersje** opcji.

    ![Wybieranie wersji pakietów do przestarzałości](media/deprecation-select-version.png)

3. Wybierz przyczynę wycofania. Jeśli pakiet nie jest już utrzymywany, wybierz opcję **Starsza.** Jeśli określona wersja ma błąd krytyczny, wybierz opcję **ma krytyczne błędy.** Z dowolnego innego powodu wybierz opcję **Inne**. Zawsze można określić alternatywny zalecany pakiet (i wersję) i niestandardowy komunikat do właścicieli. 

    ![Wybierz powody alternatywnego pakietu rekomendacji i wiadomości niestandardowej](media/deprecation-save.png)

> [!Note]
> Wiadomość niestandardowa jest wyświetlana tylko na nuget.org ale nie od klientów. Obecnie klienci, tacy `dotnet.exe` jak i Menedżer pakietów NuGet, nie wyświetlają wiadomości niestandardowej.

## <a name="client-experience-for-deprecated-packages"></a>Obsługa klienta dla przestarzałych pakietów
Gdy pakiet został przestarzały, jego konsumenci są powiadamiani o tym w następujący sposób (w zależności od używanego klienta).

### <a name="visual-studio"></a>Visual Studio 
*Dostępne od wersji Visual Studio 2019 w wersji 16.3*

Visual Studio ostrzega o użyciu przestarzałego `Installed` pakietu na karcie. Wyświetli ostrzeżenie dla pakietu i jego informacje o umorzyniu (w tym powód, dla którego został przestarzały i alternatywny pakiet do użycia zamiast tego, jeśli jest obecny).

   ![Przestarzałe pakiety w programie Visual Studio zainstalowanej karty Menedżera pakietów](media/deprecation-vs.png)

### <a name="dotnetexe"></a>plik dotnet.exe
*Dostępne począwszy od .NET SDK 3.0*

Jeśli używasz dotnet.exe, można `dotnet list package --deprecated` uruchomić polecenie w folderze rozwiązania lub projektu, aby uzyskać listę przestarzałych pakietów wraz z informacjami o umorzazaniu:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
