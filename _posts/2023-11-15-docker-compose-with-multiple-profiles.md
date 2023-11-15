---
layout: post
title: Running Docker Compose with Multiple Profiles
categories: tech
---

Official documentation on profiles: https://docs.docker.com/compose/compose-file/15-profiles/

But what they fail to cover, is running multiple profiles with multiple docker-compose files.


```yaml
## File 1

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
