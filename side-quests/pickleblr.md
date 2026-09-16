---
layout: page
title: Pickleblr
permalink: /pickleblr/
description: An interactive neighbourhood map of pickleball courts in Bengaluru.
---

I've been playing a bunch of pickleball in Bangalore and the "where should we play" question always turned into a scavenger hunt. Playo, Hudle, a club's Instagram, someone's WhatsApp screenshot of a rooftop court.

Someone would already be booking PaddleX while someone else was still googling whether Indiranagar had a rooftop. Nobody had a picture of the whole city.

I really like [Bangalore Startup Map](https://www.bangalorestartupmap.com/) — pins on a map, filter by area, click for details. So I made the pickleball version: [pickleblr.com](https://pickleblr.com).

![Pickleblr map of pickleball courts across Bengaluru](/images/pickleblr/pickleblr-map.jpg)

65 venues across 39 neighbourhoods. Dedicated clubs, rooftop courts, and the multi-sport arenas that added pickleball last year. You can filter by neighbourhood, indoor/outdoor/rooftop, venue type, and price. Click a pin and you get hours, court count, rentals, amenities, and a booking link.

![PaddleX venue card on Pickleblr](/images/pickleblr/pickleblr-court.jpg)

A few things I cared about while building it:

The map is [MapLibre](https://maplibre.org/) with [OpenFreeMap](https://openfreemap.org/) tiles, so there's no Google / Mapbox API key and no quota. It's a static Next.js export sitting on Firebase Hosting — no backend.

Venues live in a TypeScript file, compiled from public listings (club sites, Playo, Hudle, District). Pins are neighbourhood-accurate, good enough to pick a place, not a surveyed GPS point. Prices and hours change, so confirm on the booking app before you go.

Missing a court? Ping me and I'll pin it.
