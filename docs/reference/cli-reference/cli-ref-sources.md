---
title: Polecenie źródeł interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia nuget.exe sources
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 73c9cea8200a1ab1937d25a9a611ae7f2a943dba
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622593"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="08209-103">sources — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="08209-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="08209-104">**Dotyczy:** użycie pakietu, publikowanie &bullet; **obsługiwanych wersji:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="08209-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="08209-105">Zarządza listą źródeł znajdujących się w pliku konfiguracyjnym zakresu użytkownika lub w określonym pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="08209-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="08209-106">Plik konfiguracji zakresu użytkownika znajduje się w lokalizacji `%appdata%\NuGet\NuGet.Config` (Windows) i `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="08209-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="08209-107">Należy pamiętać, że źródłowy adres URL dla nuget.org to `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="08209-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="08209-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="08209-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="08209-109">gdzie `<operation>` to jeden z elementów *list, Add, Remove, Enable, Disable* lub *Update*, `<name>` jest nazwą źródła i `<source>` jest adresem URL źródła.</span><span class="sxs-lookup"><span data-stu-id="08209-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="08209-110">Jednocześnie można wykonywać tylko jedno źródło.</span><span class="sxs-lookup"><span data-stu-id="08209-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="08209-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="08209-111">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="08209-112">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="08209-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="08209-113">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="08209-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="08209-114">*(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="08209-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Format`**

  <span data-ttu-id="08209-115">Dotyczy `list` akcji i może być `Detailed` (wartość domyślna) lub `Short` .</span><span class="sxs-lookup"><span data-stu-id="08209-115">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span>

- **`-?|-help`**

  <span data-ttu-id="08209-116">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="08209-116">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="08209-117">Nazwa źródła.</span><span class="sxs-lookup"><span data-stu-id="08209-117">Name of the source.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="08209-118">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="08209-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Password`**

  <span data-ttu-id="08209-119">Określa hasło do uwierzytelniania ze źródłem.</span><span class="sxs-lookup"><span data-stu-id="08209-119">Specifies the password for authenticating with the source.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="08209-120">Ścieżka do źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="08209-120">Path to the package(s) source.</span></span>

- **`-StorePasswordInClearText`**

  <span data-ttu-id="08209-121">Wskazuje, że hasło ma być przechowywane w niezaszyfrowanym tekście zamiast w domyślnym zachowaniu zaszyfrowanego formularza.</span><span class="sxs-lookup"><span data-stu-id="08209-121">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span>

- **`-UserName`**

  <span data-ttu-id="08209-122">Określa nazwę użytkownika do uwierzytelniania ze źródłem.</span><span class="sxs-lookup"><span data-stu-id="08209-122">Specifies the user name for authenticating with the source.</span></span>

- **`-ValidAuthenticationTypes`**

  <span data-ttu-id="08209-123">Rozdzielana przecinkami lista prawidłowych typów uwierzytelniania dla tego źródła.</span><span class="sxs-lookup"><span data-stu-id="08209-123">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="08209-124">Domyślnie wszystkie typy uwierzytelniania są prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="08209-124">By default, all authentication types are valid.</span></span> <span data-ttu-id="08209-125">Przykład: `basic,negotiate`.</span><span class="sxs-lookup"><span data-stu-id="08209-125">Example: `basic,negotiate`.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="08209-126">Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .</span><span class="sxs-lookup"><span data-stu-id="08209-126">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

> [!Note]
> <span data-ttu-id="08209-127">Pamiętaj o dodaniu hasła źródeł pod tym samym kontekstem użytkownika co nuget.exe jest później używany do uzyskiwania dostępu do źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="08209-127">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="08209-128">Hasło będzie przechowywane w pliku konfiguracyjnym i może zostać odszyfrowane tylko w tym samym kontekście użytkownika, w którym został zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="08209-128">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="08209-129">Na przykład w przypadku przywracania pakietów NuGet przy użyciu serwera kompilacji hasło musi być szyfrowane za pomocą tego samego użytkownika systemu Windows, w którym zostanie uruchomione zadanie serwera kompilacji.</span><span class="sxs-lookup"><span data-stu-id="08209-129">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="08209-130">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="08209-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="08209-131">Przykłady</span><span class="sxs-lookup"><span data-stu-id="08209-131">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
