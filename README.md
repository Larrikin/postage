# Postage-PoW — Lightweight Proof-of-Work “Stamp” for Email

**Postage-PoW** is a proposal for **three optional SMTP headers** that let senders
attach a small proof-of-work (PoW) “stamp” to any message.  
Receivers can verify the stamp with **one hash call** and, if valid, lower the
message’s spam score. Senders choose the difficulty per message, trading a few
milliseconds of CPU time for better deliverability of important mail.

> **Heads-up:** the project is at the *spec-draft* stage — **no production code
> yet**. Feedback and early PoC contributions are very welcome.

---

## Why (TL;DR)

| Pain point                              | How Postage-PoW helps                                     |
|-----------------------------------------|-----------------------------------------------------------|
| AI-generated spam is cheap and fast.    | Each extra PoW bit doubles the cost per message.          |
| False positives hurt critical mail.     | Attach a higher-difficulty stamp to must-reach messages.  |
| SMTP extensions are hard to deploy.     | Pure headers: drop-in, ignored by legacy servers.         |

---

## Draft Header Spec

| Header             | Purpose                                   |
|--------------------|-------------------------------------------|
| `X-Postage`        | Integer **N** — leading-zero difficulty.  |
| `X-Postage-Hash`   | Hash algorithm, e.g. `sha256`.            |
| `X-Postage-Proof`  | Token whose hash starts with **N** zeros. |

*Full algorithm and security notes live in [`spec.md`](spec.md).*

---

## Roadmap

- [ ] Public discussion & feedback collection  
- [ ] Reference CLI / library (Python)  
- [ ] Postfix / Exim milter for on-receive verification  
- [ ] Plugins for rspamd / SpamAssassin  
- [ ] Benchmark suite on mobile & server hardware  
- [ ] Internet-Draft submission (IETF)

---

## Want to help?

1. **Open an issue** with questions, edge cases or prior-art links.  
2. **Fork this repo** and prototype a stamper/verifier in your favourite language.  
3. **Share benchmarks** — even simple hash-rate numbers are useful.  
4. **Review or extend the spec** — PRs welcome.

---

## 🇷🇺 Русская версия

### Что такое Postage-PoW

**Postage-PoW** — это три *необязательных* SMTP-заголовка, которые позволяют
отправителю прикрепить к письму маленькую «марку» — доказательство работы
(Proof-of-Work).  
Получатель делает **один** вызов хэш-функции, чтобы проверить марку, и при
успехе может снизить спам-оценку сообщения. Отправитель сам выбирает сложность
марки, обменивая миллисекунды процессора на лучшую доставляемость важных писем.

> **Статус:** пока только черновик спецификации, без готового кода. Любые идеи,
> тесты и pull-request’ы приветствуются.

---

### Зачем это нужно (коротко)

| Проблема                                   | Что даёт Postage-PoW                        |
|--------------------------------------------|---------------------------------------------|
| AI-спам рассылается бесплатно и массово.   | Каждый лишний ноль в хэше удваивает цену.   |
| Фильтры ошибочно ловят важную почту.       | Можно повысить сложность только для критики |
| Менять SMTP-команды сложно.                | Чистые заголовки, старые сервера их игнорят |

---

### Черновая спецификация заголовков

| Заголовок            | Содержит                                   |
|----------------------|--------------------------------------------|
| `X-Postage`          | Целое **N** — требуемое число нулей.       |
| `X-Postage-Hash`     | Алгоритм хэша (например `sha256`).         |
| `X-Postage-Proof`    | Строка, чей хэш начинается с **N** нулей.  |

---

### Дорожная карта

* сбор отзывов  
* эталонная CLI-утилита и библиотека на Python  
* milter для Postfix/Exim  
* плагины для rspamd / SpamAssassin  
* бенчмарки на мобильных и серверных CPU  
* черновик Internet-Draft для IETF

---

### Как помочь

* Оставляйте issues с вопросами и кейсами;  
* пробуйте писать мини-реализацию на своём языке;  
* делитесь замерами скорости хэширования;  
* присылайте PR с улучшениями спецификации.

