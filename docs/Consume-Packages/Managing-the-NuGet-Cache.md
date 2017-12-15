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
# <a name="managing-the-nuget-cache"></a><span data-ttu-id="1c0be-104">Zarządzanie pamięcią podręczną NuGet</span><span class="sxs-lookup"><span data-stu-id="1c0be-104">Managing the NuGet cache</span></span>

<span data-ttu-id="1c0be-105">NuGet zarządza kilka buforów lokalnego, aby uniknąć pobierania pakietów, które są już na komputerze, a także do obsługi w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="1c0be-105">NuGet manages several local caches to avoid downloading packages that are already on the computer, and to provide offline support.</span></span> <span data-ttu-id="1c0be-106">NuGet 2.8 + automatycznie powraca do pamięci podręcznej podczas instalowania lub ponownego instalowania pakietów bez połączenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="1c0be-106">NuGet 2.8+ automatically falls back to the cache when installing or reinstalling packages without a network connection.</span></span>

<span data-ttu-id="1c0be-107">Lokalizacje w pamięci podręcznej są dostępne przy użyciu [polecenia zmiennych lokalnych](../tools/cli-ref-locals.md):</span><span class="sxs-lookup"><span data-stu-id="1c0be-107">Cache locations are available using the [locals command](../tools/cli-ref-locals.md):</span></span>

```
nuget locals all -list
```

<span data-ttu-id="1c0be-108">Dane wyjściowe zazwyczaj wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="1c0be-108">Typical output is as follows:</span></span>

    http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
    packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
    global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
    temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder

<span data-ttu-id="1c0be-109">Jeśli występują problemy z instalacją pakietu lub w przeciwnym razie chcesz zapewnić instalowany pakiety ze zdalnego galerii, użyj `locals -clear` opcji:</span><span class="sxs-lookup"><span data-stu-id="1c0be-109">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals -clear` option:</span></span>

```
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

<span data-ttu-id="1c0be-110">Należy pamiętać, że zarządzanie pamięci podręcznej jest obecnie obsługiwane tylko z wiersza polecenia NuGet, a nie w programie Visual Studio lub za pomocą konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="1c0be-110">Note that managing the cache is presently supported only from the NuGet command line, and not within Visual Studio or through the Package Manager Console.</span></span> <span data-ttu-id="1c0be-111">Ponadto zarządzanie 2.x pamięci podręcznej nie jest obsługiwane w wersji NuGet 3,6 i nowszych.</span><span class="sxs-lookup"><span data-stu-id="1c0be-111">Also, managing the 2.x cache is not supported in NuGet 3.6 and later.</span></span>

<span data-ttu-id="1c0be-112">Następujące błędy może wystąpić, gdy przy użyciu `nuget locals`:</span><span class="sxs-lookup"><span data-stu-id="1c0be-112">The following errors can occur when using `nuget locals`:</span></span>

* <span data-ttu-id="1c0be-113">**Wyczyszczenie zasobów lokalnych nie powiodło się: nie można usunąć jednego lub więcej plików**</span><span class="sxs-lookup"><span data-stu-id="1c0be-113">**Clearing local resources failed: Unable to delete one or more files**</span></span>
* <span data-ttu-id="1c0be-114">**Katalog nie jest pusty**</span><span class="sxs-lookup"><span data-stu-id="1c0be-114">**The directory is not empty**</span></span>

<span data-ttu-id="1c0be-115">Oznaczają one, że nie masz uprawnień do usuwania plików w pamięci podręcznej lub jednym lub większej liczby plików w pamięci podręcznej są używane przez inny proces, który należy zamknąć przed elementami pliki mogą zostać usunięte.</span><span class="sxs-lookup"><span data-stu-id="1c0be-115">These indicate that you either do not have permission to delete files in the cache, or that one or more files in the cache are in use by another process, which must be closed before the those files can be removed.</span></span>
