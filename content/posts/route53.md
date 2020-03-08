---
draft: false
date: 2020-03-06T20:00:00Z
lastmod: 2020-03-05T20:00:00Z
author: Maciej Malek
title: "Route53"
subtitle: "Scalable and highly available Domain Name System (DNS)"
description: "Skalowalny i wysokowydajny serwis DNS."
---

Route53 to serwis DNS w ktorym mozemy kupowac domeny i zarzadzac nimi.

# Utworzenie recordu IN A w domenie motobelfer.org
- `Hosted zones`
  - `motobelfer.org` -> `Create Record Set`
  - w prawym menu podajemy nazwe (taka sama jak nazwa S3 bucketu ktory wczesniej stworzylismy)
  - `Type: A` - `IPv4 address`
  - `Alias`: **Yes**
  - `Alias Target`: wybierzcie swoj bucket z listy `S3 website endpoints`
  - `Create`
![Tworzenie recordu DNS](/route53/create-record.PNG)

Alias do rekordu IN A jest specjalnym typem recordu w Route53.  
Jest to alias do resource'u w AWS lub do innego recordu. Dziala podobnie jak IN CNAME.  
Glowna roznica miedzy IN CNAME a Alias IN A to cena. Ten pierwszy kosztuje $0.50 a drugi jest darmowy.