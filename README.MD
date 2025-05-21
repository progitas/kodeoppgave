
# Progit Consulting kodeoppgave 💻

## 1. Problembeskrivelse

AtB har utviklet et nytt API som leverer data om busstider per busstopp som skal legge til rette for nye sanntidstavler rundt omkring i Trondheim. Du har fått i oppdrag fra AtB å levere disse sanntidstavlene i form av en applikasjon som benytter seg av dette API-et og deretter skriver ut passeringstidene i et informativt format. 

Kravene fra AtB er at tavlen skal vise:
- Hvilket busstopp du er på
- Hvilke busser som kommer, representert ved rutenavn og rutenummer (`displayName` og `publicCode`)
- Tiden bussen passerer stoppet i et leselig format

## 2. AtB SanntidsAPI™️

API-et består av to endepunkter.

### 🚌 Busstopp – [GET /stops](https://us-central1-progit-playground.cloudfunctions.net/stops)

Dette endepunktet returnerer en liste med busstopp bestående av felter for bussstopp-id, navn, beskrivelse, informasjon om rullestolvennlighet samt geografiske koordinater.

Eksempel på et busstopp-objekt:

```json
[
  {
    "id": "ST:1",
    "name": "Gløshaugen",
    "description": null,
    "wheelchairBoarding": "noInformation",
    "coordinates": {
      "latitude": 10.02424,
      "longitude": 5.5343245
    }
  }
]
```

### ⏰ Passeringstider – [GET /passingTimes](https://us-central1-progit-playground.cloudfunctions.net/passingTimes)

Dette endepunktet returnerer en liste over passeringstider for busstoppene i Trondheim. Hver passering inneholder passeringstid-id, tid for passering i ISO-format, bussstopp-id som tiden gjelder for, og informasjon om bussen.

Eksempel på en passering:

```json
{
  "id": "PT:1",
  "passingTime": "2020-09-25T17:35:55+00:00",
  "stopId": "ST:1",
  "busInfo": {
    "displayName": "Dragvoll",
    "publicCode": "L3"
  }
}
```

## 3. Løsningen din skal

- Gjøre HTTP-kall til API-ene og hente listene med data
- Sortere listene
- Fjerne unødvendig data
- Sette sammen dataen på en fornuftig måte slik at man enkelt kan printe en representasjon
- Denne representasjonen skal være en **rutetabell per busstopp**, som beskrevet i [1. Problembeskrivelse](#1-problembeskrivelse)

## 4. Tilleggsinformasjon og begrensninger

Du står fritt til å velge programmeringsspråk og eventuelle biblioteker. For nettverkskall anbefaler vi:

- **JavaScript:** `fetch` (i nettleseren), `axios` (for Node.js)
- **Python:** `requests`

Det er ikke et krav at hele oppgaven må være løst. Vi er hovedsakelig opptatt av hvordan du tilnærmer deg problemet og hvordan du velger å strukturere koden din. Vi oppfordrer deg til å sende inn løsningen selv om den ikke er helt ferdig innen tiden!

## 5. Ekstraoppgave: Busstopp-oppsummering 🧠

Når tavlene er satt opp, har AtB etterspurt et ekstra datagrunnlag som skal brukes internt for analyseformål. Du skal derfor lage en funksjon som leverer ut et **oppsummeringsobjekt** basert på alle passeringstidene.

Denne funksjonen skal returnere et objekt hvor hvert `stopId` er en nøkkel, og verdien er et objekt som inneholder:

- `stopName`: Navnet på busstoppet
- `totalDepartures`: Totalt antall avganger fra dette stoppet (antall passeringstider)
- `uniqueLines`: En liste med unike linjenummer (`publicCode`) som passerer dette stoppet

### Eksempel på ønsket output:

```json
{
  "ST:1": {
    "stopName": "Gløshaugen",
    "totalDepartures": 4,
    "uniqueLines": ["L3", "L5"]
  },
  "ST:2": {
    "stopName": "NTNU Dragvoll",
    "totalDepartures": 2,
    "uniqueLines": ["L3"]
  }
}
```