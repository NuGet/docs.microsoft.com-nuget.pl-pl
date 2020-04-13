---
ms.openlocfilehash: b0af2000b1f43cd0b91f2c95dfc0c11540a94cab
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496061"
---
<span data-ttu-id="ef131-101">Błędy z `push` polecenia zazwyczaj wskazują na problem.</span><span class="sxs-lookup"><span data-stu-id="ef131-101">Errors from the `push` command typically indicate the problem.</span></span> <span data-ttu-id="ef131-102">Na przykład może zapomniane, aby zaktualizować numer wersji w projekcie i dlatego próbuje opublikować pakiet, który już istnieje.</span><span class="sxs-lookup"><span data-stu-id="ef131-102">For example, you may have forgotten to update the version number in your project and are therefore trying to publish a package that already exists.</span></span>

<span data-ttu-id="ef131-103">Błędy są również widoczne podczas próby opublikowania pakietu przy użyciu identyfikatora, który już istnieje na hoście.</span><span class="sxs-lookup"><span data-stu-id="ef131-103">You also see errors when trying to publish a package using an identifier that already exists on the host.</span></span> <span data-ttu-id="ef131-104">Nazwa "AppLogger", na przykład, już istnieje.</span><span class="sxs-lookup"><span data-stu-id="ef131-104">The name "AppLogger", for example, already exists.</span></span> <span data-ttu-id="ef131-105">W takim przypadku `push` polecenie podaje następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="ef131-105">In such a case, the `push` command gives the following error:</span></span>

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

<span data-ttu-id="ef131-106">Jeśli używasz prawidłowego klucza interfejsu API, który właśnie został utworzony, ten komunikat wskazuje konflikt nazewnictwa, który nie jest całkowicie jasne z "uprawnienia" część błędu.</span><span class="sxs-lookup"><span data-stu-id="ef131-106">If you're using a valid API key that you just created, then this message indicates a naming conflict, which isn't entirely clear from the "permission" part of the error.</span></span> <span data-ttu-id="ef131-107">Zmień identyfikator pakietu, odbuduj projekt, `.nupkg` ponownie stwórz `push` plik i ponów próbę wykonania polecenia.</span><span class="sxs-lookup"><span data-stu-id="ef131-107">Change the package identifier, rebuild the project, recreate the `.nupkg` file, and retry the `push` command.</span></span>