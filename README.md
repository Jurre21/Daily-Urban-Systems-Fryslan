# RUG x DataFryslân - Field Project Data Science & Society 2026: Mapping and Modelling Daily Urban Systems in Fryslân

This Github Repository contains scripts, datasources and other aspects related to the DUS Field Project

## Field Project Description (in Dutch)

Fryslân is sterk verbonden met omliggende regio’s, zowel economisch,
sociaal en cultureel. Veel inwoners
verplaatsen zich dagelijks over gemeente-
en regiogrenzen voor werk, studie of
voorzieningen. Dit netwerk van dagelijkse
stromen noemen we Daily Urban Systems
(DUS). Om beleid beter te onderbouwen
en samenwerking tussen gemeenten te
versterken, willen de leden van de
coöperatie DataFryslân deze stromen
analyseren en visualiseren.
Om regionale samenwerking en beleid
beter te ondersteunen, wil DataFryslân
meer inzicht krijgen in deze dagelijkse
verplaatsingspatronen: waar mensen
vandaan komen, waar ze naartoe gaan, en
welke plaatsen daarin een centrale rol
spelen. Studenten brengen deze patronen
in kaart en maken ze zichtbaar op een
manier die bruikbaar is voor
beleidsmakers, onderzoekers en
bestuurders.
Naast het in kaart brengen van bestaande
patronen, verkennen studenten ook
theoretische scenario’s. Hierbij kunnen ze
DUS modelleren op basis van
actieradiussen per vervoermiddel:
bijvoorbeeld loopafstanden,
fietsafstanden, afstanden met de
elektrische fiets of auto en afstanden die
met het openbaar vervoer overbrugbaar
zijn. Dit maakt het mogelijk om
verschillende toekomstscenario’s en
beleidsopties te vergelijken, bijvoorbeeld
bij woningbouw, mobiliteitsplanning of
voorzieningenbeleid.

## Getting Started

### Dependencies

- Recommended Python version: 3.14.3
    Libraries: See 'requirements.txt'
- CBSodata API
- GTFS-nl Data
- CBS Gebiedsindelingen Geopackages

### Executing program

Simulatie.ipynb

### Tutorial

1. Open de repository in your workspace
2. Download GTFS-nl Data (gtfs-nl.zip) from the following link:
   https://gtfs.ovapi.nl/nl/
   Download CBS Gebiedsindelingen data from the following link:
   https://www.cbs.nl/nl-nl/dossier/nederland-regionaal/geografische-data/cbs-gebiedsindelingen
   Important: Extract both .zip files!
4. A. Create a virtual environment 
   B. Navigate to your newly created virtual environment through the terminal
   C. Run the following command: pip install requirements.txt
5. Open 'Simulatie.ipynb' and set the correct paths to your .gpkg and GTFS folders
6. Run the Notebook (runtime ~15-30min)

## Stakeholders

### Students:
Jelmer de Boer (S5986567)
j.de.boer.76@student.rug.nl

Freark de Lange (S5925304)
f.de.lange.2@student.rug.nl

Felicia de Roos (S6110975)
f.de.roos.2@student.rug.nl

Julia Tomatala (S6126642)
j.b.m.tomatala@student.rug.nl

Jurre de Vries (S6075819)
j.r.p.de.vries@student.rug.nl

### University Contact / Supervisor
Dr. Loes Bouman
l.bouman@rug.nl

### DataFryslân
Monique van der Meer, Programme Manager
monique.van.der.meer@datafryslan.nl

Nynke Slagter, Senior Data Scientist
nynke.slagter@datafryslan.nl

Anita Nguyen, Data Scientist
anita.nguyen@datafryslan.nl

Jeska Everhard, Intern
jeska.everhard@datafryslan.nl
