# Aromatic Caffe - Digitalni Meni Sistem

## 🎯 Funkcionalnosti

✅ **Digitalni Meni**
- Dvojezični (Srpski/Engleski)
- Kategorije sa slikama
- Artikli sa cenama
- Info o alergenima
- WiFi pristup info
- O objektu (Amir-Agin Han)

✅ **Admin Panel**
- Dodavanje artikala
- Uređivanje artikala
- Brisanje artikala
- Izmena cena
- Upravljanje po kategorijama

✅ **Pristup**
- QR kod
- NFC tag
- Direktan link

---

## 📋 Potrebno za Deployment

### 1. Firebase Setup (Besplatno)

1. **Kreirajte Firebase projekat:**
   - Idite na https://console.firebase.google.com
   - Kliknite "Add project"
   - Unesite ime: "aromatic-caffe"
   - Pratite korake

2. **Omogućite Firestore:**
   - U Firebase konzoli → Build → Firestore Database
   - Kliknite "Create database"
   - Izaberite "Start in test mode" (kasnije ćete podesiti pravila)
   - Izaberite region (europe-west)

3. **Omogućite Authentication:**
   - U Firebase konzoli → Build → Authentication
   - Kliknite "Get started"
   - Omogućite "Email/Password" metod
   - Dodajte admin korisnika:
     - Email: admin@aromaticcaffe.rs
     - Password: [vaša lozinka]

4. **Kopirajte Firebase Config:**
   - U Firebase konzoli → Project settings (zupčanik ikona)
   - Scroll do "Your apps" → Web app (</> ikona)
   - Kopirajte firebaseConfig objekat

5. **Ubacite Config u kod:**
   - Otvorite `index.html`
   - Nađite `firebaseConfig` objekat (linija ~400)
   - Zamenite sa vašim podacima:
   ```javascript
   const firebaseConfig = {
       apiKey: "VAŠA_API_KEY",
       authDomain: "aromatic-caffe.firebaseapp.com",
       projectId: "aromatic-caffe",
       storageBucket: "aromatic-caffe.appspot.com",
       messagingSenderId: "VAŠ_ID",
       appId: "VAŠ_APP_ID"
   };
   ```
   - Odkomentirajte linije za inicijalizaciju Firebase-a (linije ~433-435)

### 2. Vercel Deployment (Besplatno)

**Opcija A: GitHub + Vercel (Preporučeno)**

1. **Kreirajte GitHub repozitorijum:**
   - Idite na https://github.com/new
   - Naziv: "aromatic-caffe-menu"
   - Uploadujte sve fajlove

2. **Deploy na Vercel:**
   - Idite na https://vercel.com
   - Kliknite "Import Project"
   - Izaberite vaš GitHub repo
   - Deploy!

3. **Povežite domen:**
   - U Vercel dashboard → Settings → Domains
   - Dodajte vaš domen
   - Pratite DNS instrukcije

**Opcija B: Direktan Upload**

1. Idite na https://vercel.com
2. Kliknite "Deploy"
3. Drag & drop `aromatic-caffe` folder
4. Povežite domen

### 3. QR Kod & NFC

**QR Kod:**
- Posle deploya, kopirajte URL (npr. https://menu.aromaticcaffe.rs)
- Generišite QR kod na https://www.qr-code-generator.com
- Štampajte i postavite na stolovima

**NFC Tag:**
- Kupite NFC tagove (Amazon, AliExpress)
- Koristite app "NFC Tools" (Android/iOS)
- Write → Add a record → URL → Unesite vaš URL
- Zalepite tagove na stolovima

---

## 🔐 Sigurnost - Firestore Rules

Nakon deploya, postavite Firestore pravila:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Svi mogu čitati meni
    match /menu/{document=**} {
      allow read: if true;
      allow write: if request.auth != null;
    }
    
    // Samo autentifikovani korisnici mogu pisati
    match /categories/{document=**} {
      allow read: if true;
      allow write: if request.auth != null;
    }
  }
}
```

---

## 📱 Kako Koristiti

### Za Goste:
1. Skeniraju QR kod ili približe telefon NFC tagu
2. Otvara se meni
3. Biraju jezik (Srpski/Engleski)
4. Pregledaju artikle po kategorijama
5. Vide cene
6. Pristupaju WiFi info, alergenima, i info o objektu

### Za Konobare (Admin):
1. Klik na ☰ (hamburger meni) na početnom ekranu
2. Login sa admin podacima
3. Biraju kategoriju
4. Dodaju/uređuju/brišu artikle
5. Menjaju cene
6. Izmene su odmah vidljive svim gostima

---

## 🎨 Prilagođavanje

### Logo
- Zamenite `images/Logo_Aromatic.jpg` sa vašim logoom

### Boje
- Promenite `#dc143c` (crvena za cene) u `index.html`

### Tekst
- Promenite `translations` objekat u `index.html`
- Info tekst o objektu

### Slike kategorija
- Dodajte/zamenite slike u `images/` folderu

---

## 📊 Korišćene Tehnologije

- **Frontend:** React 18 (bez build-a)
- **Backend:** Firebase Firestore
- **Auth:** Firebase Authentication
- **Hosting:** Vercel
- **Responsive:** Mobile-first dizajn

---

## 🐛 Troubleshooting

**Problem:** Slike se ne učitavaju
- Proverite putanje u `images/` folderu
- Proverite da su slike uploadovane na server

**Problem:** Admin login ne radi
- Proverite da ste dodali korisnika u Firebase Authentication
- Proverite email i password

**Problem:** Izmene se ne čuvaju
- Proverite Firebase config
- Proverite Firestore pravila
- Otvorite Console (F12) za greške

**Problem:** Meni je spor
- Optimizujte slike (kompresija)
- Koristite WebP format
- Enable caching u Vercel

---

## 📞 Podrška

Za dodatna pitanja ili pomoć:
- Email: support@aromaticcaffe.rs
- Website: www.aromaticcaffe.rs

---

## 📝 Demo Podaci

**Admin Login:**
- Email: admin@aromaticcaffe.rs
- Password: admin123

**WiFi:**
- Network: aromaticcaffe
- Password: aromaticcaffe2025

---

## ✅ Checklist Pre Launcha

- [ ] Firebase projekat kreiran
- [ ] Firestore i Authentication omogućeni
- [ ] Firebase config ubačen u kod
- [ ] Admin korisnik dodat u Firebase
- [ ] Deploy na Vercel uspešan
- [ ] Domen povezan i radi
- [ ] QR kodovi generisani i odštampani
- [ ] NFC tagovi programirani (opciono)
- [ ] Testiranje na mobilnim uređajima
- [ ] Sve slike se učitavaju pravilno
- [ ] Admin panel testiran
- [ ] Sigurnost pravila postavljena

---

Made with ☕ for Aromatic Caffe
