---
draft: false
date: 2020-03-03T20:00:00Z
lastmod: 2020-03-05T20:00:00Z
author: Maciej Malek
title: "Codepipeline"
description: "Utworzenie pipeline'a do automatycznego deploymentu kodu z GitHuba'a do AWS S3"
---

Utworzenie pipeline'a do automatycznego deploymentu kodu z GitHuba'a do AWS S3
===

`Create pipeline` 
## Step 1
- **Pipeline name** - nalezy podac swoja nazwe
- **Service role** 
  - `Existing service role` 
  - wybieramy juz istniejaca IAM Role o nazwie `WarsztatyRole`
    - **Advance settings**
      - `Artifact store` -> `Default location`
      - `Encryption key` -> `Default AWS Managed Key`
## Step 2
- **Source**
  - wybieramy co ma byc zrodlem dla naszego pipeline - do wyboru sa serwisy AWS CodeCommit (repozytorium GIT), Amazon ECR (Elastic Container Registry), Amazon S3, oraz zewnetrze takie jak GutHub, Bitbucket Cloud.
  - `GitHub`
    - **Connect to GitHub**
    - nalezy sie poprawnie zautoryzowac w serwisie GitHub
    - wybieramy rezpozytorium ktore wczesniej stworzyliscie
    - **Branch** -> `master`
    - zostawiamy standardowy sposob notyfikacji czy GitHub webhooks
## Step 3
- Add Build Stage
  - to czesc pomijamy, w naszym przypadku bedziemy przesylac pliki bezposrednio z repozytorium GIT na S3 przy kazdym merge'u do master branch.
  - AWS CodeBuild przyda sie kiedy chcemy automatycznie deploy'owac backend (AWS Lambda lub EC2 lub ECS/Fargate)
  - wybieramy `Skip build stage`
## Step 4
- Deploy
  - **Deploy provider** -> `Amazon S3`
  - jest mozliwosc wybrania innych serwisow do ktorych chcemy wyslac nasz kod (jezeli pominelismy Build Stage) lub zbudowana aplikacje.
  - wybieramy stworzony wczesniej S3 bucket
  - zaznaczamy **Extract file before deploy**
  - Deployment path pozostawiamy puste
