---
title: "Jak zarządzać pakietu buforowanie w NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3932217d-780d-4bd1-ad15-767acd3e8870
description: "Jak zarządzać inny pakiet NuGet buforuje, która istnieje na maszynie, używane podczas instalowania lub przywracanie pakietów."
keywords: "Pamięć podręczną z pakietów NuGet, buforowanie w pamięci podręcznej NuGet, zarządzaniem lokalnej pamięci podręcznej NuGet, globalnej pamięci podręcznej NuGet, polecenia NuGet zmiennych lokalnych, czyszczenie pamięci podręcznej w pamięci podręcznych pakietu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6e76c219ba420eb285af20e67b26dcdceebb6bab
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="managing-the-nuget-cache"></a>Zarządzanie pamięcią podręczną NuGet

NuGet zarządza kilka buforów lokalnego, aby uniknąć pobierania pakietów, które są już na komputerze, a także do obsługi w trybie offline. NuGet 2.8 + automatycznie powraca do pamięci podręcznej podczas instalowania lub ponownego instalowania pakietów bez połączenia sieciowego.

Lokalizacje w pamięci podręcznej są dostępne przy użyciu [polecenia zmiennych lokalnych](../tools/cli-ref-locals.md):

```
nuget locals all -list
```

Dane wyjściowe zazwyczaj wygląda następująco:

    http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
    packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
    global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
    temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder

Jeśli występują problemy z instalacją pakietu lub w przeciwnym razie chcesz zapewnić instalowany pakiety ze zdalnego galerii, użyj `locals -clear` opcji:

```
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

Należy pamiętać, że zarządzanie pamięci podręcznej jest obecnie obsługiwane tylko z wiersza polecenia NuGet, a nie w programie Visual Studio lub za pomocą konsoli Menedżera pakietów. Ponadto zarządzanie 2.x pamięci podręcznej nie jest obsługiwane w wersji NuGet 3,6 i nowszych.

Następujące błędy może wystąpić, gdy przy użyciu `nuget locals`:

* **Wyczyszczenie zasobów lokalnych nie powiodło się: nie można usunąć jednego lub więcej plików**
* **Katalog nie jest pusty**

Oznaczają one, że nie masz uprawnień do usuwania plików w pamięci podręcznej lub jednym lub większej liczby plików w pamięci podręcznej są używane przez inny proces, który należy zamknąć przed elementami pliki mogą zostać usunięte.
