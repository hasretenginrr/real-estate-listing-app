# Real Estate Listing App

[English](#overview) | [Türkçe](#türkçe)

## Overview

A React application for browsing, filtering, and adding real estate listings. Property records are read from and submitted to Google Sheets through NoCodeAPI.

This is a frontend prototype with a Turkish interface, not a production-ready real estate management system. No custom backend is included.

## Features

- Property cards and individual detail pages.
- Filters for rooms, bathrooms, balconies, garden, location, orientation, floor, and furnishing.
- Three filter modes: any, must-have, and must-not-have.
- Form for adding property records through an HTTP POST request.
- Client-side demo login/logout and conditional routing.
- Loading indicators and error handling in selected components.
- Simulated property approval flow.

> The “Onayla ve Mail At” button displays a success dialog after a delay. It does **not** send an email or persist an approval.

## Technology Stack

| Technology | Use |
| --- | --- |
| React 18 / JavaScript | Components, state, and effects |
| React Router DOM 6 | Client-side navigation |
| Ant Design 5 | Forms, cards, feedback, and dialogs |
| Fetch API | GET and POST requests |
| Google Sheets / NoCodeAPI | External property data integration |
| CSS | Interface styling |
| Create React App / react-scripts 5 | Development and build scripts |

Formik and Yup are declared dependencies, but the inspected property and login forms do not use them.

## Source Guide

| File | Responsibility |
| --- | --- |
| `src/App.js` | Routes and in-memory login state |
| `src/Login/Login.js` | Demo login form |
| `src/Evler/EvListele.js` | Fetching, displaying, and filtering listings |
| `src/Evler/Filtrele.js` | Filter controls |
| `src/Evler/EvIcerik.js` | Property details and simulated approval |
| `src/Evler/EvEkle.js` | Property creation form and POST request |
| `src/image/` | Branding images |

## Local Setup

Prerequisites: Node.js, npm, and a Google Sheets/NoCodeAPI test integration matching the expected data format. The repository does not pin a Node.js version.

1. Clone this repository using its current URL from GitHub's **Code** menu.
2. Open a terminal in the cloned directory.
3. Before running the app, replace the existing NoCodeAPI URLs in `EvListele.js`, `EvIcerik.js`, and `EvEkle.js` with an integration you control, backed by disposable test data. Do not submit records to the original integration.
4. Install dependencies and start the development server:

   ```bash
   npm ci
   npm start
   ```

5. Open `http://localhost:3000` and use the demo login defined in `src/Login/Login.js`. It is only a UI demonstration, not secure authentication.

The existing requests use the sheet tab `sayfa1`. Adjust the tab parameter if your test sheet uses a different name.

### Expected Data

The listing components expect a JSON object with a `data` array containing objects with these keys. The creation form submits a nested array in the same column order:

| Key | Meaning / expected value |
| --- | --- |
| `id` | Numeric property identifier |
| `oda` | Room count |
| `banyo` | Bathroom count |
| `bahce` | `var` or `yok` |
| `balkon` | Balcony count |
| `konum` | Location text |
| `cephe` | Orientation text |
| `esya` | `eşyalı` or `eşyasız` |
| `kat` | Floor number |

## Scripts

| Command | Purpose |
| --- | --- |
| `npm start` | Start the development server |
| `npm run build` | Generate a build in `build/` |
| `npm test` | Run the configured test runner |

The build and tests were not executed during this documentation update. The existing `App.test.js` still checks for the default “learn react” text, which the current application does not render.

## Limitations and Security Notes

- Login credentials are hardcoded in client code, and submitted login values are logged to the console. Do not use real passwords with this prototype.
- Login state is held in React memory, so refreshing clears it. “Remember me” does not implement persistence.
- Conditional frontend routes do not protect the external data API.
- The NoCodeAPI endpoint is embedded in client code. If it grants access without separate authorization, treat that access as exposed and rotate or revoke it with the provider. Moving a secret to a frontend environment variable would not keep it private.
- Duplicate-ID validation in `EvEkle.js` uses `row[0]`, whereas the listing components expect objects with an `id` field. This inconsistency needs correction, and uniqueness should be enforced server-side.
- Approval/email behavior is simulated. Listing editing and deletion are not implemented.
- No application-specific automated tests or CI workflow are included.

## Türkçe

### Proje Hakkında

Gayrimenkul kayıtlarını listelemek, filtrelemek, detaylarını görüntülemek ve yeni kayıt eklemek için geliştirilmiş React tabanlı bir ön yüz prototipidir. Veriler, NoCodeAPI üzerinden Google Sheets ile okunur ve kaydedilir.

Arayüz Türkçedir. Depoda özel bir backend bulunmaz; proje üretime hazır bir emlak yönetim sistemi olarak sunulmamaktadır.

### Özellikler

- Kartlarla ev listeleme ve detay sayfaları.
- Oda, banyo, balkon, bahçe, konum, cephe, kat ve eşya durumuna göre filtreleme.
- “Farketmez”, “Mutlaka Olmalı” ve “Mutlaka Olmamalı” filtre seçenekleri.
- HTTP POST isteğiyle yeni ev kaydı ekleme.
- Tarayıcı tarafında örnek giriş/çıkış ve koşullu yönlendirme.
- Bazı bileşenlerde yüklenme ve hata durumlarının gösterimi.
- Simülasyon olarak çalışan onay ekranı; **gerçek e-posta gönderimi yoktur**.

### Kurulum

1. GitHub'daki **Code** menüsünden deponun güncel bağlantısını kullanarak projeyi klonlayın.
2. `EvListele.js`, `EvIcerik.js` ve `EvEkle.js` içindeki NoCodeAPI adreslerini, size ait deneme verileri kullanan bir entegrasyonla değiştirin. Özgün entegrasyona kayıt göndermeyin.
3. Yukarıdaki veri tablosunda belirtilen alanları ve sütun sırasını kullanın. Mevcut kodun sekme adı `sayfa1` şeklindedir.
4. Proje klasöründe `npm ci` ve ardından `npm start` çalıştırın.
5. `http://localhost:3000` adresini açın. Örnek giriş bilgileri `src/Login/Login.js` içindedir; gerçek kimlik doğrulama sağlamaz.

### Mevcut Durum

Giriş bilgileri istemci kodunda sabittir ve giriş formu değerleri konsola yazdırılır. Gerçek parola kullanmayın. Sayfa yenilendiğinde oturum durumu sıfırlanır; “Beni Hatırla” kalıcı oturum sağlamaz.

API adresi istemci kodunda yer almaktadır. Adres tek başına erişim sağlıyorsa sağlayıcı üzerinden bu erişim yenilenmeli veya iptal edilmelidir. Ön yüz ortam değişkenleri sırları gizlemez.

Yeni kayıt formundaki benzersiz ID kontrolü, diğer bileşenlerin beklediği veri yapısıyla tutarlı değildir. Düzenleme, silme ve gerçek e-posta gönderimi uygulanmamıştır. Varsayılan React testi mevcut arayüzle eşleşmez.

Bu güncellemede kaynak kod incelenmiş, yalnızca dokümantasyon değiştirilmiştir. Uygulama, harici entegrasyon, derleme ve testler çalıştırılmamıştır.
