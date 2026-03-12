# Projekt: EUROSKLEP  
**Sklep elektroniczny – EuroSklep**

## 1. Cel projektu

Stworzenie nowoczesnego, szybkiego i przyjaznego użytkownikowi sklepu internetowego umożliwiającego sprzedaż produktów fizycznych / cyfrowych / usług z naciskiem na konwersję, mobilność i zgodność z aktualnymi wymaganiami prawnymi oraz trendami UX/UI 2025–2026.

## 2. Architektura

- **Typ aplikacji**: SPA + SSR (hybryda)  
- **Model**: Monolit na start → możliwość ewolucji w kierunku mikroserwisów (np. oddzielny moduł zamówień / płatności / wyszukiwarka w przyszłości)  
- **Frontend ↔ Backend**: REST API + GraphQL (opcjonalnie na bardziej złożone zapytania)  
- **Renderowanie**: SSR dla SEO + krytycznych stron (produkt, kategoria, strona główna) + CSR dla panelu koszyka / konta użytkownika  
- **Wzór projektowy**: MVC na backendzie + komponentowy frontend (kompozycja + feature-sliced design)

## 3. Stos technologiczny 

### Frontend
- JavaScript / TypeScript
- Vite + React 19 / Next.js 15 (App Router + Server Components)
- Styling: Tailwind CSS + shadcn/ui lub Radix UI + clsx
- Markdown → HTML: marked.js + highlight.js (jeśli potrzebne opisy bogate)
- State management: Zustand lub Jotai (lekko) + React Query / TanStack Query
- Ikony: lucide-react

### Backend
- Node.js 22+ / Bun / Deno (alternatywnie PHP 8.3+)
- Framework: NestJS / Fastify / Express (lub Laravel 12 jeśli PHP)
- Baza danych: PostgreSQL (główna) + Redis (sesje, cache, kolejki)
- ORM: Prisma / Drizzle ORM (lub Eloquent jeśli PHP)

### Inne
- Deployment: Vercel (frontend) + Railway / Render / Hetzner + Docker
- CI/CD: GitHub Actions
- Autentykacja: JWT + refresh tokens + next-auth / Lucia (lub Laravel Sanctum)
- Płatności: Stripe + Przelewy24 / PayU / Tpay
- Wysyłka / logistyka: InPost / DPD / ApiShip / Furgonetka
- Wyszukiwarka: Meilisearch / Typesense / Algolia (jeśli budżet)

## 4. Grupa docelowa

- Główni odbiorcy:  
  - Kobiety i mężczyźni 18–45 lat  
  - Mieszkańcy miast i przedmieść (70%+ zakupy mobile)  
  - Osoby ceniące szybką i bezproblemową obsługę  
  - Świadomi ceny, ale otwarci na wartość dodaną (szybka dostawa, ładne zdjęcia, opinie, personalizacja)

- Najważniejsze potrzeby i bolączki:
  - Szybkie znalezienie produktu (wyszukiwarka + filtry)
  - Jasna informacja o dostępności, czasie i koszcie wysyłki
  - Bezpieczne i wygodne płatności (BLIK, szybkie przelewy, Apple Pay / Google Pay)
  - Możliwość zakupu bez zakładania konta (guest checkout)
  - Intuicyjny proces zakupowy (≤ 3 kliknięcia do finalizacji)
  - Dobra obsługa zwrotów i reklamacji (widoczna na stronie)
  - Opinie i zdjęcia od klientów

## 5. Kluczowe funkcjonalności 

### Strony publiczne
- Strona główna (hero + bestsellery + kategorie + newsletter)
- Lista produktów / kategorie / filtry / sortowanie
- Karta produktu (zdjęcia 360°/zoom, warianty, opinie, akcesoria, „kup z tym produktem”, FAQ)
- Koszyk + mini-koszyk
- Checkout (gość + zalogowany) – 1-stronicowy lub 3-krokowy
- Strona „Dziękujemy za zakup” + potwierdzenie e-mail
- Strony statyczne: O nas, Kontakt, Regulamin, Polityka prywatności, Zwroty i reklamacje, Dostawa, Płatności

### Konto użytkownika
- Rejestracja / logowanie (e-mail + hasło, Google, Facebook)
- Historia zamówień + szczegóły + faktura PDF
- Edycja danych + adresy dostaw
- Ulubione / lista życzeń
- Subskrypcje newslettera / powiadomienia o stanie zamówienia

### Panel administracyjny 
- CRUD produktów + warianty + zdjęcia
- Zarządzanie kategoriami i atrybutami
- Zamówienia (statusy, notatki, wysyłka)
- Podstawowe statystyki (sprzedaż, konwersja, porzucone koszyki)
- Zarządzanie treścią (banery, promocje, strony statyczne)

### Must-have 
- Pełna responsywność + PWA (opcjonalnie)
- Szybkość ładowania < 2–2,5 s (LCP, CLS, FID/INP)
- Zaawansowana wyszukiwarka + autouzupełnianie + synonimy
- Porzucony koszyk – automatyczny e-mail / SMS (po 1 h)
- Opinie + oceny + zdjęcia od klientów
- Cross-sell / up-sell / frequently bought together
- Porównywarka produktów (2–4 produkty)
- Rabaty / kody promocyjne / vouchery
- Integracja z Google Analytics 4 / Meta Pixel / Hotjar / Plausible

## 6. Wymagania techniczne i prawne 

### Prawne (Polska / UE)
- Regulamin sklepu zgodny z UOKiK + Dyrektywą Omnibus
- Polityka prywatności + RODO + Information clause
- Zgoda na cookies (banner + CMP – np. CookieYes / Usercentrics)
- Informacja o prawie odstąpienia od umowy (14 dni)
- Wzór formularza odstąpienia od umowy (do pobrania)
- Informacje o sprzedawcy (dane firmy, NIP, REGON, KRS, adres)
- Najniższa cena z ostatnich 30 dni (przy promocjach – Omnibus)
- WCAG 2.2 poziom AA (obowiązek od czerwca 2025 dla wielu podmiotów)

### Techniczne / jakościowe
- SEO: meta tagi, schema.org (Product, Offer, Review, Breadcrumb), sitemap, robots.txt, hreflang (jeśli wielojęzyczność)
- Core Web Vitals passing
- Bezpieczeństwo: HTTPS, CSP, HSTS, secure cookies, rate limiting, OWASP Top 10
- Backup bazy + plików (codzienny / co 6 h)
- Monitoring błędów (Sentry / Logflare)

## 7. Dokumentacja 

- **Kod** — JSDoc / TypeDoc (frontend) + PHPDoc / TSDoc (backend)
- **Architektura i decyzje** — `/docs/architecture.md` + ADR (Architectural Decision Records)
- **Logika biznesowa** — osobny plik `/docs/business-logic.md` (przepływy: zakup, zwrot, reklamacja, zamówienie, promocje)
- **API** — OpenAPI / Swagger lub `/docs/api.md`
- **Środowiska** — `.env.example` + opis (dev / staging / prod)
- **Instrukcja uruchomienia** — `/README.md` + `/docs/setup.md`
- **Checklista wdrożeniowa** — osobny plik przed każdym releasem

## 8. Kolejne etapy 

- Moduł subskrypcji / płatności cykliczne
- B2B (cenniki indywidualne, faktury proforma)
- Wielojęzyczność + wielowalutowość
- Aplikacja mobilna (PWA → native lub React Native)
- AI rekomendacje produktów
- Live chat + chatbot
- Integracja z TikTok Shop / Allegro / Amazon

