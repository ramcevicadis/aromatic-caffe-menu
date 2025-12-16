# ❓ Često Postavljana Pitanja (FAQ)

## 📱 Korisničke Funkcije

### Kako gosti pristupaju meniju?
Gosti mogu pristupiti meniju na 3 načina:
1. **QR kodom** - Skeniranje QR koda kamerom telefona
2. **NFC tagom** - Približavanje telefona NFC tagu (ako ga imate)
3. **Direktnim linkom** - Kucanjem URL-a: menu.aromaticcaffe.rs

### Da li gosti moraju instalirati aplikaciju?
**Ne!** Meni radi direktno u browseru, bez instalacije.

### Koje telefone podržava?
- ✅ iPhone (iOS 12+)
- ✅ Android (verzija 6+)
- ✅ Tablet uređaji
- ✅ Desktop računare (ali je optimizovan za mobilne)

### Može li se koristiti bez interneta?
**Ne**, potrebna je internet konekcija. Ali:
- Meni se brzo učitava (optimizovan je)
- Radi na WiFi mreži kafića
- Minimalna potrošnja mobilnih podataka

---

## 🔐 Admin Panel

### Ko može pristupiti admin panelu?
Samo korisnici sa admin nalogom u Firebase Authentication.
Inicijalno: admin@aromaticcaffe.rs

### Kako dodati novog admin korisnika?
1. Firebase Console → Authentication → Users
2. Kliknite "Add user"
3. Unesite email i password
4. Novi korisnik može pristupiti admin panelu

### Kako resetovati lozinku?
1. Firebase Console → Authentication → Users
2. Nađite korisnika
3. Kliknite tri tačke → "Reset password"
4. Pratite email instrukcije

### Da li se izmene odmah prikazuju gostima?
**Da!** Sve izmene u admin panelu su trenutne.
- Dodavanje artikla → odmah vidljivo
- Izmena cene → odmah ažurirana
- Brisanje → odmah uklonjeno

### Šta ako slučajno obrišem artikal?
Nema "undo" funkcije, ali možete:
1. Ručno dodati artikal ponovo
2. Koristiti backup iz firestore-data.json
3. Napraviti Firebase backup unapred (preporučeno)

---

## 🛠️ Tehnička Pitanja

### Koja tehnologija je korišćena?
- **Frontend:** React 18 (bez build sistema)
- **Backend:** Firebase Firestore (NoSQL database)
- **Hosting:** Vercel (CDN)
- **Auth:** Firebase Authentication

### Koliko košta održavanje?
**Besplatno za male kafićе!**
- Firebase: 50,000 čitanja/dan besplatno (dovoljno)
- Vercel: 100GB bandwidth besplatno
- Verovatno nikad nećete preći free tier

### Šta ako prekoračim besplatne limite?
- Firebase: ~$0.06 za 100,000 dodatnih čitanja
- Vercel: ~$20/mesec za pro plan (retko potrebno)
- Monitoring dostupan u dashboard-u

### Kako napraviti backup?
**Automatski backup:**
1. Firebase Console → Firestore Database
2. Kliknite tri tačke → "Export data"
3. Izaberite destinaciju (Google Cloud Storage)

**Ručni backup:**
1. Kopirajte trenutno stanje iz Firestore
2. Sačuvajte JSON fajl lokalno

### Kako update-ovati dizajn?
1. Promenite CSS u `index.html`
2. Commit i push na GitHub
3. Vercel automatski deploy-uje novu verziju

---

## 🎨 Prilagođavanje

### Kako promeniti boje?
U `index.html` fajlu:
- Crvena za cene: `#dc143c`
- Pozadina kartica: `#f5f5f5`
- Tekst: `#1a1a1a`

Find & Replace sa vašom bojom.

### Kako dodati novi jezik?
1. U `index.html`, nađite `translations` objekat
2. Dodajte novi jezik:
```javascript
translations: {
  sr: { ... },
  en: { ... },
  de: {  // Nemački
    menu: 'SPEISEKARTE',
    // ...
  }
}
```
3. Dodajte button za novi jezik
4. Update kategorije i artikle

### Kako promeniti logo?
1. Zamenite `images/Logo_Aromatic.jpg` sa vašim logoom
2. Ime fajla može biti različito, ali ažurirajte putanju u HTML-u
3. Preporučena veličina: 300x300px, PNG sa transparentnom pozadinom

---

## 🍽️ Upravljanje Menijem

### Kako organizovati artikle?
Organizujte po kategorijama:
- Topli napici
- Sokovi
- Hrana
- Deserti
- itd.

### Kako privremeno sakriti artikal (nije dostupan)?
**Trenutno:** Morate obrisati artikal
**Buduća funkcija:** Dodaćemo "available" toggle

**Workaround:** 
- Promenite cenu u 0 ili "NA"
- Ili dodajte "(trenutno nedostupno)" u naziv

### Mogu li dodati slike artikala?
**Trenutno:** Ne, ali može se implementirati
**Workaround:** Koristite slike kategorija

### Kako dodati opise artikala?
Trenutno sistem ne podržava opise, ali može se dodati:
1. U Firestore, dodajte `description_sr` i `description_en` polja
2. Update UI da prikazuje opise
3. Ili kontaktirajte za help sa implementacijom

---

## 🔧 Problemi i Rešenja

### Meni se sporo učitava
**Moguća rešenja:**
- Optimizujte slike (kompresija)
- Koristite WebP format umesto PNG
- Check internet konekciju
- Clear browser cache

### Slike se ne prikazuju
**Provere:**
- Da li su slike u `images/` folderu?
- Da li su putanje tačne u kodu?
- Da li su slike uploadovane na Vercel?
- Da li su imena fajlova identična (case-sensitive)?

### Admin panel ne radi
**Provere:**
- Da li ste odkomentarisali Firebase init kod?
- Da li je Firebase config tačan?
- Da li postoji user u Firebase Authentication?
- Console errors (F12 u browseru)?

### Izmene se ne čuvaju
**Provere:**
- Da li su Firestore pravila postavljena?
- Da li je Firebase inicijalizovan?
- Network tab u DevTools - da li ima requesta?

### QR kod ne radi
**Moguće greške:**
- URL u QR kodu je pogrešan
- QR kod je previše mal ili oštećen
- Kamera telefona ne podržava skeniranje
- Potrebna QR scanner app (stariji telefoni)

### NFC ne radi
**Provere:**
- Da li telefon podržava NFC? (Settings → NFC)
- Da li je NFC uključen?
- Da li je tag pravilno programiran?
- Neki telefoni zahtevaju app za NFC

---

## 💡 Best Practices

### Održavanje menija
- ✅ Ažurirajte cene redovno
- ✅ Uklonite nedostupne artikle
- ✅ Dodajte sezonske ponude
- ✅ Proverite gramatiku (SR i EN)
- ✅ Testirajte novi sadržaj pre objave

### Korisničko iskustvo
- ✅ QR kodovi vidljivi na svakom stolu
- ✅ WiFi lozinka dostupna u meniju
- ✅ Instrukcije za korišćenje (opciono)
- ✅ Brzo učitavanje (optimizovane slike)

### Sigurnost
- ✅ Jaka lozinka za admin
- ✅ Ne delite admin pristup
- ✅ Redovno pravite backup
- ✅ Firestore pravila postavljena

---

## 📊 Analytics i Praćenje

### Kako videti statistiku poseta?
**Opcija 1:** Vercel Analytics (besplatno)
1. Vercel Dashboard → projekt → Analytics
2. Vidite broj poseta, pageviews, itd.

**Opcija 2:** Google Analytics
1. Dodajte GA tracking kod u `index.html`
2. Pratite detaljnu analitiku

### Koje metrike su važne?
- **Page views** - koliko puta je meni otvoren
- **Unique visitors** - broj različitih gostiju
- **Bounce rate** - da li ljudi ostaju na meniju
- **Most viewed categories** - najpopularnije kategorije

---

## 🚀 Buduće Funkcionalnosti

Planiramo dodati:
- [ ] Slike artikala
- [ ] Opisi artikala
- [ ] "Available/Not available" toggle
- [ ] Favoriti artikala za goste
- [ ] Push notifikacije za promocije
- [ ] Multi-valuta (RSD, EUR)
- [ ] Alergeni marker na artiklima
- [ ] Ocenjivanje artikala
- [ ] Integracija sa POS sistemom

---

## 📞 Kontakt i Podrška

**Za dodatna pitanja:**
- Email: support@aromaticcaffe.rs
- Website: www.aromaticcaffe.rs

**Za tehničku pomoć:**
- GitHub Issues (ako je projekat na GitHub)
- Email sa screenshot-om problema

---

**Poslednja izmena:** Decembar 2025
