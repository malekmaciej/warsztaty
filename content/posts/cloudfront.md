---
draft: false
date: 2020-03-04T22:00:00+01:00
lastmod: 2020-03-05T20:00:00Z
author: Maciej Malek
title: "Cloudfront"
subtitle: "Tworzenie CloudFront Distribution."
description: "Usługa CDN Content Delivery Network - towrzenie dystrybucji."
---
Co to jest CloudFront?
====
CloudFront to CDN Content Delivery Network – jest to usługa polegająca na instalowaniu fragmentów strony internetowej na wielu serwerach na całym świecie (sieć odwrotnych serwerów pośredniczących tzw. Reverse Proxy). W efekcie, strona działa zawsze szybciej, dysponujemy dużo większą przepustowością łączy ale co najważniejsze, lokalizacja serwera (czyli to gdzie jest przechowywana strona internetowa) przestaje mieć jakiekolwiek przełożenie na dodatkowe opóźnienia wynikające z odległości jaką musi pokonać połączenie internetowe.

Zadania do wykonania na zajeciach:
===
- `Create Distribution`
  - wybieramy **Web** -> **Get Started**
  - `Origin Domain Name` 
    - **wybieramy swój S3 bucket**
  - `Origin Path` 
    - **zostawiamy puste**
  - `Origin ID` 
    - wygenerowało się automatycznie - **zostawiamy tak jak jest**
  - `Restrict Bucket Access` 
    - do celów szkoleniowych zostawiamy **No**. 
    - W pracy, ze względów bezpieczeństwa, zawsze włączamy tak aby mozna bylo sie odwolac do naszej strony tylko przez CloudFront a nie bezposrednio do S3.
  - `Origin Custom Headers` 
    - **pozostawiamy puste**
  - `Viewer Protocol Policy` 
    - zmieniamy na **Redirect HTTP to HTTPS**
![Pierwszy krok](/cloudfront/step-1.PNG)
  - `Object Caching` 
    - wybieramy **Customize** 
    - zmieniamy `Maximum TTL` i `Default TTL` na **30** 
    - Jest to czas jaki pliki naszej strony beda trzymane w cache'u CloudFronta - do dewelopmentu potrzebujemy miec mala wartosc tak aby zmiany w kodzie byly szybko widoczne.
  - `Distribution Settings`
    - Price Class -> **Use Only U.S., Canada and Europe**
![Drugi krok](/cloudfront/step-2.PNG)
  - `Alternate Domain Names (CNAMEs)` 
    - wpisujemy nasza domene np. jannowak.motobelfer.org
  - `SSL Certificate` 
    - ustawiamy **Custom SSL Certificate** 
    - wybieramy nasz wcześniej utworzony certyfikat (lub certyfikat z * jezeli nasz certyfikat nie zostal jeszcze zwalidowany)
  - `Default Root Object` 
    - to jest główny plik naszej strony - wpisujemy **index.html**
  - **Create Distribution** - czas tworzenia sie dystrybucji to okolo 20 minut.
![Trzeci krok](/cloudfront/step-3.PNG)

Po utworzeniu dystrybucji przechodzimy do Route53 i modyfikujemy nasz DNSowy record tak aby zamiast na S3 wskazywal na nasza dystrybucje CloudFront ktora powinna byc na liscie.
