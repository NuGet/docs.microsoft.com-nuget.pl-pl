---
title: NuGet cross platform, wtyczki uwierzytelniania
description: NuGet cross platform, wtyczki uwierzytelniania NuGet.exe, dotnet.exe, msbuild.exe i programu Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 1258ca4b30cb674c3832f12262940729438dd5b0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546637"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>NuGet cross platform, wtyczki uwierzytelniania

W wersji + NuGet wszystkich klientów (NuGet.exe, Visual Studio, dotnet.exe i MSBuild.exe) można użyć wtyczki uwierzytelniania skompilowane na 4.8 [NuGet cross platform wtyczek](NuGet-Cross-Platform-Plugins.md) modelu.

## <a name="authentication-in-dotnetexe"></a>Uwierzytelnianie w dotnet.exe

Program Visual Studio i NuGet.exe są domyślnie interaktywne. NuGet.exe zawiera przełącznik, aby stał się [nieinterakcyjny](../../tools/nuget-exe-CLI-Reference.md).
Ponadto wtyczek NuGet.exe i programu Visual Studio monit o wprowadzenie danych wejściowych.
W dotnet.exe istnieje nie monitowania użytkownika, a wartość domyślna to nieinterakcyjny.

Mechanizm uwierzytelniania w dotnet.exe jest przepływ urządzenia. Podczas przywracania lub dodać pakiet uruchomienia operacji interaktywnie bloków operacji i instrukcje dla użytkownika, jak na zakończenie uwierzytelnieniami będzie świadczona w wierszu polecenia.
Operacja będzie kontynuowana, gdy użytkownik zakończy uwierzytelnianie.

Operacja interaktywne, jeden powinien polega na przekazaniu `--interactive`.
Obecnie tylko jawne `dotnet restore` i `dotnet add package` polecenia obsługuje interakcyjne przełącznika.
Brak Brak przełącznika interaktywne na `dotnet build` i `dotnet publish`.

## <a name="authentication-in-msbuild"></a>Uwierzytelnianie w programie MSBuild

Podobnie jak dotnet.exe MSBuild.exe jest domyślnie nie jest mechanizm uwierzytelniania MSBuild.exe interaktywne, przepływ urządzenia.
Aby umożliwić Przywracanie wstrzymać i poczekaj na potrzeby uwierzytelniania, wywołania do przywracania `msbuild /t:restore /p:NuGetInteractive="true"`.

## <a name="creating-a-cross-platform-authentication-plugin"></a>Tworzenie wtyczki uwierzytelniania dla wielu platform

Przykładową implementację można znaleźć w [wtyczki MSCredProvider](https://github.com/Microsoft/mscredprovider).

Jest to bardzo ważne jest, że wtyczki spełnia wymagania dotyczące zabezpieczeń Harbor ustalonych przez narzędzia klienta programu NuGet.
Minimalna wymagana wersja dla wtyczki do wtyczki uwierzytelniania jest *2.0.0*.
NuGet wykona uzgadnianie za pomocą wtyczki i zapytania dla oświadczeń obsługiwaną operacją.
Można znaleźć pakietu NuGet cross platform wtyczki [protokołu komunikatów](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) więcej szczegółowych informacji dotyczących określonych wiadomości.

NuGet zostanie ustawiony poziom dziennika i podaj informacje o serwerze proxy, aby dodatek, jeśli ma to zastosowanie.
Rejestrowanie pakietu NuGet konsoli jest dozwolone tylko wtedy po NuGet został ustawiony poziom dziennika do wtyczki.

- Zachowanie uwierzytelniania wtyczka .NET framework

W programie .NET Framework wtyczki mogą monitować użytkownika o dane wejściowe w postaci okna dialogowego.

- Zachowanie uwierzytelniania wtyczkę dla platformy .NET core

Okno dialogowe nie można wyświetlić w programie .NET Core. Wtyczki należy używać przepływu urządzenie do uwierzytelniania.
Wtyczka może wysyłać komunikaty dziennika do NuGet za pomocą instrukcji dla użytkownika.
Należy pamiętać, że rejestrowanie dostępne po ustawieniu poziomu dziennika do wtyczki.
NuGet nie podejmie żadnych interaktywne dane wejściowe z wiersza polecenia.

Gdy klient wywołuje wtyczkę przy użyciu poświadczeń uwierzytelniania Pobierz, wtyczki konieczne są zgodne z przełącznikiem interakcyjność i przestrzegać przełącznika okna dialogowego. 

W poniższej tabeli przedstawiono, jak wtyczki powinny zachowywać się dla wszystkich kombinacji.

| IsNonInteractive | CanShowDialog | Zachowanie wtyczki |
| ---------------- | ------------- | --------------- |
| true | true | Przełącznik IsNonInteractive mają pierwszeństwo przed przełącznika okna dialogowego. Wtyczka jest niedozwolone pop okna dialogowego. Ta kombinacja jest prawidłowy tylko dla wtyczek platformy .NET Framework |
| true | false | Przełącznik IsNonInteractive mają pierwszeństwo przed przełącznika okna dialogowego. Wtyczka nie może zablokować. Ta kombinacja jest prawidłowy tylko dla wtyczek platformy .NET Core |
| false | true | Wtyczka powinny być wyświetlane okno dialogowe. Ta kombinacja jest prawidłowy tylko dla wtyczek platformy .NET Framework |
| false | false | Wtyczka powinna może są wyświetlane okno dialogowe. Wtyczkę należy używać przepływu urządzenie do uwierzytelniania przez rejestrowanie komunikatów instrukcji za pomocą rejestratora. Ta kombinacja jest prawidłowy tylko dla wtyczek platformy .NET Core |

Zapoznaj się następujące dane techniczne przed napisaniem wtyczkę.

- [Wtyczka pobierania pakietu NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet krzyżowe wtyczki uwierzytelniania plat](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
