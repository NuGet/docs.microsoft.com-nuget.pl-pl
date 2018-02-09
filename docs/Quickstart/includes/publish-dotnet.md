1. Zmień folder zawierający `.nupkg` pliku.

1. Uruchom następujące polecenie, określając nazwę pakietu i zamianę klucza wartość klucza interfejsu API:

    ```cli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. DotNet wyświetla wyniki procesu publikowania:

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

Zobacz [wypychania nuget dotnet](/dotnet/core/tools/dotnet-nuget-push).