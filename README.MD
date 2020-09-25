# Progit Summer internship 2021 💻

## 1. Problembeskrivelse

AtB har utviklet et nytt API som leverer data om busstider per busstopp som skal legge til rette for nye sanntidstavler rundt omkring i Trondheim. Du har fått i oppdrag fra AtB å levere disse sanntidstavlene i form av en applikasjon som benytter seg av dette API'et og deretter skriver ut passeringstidene i et informativt format.

## 2. AtB SanntidsAPI™️

API'et består av to endepunkter.

### Busstopp - GET https://us-central1-progit-playground.cloudfunctions.net/stops

Dette endepunktet returnerer en liste med busstopp bestående felter for bussstopp-id, navn, beskrivelse, informasjon om rullestolvennlighet samt geografiske koordinater.

Her er et eksempel på et busstopp-objekt:

```
[
  ...
  {
    id: "ST:1",
    name: "Gløshaugen",
    description: null,
    wheelchairBoarding: "noInformation",
    coordinates: {
      latitude: 10.02424,
      longitude: 5.5343245,
    },
  },
];

```

### Passeringstider - GET https://us-central1-progit-playground.cloudfunctions.net/passingTimes

Dette endepunktet returnerer en liste over passeringstider for busstoppene i Trondheim bestående av passeringstid-id, tid for passering i ISO-format, bussstopp-id som tiden gjelder for og informasjon om bussen.

```
 {
        id: "PT:1",
        passingTime: "2020-09-25T17:35:55+00:00"
        stopId: "ST:1",
        busInfo: {
            displayName: "Dragvoll",
            publicCode: "L3"
        }
    }
```

Løsningen din skal gjøre et GET-kall til API-endepunktene, lese listene, fjerne unødvendig data og deretter sette sammen dataen på fornuftig måte slik at man enkelt kan printe en representasjon.