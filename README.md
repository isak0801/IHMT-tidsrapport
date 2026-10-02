# IHMT Tidrapport – så kommer du igång

Appen består av två gratis delar:

- **GitHub Pages** visar själva sidan/appen (gratis).
- **Firebase** (Google) sköter inloggningen och sparar alla pass (gratisnivån "Spark" räcker gott).

Det tar ungefär 20 minuter första gången.

---

## Steg 1 – Skapa ett Firebase-projekt

1. Gå till https://console.firebase.google.com och logga in med ditt Google-konto.
2. Klicka på **Skapa ett projekt** (Create a project) och döp det till t.ex. `ihmt-tidrapport`.
   Google Analytics behövs inte, så du kan stänga av det.

## Steg 2 – Koppla en webbapp och fyll i config.js

1. I projektet klickar du på ikonen **</>** (Webb) under "Kom igång genom att lägga till Firebase i din app".
2. Döp appen till `Tidrapport` och klicka på **Registrera app**. Hosting behövs inte.
3. Du får en kodbit med `const firebaseConfig = { apiKey: ..., ... }`.
   Kopiera värdena till filen **config.js** och ersätt alla `KLISTRA-IN`.
4. Kontrollera att `OWNER_EMAIL` i config.js är den e-post du själv loggar in med.

> Värdena i firebaseConfig får synas öppet, det är normalt. Det som skyddar datan är reglerna i steg 4.

## Steg 3 – Slå på inloggning och skapa konton

1. Gå till **Build → Authentication → Kom igång**.
2. Under **Sign-in method** väljer du **Email/Password**, slår på det och sparar.
3. Under **Settings → User actions**: **bocka ur "Enable create (sign-up)"**.
   Då kan ingen skapa ett eget konto, utan bara du lägger till personal.
4. Under **Users → Add user** skapar du ett konto åt dig själv (samma e-post som `OWNER_EMAIL`)
   och ett åt varje anställd, med e-post och ett startlösenord.
   Den anställda kan själv byta lösenord via "Glömt lösenordet?" på inloggningssidan.

Ska någon sluta? Gå till Users, klicka på de tre prickarna och välj **Disable account**.

## Steg 4 – Skapa databasen och säkerhetsreglerna

1. Gå till **Build → Firestore Database → Create database**.
2. Välj en plats i Europa (t.ex. `eur3` eller `europe-north1`) och **Start in production mode**.
3. Öppna fliken **Rules**, radera allt som står där och klistra in hela innehållet i filen
   **firestore.rules**. Kontrollera att e-posten i regeln är din. Klicka på **Publish**.

Reglerna gör att:
- varje anställd bara kan läsa och ändra sina egna pass,
- bara du (ägaren) ser alla pass, priser, löner och fakturan.

## Steg 5 – Lägg upp sidan gratis på GitHub Pages

1. Skapa ett gratis konto på https://github.com om du inte har ett.
2. Klicka på **+ → New repository**. Döp det till `tidrapport`, välj **Public** och klicka på **Create repository**.
3. Klicka på **uploading an existing file** och dra in alla filer i den här mappen
   (index.html, config.js, sw.js, manifest.webmanifest, ikonerna). firestore.rules och README.md kan också följa med.
   Klicka på **Commit changes**.
4. Gå till **Settings → Pages**. Under "Build and deployment" väljer du **Deploy from a branch**,
   branch **main** och mapp **/ (root)**. Klicka på **Save**.
5. Efter någon minut finns sidan på `https://DITT-ANVÄNDARNAMN.github.io/tidrapport/`.

## Steg 6 – Tillåt GitHub-adressen i Firebase

1. Tillbaka i Firebase: **Authentication → Settings → Authorized domains → Add domain**.
2. Lägg till `DITT-ANVÄNDARNAMN.github.io` (utan https och utan /tidrapport).

Nu kan alla logga in.

## Steg 7 – Installera som app på telefonen

- **iPhone (Safari):** öppna adressen, tryck på **Dela**-knappen och välj **Lägg till på hemskärmen**.
- **Android (Chrome):** öppna adressen, tryck på menyn **⋮** och välj **Installera app** (eller "Lägg till på startskärmen").

Appen öppnas då i helskärm med egen ikon, precis som en vanlig app.

---

## Bra att veta

- **Dålig täckning:** startar eller avslutar någon ett pass utan täckning sparas det i telefonen
  och skickas upp automatiskt när täckningen kommer tillbaka.
- **Uppdatera appen:** ladda upp den nya index.html till GitHub igen (samma sätt som i steg 5).
- **Notiser:** du ser nya avslutade pass under "Notiser" när du öppnar appen, och direkt om appen är öppen.
  Riktiga push-notiser till telefonen kräver Firebase betalnivå (Blaze), så det är inte med i gratisversionen.
- **Byta ägar-e-post:** ändra både `OWNER_EMAIL` i config.js och e-posten i Firestore-reglerna.
