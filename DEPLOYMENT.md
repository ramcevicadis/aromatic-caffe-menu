# 🚀 DEPLOYMENT UPUTSTVO - KORAK PO KORAK

## ⏱️ Procenjeno vreme: 30-45 minuta

---

## KORAK 1: Firebase Setup (10-15 min)

### 1.1 Kreirajte Firebase projekat

1. Idite na: https://console.firebase.google.com
2. Kliknite **"Add project"** (Dodaj projekat)
3. Unesite ime projekta: **aromatic-caffe**
4. Kliknite **Continue**
5. Onemogućite Google Analytics (nije potreban)
6. Kliknite **Create project**
7. Sačekajte da se projekat kreira (~30 sekundi)
8. Kliknite **Continue**

### 1.2 Omogućite Firestore Database

1. U levom meniju kliknite **Build → Firestore Database**
2. Kliknite **Create database**
3. Izaberite **Start in test mode** (kasnije ćemo podesiti sigurnost)
4. Izaberite lokaciju: **europe-west3 (Frankfurt)** ili **europe-central2**
5. Kliknite **Enable**
6. Sačekajte da se baza kreira (~1 minut)

### 1.3 Omogućite Authentication

1. U levom meniju kliknite **Build → Authentication**
2. Kliknite **Get started**
3. U tab-u **Sign-in method**, kliknite na **Email/Password**
4. Omogućite **Email/Password** (prvi switch)
5. Kliknite **Save**
6. Kliknite na tab **Users**
7. Kliknite **Add user**
8. Unesite:
   - Email: **admin@aromaticcaffe.rs**
   - Password: **[VAŠA SIGURNA LOZINKA]** (zapamtite je!)
9. Kliknite **Add user**

### 1.4 Kopirajte Firebase Config

1. Kliknite na **ikonu zupčanika** (⚙️) pored "Project Overview"
2. Kliknite **Project settings**
3. Scroll dole do sekcije **"Your apps"**
4. Kliknite na **Web ikonu** (</>)
5. Registrujte app:
   - App nickname: **aromatic-menu**
   - NE čekirajte Firebase Hosting
   - Kliknite **Register app**
6. **Kopirajte ceo firebaseConfig objekat** (od `const firebaseConfig = {` do `};`)
7. Kliknite **Continue to console**

### 1.5 Ubacite Config u kod

1. Otvorite fajl **index.html** u text editoru
2. Nađite liniju sa `const firebaseConfig = {` (oko linije 400)
3. **ZAMENITE** ceo firebaseConfig objekat sa kopiranim vrednostima
4. Nađite linije sa:
   ```javascript
   // firebase.initializeApp(firebaseConfig);
   // const db = firebase.firestore();
   // const auth = firebase.auth();
   ```
5. **OBRIŠITE** `//` ispred svake linije (odkomentirajte ih)
6. Sačuvajte fajl

---

## KORAK 2: Postavljanje Sigurnosnih Pravila (5 min)

### 2.1 Firestore Security Rules

1. U Firebase konzoli → **Firestore Database**
2. Kliknite na tab **Rules**
3. **OBRIŠITE** sve postojeće pravila
4. Otvorite fajl **firestore.rules** iz projekta
5. **KOPIRAJTE** sav sadržaj
6. **NALEPITE** u Firebase Rules editor
7. Kliknite **Publish**

---

## KORAK 3: Vercel Deployment (10-15 min)

### Opcija A: GitHub + Vercel (Preporučeno)

#### 3.1 Upload na GitHub

1. Idite na https://github.com/new
2. Repository name: **aromatic-caffe-menu**
3. Izaberite **Private** (ili Public, kako želite)
4. Kliknite **Create repository**
5. Pratite uputstva za upload postojećeg projekta:
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/[vaš-username]/aromatic-caffe-menu.git
   git push -u origin main
   ```

#### 3.2 Deploy na Vercel

1. Idite na https://vercel.com/signup
2. Sign up sa GitHub nalogom
3. Na Vercel dashboard-u, kliknite **Add New... → Project**
4. **Import** vaš GitHub repozitorijum (aromatic-caffe-menu)
5. Kliknite **Import**
6. Project Name: **aromatic-caffe-menu**
7. Root Directory: **./aromatic-caffe** (ili ostavljate `.` ako su fajlovi u root-u)
8. Kliknite **Deploy**
9. Sačekajte deployment (~2-3 minuta)
10. Kada je gotovo, kopirajte **Production URL**

### Opcija B: Direktan Upload (Brži, ali bez git kontrole)

1. Idite na https://vercel.com/signup
2. Sign up (može i sa email-om)
3. Kliknite **Add New... → Project**
4. Kliknite **Continue with Other**
5. Drag & drop **aromatic-caffe** folder
6. Ili kliknite **Browse** i izaberite folder
7. Kliknite **Deploy**
8. Sačekajte (~2-3 minuta)
9. Kopirajte URL

---

## KORAK 4: Povezivanje Domena (10 min)

### 4.1 U Vercel-u

1. Idite na vaš projekat u Vercel dashboard-u
2. Kliknite na tab **Settings**
3. U levom meniju kliknite **Domains**
4. Kliknite **Add**
5. Unesite vaš domen (npr: **menu.aromaticcaffe.rs**)
6. Kliknite **Add**

### 4.2 DNS Podešavanja (kod vašeg hosting provajdera)

Vercel će vam dati DNS instrukcije. Obično je:

**Za subdomen (menu.aromaticcaffe.rs):**
```
Type: CNAME
Name: menu
Value: cname.vercel-dns.com
```

**Za root domen (aromaticcaffe.rs):**
```
Type: A
Name: @
Value: 76.76.21.21
```

1. Idite kod vašeg registrara domena
2. Nađite DNS ili Domain management sekciju
3. Dodajte CNAME zapis kao što je navedeno
4. Sačuvajte izmene
5. Sačekajte propagaciju (5-60 minuta)

---

## KORAK 5: QR Kod i NFC (15 min)

### 5.1 Generisanje QR Koda

1. Idite na: https://www.qr-code-generator.com
2. Izaberite **URL** tip
3. Unesite vaš URL (npr: https://menu.aromaticcaffe.rs)
4. Prilagodite dizajn:
   - Boja: Crvena (#dc143c) za brand
   - Logo: Možete dodati Aromatic logo u centar
5. Kliknite **Download** (PNG, 300 DPI)
6. Štampajte QR kodove (10x10 cm je idealno)
7. Laminirajte ili stavite u pleksi holder
8. Postavite na stolove

### 5.2 NFC Tagovi (Opciono)

**Kupovina:**
- Amazon.rs: "NFC 215 tags"
- AliExpress: "NTAG215 NFC stickers"
- Cena: ~5-10€ za 10 komada

**Programiranje:**
1. Preuzmite app: **"NFC Tools"** (iOS ili Android)
2. Otvorite app
3. Idite na **Write**
4. Kliknite **Add a record**
5. Izaberite **URL/URI**
6. Unesite: https://menu.aromaticcaffe.rs
7. Kliknite **OK**
8. Približite NFC tag telefonu
9. Kliknite **Write**
10. Ponavljajte za svaki tag

**Postavljanje:**
- Zalepite na stolove (diskretno mesto)
- Ili u pleksi holdere sa instrukcijama
- Dodajte nalepnicu: "📱 Približite telefon za meni"

---

## KORAK 6: Testiranje (10 min)

### 6.1 Osnovne Funkcije
- [ ] Otvara se glavni ekran
- [ ] Logo se prikazuje
- [ ] Prebacivanje jezika radi
- [ ] Klik na MENI otvara kategorije
- [ ] Slike kategorija se učitavaju
- [ ] Klik na kategoriju prikazuje artikle
- [ ] Cene su vidljive
- [ ] WiFi info modal radi
- [ ] Alergeni modal radi
- [ ] Info modal radi

### 6.2 Admin Panel
- [ ] Klik na ☰ otvara login
- [ ] Login sa admin podacima radi
- [ ] Prikazuju se sve kategorije
- [ ] Artikli se učitavaju
- [ ] Izmena artikla čuva promene
- [ ] Dodavanje novog artikla radi
- [ ] Brisanje artikla radi
- [ ] Izmene su vidljive i u guest meniju

### 6.3 Mobilni Uređaji
- [ ] Testirajte na Android telefonu
- [ ] Testirajte na iPhone-u
- [ ] Testirajte na tabletu
- [ ] Responsive dizajn izgleda dobro
- [ ] Touch gestures rade pravilno

### 6.4 QR / NFC
- [ ] QR kod skeniranje otvara meni
- [ ] NFC tag otvara meni
- [ ] Radi na različitim telefonima

---

## KORAK 7: Popunjavanje Sadržajem

### 7.1 Dodavanje Kompletan Menija

Preko admin panela:
1. Login kao admin
2. Birajte kategoriju
3. Dodajte sve artikle sa cenama
4. Proverite srpske i engleske nazive
5. Obratite pažnju na gramatiku

### 7.2 Update Info Tekstova

U `index.html` fajlu, nađite `translations` objekat i:
- Prilagodite tekst o objektu (Amir-Agin Han)
- Proverite WiFi podatke
- Update alergene ako je potrebno

---

## 🎉 GOTOVO!

Vaš digitalni meni je live!

### Poslednji koraci:

1. **Obavestite tim:**
   - Pokažite konobarima kako se koristi admin panel
   - Napravite kratko uputstvo

2. **Marketing:**
   - Postavite QR kodove na stolove
   - Nalepnice "Skenujte za meni"
   - Social media objava

3. **Monitoring:**
   - Proveravajte da li sve radi
   - Pratite feedback od gostiju
   - Ažurirajte meni redovno

---

## 🆘 Pomoć i Podrška

**Ako nešto ne radi:**

1. Proverite Firebase config u `index.html`
2. Otvorite Chrome DevTools (F12) → Console tab
3. Tražite greške (crveno)
4. Proverite da li su Firebase pravila postavljena
5. Proverite da li je domen pravilno povezan

**Česte greške:**

- **"Firebase not defined"** → Niste odkomentarisali Firebase init kod
- **"Permission denied"** → Firestore pravila nisu postavljena
- **Slike se ne učitavaju** → Proverite putanje u `images/` folderu
- **Admin login ne radi** → Proverite Firebase Authentication

---

**Srećno! ☕✨**

Made with ❤️ for Aromatic Caffe
