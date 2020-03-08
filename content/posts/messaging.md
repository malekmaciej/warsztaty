---
title: "Messaging"
date: 2020-03-01T23:20:20+01:00
draft: false
---

# SES - Simple Email Service
- Różne protokoły (SMTP , REST API, AWS CLI, AWS SDK)
- Wsparcie dla nagłówków email
- Załaczniki, HTML, templates
- Możliwość wysyłania i odbierania maili na dużą skalę
- Symulator
- Cena
- Służy do komunikacji z ludźmi (email)
# SNS - Simple Notification Service
- Integracja z większością serwisów AWS
- Typ - jeden nadawca -> wielu odbiorców
- Limit na długość wiadomości to 8192 znaki UTF-8
- Brak możliwości przesyłania załączników, HTML
- Wymagane potwierdzenie odbiorcy przy subskrypcji
- Służy do natychmiastowej komunikacji pomiędzy aplikacjami lub serwisami AWS
# SQS - Simple Queue Service
- Najstarsza usługa AWS
- Możliwość wyboru standardowej kolejki lub FIFO (First-In-First-Out)
- Możliwość przechowywania wiadomości do 14 dni
- Brak ograniczeń w ilość wiadomości w kolejce
- Standardowo maksymalna wielkość wiadomości to 256KB
- Służy do buforowania wiadomość - wielu nadawców -> jeden odbiorca