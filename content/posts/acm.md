---
draft: false
date: 2020-03-05T20:00:00Z
lastmod: 2020-03-05T20:00:00Z
author: Maciej Malek
title: "AWS Certificate Manager"
subtitle: "Utworzenie certyfikatu SSL w AWS Certificate Manager."
description: "Tworzenie darmowych certyfikatow SSL nigdy nie bylo latwiejsze."
---

Utworzenie certyfikatu SSL w AWS Certificate Manager
===
Serwis - AWS Certificate Manager
- wybierzcie region - N. Virginia (prawy górny róg) 
  - jest to bardzo wazne gdyz usługa `CloudFront` nie jest zregionalizowana i nie mozemy w tym przypadku użyć regionu Frankfurt
- `Request a certificate`
    - nalezy wybrac `Request a public certificate` -> Request a certificate
    - w `Domain name` nalezy podac pełna nazwe swojej domeny dla ktorej tworzycie certyfikat np. **jannowak.motobelfer.org**
    - prosze wybrac `DNS validation` (czyli utworzenie specjalnego rekordu IN CNAME ktory potwierdzi dostep do domeny w ktorej tworzycie certyfikat)
- tagi 
  - Tag **Name = owner**, **Value = <nazwa waszego użytkownika></nazwa>**
- następnie `Review` i `Confirm` - nalezy chwile poczekac na przetworzenie zgloszenia.
- `Validation` - tworzymy record DNS w Route53 
![SSL Certificate DNS validation](/acm/SSL_DNS_Validation.png)

Teraz trzeba poczekac az certyikat zostanie utworzony i zwalidowany.

