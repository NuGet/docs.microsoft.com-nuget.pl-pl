---
title: Indywidualne konta
description: Poszczególne acccounts w witrynie NuGet.org są wymagane do publikowania pakietów
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: e1e31e0534706dab43f8d7b1b0db059cd6f29b80
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427558"
---
# <a name="individual-accounts"></a>Indywidualne konta

Należy utworzyć indywidualne konta do publikowania i zarządzania pakietami w witrynie NuGet.org.

## <a name="individual-accounts-vs-organization-accounts"></a>Indywidualne konta i kont organizacji

Kontem osoby (użytkownik) jest swoją tożsamość w witrynie NuGet.org i może należeć do dowolnej liczby organizacji. Pakiet może należeć do organizacji, takich jak mogą należeć do indywidualnych kont. Konsumentów pakietu nie jest widoczna różnica między indywidualne konto lub konta organizacji: oba są wyświetlane jako pakiet `owners`.

Konto organizacji ma co najmniej jeden z indywidualnych kont jako elementy członkowskie. Członkowie mogą zarządzać zestaw pakietów przy zachowaniu jednej tożsamości dla własności.

## <a name="add-a-new-individual-account"></a>Dodaj nowe konto indywidualne

Aby utworzyć konto w witrynie NuGet.org, musisz mieć konto usługi Azure Active Directory (AAD) lub osobistego konta Microsoft (MSA). Jeśli nie masz, możesz to zrobić [tworzenie](https://signup.live.com) jeden. Wykonaj poniższe kroki, jeśli masz konto MSA lub usługi AAD.

1. Przejdź do [strony logowania w witrynie NuGet.org](https://www.nuget.org/users/account/LogOn).

1. Kliknij pozycję **Zaloguj się przy użyciu Microsoft** przycisku.

1. Wprowadź szczegóły konta usługi Azure Active Directory lub konta Microsoft.

1. Kliknij **tak** zaakceptowania uprawnień do *NuGet.org* aplikacji.

   ![Przyznawanie uprawnień do NuGet.org](media/nuget-org-permissions.png)

1. Nastąpi przekierowanie do *nuget.org*oraz pytanie zarejestrować nazwę użytkownika.

1. Określ nazwę użytkownika w polu wejściowym. Należy pamiętać, że nazwa użytkownika **jest** zamierzone, Zapisz poufne i nie można zmienić ani zmienić nazwy później.

   ![Podaj nazwę użytkownika w witrynie NuGet.org](media/nuget-org-register.png) 

1. Kliknij przycisk **zarejestrować** przycisku.

Masz teraz konto NuGet.org. Zarządzanie kontami można wykonywać na [ustawienia konta](https://www.nuget.org/account) strony.
