# Kollektivet: slik legger du appen ut på nett

Mappen inneholder alt som trengs:

| Fil | Hva den gjør |
|---|---|
| `index.html` | Nedlastingssiden folk kommer til, med «Last ned appen» og veiledning for iPhone og Android |
| `app.html` | Selve appen. Firebase-oppsettet limes inn her |
| `manifest.webmanifest`, `sw.js` | Gjør at mobilen kan installere siden som en app |
| `apple-touch-icon.png`, `icon-192.png`, `icon-512.png` | Appikonet |
| `firestore.rules` | Sikkerhetsreglene for databasen |

Det tar rundt 15 minutter, og alt er gratis.

## Del 1: Lag databasen (Firebase)

1. Gå til https://console.firebase.google.com og logg inn med en Google-konto.
2. Trykk **Opprett et prosjekt** (Create a project). Kall det for eksempel `kollektivet`. Google Analytics kan du slå av.
3. Velg **Build → Authentication** i menyen til venstre. Trykk **Get started**, velg **Anonymous** og slå det på.
4. Velg **Build → Firestore Database** og trykk **Create database**. Velg region `eur3 (europe-west)` og start i **production mode**.
5. Åpne fanen **Rules** i Firestore. Slett alt som står der, lim inn innholdet fra `firestore.rules` og trykk **Publish**.
6. Gå til **Project settings** (tannhjulet øverst til venstre). Under **Your apps** trykker du på web-ikonet `</>`. Gi appen et navn og trykk **Register app**. Du trenger ikke Firebase Hosting.
7. Du får nå opp et `firebaseConfig`-objekt med `apiKey`, `projectId` og så videre. Åpne `app.html` i en teksteditor, finn blokken `LIM INN FIREBASE-KONFIGURASJONEN DIN HER` og fyll inn verdiene. Lagre filen.

> `apiKey` i Firebase er ikke hemmelig. Den skal ligge i nettsiden. Det er sikkerhetsreglene og den hemmelige husholdningskoden som beskytter dataene.

## Del 2: Legg appen på nett (Netlify)

1. Gå til https://app.netlify.com/drop og lag en gratis konto.
2. Dra hele mappen `kollektivet` inn i ruten på siden.
3. Etter noen sekunder får du en adresse, for eksempel `https://glad-pingvin-123.netlify.app`. Under **Site configuration → Change site name** kan du endre den til noe som `vaarkollektiv.netlify.app`.
4. **Viktig:** Gå til Firebase igjen, velg **Authentication → Settings → Authorized domains** og legg til Netlify-adressen din.

Når du endrer appen senere, drar du mappen inn på nytt under **Deploys** i Netlify.

## Del 3: Del nedlastingssiden

Adressen din (for eksempel `vaarkollektiv.netlify.app`) er nedlastingssiden. Den kan du dele fritt i gruppechatter, på Facebook eller i studentgrupper.

- På **Android** trykker man «Last ned appen» og bekrefter. Appen legges blant de andre appene.
- På **iPhone** viser siden hvordan man legger appen til på Hjem-skjermen via Del-knappen i Safari.
- På PC ber siden folk åpne den på mobilen, eller bruke appen rett i nettleseren.

Alle som åpner appen får sitt **eget** kollektiv. Inne i appen er det to knapper for å dele:
- **Inviter de du bor med** sender en lenke med hemmelig kode, til akkurat dette kollektivet.
- **Tips et annet kollektiv** sender nedlastingssiden, slik at andre lager sitt eget.

**Tips for iPhone:** En app på Hjem-skjermen har sin egen lagring, atskilt fra Safari. Har du installert appen før du fikk invitasjonslenken, kopierer du lenken og limer den inn i appen under «Har du fått en invitasjon?».

## Godt å vite

- Alle som har invitasjonslenken (den med koden etter `#`) kan se og endre dataene i det kollektivet. Del den bare med de du bor med. Vanlig adresse uten kode er trygg å dele med hvem som helst.
- Firebase sitt gratisnivå (Spark) tåler langt mer enn et kollektiv trenger.
- Hvis noen mister appen, kan de bare åpne invitasjonslenken igjen. Alle dataene ligger i databasen.
- Uten Firebase-konfigurasjon virker appen også, men da lagres alt bare på den ene enheten. Det er fint for å teste.
