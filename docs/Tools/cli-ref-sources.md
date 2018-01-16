---
title: "Polecenie źródła interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 997ce736-91ba-4cd2-88c9-b4b168e3130a
description: "Dokumentacja dotycząca nuget.exe źródeł polecenia"
keywords: "nuget źródeł odwołania, źródłem polecenia"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2eca8557840c467a60f5f708efe242cd83609164
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/10/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="61caa-104">polecenie źródeł (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="61caa-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="61caa-105">**Dotyczy:** zużycie pakietu, publikowanie &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="61caa-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="61caa-106">Zarządza listy źródeł znajduje się w `%AppData%\NuGet\NuGet.Config` lub określonego pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="61caa-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

<span data-ttu-id="61caa-107">Należy zauważyć, że adres URL źródła dla nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="61caa-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="61caa-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="61caa-108">Usage</span></span>

```
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="61caa-109">gdzie `<operation>` jest jednym z *listy, dodawanie, usuwanie, włączanie i wyłączanie,* lub *aktualizacji*, `<name>` to nazwa źródła i `<source>` jest adres URL źródła.</span><span class="sxs-lookup"><span data-stu-id="61caa-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="61caa-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="61caa-110">Options</span></span>

| <span data-ttu-id="61caa-111">Opcja</span><span class="sxs-lookup"><span data-stu-id="61caa-111">Option</span></span> | <span data-ttu-id="61caa-112">Opis</span><span class="sxs-lookup"><span data-stu-id="61caa-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="61caa-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="61caa-113">ConfigFile</span></span> | <span data-ttu-id="61caa-114">*(2.5 +)*  Pliku konfiguracji NuGet w celu zastosowania.</span><span class="sxs-lookup"><span data-stu-id="61caa-114">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="61caa-115">Jeśli nie zostanie określony, *%AppData%\NuGet\NuGet.Config* jest używany.</span><span class="sxs-lookup"><span data-stu-id="61caa-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="61caa-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="61caa-116">ForceEnglishOutput</span></span> | <span data-ttu-id="61caa-117">*(3.5 +)*  Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="61caa-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="61caa-118">Format</span><span class="sxs-lookup"><span data-stu-id="61caa-118">Format</span></span> | <span data-ttu-id="61caa-119">Dotyczy `list` akcji i może być `Detailed` (ustawienie domyślne) lub `Short`.</span><span class="sxs-lookup"><span data-stu-id="61caa-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="61caa-120">Pomoc</span><span class="sxs-lookup"><span data-stu-id="61caa-120">Help</span></span> | <span data-ttu-id="61caa-121">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="61caa-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="61caa-122">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="61caa-122">NonInteractive</span></span> | <span data-ttu-id="61caa-123">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="61caa-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="61caa-124">Hasło</span><span class="sxs-lookup"><span data-stu-id="61caa-124">Password</span></span> | <span data-ttu-id="61caa-125">Określa hasło do uwierzytelniania w źródle.</span><span class="sxs-lookup"><span data-stu-id="61caa-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="61caa-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="61caa-126">StorePasswordInClearText</span></span> | <span data-ttu-id="61caa-127">Wskazuje, aby zapisać hasło w tekście niezaszyfrowane zamiast domyślnego zachowania przechowywania zaszyfrowane.</span><span class="sxs-lookup"><span data-stu-id="61caa-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="61caa-128">UserName</span><span class="sxs-lookup"><span data-stu-id="61caa-128">UserName</span></span> | <span data-ttu-id="61caa-129">Określa nazwę użytkownika do uwierzytelniania w źródle.</span><span class="sxs-lookup"><span data-stu-id="61caa-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="61caa-130">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="61caa-130">Verbosity</span></span> | <span data-ttu-id="61caa-131">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="61caa-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

> [!Note]
> <span data-ttu-id="61caa-132">Upewnij się, że dodanie hasła źródeł w tym samym kontekście użytkownika, ponieważ nuget.exe jest później używany do uzyskiwania dostępu do źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="61caa-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="61caa-133">Hasło będzie przechowywany zaszyfrowany w pliku konfiguracji i mogły być odszyfrowane tylko w kontekście tego samego użytkownika, ponieważ został on zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="61caa-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="61caa-134">Tak na przykład jeśli używasz serwera kompilacji do przywracania pakietów NuGet, które muszą być szyfrowane hasło z tego samego użytkownika systemu Windows, uruchamiania zadań serwera kompilacji.</span><span class="sxs-lookup"><span data-stu-id="61caa-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="61caa-135">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="61caa-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="61caa-136">Przykłady</span><span class="sxs-lookup"><span data-stu-id="61caa-136">Examples</span></span>

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
