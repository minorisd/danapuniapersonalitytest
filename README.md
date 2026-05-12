# Career Test Application

Sander, Ilona en Sofie werken voor het project van Yayasan Dana Punia aan een loopbaantest voor studenten. Het doel van deze test is om studenten beter inzicht te geven in hun interesses, sterke punten en mogelijke toekomst. Veel studenten weten namelijk nog niet goed welke richting of studie het beste bij hen past.

In de persoonlijkheidstest worden verschillende vragen gesteld die gericht zijn op interesses en eigenschappen van de student. Aan het einde van de test komt er een profiel uit een van de volgende domeinen:

- Achiever
- Thinker
- Socialforce
- Creative
- Entrepreneur

Op deze manier kunnen studenten ontdekken welke vakken en richtingen goed bij hen passen, maar ook welke misschien minder geschikt zijn. Een voorbeeld hiervan is hospitality: hiervoor is een goede beheersing van de Engelse taal belangrijk, terwijl veel studenten op dit moment weinig motivatie hebben om Engels te leren. Door middel van de loopbaantest kunnen studenten beter begrijpen welke opleiding en welk lespakket het beste aansluiten bij hun talenten en interesses.

Het probleem waar Sander, Ilona en Sofie momenteel tegenaan lopen, is dat zij de test online willen aanbieden, maar nog geen geschikte tool hebben gevonden waarmee dit mogelijk is. Hier kan ik aan bijdragen door zelf een applicatie te programmeren.

Het idee achter de applicatie is dat ieder domein een eigen verzameling vragen heeft. Studenten kunnen per vraag antwoorden met:

- Strongly disagree
- Disagree
- Neutral
- Agree
- Strongly agree

Alle vragen worden willekeurig door elkaar weergegeven en de gebruiker gaat stap voor stap door de test heen. Op basis van de antwoorden wordt uiteindelijk bepaald binnen welk domein de student het beste past. Dit gebeurt door te kijken op welk domein de meeste positieve antwoorden zijn gegeven.

Voor dit project ga ik een SvelteKit-applicatie ontwikkelen. De applicatie zal gebruikmaken van een static configuratie, zodat deze eenvoudig gehost kan worden op GitHub Pages. Hierdoor hoeft Yayasan Dana Punia geen kosten te maken voor hosting. Daarnaast ga ik een GitHub Organization aanmaken, zodat het project in de toekomst gemakkelijk kan worden overgedragen aan een nieuwe developer binnen het minor ISD-project.

---

# Requirements

- De applicatie moet online beschikbaar zijn zodat studenten de test gemakkelijk kunnen openen via een website.

- Studenten moeten stap voor stap door verschillende vragen heen kunnen gaan.

- Bij iedere vraag moeten studenten kunnen kiezen uit vijf antwoordmogelijkheden:
    - Strongly disagree
    - Disagree
    - Neutral
    - Agree
    - Strongly agree

- De vragen moeten standaard in het Engels worden weergegeven.

- Bij iedere vraag moet een optie, zoals een vraagteken-icoon, beschikbaar zijn waarmee de student de vraag ook in het Indonesisch kan bekijken.

- Aan het einde van de test moet één hoofddomein naar voren komen dat het profiel van de student weergeeft.

- De applicatie moet geschikt zijn voor mobiel gebruik zodat studenten de test eenvoudig op hun telefoon kunnen maken.

- Het eindresultaat moet een overzicht tonen van de scores per domein, zodat studenten ook kunnen zien welke domeinen minder goed bij hen passen.

- De vragen van de verschillende domeinen moeten willekeurig door elkaar worden weergegeven zodat iedere test uniek aanvoelt.

- Het systeem moet de antwoorden automatisch verwerken en op basis daarvan een profiel berekenen.