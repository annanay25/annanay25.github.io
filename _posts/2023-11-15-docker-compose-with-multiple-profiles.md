---
layout: post
title: Running Docker Compose with Multiple Profiles
categories: tech
---

So, this is the official documentation on profiles: [https://docs.docker.com/compose/compose-file/15-profiles/]([url](https://docs.docker.com/compose/compose-file/15-profiles/)).
Let's see how we can run multiple profiles _with overrides_ using docker-compose.


```yaml
## docker-compose.yaml
services:
  foo:
    image: foo

  bar:
    image: bar
    profiles:
      - test

  baz:
    image: baz
    depends_on:
      - bar
    profiles:
      - test

  zot:
    image: zot
    depends_on:
      - bar
    profiles:
      - debug
```

What if you want to run multiple profiles in a single run? That can be done with the `COMPOSE_PROFILES` environment flag as follows:

```console
COMPOSE_PROFILES=test,debug docker compose -f docker-compose.yaml up -d
```

Now what if you have a use-case to run overrides on a service? Exposing a port during local development for example:

```yaml
## docker-compose.override.yaml
services:
  bar:
    ports:
      - "80:80"
```

This can be run with:

```console
COMPOSE_PROFILES=test,debug docker compose -f docker-compose.yaml -f docker-compose.override.yaml up -d
```
