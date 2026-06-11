## Methodology (In Dutch)

### Databronnen & Benodigdheden
We hebben ervoor gekozen om een simulatie in Python te maken van het woon-werkverkeer in Friesland. Hiervoor hebben we de volgende onderdelen gebruikt:
Python versie 3.14.3 met benodigde libraries (oa. OSM, Geopandas, SimPy, Folium…)
GTFS-nl Data van het Openbaar Vervoer
CBS Gebiedsindelingen (2024)
CBS Dataset Werknemersbanen en Reisafstand; Woon- en Werkregio
CBS Dataset Kerncijfers Wijken en Buurten

### Globale Aanpak
Met de CBS Gebiedsindelingen worden de Friese regio’s geïmporteerd in Python Vervolgens bestaat het netwerk uit twee delen:
De pendelaars.
De pendelaars zijn de virtuele reizigers in het netwerk. Deze worden ingespawned op basis van de CBS dataset over woon- en werkregio, dat cijfers bevat over aantal pendelaar binnen en tussen gemeenten. Ook hun bestemming wordt op basis van deze dataset bepaald. Om de spawn locaties iets nauwkeuriger en evenredig te maken, wordt de CBS dataset Kerncijfers Wijken en Buurten gebruikt.
Het netwerk
Het netwerk in het model bestaat uit het wegennet, ingeladen via de OpenStreetMap (OSM) library en de spoor- en buslijnen met General Transit Feed Specification (GTFS) data. 

### Gravity Model
De volgende stap van het model is de toepassing van het gravity model, zoals beschreven in hoofdstuk 3.1.3. Met het gravity model wordt de interactie tussen gemeenten en de aantrekkingskracht van gemeenten berekend. Naarmate de afstand groter wordt, neemt het aantal gesimuleerde pendelaars af volgens een vervalfunctie, bepaald door de beta parameter.

### Logit Modal Split
Na het gravity model wordt de modal split berekend, ofwel het deel van de pendelaars dat de auto pakt, het OV gebruikt, fietst of loopt. Hierin wordt rekening gehouden met de dimensies van afstand, tijd en kosten. Op basis van deze gegevens wordt een utility (nut) score gegeven. Ook dit wordt bepaald door parameters instelbaar boven in de notebook.

### De Simulatie
De data is nu gereed voor de daadwerkelijke simulatie. De simulatie bestaat uit 24 uur op een willekeurige werkdag. 
We beginnen met het OV. Op basis van de dienstregeling, de routes (edges), stations (nodes) wordt het OV gesimuleerd in de SimPy library. Virtuele passagiers komen aan op het station, wachten op vertrek volgens de GTFS-dienstregeling en rijden langs de haltes tot ze aankomen op de overstaphalte of de eindbestemming. In het geval dat een trein of bus vol zit wordt de wachttijd vergroot. Elke in- en uitstap wordt gelogd en gebruikt voor de resultaten.
Voor het eerder berekende gedeelte virtuele reizigers dat de auto neemt, worden de routes bepaald door middel van Dijkstra’s algoritme om de kortste route (in tijd, via maximumsnelheid) te berekenen. Alle auto’s worden aan de ‘edge_counts’ toegewezen, een bepaalde weg in het netwerk.

### Simulatie-Resultaten en -Validatie
Na de simulatie, worden de resultaten verzameld door middel van een Folium map (Friesland_Simulatie_Map.html) waarop de in- en uitstappers per halte/station, de 100 drukste pendelstromen tussen gemeenten en de autowegen worden getekend. Dit html-bestand kan worden geopend en bekeken in de browser en werkt als een interactieve kaart, waarop de resultaten visueel gecontroleerd kunnen worden.
Naast de map maakt het script 5 verschillende csv datasets aan die samen het numerieke resultaat vormen van beide simulaties.
Ook wordt in deze stap een validatie gedaan van de resultaten. Voor het OV hebben we helaas geen data om onze simulatie te valideren, maar voor de auto wel. Hiervoor wordt de dataset ‘avondspits.csv’ gebruikt, afkomstig van het Nationaal Dataportaal Wegverkeer (NDW), gefilterd en opgeschoond. Deze dataset bevat data van meetpalen van over de gehele provincie. Deze meetpalen houden het aantal auto’s bij dat het passeert. Deze cijfers vergelijken we met de cijfers uit de simulatie, door voor elke meetpaal de dichtstbijzijnde edge op te zoeken en de volumes vergeleken.
Uit de correlatie test en bijbehorende score (0.17) is gebleken dat de simulatie niet foutloos is en de verschillen tussen ‘avondspits.csv’ en de resultaten van het model te groot zijn. Mogelijke redenen voor de lage correlatiescore zijn:
De simulatie berekent slechts woon-werkverkeer op basis van de CBS dataset. De meetpalen in ‘avondspits.csv’ meten al het verkeer op de weg.
Het Dijkstra algoritme is niet geavanceerd genoeg; Het kan niet rekening houden met het scenario dat een automobilist niet altijd de wiskundig kortste route neemt.
Sommige meetpalen meten slechts het verkeer een kant op, terwijl de simulatie cijfers altijd twee kanten op zijn

### Inzichten en Analyse
Tot slot hebben we een kleine stap gemaakt in het afleiden van inzichten uit de data. Om knelpunten van specifiek het autonetwerk op te kunnen sporen, printen we de wegen met de hoogste volumes aan auto’s. Daarnaast berekenen we voor zowel de auto als het OV de top 10 traagste pendelverbindingen in minuten per kilometer, hiervoor geldt: Des te meer minuten per kilometer op een traject, des te lager de efficiëntie en de snelheid van de verbinding. 
