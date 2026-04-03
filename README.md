![Backend](https://img.shields.io/badge/Backend-.NET%2010-512BD4?logo=dotnet&logoColor=white)
![Database](https://img.shields.io/badge/Database-PostgreSQL%2016-4169E1?logo=postgresql&logoColor=white)
![Infrastructure](https://img.shields.io/badge/Infra-Docker-2496ED?logo=docker&logoColor=white)

### Run me

For convenience purposes, a ``run.sh`` script is available which is essentially a wrapper on top of ``docker compose``.
It is meant to do the following:

  * create the EF migration
  * fire up the containers for ``postgres`` and the ``cms api``

---

Make the ``run.sh`` executable (run this only once):

```shell
$ chmod +x run.sh
```

Run the docker compose wrapper script:

```shell
$ ./run.sh
```

The first run may take a while, as Docker fetches the dotnet image(s). 
Once all containers are up and running, you can start interacting with the ``cms api`` via curl.

---

##### Examples:

Get a basic authorization token:

```shell
$ BASICAUTH=$(echo -n 'admin:password' | base64)
$ echo $BASICAUTH
```

Check the cms api health

```shell
$  curl 127.1:8080/health -H "Authorization: Basic $BASICAUTH"
```

Post some events

```shell
$ curl 127.1:8080/cms/events -d "@data.json" -H "Content-Type: application/json" -H "Authorization: Basic $BASICAUTH"
```

Fetch current events (assumes ``jq`` is available in your PATH)

```shell
$ curl 127.1:8080/cms/entities  -H "Authorization: Basic $BASICAUTH"  | jq
```
