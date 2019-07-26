---
title: Wtyczka uwierzytelniania NuGet dla wielu platform
description: Wtyczki do uwierzytelniania dla wielu platform NuGet dla NuGet. exe, dotnet. exe, MSBuild. exe i Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: a716737343ea826d28da6de46c32ca73aef590bd
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317276"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>Wtyczka uwierzytelniania NuGet dla wielu platform

W wersji 4.8 + wszystkie klienckie narzędzia NuGet (NuGet. exe, Visual Studio, dotnet. exe i MSBuild. exe) mogą używać wtyczki uwierzytelniania utworzonej na podstawie modelu [wtyczki międzyplatformowej NuGet](NuGet-Cross-Platform-Plugins.md) .

## <a name="authentication-in-dotnetexe"></a>Uwierzytelnianie w programie dotnet. exe

Programy Visual Studio i NuGet. exe są domyślnie interaktywne. Plik NuGet. exe zawiera przełącznik, który [nie](../nuget-exe-CLI-Reference.md)jest interaktywny.
Ponadto Dodatki NuGet. exe i Visual Studio monitują użytkownika o dane wejściowe.
W programie dotnet. exe nie ma monitu i domyślnie nie jest to interaktywny.

Mechanizm uwierzytelniania w programie dotnet. exe jest przepływem urządzenia. Gdy operacja przywracania lub dodawania pakietu jest uruchamiana interaktywnie, to bloki operacji i instrukcje dla użytkownika, jak ukończyć uwierzytelnianie, zostaną podane w wierszu polecenia.
Gdy użytkownik ukończy uwierzytelnianie, operacja będzie kontynuowana.

Aby operacja była interaktywna, należy ją przekazać `--interactive`.
Obecnie tylko jawne `dotnet restore` i `dotnet add package` polecenia obsługują przełącznik interaktywny.
Nie istnieje interaktywny przełącznik włączony `dotnet build` i `dotnet publish`.

## <a name="authentication-in-msbuild"></a>Uwierzytelnianie w programie MSBuild

Podobnie jak w przypadku programu dotnet. exe, MSBuild. exe jest domyślnie nieinteraktywny mechanizm uwierzytelniania MSBuild. exe jest przepływem urządzenia.
Aby pozwolić na wstrzymanie przywracania i poczekać na uwierzytelnienie, wywołaj polecenie Restore with `msbuild -t:restore -p:NuGetInteractive="true"`.

## <a name="creating-a-cross-platform-authentication-plugin"></a>Tworzenie wtyczki uwierzytelniania dla wielu platform

Przykładową implementację można znaleźć w [wtyczki dostawcy poświadczeń firmy Microsoft](https://github.com/Microsoft/artifacts-credprovider).

Bardzo ważne jest, aby wtyczki zgodne z wymaganiami dotyczącymi zabezpieczeń określonymi przez narzędzia klienckie programu NuGet.
Minimalna wymagana wersja wtyczki jako wtyczki uwierzytelniania to *2.0.0*.
Pakiet NuGet wykona uzgadnianie z wtyczką i kwerendą dla obsługiwanych oświadczeń operacji.
Aby uzyskać więcej informacji na temat konkretnych komunikatów [](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) , zapoznaj się z informacjami o protokole wtyczek NuGet cross platform.

Pakiet NuGet ustawi poziom dziennika i dostarczy informacje o serwerze proxy do wtyczki, jeśli ma to zastosowanie.
Rejestrowanie w konsoli programu NuGet jest akceptowalne tylko po ustawieniu przez pakiet NuGet poziomu dziennika na wtyczkę.

- Zachowanie uwierzytelniania wtyczki .NET Framework

W .NET Framework Dodatki mogą monitować użytkownika o dane wejściowe w postaci okna dialogowego.

- Zachowanie uwierzytelniania wtyczki .NET Core

W programie .NET Core nie można wyświetlić okna dialogowego. Wtyczki powinny używać przepływu urządzenia do uwierzytelniania.
Wtyczka może wysyłać komunikaty dziennika do narzędzia NuGet z instrukcjami dla użytkownika.
Należy pamiętać, że rejestrowanie jest dostępne po ustawieniu poziomu dziennika na wtyczkę.
Pakiet NuGet nie będzie pobierał żadnych interaktywnych danych wejściowych z wiersza polecenia.

Gdy klient wywołuje wtyczkę z poświadczeniami pobierania uwierzytelniania, wtyczki muszą być zgodne z przełącznikiem interaktywnym i mieć poszanowanie przełączenia okna dialogowego. 

Poniższa tabela zawiera podsumowanie sposobu zachowania wtyczki dla wszystkich kombinacji.

| IsNonInteractive | Zashowdialog | Zachowanie wtyczki |
| ---------------- | ------------- | --------------- |
| true | true | Przełącznik IsNonInteractive ma pierwszeństwo przed przełącznikiem okna dialogowego. Wtyczka nie zezwala na wyskakujące okno dialogowe. Ta kombinacja jest prawidłowa tylko dla wtyczek .NET Framework |
| true | false | Przełącznik IsNonInteractive ma pierwszeństwo przed przełącznikiem okna dialogowego. Nie można zablokować wtyczki. Ta kombinacja jest prawidłowa tylko dla wtyczek .NET Core |
| false | true | Wtyczka powinna wyświetlić okno dialogowe. Ta kombinacja jest prawidłowa tylko dla wtyczek .NET Framework |
| false | false | Wtyczka nie może wyświetlić okna dialogowego. Wtyczka powinna używać przepływu urządzenia do uwierzytelniania przez rejestrowanie komunikatu instrukcji za pośrednictwem rejestratora. Ta kombinacja jest prawidłowa tylko dla wtyczek .NET Core |

Przed zapisaniem wtyczki zapoznaj się z poniższymi specyfikacją.

- [Wtyczka pobierania pakietu NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [Wtyczka do uwierzytelniania między płytkami NuGet](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
