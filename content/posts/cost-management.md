---
draft: false
date: 2020-03-02
author: Maciej Malek
title: "AWS Cost Explorer i Budgets"
subtitle: "Zarzadzanie budgetem swojego konta AWS"
description: "Kontrolowanie wydatkow w chmurze AWS nie jest latwe"
---

# Zarzadzanie budgetem i monitorowanie kosztow

Amazon Web Services reklamuje swoje uslugi jako *placicz tylko za tyle ile zuzyjesz, zadnych oplat wstepnych*
W zwiazku z tym kazda osoba ktora uzywa i tworzy zasoby (resource'y) w AWS musi byc swiadoma ile one kosztuja.
Dotyczy to:
- Deweloperow 
    - aby usuwali lub wylaczali uslugi z ktorych aktualnie nie korzystaja
- DevOps'ow 
    - aby tworzyli infrastrukture w oparciu o Best Practises i Well Architected Framework 
    - projektujac systemy dla deweloperow mysleli nie tylko o wymaganiach technicznych ale tez o tym ile takie rozwiazanie bedzie kosztowac
- SRE's (Site Relability Engineers)
    - aby tworzac systemy monitorowania pamietali o kosztach, np. czy np. wysylanie wszystkich logow i eventow do zewnetrznego narzedzia jest wymagane czy moze lepiej filtrowac jeszcze po stronie AWS i wysylac tylko te dane, ktore sa potrzebne.
    - monitorowali koszt resource'ow wzgledem ich uzycia (wazne w przypadku serwerow wirtualnych w EC2)
- Operation Team
    - aby jak najszybciej usuwali tymczasowe resource'y stworzone przy diagnozowaniu problemow zglaszanych przez uzytkownikow.

# AWS Budgets

Narzedzie to oferuje mozliwosc ustalenia swojego budzetu (miesieczny / kwartalny / roczny) i po przekroczeniu go wykonania zadanej akcji.  
Sa 4 typy budzetow:
1. Koszty
2. Zuzycie zasobow
3. Wykorzystanie zakupionych Reserved Instances (RIs)
4. Wykorzystanie zakupionych Savings Plans

![Typy budzetow](/cost-management/budget-types-1.PNG)

# AWS Cost Explorer

Narzedzie do monitorowania na biezaco kosztow w ramach jednego konta AWS. Standardowo dane odswiezane sa raz na dobe.  
Posiada rozbudowana mozliwosc filtrowania i grupowania wynikow.  
Aby w pelni wykorzystac mozliwosci tego narzedzia wymagane jest dobre zaplanowanie i konsekwencja w tagowaniu resourcow.
W przypadku bardzo wielu resource'ow i wielu osob uzywajacych tego samego konta AWS bez tagow, identyfikacja kosztow per zespol / projekt jest bardzo trudna i czasochlonna.  
Przyklad:
![Przyklad AWS Cost Explorer](/cost-management/cost-explorer-1.PNG)

# Reserved Instances i Savings Plans

AWS oferuje znizku na niektore swoje serwisy w zamian za zobligowanie sie do ich wykorzystywania przez okreslony czas (1 do 3 lat) w okreslonym zakresie.
- Compute Savings Plans
    - znizka do 66% 
    - dotyczy uzycia serwisow EC2, AWS Fargate, AWS Lambda
- EC2 Instance Savings Plans
    - znizka do 72%
    - dotyczy uzycia wybranego typu instancji (np. m5) w danych regionie (np. EU Frankfurt)
- Reserved Instances
    - znizka do 75%
    - dotyczy uzycia wybranej wielkosci i typu instancji (np. m5.2xlarge) w danym regionie (np. EU Frankfurt) na danej platformie (np. Windows)

Przy zakupie duzej ilosci Reserved Instances jak i Savings Plans nalezy pamietac o podatku (Tax)!

Uzycie tych planow mozna monitorowowac i skonfigurowac alarmy i notyfikacje tak abysmy byli informowani kiedy nie wykorzystujemy w/w planow.  
Przyklad: moze sie zdarzyc ze w ramach cost optimization wszystkie serwery m4.xlarge zamieniono na m4.large. W zwiazku z tym znizki:
- za serwery m4.large placimy normalna cene (on-demand price)
- placimy w ramach Reserved Instances za serwery m4.xlarge ktorych juz nie ma.

# Uslugi, ktore sa za darmo przez caly czas
Przyklady:
## Amazon DynamoDB
- 25 GB of Storage
- 25 provisioned Write Capacity Units (WCU)
- 25 provisioned Read Capacity Units (RCU)
- Enough to handle up to 200M requests per month.
## AWS Lambda
- 1,000,000 milion darmowych requestow na miesiac
Up to 3.2 million seconds of compute time per month
## Amazon SNS 
- 1,000,000 Publishes
- 100,000 HTTP/S Deliveries
- 1,000 Email Deliveries
## Amazon CloudWatch
- 10 Custom Metrics and 10 Alarms
- 1,000,000 API Requests
- 5GB of Log Data Ingestion and 5GB of Log Data Archive
- 3 Dashboards with up to 50 Metrics Each per Month
## Wiecej na stronie [AWS Free Tier](https://aws.amazon.com/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc&awsf.Free%20Tier%20Types=tier%23always-free&awsm.page-all-free-tier=1) 