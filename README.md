# GTIN-API for E-Commerce Integration README

## Introduction

Welcome to the documentation for the GTIN-13 API for E-Commerce Integration, a work-in-progress (WIP) project committed to facilitating seamless product listings on global e-commerce platforms like Bol.com and Amazon. As we journey towards becoming a certified GS1 Solution Provider, this project aims to generate GTIN-13 (formerly known as EAN-13) codes, the most commonly used GS1 product code, ensuring your products meet the global standard for identification and traceability.

### What is GTIN-13?

GTIN-13, the cornerstone of the GS1 system of standards, is a 13-digit number used to uniquely identify products at the item level in the retail sector. These identifiers are crucial for managing products in the supply chain, from the manufacturer to the consumer, ensuring compatibility and visibility across global markets and digital platforms.

## Utilizing the GTIN-13 API for E-Commerce Listings

This API serves as an invaluable tool for businesses aiming to streamline their online sales channels. By integrating with our GTIN-13 API, companies can automate the generation of global standard product identifiers, thereby simplifying the process of listing products on major e-commerce platforms such as Bol.com and Amazon.

### Technical Documentation: REST API Usage

Our RESTful API provides an intuitive interface for the asynchronous generation of GTIN-13 codes. Below, we detail the API's functionality, including request and response formats and guidelines for using the endpoints effectively.

### API Endpoints Overview

There are two primary endpoints in the API:

1. **GTIN-13 Generation Request Endpoint** - Initiates the GTIN-13 code generation process.
2. **Status & GTIN-13 Retrieval Endpoint** - Monitors the status of requests and retrieves generated GTIN-13 codes.

#### GTIN-13 Generation Request Endpoint

Submit your product details to this endpoint to generate GTIN-13 codes. The request supports batch operations:

```http
POST /api/gtin
```

```json
[
  {
    "accountNumber": "YourAccountNumber",
    "status": "active",
    "gpc": "Gastrointestinal Drugs - Other",
    "consumerUnit": "Yes",
    "packagingType": "Drum",
    "targetMarketCountry": "Global Market",
    "description": "Sample product",
    "language": "English",
    "brandName": "Brand sample",
    "subBrandName": "Sub brand name",
    "netContent": 100,
    "measurementUnit": "Pound (0.45359237 kg)",
    "imageUrl": "",
    "contractNumber": "YourContractNumber"
  }
]
```

Success responses (200 OK) include a `jobId` of the UUID format for precise tracking:

```json
{
  "jobId": "e0a953c3-ee58-4b05-9d1b-174509c4e4d7"
}
```

Invalid requests will return a 403.

#### Job Status & GTIN-13 Retrieval Endpoint

With the `jobId`, check the status and retrieve your GTIN-13 codes:

```http
GET /api/gtin/status/e0a953c3-ee58-4b05-9d1b-174509c4e4d7
```

The response includes the request status and the GTIN-13 details for each product:

```json
{
  "status": "processing",
  "results": [
    {
      "status": "done",
      "result": {
        "gtin": "1212323312345",
        "accountNumber": "YourAccountNumber",
        "description": "Sample product",
        "language": "English",
        "brandName": "Brand sample",
        // Additional fields as submitted
      }
    }
  ]
}
```

#### GTIN-13 Retrieval Endpoint

With the `gtin`, retrieve the details:

```http
GET /api/gtin/1212323312345
```

The response includes the request status and the GTIN-13 details for each product:

```json
{
    "gtin": "1212323312345",
    "accountNumber": "YourAccountNumber",
    "description": "Sample product",
    "language": "English",
    "brandName": "Brand sample",
    // Additional fields as submitted
}
```

### API options

#### Field Length Restrictions

Please note the following restrictions on field lengths when submitting your product information:

* `brandName` and `subBrandName`: Maximum of 70 characters
* `description`: Maximum of 300 characters
* `language`: Options shown below
* `targetMarketCountry`: Options shown below

#### Packaging Type Options

```plaintext
Ampul 
Bag-In-Box
Bakje
Beker/kuipje
Blik 
Blister­verpakking
Bus
Cartridge
Clamshell verpakking
Doos
Draad
Emmer
Fles
Hoes(je)
Huls
Kaart
Kan
Koker
Kooi
Krat 
Krimp­verpakking
Mand
Multi-pack
Net 
Niet verpakt
Pak 
Pak met punt
Pallet 
Palletkrat
Peel-pack
Pot 
Rek
Rol
Spoel
Spuitbus
Stazak 
Stretch-verpakking 
Tray
Tube
Tussenmodel bulk container, flexibel
Tussenmodel bulk container, inflexibel
Vat
Verpakkings­band
Verpakt, geen specificatie
Wikkel
Zak 
Zakje
```

#### GPC Options

Use valid values from the GPC list available at [GPC Browser](https://gpc-browser.gs1.org/) (select Dutch).

```plaintext
Aalbessen
Aambeelden (DHZ)
Aangedreven Tuingereedschap - Assortimenten
Aangedreven Tuingereedschap - Overig
Aangedreven Tuingereedschap Onderdelen/Accessoires
Aanhangwagen - Aansluitstekker/-stekkerdoos
Aanhangwagen/Accessoires van Aanhangwagen - Assortimenten
Aanhangwagen/Accessoires van Aanhangwagen - Overig
Aanhangwagens/caravans
Aansluitadapters/Convertors
Aansluitblokken/-strips
Aansluitkranen - Water en Gas
Aansluitslangen - Water, Gas, CV
Aansluitstukken/Koppelingen - Water, Gas, CV en Luchtkanalen
Aanstekers/Lucifers
Aanstekers/Lucifers - Accessoires
Aanwijsapparatuur / muizen
Aanwijzers (Elektrisch)
Aanwijzers (Niet-elektrisch)
Aardakerplanten (Lathyrus Tuberosus)
Aardappelen
Aardappelplanten (Solanum Tuberosum)
Aardbeiboomvruchten
Aardbeien
Aardbeienbomen (Muntingia calabura)
Aardbeienplanten (Fragaria x ananassa)
Aardkabels
Aardkastanjeplanten (Bunium Bulbocastanum)
Aardpeerplanten (Helianthus Tuberosus)
Aas/Kunstvliegen
Abacaplanten (Musa textilis)
Abrikozen
Abrikozenbomen (Prunus armeniaca)
Absintplanten (Artemisia Absinthium)
Absorberende stoffen (DHZ)
Acaciabomen (Acacia Spp.)
Acai-bessen
Acaipalmbomen (Euterpe oleracea)
Accessoires voor Actiefiguren
Accessoires voor Bloemen en Planten
Accessoires voor Computer/PC's/Spelcomputers/Games - Assortimenten
Accessoires voor Computerkasten/-Behuizing
Accessoires voor Elektronische Circuits
Accessoires voor Flitsers
Accessoires voor Gordijnrails
Accessoires voor Gordijnroedes/-stangen
Accessoires voor het Inbinden
Accessoires voor Houten Blaasinstrument (Niet-elektrisch)
Accessoires voor Kabelmerker
Accessoires voor Keuboard/Piano (Elektrisch)
Accessoires voor Kunstenaars
Accessoires voor Mobiele Telefoons/Smartphones
Accessoires voor Muziekinstrumenten - Assortimenten
Accessoires voor Opberg-/Bureauartikelen
Accessoires voor Papierkunst/Kaartvervaardiging
Accessoires voor Poppen/Handpoppen/Pluchen Speelgoed - Assortimenten
Accessoires voor Poppen/Handpoppen/Pluchen Speelgoed - Overig
Accessoires voor Satellietontvangst
Accessoires voor Slaginstrument (Niet-elektrisch)
Accessoires voor Sleepvergrendeling
Accessoires voor Snaarinstrument (Niet-elektrisch)
Accessoires voor Verzendmaterialen/Postverwerking
Accessoires/gereedschappen voor wielen/banden
Accessoires/Kits Vrachtwagens
Accukabels
Acerola/West-Indische kersbomen (Malpighia emarginata)
Achterlichtarmaturen
Achterruit Zonnekleppen
Achteruitkijkspiegel Reparatiekits
Achteruitrij Alarmen/Sensoren
Acne/Gordelroos Behandelingen
Actiefiguren (Elektrisch)
Actiefiguren (Niet-elektrisch)
Adapters (Elektrisch)
Additieven voor Mortel/Cement/Gips/Voegmortel
Adelaarsvarens (Pteridium Aquilinum)
Ademhalings-/Allergiemiddelen - Assortimenten
Ademhalings-/Allergiemiddelen - Overig
Ademhalingsbescherming - Aangedreven
Ademhalingsbescherming - Niet-aangedreven
Ademverfrissers/Mondspoelingen
Advertentiediensten
Adzukibonen
Adzukiboonplanten (Vigna Angularis)
Aeonium Arboreum - Levende Plant
Aeschynomene Americanaplanten (Aeschynomene Americana)
Afbeeldingen - Digitaal
Afbranders
Afdekfolies/Afdekdekens
Afdichtingsproducten/Vulmiddelen/Kleefstoffen/Reparatiepasta - Assortimenten
Afdichtingsproducten/Vulmiddelen/Kleefstoffen/Reparatiepasta - Overig
Afdichtplaten/Inzetstukken
Afgeknotte luzerne (Medicago Truncatula)
Afluister- en anti-afluisterapparatuur
Afrikaans Sint-Jansbrood (Parkia Africana)
Afrikaans Wormkruidplanten (Artemisia Afra)
Afrikaanse Laburnumbomen (Cassia Sieberiana)
Afrikaanse Lelie / Kaapse Lelie / Blauwe Tuberoos (Agapanthus) - Levende Plant
Afrikaanse Lelie / Kaapse Lelie / Blauwe Tuberoos (Agapanthus) - Snijbloem
Afrikaanse Lelie / Kaapse Lelie / Blauwe Tuberoos (Agapanthus) - Snijgroen
Afrikaanse Rijstplanten (Oryza Glaberrima)
Afrikaanse sterappelbomen (Chrysophyllum albidum)
Afrikaanse Yamboonplanten (Sphenostylis Stenocarpa)
Afrikaantje (Tagetes) - Levende Plant
Afrikaantjesplanten (Tagetes Erecta)
Afsluitdeksels/Toegangspanelen
Afstand-/Lengtemeters (Aangedreven)
Afstandmeters
Aftershave
After-sun Vochtinbrengende Producten
Afvalemmers
Afvalopslagproducten - Assortimenten
Afvalopslagproducten - Onderdelen
Afvalopslagproducten - Overig
Afvalpersen
Afvalvernietigers voor Levensmiddelen
Afvalverwerkings/Perstoestellen - Onderdelen/Accessoires
Afvalverwerkings/Perstoestellen - Overig
Afvalzakken
Afvoeraansluitingen (Dakgoten/Afwatering)
Afvoerbuizen/-slangen voor Zwembad/Vijver/Waterpartij
Afvoergoten
Afvoeronderdelen/-artikelen voor Tuin/Grondniveau
Afvoerontstopper
Afvoerroosters
Afwas Voorspoelmiddelen
Afwateringssystemen voor Terras
Afwerklijsten/Profielen (Hout)
Afwerklijsten/Profielen (Niet-Hout)
Afzuigkappen
Agarhoutbomen (Aquilaria malaccensis)
Agave Lechuguilla Cactussen (Agave lecheguilla)
Ahuhuplanten (Tephrosia Purpurea)
Airconditioningapparatuur - Multifunctioneel - Vast
Airconditionings/Koel-/Ventilatieapparatuur - Assortimenten
Airconditionings/Koel-/Ventilatieapparatuur - Onderdelen/Accessoires
Airconditionings/Koelapparaten - Vast
Ajiplanten (Capsicum Baccatum)
Ajipoplanten (Pachyrhizus Tuberosus)
Ajowanplanten (Trachyspermum Ammi)
Akibomen (Blighia sapida)
Akkerschermplanten (Ammi)
Aktetas
Alarmfluitjes
Alarmsystemen (Inbraak)
Alarmsystemen Onderdelen/Accessoires
Alcoholhoudende Dranken gefermenteerd, niet op basis van Druiven - Mousserend
Alcoholhoudende Dranken gefermenteerd, niet op basis van Druiven - Niet-mousserend
Alcoholische Dranken - Assortimenten
Alcoholvrij Bier
Alcoholvrije Dranken - Assortimenten (Gebruiksklaar)
Alcoholvrije Dranken - Assortimenten (Niet-gebruiksklaar)
Alcoholvrije Likeuren
Alcoholvrije Mixdranken
Alcoholvrije Mousserende Cider/Perry
Alcoholvrije Mousserende Wijn
Alcoholvrije Stille Cider/Perry
Alcoholvrije Stille Wijn
Alexandrijnse Klaverplanten (Trifolium Alexandrinum)
Alfalfaplanten (Medicago Sativa)
Algemene Lichaamsverzorging - Assortimenten
Algemene Lichaamsverzorging - Overig
Algemene/Veelzijdige Gastro-intestinale Middelen
Algemene/Veelzijdige Huid/Hoofdhuidbehandelingen
Algemene/Veelzijdige Pijnstiller
Allergiepreventie/Allergievermindering/Antihistamines
Allium/Sierui - Bol/Knol
Aloë - Levende Plant
Aloë Vera
Aloe Veraplanten (Aloe vera)
Alpenden (Pinus cembra)
Alpenzilverspar (Abies lasiocarpa)
Alruinplanten (Mandragora Officinarum)
Alternatieve Soorten Vlees/Gevogelte/Wild - Bereid/Bewerkt
Alternatieve Soorten Vlees/Gevogelte/Wild - Niet-bereid/Niet-bewerkt
Aluminium (Gerecycled/Hernieuwbaar)
Aluminium (Gevormd)
Aluminium (Ongevormd)
Alyce-klaverplanten (Alysicarpus Spp.)
Amandelbomen (Prunus dulcis var. dulcis)
Amarantplanten (Amaranthus Spp.)
Amarantplanten (Amaranthus)
Amaryllis / Ridderster (Hippeastrum) - Bol/Knol
Amaryllis / Ridderster (Hippeastrum) - Levende Plant
Amaryllis / Ridderster (Hippeastrum) - Snijbloem
Ambarellabomen (Spondias dulcis)
Americaanse grondnootplanten (Apios americana)
Amerikaans Katoenplanten (Gossypium barbadense)
Amerikaanse bosbesheesters (Vaccinium sect. Cyanococcus)
Amerikaanse Cranberryheesters (Vaccinium macrocarpon)
Amerikaanse Dadelpruimen
Amerikaanse Eik (Quercas) - Snijgroen
Amerikaanse mammi-appelbomen (Mammea americana)
Amerikaanse Oliepalmbomen (Elaeis Oleifera)
Amerikaanse Persimoenbomen (Diospyros virginiana)
Amerikaans-helmgras (Ammophila Breviligulata)
Amfibieën
Amomum Subulatumbomen (Amomum Subulatum)
Anabomen (Faidherbia Albida)
Analoge Camera's
Analoog/Digitaal Omzetters
Ananasplanten (Ananas comosus)
Ananassen
Ananassen (Vers Gesneden)
Andere blauwgrassen (Poa spp.)
Andere Lampbevestigingsproducten/Fittingen
Andere Muziekinstrumenten (Elektrisch)
Andere Muziekinstrumenten (Niet-elektrisch)
Andere Onderdelen voor Remsystemen
Andere Worsten Vlees/Gevogelte/Wild - Bereid/Bewerkt
Andes Lupineplanten (Lupinus Mutabilis)
Andijvie
Andijvieplanten (Cichorium Endivia)
Anemoon - Snijbloem
Angelica/Engelwortel
Anijs
Anijsplanten (Pimpinella Anisum)
Anjer / Anjelier / Bruidsanjer (Dianthus) - Levende Plant
Ankers/Muurpluggen
Annona (Vers Gesneden)
Antennes
Antephoragrassen (Anthephora spp.)
Anthurium / Flamingoplant - Levende Plant
Anthurium / Flamingoplant - Snijbloem
Anthurium / Flamingoplant - Snijgroen
Anti-acné Hulpmiddelen (Elektrisch)
Anti-acné Hulpmiddelen (Niet-elektrisch)
Anticonceptiva - Spiraaltje
Anti-corrosiva
Anti-diefstalartikelen - Assortimenten
Anti-diefstalartikelen - Onderdelen/Accessoires
Anti-diefstalartikelen - Overig
Anti-inbraak Tralies/Panelen/Rolluiken
Anti-klim Veiligheidsproduct
Antilopenvlees - Bereid/Bewerkt
Antilopenvlees - Niet-bereid/Niet-bewerkt
Anti-rook Hulpmiddelen
Anti-schimmel Producten
Antiseptica
Antislip Hulpmiddelen (DHZ)
Antispatproducten
Antivries/Koelmiddelen
Antroewaplanten (Solanum Macrocarpon)
Antroewa's (Afrikaanse Aubergine)
Antwoordmachines
Apparatuur voor Bereiding van Levensmiddelen/Dranken - Assortimenten
Apparatuur voor Bereiding van Levensmiddelen/Dranken - Onderdelen/Accessoires
Apparatuur voor Bereiding van Levensmiddelen/Dranken - Overig
Apparatuur voor Decoratieve Verftechnieken
Apparatuur voor Ongediertebestrijding (Elektrisch)
Apparatuur voor Ongediertebestrijding (Niet-elektrisch)
Apparatuur/Accessoires voor Stuurwielen
Appelbananen
Appelbesheesters (Aronia)
Appelbomen (Malus domestica)
Appels
Aquarium/Vivarium
Arabische Gombomen (Acacia senegal)
Arachis Glabrata-planten (Arachis Glabrata)
Arachis Pintoi-planten (Arachis Pintoi)
Arakbomen (Salvadora Persica)
Aralia (Polyscias) - Levende Plant
Archiefkasten
Architectonische en Technische Diensten
Areng Palmbomen (Arenga Saccharifera)
Arganbomen (Argania Spinosa)
Armbanden
Armeense Komkommer
Armeense komkommerplanten (Cucumis Melo var. Flexuosus)
Aromadiffusors (Elektrisch)
Aromadiffusors (Niet-elektrisch)
Aromatherapie - Assortimenten
Aromatherapie - Overig
Aromatherapie Kussens
Aronskelk (Zantedeschia) - Snijbloem
Aronskelk (Zantedeschia) - Snijgroen
Arracacha
Arracachaplanten (Arracacia Xanthorrhiza)
Arrowroot (Pijlwortel)
Artikelen voor Oosterse Vechtsporten
Artikelen voor Ritmische Gymnastiek
Artisjokken
Artisjokplanten (Cynara Scolymus)
Asam Gelugurbomen (Garcinia atroviridis)
Asfalt/Beton Reparatiebouwstoffen
Asfalt/Beton/Metselwerk - Assortimenten
Asfalt/Beton/Metselwerk - Onderdelen/Accessoires
Asfalt/Beton/Metselwerk - Overig
Asperge-erwten
Asperge-erwtplanten (Tetragonolobus Purpureus)
Aspergeplanten (Asparagus Officinalis)
Asperges
Aster / Septemberkruid - Levende Plant
Aster / Septemberkruid - Snijbloem
Astilbe / Spirea / Pluimspirea - Levende Plant
Aszuigers
Atemoyabomen (Annona x atemoya)
Atletiek Artikelen - Assortimenten
Atletiek Artikelen - Overig
ATV's
ATV's/UTV's - Apparatuur/Accessoires
Aubergineplanten (Solanum Melongena)
Aubergines
Audio (Niet Muziek) - Digitaal
Audio Antennes voor Auto
Audio Cassettespelers/Wisselaars voor Auto
Audio CD-Spelers/Wisselaars voor Auto's
Audio Luidsprekers voor Auto's
Audio MD-Spelers/Wisselaars voor Auto's
Audio Subwoofers voor Auto
Audio Tijdschriften en Kranten
Audio Versterkers voor Auto's
Audio voor Auto's - Assortimenten
Audio voor Auto's - Onderdelen/Accessoires
Audio voor Auto's - Overig
Audio/Video Accessoires - Assortimenten
Audio/Video Accessoires - Onderdelen
Audio/Video Accessoires - Overig
Audio/Video Apparatuur en Accessoires - Assortimenten
Audio/Video Etiketteringssystemen
Audio/Video in de Auto - Assortimenten
Audio/Video Kabels
Audio/Video Ontvangers
Audio/Video/Fotografie - Assortimenten
Audio-Besturingseenheden voor Auto's
Audioboeken
Audiocassettes - Opneembaar
Audiocassettes - Voorbespeeld
Audio-Tuners/Ontvangers voor Auto's
Audiovisuele Diensten
Augurken
Augurken/Pikante sauzen/Chutneys/Olijven - Assortimenten
Australisch Madeliefje (Bracyscome) - Levende Plant
Auto Alarmsystemen
Auto Beeldschermen
Auto DVD-Spelers
Auto Video Ontvangstapparatuur
Auto Video/Navigatie - Assortimenten
Auto Video/Navigatie - Onderdelen/Accessoires
Auto Video/Navigatie - Overig
Auto Videorecorders
Auto/Treinset - Onderdelen/Accessoires
Auto/Treinsets (Elektrisch)
Auto/Treinsets (Niet-elektrisch)
Autobandverzorging - Schoonmaakmiddelen/Schuim/Glansmiddelen
Autocarrosserieverzorging - Was-/Boen-/Beschermings-/Verwijderproducten
Auto-Interieur Reinigingsmiddelen
Autolak
Autoruit Zonnekleppen/Zonneschermen
Autoruitfolies
Auto's/Bestelwagens/Sportwagens/Lichte Vrachtwagens
Autowielverzorging - Schoonmaak/Glansmiddelen
Avocado’s (Vers Gesneden)
Avocadobomen (Persea americana)
Avocado's - Gladde Schil
Avocado's - Ruwe Schil (Type Hass)
Axonopusgras (Axonopus spp.)
Azalea / Rododendron - Levende Plant
Azijnen
Azijnen/Kookwijnen - Assortimenten
Baardgras (Andropogon spp.)
Baardmos (Usnea)
Babussa Palmbomen (Attalea Speciosa)
Baby Autostoelen/Stoelverhogers
Baby Bad Veiligheidsproducten
Baby Badjes/Badstoelen/Badwiegen
Baby Bescherming (Niet-elektrisch)
Baby Bewaking (Elektrisch)
Baby Bewaking (Niet-elektrisch)
Baby Deurschommel
Baby Hygiënische Oppervlaktereiniger
Baby Inlegluiers
Baby Looprek/Box
Baby Luierkussens
Baby Luiertafel
Baby Oefenspeeltuig/Vervoer - Assortimenten
Baby Oefenspeeltuig/Vervoer - Onderdelen/Accessoires
Baby Oefenspeeltuig/Vervoer - Overig
Baby Potjes/WC-Trainers
Baby Riemen/Gordels
Baby Wipstoeltjes/Schommelstoelen (Elektrisch)
Baby Wipstoeltjes/Schommelstoelen (Niet-elektrisch)
Baby/Peuter - Babymelkproducten (Houdbaar)
Baby/Peuter - Dranken (Houdbaar)
Baby/Peuter - Levensmiddelen (Diepvries)
Baby/Peuter - Levensmiddelen (Houdbaar)
Baby/Peuter - Levensmiddelen/Dranken - Assortimenten
Baby/Peuter Stimuleringsspeelgoed (Elektrisch)
Baby/Peuter Stimuleringsspeelgoed (Niet-elektrisch)
Baby-/Peuterbehandelingen
Babybananen
Babybedjes/Babymatrassen - Assortimenten
Babybedjes/Babymatrassen - Onderdelen
Babybedjes/Babymatrassen - Overig
Babybestek (Geen Wegwerpartikel)
Babydrager
Babyleaves
Babyloopleermiddelen
Babyluiers (Geen Wegwerpartikel)
Babyluiers (Wegwerpartikel)
Babyluiers Accessoires
Babyluiers en Accessoires - Assortimenten
Babyluiers en Accessoires - Overig
Babymatras
Babyschommels/Babyswings
Babystoel
Babystoelen - Assortimenten
Babystoelen - Onderdelen
Babystoelen - Overig
Babyvoeding - Accessoires
Babyvoeding - Assortimenten
Babyvoeding - Flessen
Babyvoeding - Onderdelen
Babyvoeding - Overig
Babyvoeding - Serviesgoed
Babyvoeding - Spenen
Babywiegen/Bedjes
Bacopa (Sutera) - Levende Plant
Bad/Douche Accessoires - Persoonlijk
Bad-/Douchecabinewanden
Bad-/Douchedeuren
Bad/Douchemodulen - met Waterjets
Bad-/Doucherekjes - Muurbevestiging
Badadditieven
Badkamer Accessoires - Assortimenten
Badkamersets
Badkuip-/Douchemodulen
Badkuipen
Badkuipen met Waterjets (Hot Tubs/Spabaden)
Badliften
Badmatten/WC-matten
Badzitjes
Bagage Alarmsystemen
Bagage/Koffers/Kledinghoezen
Bagage/Tassen/Paraplu's - Accessoires
Bahiagras (Paspalum Notatum)
Bak- en Braadpannen
Bak/Kook Benodigdheden (Beperkt Houdbaar)
Bak/Kook Benodigdheden (Diepvries)
Bak/Kook Benodigdheden (Houdbaar)
Bak/Kook Samenstellingen (Beperkt Houdbaar)
Bak/Kook Samenstellingen (Diepvries)
Bak/Kook Samenstellingen (Houdbaar)
Bak/Kook Samenstellingen/Benodigdheden - Assortimenten
Bakbananen
Bakgerei/Ovengerei/Grillgerei (Niet Wegwerp)
Ballasten/Starters
Ballonklokje (Platycodon) - Levende Plant
Ballonnen
Balsemwormkruidplanten (Tanacetum Balsamita)
Balsemzilverparbomen (Abies balsamea)
Balsemzilverspar (Abies balsamea)
Balustrade/Trapleuningsystemen
Bambara grondnootplanten (Vigna subterranea)
Bambaraplanten (Anogeissus Leiocarpa)
Bamboe (Dendrocalamus Strictus)
Bamboe (Fargesia) - Levende Plant
Bamboescheuten
Bamboestruiken (Bambuseae)
Bananen - (Vers Gesneden)
Bananen (Cavendish)
Bananenbladeren (Garnering van Voedsel)
Bananenplant (Musa) - Levende Plant
Banden
Bandenhoes
Bandenhouder
Bandenspanningsmeter
Bandschuurmachines - Draagbaar
Bandschuurmachines - Vastgemonteerd
Bandzagen - Draagbaar
Bandzagen/Lintzagen - Vastgemonteerd
Bankbiljetten/Cheques
Bankschroeven
Bankschroeven/Klemmen/Spangereedschap - Onderdelen/Accessoires
Baobabbomen (Adansonia Digitata)
Barbecues
Bargerei - Assortimenten
Barografen - Niet-elektrisch
Barometers - Niet-elektrisch
Barwoodbomen (Pterocarpus Erinaceus)
Basilicum
Basilicumplanten (Basilicum Spp.)
Basis-/Drageroliën
Basterdklaverplanten (Trifolium Hybridum)
Bataviasla
Batterijdozen
Batterijen
Batterijen/Opladers - Assortimenten
Batterij-starthulp (Jumpstarter)
Bauhiniaplanten (Bauhinia Spp.)
Bedden - Onderdelen
Bedden-/hoeslakens
Bedden/Matrassen - Assortimenten
Bedden/Matrassen - Overig
Bedframes/Ledikanten
Bedieningsapparaten voor Computer/PC's/Spelcomputers/Games
Bedrijfsmanagement en Consultingdiensten
Beefalo-/Cattalovlees - Bereid/Bewerkt
Beefalo-/Cattalovlees - Niet-bereid/Niet-bewerkt
Beeldhouwersgereedschap (Aangedreven)
Beeldhouwersgereedschap (Niet-aangedreven)
Beemdlangbloemgras (Festuca Pratensis)
Begonia - Levende Plant
Behaard Katoenplanten (Gossypium hirsutum)
Behandeld Hout
Behandeling tegen Verslaving - Assortimenten
Behandeling tegen Verslavingen
Behandeling van Levensmiddelen
Beha's/Bodies/Korsetten
Beitels
Beitels (Aangedreven)
Beitels/Gutsen - Assortimenten
Bellen/Zoemers
Benodigdheden Glasbewerking/Emailleerkunst/Marqueterie - Assortimenten
Benodigdheden voor Alcoholvervaardiging
Benodigdheden voor Beeldhouwers/Pottenbakkers - Assortimenten
Benodigdheden voor Beeldhouwers/Pottenbakkers - Overig
Benodigdheden voor Drukkunst - Assortimenten
Benodigdheden voor Drukkunst - Overig
Benodigdheden voor Glasbewerking/Emailleerkunst/Marqueterie - Overig
Benodigdheden voor Handwerken/Speelgoedvervaardiging - Assortimenten
Benodigdheden voor Handwerken/Speelgoedvervaardiging - Overig
Benodigdheden voor Houtbrand/Graveerkunst - Overig
Benodigdheden voor Kaarsen-/Zeepgieten - Assortimenten
Benodigdheden voor Kaarsen-/Zeepgieten - Overig
Benodigdheden voor Mandenvlechtwerk - Assortimenten
Benodigdheden voor Mandenvlechtwerk - Overig
Benodigdheden voor Papierkunst/Kaartvervaardiging - Assortimenten
Benodigdheden voor Papierkunst/Kaartvervaardiging - Overig
Benodigdheden voor Presentaties - Accessoires
Benodigdheden voor Presentaties - Assortimenten
Benodigdheden voor Presentaties - Overig
Benodigdheden voor Sieradenvervaardiging - Assortimenten
Benodigdheden voor Sieradenvervaardiging - Overig
Benodigdheden voor Spin-/Weefkunst - Assortimenten
Benodigdheden voor Spin/Weefkunst - Overig
Benodigdheden voor Spuitlakken - Assortimenten
Benodigdheden voor Spuitlakken - Overig
Benodigdheden voor Wenskaarten/Geschenkverpakkingen/Feestartikelen - Assortimenten
Bereide/Bewerkte Levensmiddelen - Assortimenten
Berendruifplanten (Arctostaphylos uva-ursi)
Bergamotplanten (Monarda Didyma)
Bergbonenkruid
Bergpapajabomen (Vasconcellea pubescens)
Bergpapaja's
Bergsteentijmplanten (Clinopodium Nepeta)
Bernagieplanten (Borago Officinalis)
Beschermbrillen/Oogmaskers
Beschermende Bedekking voor Zwembad/Vijver/Waterpartij
Beschermende Handschoenen
Beschermende Kleding - Accessoires
Beschermende Kleding - Assortimenten
Beschermende Kleding voor het Bovenlichaam
Beschermende Kleding voor het Hele Lichaam
Beschermende Kleding voor het Onderlichaam
Beschermende Middelen - Assortimenten
Beschermende Steunriemen
Beschermers voor Dekbedden/Quilts/Gewatteerde deken/Overtrekken - Afneembaar
Beschermers voor Wiellagers
Bescherming/Verpakking voor Bekabeling/Bedrading
Beschermingsproducten voor Vaatwasmachines
Bessen/Zachtfruit/Kleinfruit (Vers Gesneden)
Bestek - Assortimenten (Niet Wegwerp)
Bestek - Overig (Niet Wegwerp)
Bestek (Wegwerp)
Bestek voor Vis/Schaaldieren/Slakken (Niet Wegwerp)
Bestek voor Voorgerecht/Nagerecht/Kaas (Niet Wegwerp)
Bestekzakmes
Besturings-/Invoerapparatuur voor Computers/PC's/Spelcomputers/Games - Assortimenten
Besturings-/Invoerapparatuur voor Computers/PC's/Spelcomputers/Games - Onderdelen/Accessoires
Besturings-/Invoerapparatuur voor Computers/PC's/Spelcomputers/Games - Overig
Betel- of arecapalmbomen (Areca catechu)
Beton Luchtbelvormende Middelen
Betonbindmiddelen
Betonkleurmiddelen/-kleurstoffen
Betonmortel
Beukenzwam fungus (Hypsizygus Tessellatus)
Beukenzwammen/Shimeji's
Bevestigingen voor Niet-/Nagelmachine (Nieten/Nagels)
Bevestigingsmaterialen - Accessoires
Bevestigingsmaterialen - Assortimenten
Bevestigingsmaterialen - Overig
Bevestigingsrails
Bevochtigingsapparaten/Verstuivers (Elektrisch)
Bevochtigingsapparaten/Verstuivers (Niet-elektrisch)
Bevordering Gezondheid - Assortimenten
Bewaar-/Conserveringsmiddelen
Bewaarhulpmiddelen voor Levensmiddelen/Drank
Bewakingscamera's
Bewateringssystemen
Bewateringssystemen (Niet-aangedreven)
Bewerkte Graanproducten - Assortimenten
Bezems (Niet–elektrisch)
Bezems/ Borstels
Bidets
Bier
Bierglazen
Bieslook
Bieslookplanten (Allium Schoenoprasum)
Bigbags / Flexibele Bulkcontainers (Leeg)
Bijen/Wespen/Anten - Niet-bereid/Niet-bewerkt
Bijen/Wespen/Mieren - Bereid/Bewerkt
Bijlen
Bijlen (DHZ)
Bijproducten Zuivel
Bijvoet
Bijvoetplanten (Artemisia Vulgaris)
Bijzettafels voor Levensmiddelen (Niet-elektrisch)
Bilzekruidplanten (Hyoscyamus Niger)
Bimi (Broccolini) en andere Koolachtige Kruisingen
Bimi- of Broccoliniplanten (Brassica Oleracea Italica x Alboglabra)
Bindsla/Romeinse Sla
Binnenband
Binnendeuren
Biologische Activator
Biscuits/Koekjes - Assortimenten
Biscuits/Koekjes (Beperkt Houdbaar)
Biscuits/Koekjes (Diepvries)
Biscuits/Koekjes (Houdbaar)
Bittere aloeplanten (Aloe ferox)
Bittere amandelbomen (Prunus dulcis var. amara)
Bitterhoutbomen (Quassia Amara)
Bitterkruid (Lewisia) - Levende Plant
Bitterzoetplanten (Solanum Dulcamara)
Bizon-/Buffelvlees - Bereid/Bewerkt
Bizon-/Buffelvlees - Niet-bereid/Niet-bewerkt
Blaas/Genitale/Rectale Producten - Assortimenten
Blaas/Genitale/Rectale Producten - Overig
Blaasontstekingsproducten
Bladglansproduct/Plantreiniger
Bladgroenten - Onbewerkt/Onverwerkt - Mengsels (Verse Sla mixen)
Bladgroenten (Vers Gesneden)
Bladkoolplanten (Brassica oleracea var. viridis)
Bladpeterselie (Italiaans)
Bladselderij (bosselderij)
Blauw Druifje (Muscari) - Bol/Knol
Blauw Druifje (Muscari) - Levende Plant
Blauw Madeliefje (Felicia) - Levende Plant
Blauw Schapengras (Festuca) - Levende Plant
Blauwe Aardappelstruik (Solanum) - Levende Plant
Blauwe bosbesplanten (Vaccinium myrtillus)
Blauwe Distel / Kruisdistel (Eryngium) - Snijbloem
Blauwkussen (Aubrieta) - Levende Plant
Blauwspar (Picea pungens)
Bleekmiddel
Bleekselderij
Blikjes (leeg)
Blikopeners (Elektrisch)
Bliksemafleiders en Accessoires
Bliksemdetectors - Elektrisch
Blimbingbomen (Averrhoa bilimbi)
Bloedwortelplanten (Sanguinaria Canadensis)
Bloem-/Suikerstrooiers
Bloembolplanters
Bloemenschepjes
Bloemkool
Bloemkoolplanten (Brassica Oleracea var. Botrytis)
Blokpaprika's
Bluegrass (Dichanthium spp.)
Blueleaf/Cascadebesheesters (Vaccinium deliciosum)
Bluestemgras (Bothriochloa spp.)
Blusdekens
Boards/Ski's (Watersport)
Boards/Ski's (Watersport) - Onderdelen/Accessoires
Bodembedekkende/Landschapsvormende Materialen
Bodembedekking voor Dieren
Bodemfolie voor Zwembad/Vijver/Waterpartij
Bodemplaten
Bodemstampers (Niet-aangedreven)
Body Poeder
Boeken - Assortimenten
Boeket Anjers
Boeket Chrysanten
Boeket Gemengd
Boeket Incalelies (Alstroemeria)
Boeket Lelies
Boeket Overig
Boeket Rozen
Boeket Tropische Bloemen
Boeket Trosanjers
Boekhoudkundige Diensten
Boekomslagen
Boekweitplanten (Fagopyrum Esculentum)
Boemerangs
Boenmachines/Tapijtreinigers
Boerenkers (Thlaspi) - Snijgroen
Boerenkool
Boerenkoolplanten (Brassica Oleracea var. Sabellica)
Boerenwormkruidplanten (Tanacetum Vulgare)
Bogen
Bokschaafmachines - Vastgemonteerd
Boldoplanten (Peumus Boldus)
Bolgroenten (Vers Gesneden)
Bollen/Knollen - Overig
Bolvormige Buitenspiegels
Bonen (met Peulen) (Vers Gesneden)
Bonenkruid
Bonenkruidplanten (Satureja)
Bontewikkeplanten (Vicia Villosa)
Boodschappentassen/Trolleys
Boogschieten/Darts Artikelen - Assortimenten
Boogschieten/Darts Artikelen - Onderdelen/Accessoires
Boogschieten/Darts Artikelen - Overig
Boomalsemstruiken (Artemisia Arborescens)
Boor/Schroevendraaiers (Aangedreven)
Boorhamer en Schroevendraaier Set
Boorhamers
Boormachines - Onderdelen/Accessoires
Borden - Gecombineerd
Borden - Onderdelen/Accessoires
Borden (Niet Wegwerp)
Bordspelen (Elektrisch)
Bordspelen (Niet-elektrisch)
Bordspelen/Kaarten/Puzzels - Accessoires/Onderdelen
Bordspelen/Kaarten/Puzzels - Assortimenten
Bordspelen/Kaarten/Puzzels - Overig
Boren - Combinatie (Aangedreven)
Boren/Schillers
Boroniastruiken (Boronia)
Borst-/Heupvergroters
Borstcompres
Borstel-/veegmachines (Elektrisch)
Borsteltjes/Olieverstuivers/Pipetten voor Voedselbereiding
Borstinwrijfmiddelen
Borstkolf
Borstvoedingshygiëne Accessoires
Bosaardbeien
Bosbessen
Bosmaaier/Lijntrimmers/Graskantensnijders (Aangedreven)
Bossalie (Salvia) - Levende Plant
Bosvergeet-mij-nietje (Myosotis) - Levende Plant
Boter (Beperkt Houdbaar)
Boter (Diepvries)
Boter (Houdbaar)
Boter- of swarri notenbomen (Caryocar nuciferum)
Botermakers (Elektrisch)
Bougainville - Levende Plant
Bouillon/Vleesjus/Glaceermiddelen (Houdbaar)
Bout-/Kettingsnijders
Bouvardia - Snijbloem
Bouw- en Aanverwante Diensten
Bouwbenodigdheden - Assortimenten
Bouwbenodigdheden - Overig
Bouwhelmen/Veiligheidspetten
Bouwstenen
Bovenfrezen
Boysenbessen
Braakwortelbomen (Carapichea Ipecacuanha)
Bramen
Bramenplanten (Rubus fruticosus)
Brandbeveiliging/Chemische Veiligheidsproducten - Assortimenten
Brandblusapparaten - Assortimenten
Brandblusapparaten - Onder druk
Brandkasten
Brandkraaninstallaties
Brandslangen
Brandstof/Brandstofadditieven - Assortimenten
Brandstof/Ontstekingshulpmiddelen - Assortimenten
Brandstofadditieven
Brandstofinjectoren
Brandstoftank/-leiding Reparatiekits
Brandtrappen/Ladders
Brandvertragende Middelen/Vuurdovende Stoffen
Breekijzers/Rolkoevoeten
Briefopeners (Elektrisch)
Briefopeners (Niet-elektrisch)
Briefweegschaal (Elektrisch)
Briefweegschaal (Niet-elektrisch)
Brievenbus
Brievenbusklep (inbouw)
Brillen - Klaar voor Gebruik
Brillenglazen
Brilmonturen
Broccoli
Broccoliplanten (Brassica Oleracea var. Italica)
Broches
Broeikas Frames
Broeikas Verwarmingstoestellen/Ventilatoren
Broeikassen (Compleet)
Broeken/Korte Broeken
Bromelia - Levende Plant
Brood (Beperkt Houdbaar)
Brood (Diepvries)
Brood (Houdbaar)
Brood/Bakkerijproducten - Assortimenten
Broodboom (Artocarpus Altilis)
Broodmachines
Broodroosters
Broodtrommels/Lunchboxes (Niet-Elektrisch)
Broodvruchten
Bruidsbloem (Stephanotis) - Levende Plant
Bruinen Zonder Zon - Oraal (Niet-elektrisch)
Bruinen Zonder Zon - Topisch (Niet-elektrisch)
Bruinen Zonder Zon (Elektrisch)
Bruiningsproducten - Assortimenten
Bruiningsproducten - Onderdelen
Bruiningsproducten - Overig
Buchuplanten (Agathosma)
Buffalgras (Paspalum Conjugatum)
Buffelgras (Cenchrus Ciliaris)
Buffet
Buggies/Boards voor Vlieger/Parachute (Niet-elektrisch)
Buideldieren
Buitenaccessoires voor Motorvoertuigen - Assortimenten
Buitenaccessoires voor Motorvoertuigen - Overig
Buitendeuren
Buitengevel - Accessoires
Buitengevel - Draagstenen/Frontons
Buitengevelbekleding
Buitenkeuken (Tuin)
Buitenlampen/Toortsen/Lantaarns - Elektrisch
Buitenlampen/Toortsen/Lantaarns - Niet-elektrisch
Buitenthermometers - Elektrisch
Buitenthermometers - Niet-elektrisch
Buizen
Buizen - Onderdelen/Accessoires
Bumper-/Grillebeschermers
Bumpers
Bureauonderleggers
Burmese druivenbomen (Baccaurea ramiflora)
Burrageara - Levende Plant
Cabreuvaplanten (Myrocarpus Frondosus)
Cacaobomen (Theobroma cacao)
Cactusbladeren (Garnering van Voedsel)
Cactusvijgen/Woestijnvijgen
Cactusvijgplanten (Opuntia ficus-indica)
Cadaba farinosaplanten (Cadaba Farinosa)
Cadeaukaarthouder/-hoes
Cainitobomen (Chrysophyllum cainito)
Cake-/Taartjesmakers (Elektrisch)
Cakes - Zoet (Beperkt Houdbaar)
Cakes - Zoet (Diepvries)
Cakes - Zoet (Houdbaar)
Calamondin (Citrofortunella) - Levende Plant
Calamondinbomen (Citrofortunella microcarpa)
Calathea - Levende Plant
Calibrachoa - Levende Plant
Californische dauwbraamplanten (Rubus ursinus)
Calla (Zantedeschia) - Levende Plant
Calliandra calothyrsusbomen (Calliandra Calothyrsus)
Calopogoniumplanten (Calopogonium Spp.)
Camachilbomen (Pithecellobium dulce)
Camcorders
Camomilaplanten (Matricaria chamomilla)
Campanula Portenschlagiana / Dalmatiëklokje - Levende Plant
Camper/Caravan Installatie/Set-up Materiaal
Canavaliabonen
Cannabis - Bad en douche
Cannabis - Biscuits/Koekjes - Gebruiksklaar (Houdbaar)
Cannabis - Biscuits/Koekjes (Beperkt Houdbaar)
Cannabis - Biscuits/Koekjes (Diepvries)
Cannabis - Biscuits/Koekjes (Houdbaar)
Cannabis - Biscuits/Koekjes Gemengd (Houdbaar)
Cannabis - Budder
Cannabis - Capsules, Tabletten, Softgels
Cannabis - Cartridge voor e-Sigaret
Cannabis - Chocolade/Chocoladesnoepjes
Cannabis - Dranken met Toegevoegde Ingrediënten (Houdbaar)
Cannabis - Dranken met Vruchtensap - Gebruiksklaar (Beperkt Houdbaar)
Cannabis - Dranken met Vruchtensap - Gebruiksklaar (Houdbaar)
Cannabis - Eetbare Oliën - Plantaardig (Houdbaar)
Cannabis - e-Sigaret
Cannabis - Gearomatiseerde Dranken - Gebruiksklaar (Houdbaar)
Cannabis - Gedroogde Bloem - Gemalen
Cannabis - Gedroogde Bloem - Heel
Cannabis - Harde/Zachte Snoepjes
Cannabis - Hars (Biologisch)
Cannabis - Hars (Plantaardig/Synthetisch)
Cannabis - Hartige Snack - Kant-en-klaar (Houdbaar)
Cannabis - Hasj
Cannabis - Kief
Cannabis - Kruidensigaretten - Geen tabak
Cannabis - Levende Hars
Cannabis - Live Rosin
Cannabis - Muffins/Brownies/Cakes - Gebruiksklaar (Houdbaar)
Cannabis - Olie
Cannabis - opneembaar extract - Olie/orale spray/tinctuur
Cannabis - Plant
Cannabis - Shatter
Cannabis - stevig doordrenkt
Cannabis - Thee/Kruidenthee - Gebruiksklaar (Houdbaar)
Cannabis - Topisch - Crème/Lotion voor Gezicht en Lichaam
Cannabis - Vers
Cannabis - Voorgerold
Cannabis - Vruchtensap - Gebruiksklaar (Beperkt Houdbaar)
Cannabis - Vruchtensap - Gebruiksklaar (Houdbaar)
Cannabis - Vruchtenthee/Kruidenthee - Gebruiksklaar
Cannabis - Was
Cannabis - Wegwerp e-Sigaret
Cannabis - Zaden
Cannabis - Zoetwaren/Kunstmatige Zoetstof - Assortimenten
Cannabis -Thee/Kruidenthee - Blaadjes/Zakjes (Houdbaar)
Cantala Cactussen (Agave cantala)
Cantaloepmeloenplanten (Cucumis Melo var. Cantaloupensis)
Cantaloupemeloenen (Schil zonder Netstructuur)
Cantharellen
Cantharellenfungus (Cantharellus Cibarius)
Cappuccino Roomkloppers (Niet-elektrisch)
Carambola/Stervruchtbomen (Averrhoa carambola)
Carambola's (Zoete Blimbingen)
Carburateur-/Brandstofsysteemreiniging Sprays
Carburateur-/Brandstofsysteemreiniging Vloeibaar
Carport
Carrosserie herstelset
Cashewnootbomen (Anacardium occidentale)
Cassave/Maniok
Cassaveplanten (Manihot Esculenta)
Cassiabomen (Chamaecrista Rotundifolia)
Cassiakaneelbomen (Cinnamomum Cassia)
Castanospermum - Levende Plant
Cavendish Banaanstruiken (Musa acuminata - AAA)
Cayennepeperplanten (Capsicum Annuum)
CD/MD - Opneembaar
CD/MD - Voorbespeeld
Celtuce/Chinese sla/Stengelsla
Cement
Cement/Mortelmolens
Centrale Stofzuigers
Centrale Stofzuigers - Onderdelen/Accessoires
Champagnebladplanten (Acmella Oleracea)
Champignonfungus (Agaricus)
Champignons
Chayabomen (Cnidoscolus Aconitifolius)
Chayote
Chayoteplanten (Sechium Edule)
Chemicaliën (ongevormd)
Chemisch Reinigen/Stomerij
Chemische Producten voor Foto-ontwikkeling
Cherimoyabomen (Annona cherimola)
Cherimoya's
Chilipeperplanten (Capsicum Frutescens)
Chilipepers
Chinese Bieslookplanten (Allium Tuberosum)
Chinese bosklaverplanten (Lespedeza Cuneata)
Chinese Jujubebomen (Ziziphus jujuba)
Chinese Kool
Chinese Roos (Hibiscus) - Levende Plant
Chinesekoolplanten (Brassica Pekinensis)
Chinquapinbomen (Castanopsis)
Chips/Snacks/Gemengde Snacks - Naturel/Geëxtrudeerd (Houdbaar)
Chocolade/Cacao/Mout - Gebruiksklaar
Chocolade/Cacao/Mout - Niet-gebruiksklaar
Chocolade/Combinatie van Chocolade en Snoepjes
Chocoladefonteinen (Elektrisch)
Choi Sum
Choisamplanten (Brassica Chinensis var. Parachinensis)
Chrysant - Levende Plant
Chrysant - Snijbloem
Chrysopogongras (Chrysopogon spp.)
Chutneys/Pikante sauzen (Beperkt Houdbaar)
Chutneys/Pikante sauzen (Diepvries)
Chutneys/Pikante sauzen (Houdbaar)
Cichoreibladeren (Vers Gesneden)
Cider/Perry - Mousserend
Cider/Perry - Stil
Circuitmontages/Geïntegreerde Circuits
Cirkelzagen
Citroenbomen (Citrus limon)
Citroenen
Citroengras
Citroengrasplanten (Cymbopogon Citratus)
Citroenkruidplanten (Artemisia Abrotanum)
Citroenmelisse
Citroenmelisseplanten (Melissa Officinalis)
Citroenmirteplant (Backhousia Citriodoria)
Citroentijm
Citroenverbena/Verveine
Citroenverbenaplanten (Aloysia Citriodora)
Citrusvruchten (Vers Gesneden)
Clementine Mandarijnen
Clementinebomen (Citrus clementina)
Clivia Miniata - Levende Plant
Coatings voor Afwerking en Textuur
Cocaplanten (Erythroxylum Coca)
Cocktail Avocado's
Cocktailaccessoires (Niet Wegwerp)
Cocktailglazen
Colabomen (Cola acuminata)
Collectieve Beschermingsmiddelen - Onderdelen/Accessoires
Collectieve Beschermingsmiddelen - Overig
Colorado Zilverspar (Abies concolor)
Columbusgras (Sorghum X Almum)
Combi Koelkast/Diepvriezers
Combinatie Snijgereedschap (Niet-aangedreven)
Combinatie Spelers/Recorders
Combinatie Vlakschuurmachines - Schijf/Riem
Combinatie Wasautomaat/Wasdroger
Combretumbomen (Combretum Aculeatum)
Communicatie - Accessoires - Assortimenten
Communicatie - Accessoires - Overig
Communicatie - Assortimenten
Communicatiespeelgoed (Elektrisch)
Communicatiespeelgoed (Niet-elektrisch)
Compost-/Wormenbakken
Computer Docking Stations
Computer- en Technologiediensten
Computer Luidsprekers/Miniluidsprekers
Computer Moederborden
Computer Software (Geen Games)
Computer Software (Geen Games) - Digitaal
Computer/PC's/Spelcomputers/Games - Overig
Computercomponenten - Assortimenten
Computercomponenten - Onderdelen/Accessoires
Computercomponenten - Overig
Computergeheugen
Computerkabels
Computerkasten/-behuizing
Computerkoeling
Computernetwerkapparatuur - Assortimenten
Computernetwerkapparatuur - Onderdelen/Accessoires
Computernetwerkapparatuur - Overig
Computerprocessors
Computers - Onderdelen/Accessoires
Computers - Overig
Computers/PC's/Spelcomputers/Games - Assortimenten
Computers/PC's/Spelcomputers/Games - Game Software - Digitaal
Computers/PC's/Spelcomputers/Games - Software
Computers/PC's/Spelcomputers/Games - Software - Assortimenten
Computers/PC's/Spelcomputers/Games - Software - Overig
Computerschijven - Onderdelen/Accessoires
Computerstandaarden/Steunen
Computerstations - Assortimenten
Computerstations - Overig
Condensators
Condooms
Conferentiesystemen
Confetti
Confetti/Serpentine Kanonnen
Connectoren (Elektrisch)
Conomon Meloenen
Conomonmeloenplanten (Cucumis Melo var. Conomon)
Contactlenzen
Containers / ISO- Containers (Leeg)
Copaibaharsbomen (Copaifera Langsdorfii)
Cordyline Australis - Levende Plant
Cornuco's
Correctiehulpmiddelen
Cosmea (Cosmos) - Levende Plant
Cosmetica/Make-up - Gezichtstint
Cosmetica/Make-up - Hulpmiddelen/Accessoires
Cosmetica/Make-up - Lippen
Cosmetica/Make-up - Ogen
Cosmetica/Make-up - Testdisplay
Cosmetica/Make-up Applicators
Cosmetica/Make-up Assortimenten
Cosmetica/Make-up Multizone
Cosmetica/Make-up Producten Overig
Cosmetica/Make-up Verf/Glinsters/Glitters
Cosmetica/Parfums - Assortimenten
Cosmetica/Verzorgingsproducten voor Nagels - Assortimenten
Cosmetica/Verzorgingsproducten voor Nagels - Onderdelen
Cosmetica/Verzorgingsproducten voor Nagels - Overig
Courgetteplanten (Cucurbita Pepo)
Courgettes
Cranberries
Cratyllaplanten (Cratylia Argentea)
Crotolariaplanten (Crotalaria Spp.)
Croton (Codiaeum) - Levende Plant
Cubaanse Oreganoplanten (Plectranthus Amboinicus)
Cultivatoren/Diepwoelers (Niet-aangedreven)
Cupuazubomen (Theobroma grandiflora)
Curababomen (Passiflora Mollissima)
Curlingstenen
Curuba's
Custardappelbomen (Annona reticulata)
Custardappels
Cycaden/bladluizen/Sprinkhanen - Niet-bereid/Niet-bewerkt
Cyclaam / Alpenviooltje - Levende Plant
Cypergras (Papyrus) (Cyperus spp.)
Cypergras (Vers Gesneden)
Cypres (Cupressus) - Levende Plant
Cytisusbomen (Cytisus Proliferus)
Dadelpalmbomen (Phoenix dactylifera)
Dadelpruimen (Vers Gesneden)
Dadels (vers)
Dahlia - Bol/Knol
Dahlia - Levende Plant
Dahlia - Snijbloem
Daikon (Witte Rammenas)
Dakbedekking - Accessoires
Dakbedekking - Assortimenten
Dakbedekking - Dakstro
Dakbedekking - Overig
Dakbedekkingslagen
Dakconstructies
Dakgoten Onderdelen/Hulpstukken
Dakgoten/Afwatering - Assortimenten
Dakgoten/Afwatering - Overig
Dakpannen/Dakleien/Dakshingles
Dakramen - Buisvormig
Dakramen - Gelamineerd Hout
Dakramen (Niet-Hout)
Dakspoilers
Damascusroosplanten (Rosa × Damascena)
Dampschermen en Isolerende Folies
Damson-Pruimen
Darts
Dashboard Matjes/Overtrekken
Dashboard Sierkits
Daslook
Daslookplanten (Allium Ursinum)
Daturaplanten (Datura)
Dauwbraamheesters (Rubus flagellaris)
Decongestiva - Overig
Decoraties - Accessoires
Decoraties - Assortimenten
Decoraties/Muurplaten
Decoratieve Accessoires - Assortimenten
Decoratieve Accessoires Knoppen/Toetsen
Decoratieve Glazen Inzetstukken
Decoratieve Handgrepen/Slingers
Decoratieve Magneten/Stickers/Raamklevers
Decoratieve Spandoeken/Vlaggen
Decoratieve Spandoeken/Vlaggen - Accessoires
Decoratieve/Gepersonaliseerde Grilles
Decoupeerzagen
DECT-Repeater (Signaalversterker)
Deegpistolen (Elektrisch)
Deegrollen
Dekbedden/Quilts/Gewatteerde deken
Dekens/Plaids (Elektrisch)
Dekens/Plaids (Niet-elektrisch)
Dekvloer
Dekvloerroller/Stachelroller
Depilatie/Epilatie (Elektrisch)
Depilatie/Epilatie (Niet-elektrisch)
Desinfecterende Middelen
Desinfectiemachines
Desmanthusplanten (Desmanthus Spp.)
Desmodiunplanten (Desmodium Spp.)
Desserts (Beperkt Houdbaar)
Desserts (Diepvries)
Desserts (Houdbaar)
Desserts/Dessert Toppings - Assortimenten
Dessertsauzen/Toppings/Vullingen (Beperkt Houdbaar)
Dessertsauzen/Toppings/Vullingen (Diepvries)
Dessertsauzen/Toppings/Vullingen (Houdbaar)
Detectiemiddelen voor Materiaaldefecten
Deur/Poort Intercoms
Deur/Poort Spionnen
Deur/Poort/Raam Grendels/Sloten/Sleutels
Deur/Raam/Onroerend Goed Beveiligingsproducten - Assortimenten
Deur-/Raamkozijnen
Deurbeslag/-accessoires - Assortimenten
Deurbeslag/-accessoires - Overig
Deurdrempels
Deuren - Accessoires
Deuren - Assortimenten
Deuren - Overig
Deurisolatie
Deurkettingen
Deurkloppers
Deurkrukken/-knoppen/-klinken
Deurmatten
Deurplaatjes
Deurscharnieren
Deursluiters
Deuvels
Diademen
Diagnosemonitoren - Overig
Diagnosemonitoren voor Thuisgebruik/Weegschalen
Diagnosetesten - Assortimenten
Diagnosetesten - Overig
Diagnosetests voor Thuis
Diaprojectors
Dia's
Dichtingsproducten
Dicteerapparaten
Dieetmiddel - Eetlust-/Vetcontrole
Dieetmiddel - Maaltijdvervanger
Dieetmiddelen - Assortimenten
Dieetmiddelen - Overig
Dieffenbachia - Levende Plant
Dienbladen
Diepe Serveerschalen
Diepvriezers
Digitale Camera's
Digitale Fotolijsten
Digitale Pennen
Digitale Valuta
Dille
Dilleplanten (Anethum Graveolens)
Dimmers
Dipsauzen/Smaakmakers/Hartige Toppings/Hartige Spreads/Marinades (Beperkt Houdbaar)
Dipsauzen/Smaakmakers/Hartige Toppings/Hartige Spreads/Marinades (Diepvries)
Dipsauzen/Smaakmakers/Hartige Toppings/Hartige Spreads/Marinades (Houdbaar)
Diskettestations
Dispensers voor Schoonmaak-/Hygiënemiddelen
Diuretica
Djamboe-bolbomen (Syzygium malaccense)
Djamboe-semarangbomen (Syzygium samarangense)
Djambolanbomen (Syzygium cumini)
Dobbers
Doek/Van een Grondlaag voorziene Panelen voor Kunstenaars
Doelwitten (Elektrisch)
Doelwitten (Niet-elektrisch)
Doerians
Domotica - Apparaten voor Temperatuurregeling
Domotica - Bedieningspaneel
Domotica - Beveiligingsapparatuur
Domotica - Tuinapparatuur
Domotica - Verlichtingsapparatuur
Domotica - Vermogen Bewakingsapparaat
Dompelaars
Dompelpompen
Donkere Kamer Apparatuur en Accessoires - Assortimenten
Donkere Kamer Apparatuur en Accessoires - Onderdelen/Accessoires
Donkere Kamer Apparatuur en Accessoires - Overig
Doorspoel Bedieningspaneel/Duwplaat
Dopsleutelsets
Douche Thermoalarm
Douche Veiligheidsstrips
Douchearmen
Douchebakken
Douchecabines
Douchegordijnen
Douchegordijnen - Onderdelen/Accessoires
Douchekoppen
Douchesets
Doucheslang
Douchestangen/Glijstangen
Draadloze Televisieverbindingen
Draadscharen
Draadtapmachines
Draag/Hef/Klimuitrusting - Onderdelen/Accessoires
Draagbare Alarmapparaten
Draagbare Audio/Video Toestellen - Assortimenten
Draagbare Audio/Video Toestellen - Onderdelen/Accessoires
Draagbare Audio/Video Toestellen - Overig
Draagbare Audiocassettespelers
Draagbare Babybedjes en Wiegen
Draagbare CD-Spelers
Draagbare Digitale Videorecorders
Draagbare Draadloze Webcams
Draagbare DVD-Spelers
Draagbare Elektrische Lantaarns
Draagbare FM Zenders
Draagbare Inspectielamp
Draagbare Luchtbehandelingsapparatuur - Onderdelen/Accessoires
Draagbare Luidsprekers
Draagbare MD-Spelers
Draagbare MP3-Spelers
Draagbare Opslag Cilinders (Leeg)
Draagbare PA-Systemen
Draagbare Radiorecorders
Draagbare Radio's
Draagbare Wapens - Granaten/Explosieven
Draagbare Wapens - Raket Aangedreven
Draaibanken - Vastgemonteerd (Aangedreven)
Draaiende Schuurmachines
Draaitafels - CD
Draaitafels - Vinyl
Dracontomelon daobomen (Dracontomelon dao)
Dragende Balken
Dragende Componenten/Bouwelementen - Onderdelen/Accessoires
Dragende Componenten/Bouwelementen - Overig
Dragon
Dragonplanten (Artemisia Dracunculus)
Drakenbloedboom (Dracaena) - Levende Plant
Drank Decoratiematerialen/Accessoires (Niet- Eetbaar)
Dranken - Assortimenten
Dranken met Groentesap - Gebruiksklaar (Beperkt Houdbaar)
Dranken met Groentesap - Gebruiksklaar (Houdbaar)
Dranken met Groentesap - Niet-gebruiksklaar (Houdbaar)
Dranken met Vruchtensap - Gebruiksklaar (Beperkt Houdbaar)
Dranken met Vruchtensap - Gebruiksklaar (Houdbaar)
Dranken met Vruchtensap - Niet-gebruiksklaar (Houdbaar)
Dranken voor dieren (Beperkt Houdbaar)
Dranken voor dieren (Diepvries)
Dranken voor dieren (Houdbaar)
Drankgerei (Wegwerp)
Drankkoelers - Overig
Dressing/Dipsausjes (Diepvries)
Drinkflessen
Drinkgerei - Assortimenten
Drinkgerei - Overig
Drinkglazen op Voet voor Wijn/Water/Champagne
Drinkglazen zonder Voet
Drooginstallatie voor Fotografie
Droogrekken en Molens - Onderdelen/Accessoires
Droogtoestellen (Elektrisch)
Drukpers (Elektrisch)
Drukpers (Niet-elektrisch)
Drukwerk - Assortimenten
Dubbelzijdige Discs - Voorbespeeld
Duikuitrusting
Duindoornheesters (Hippophae)
Duivelsdrekplanten (Ferula assa-foetida)
Duivenerwtplanten (Cajanus Cajan)
Duivenvlees - Bereid/Bewerkt
Duivenvlees - Niet-bereid/Niet-bewerkt
Duizendbladplanten (Achillea Millefolium)
Duizendpootgras (Eremochloa Ophiuroides)
Duizendschoon (Dianthus) - Snijbloem
Durianbomen (Durio zibethinus)
DVD - Opneembaar
DVD - Voorbespeeld
DVD Spelers/Recorders
Dwergbanaanstruiken (Musa acuminata - AA)
Dwergdadelpalm (Phoenix) - Levende Plant
E-boeken/Elektronische Tekst
Echeveria - Levende Plant
Echte Gamander (Teucrium Chamaedrys))
Edelspar (Abies procera)
Educatieve Diensten
Eekhoorntjesbrood
Eekhoorntjesbroodfungus (Boletus Edulis)
Eenbladige Saladegroenten (Vers Gesneden)
Eendenvlees - Bereid/Bewerkt
Eendenvlees - Niet-bereid/Niet-bewerkt
Eerste Hulp - Accessoires
Eerste Hulp - Assortimenten
Eerste Hulp - Mitella/Hulpmiddel
Eerste Hulp - Overig
Eerste Hulp - Verbandmateriaal/Verbanden/Gips
Eet- en Drankdiensten
Eetbare Bloemen
Eetbare Bloemen (Vers Gesneden)
Eetbare Oliën - Plantaardig (Beperkt Houdbaar)
Eetbare Oliën - Plantaardig (Houdbaar)
Eetbare Oliën en Vetten - Assortimenten
Eetbare Vetten - Assortimenten
Eetbare Vetten - Dierlijk (Beperkt Houdbaar)
Eetbare Vetten - Dierlijk (Houdbaar)
Eetbare Vetten - Gemengd (Beperkt Houdbaar)
Eetbare Vetten - Gemengd (Houdbaar)
Eetbare Vetten - Plantaardig (Beperkt Houdbaar)
Eetbare Vetten - Plantaardig (Houdbaar)
Eetgerei - Assortimenten
Egalisatiemortel
Eggen
Ehrhartagras (Ehrharta Stipoides)
Eierdopjes
Eieren in Schaal
Eierextracten
Eierkokers
Eikebomen (Quercus Spp)
Eikenbladsla
Eikenmos (Evernia Prunastri)
Eiproducten/Eivervangers (met Eieren)
Eivervangers (zonder Eieren)
Elandvlees - Bereid/Bewerkt
Elandvlees - Niet-bereid/Niet-bewerkt
Elektrisch Gereedschap - Handbediend Draagbaar - Onderdelen/Accessoires
Elektrisch Gereedschap - Handbediend Draagbaar - Overig
Elektrisch Gereedschap - Hef-/Transportapparatuur - Onderdelen/Accessoires
Elektrisch Gereedschap - Hef-/Transportapparatuur - Overig
Elektrisch Gereedschap - Vastgemonteerd - Onderdelen/Accessoires
Elektrisch Gereedschap - Vastgemonteerd - Overig
Elektrisch Gereedschap/Apparatuur - Assortimenten
Elektrische Bedrading
Elektrische Verbinding - Assortimenten
Elektrische Verdeling - Onderdelen/Accessoires
Elektrische Verlichting - Overig
Elektrische Zaklampen/Zaklantaarns
Elektronische Kaarten
Elektronische Organisers
Elektronische Testapparaten
Elektronische Tijdschriften en Kranten
Emmers
Emmertarweplanten (Triticum Turgidum subsp. Turanicum)
Emoevlees - Bereid/Bewerkt
Emoevlees - Niet-bereid/Niet-bewerkt
Energiediensten
Energiedranken - Gebruiksklaar
Energiedranken - Niet-gebruiksklaar
Energieopwekkende/Stimulerende Middelen
Energieopwekkende/Stimulerende Middelen - Overig
Engelentrompet (Brugmansia) - Levende Plant
Engels Gras (Armeria) - Levende Plant
Engels Raaigras (Lolium Perenne)
Enkel Blad Pinyon Den (Pinus monophylla)
Enkelbandjes
Enkelvoudig Raam (Gelamineerd Hout)
Enkelvoudig Raam (Hout)
Enkelvoudig Raam (Niet-Hout)
Enterale Voeding Gastrostomie Kits
Enterale Voeding Voedingszakken/-dozen
Enterale Voedingsbuisjes
Enterale Voedingspompen/Voedingssets
Enterale Voedingsuitrusting - Assortimenten
Enterale Voedingsuitrusting - Overig
Entertainmentdiensten
Enveloppen
Epazote/Welriekende Ganzenvoet
Epipremnum Pinnatum / Scindapsus - Levende Plant
Ereprijs / Draadereprijs / Beekpunge (Veronica) - Snijbloem
Erkerraam (Gelamineerd Hout)
Erkerramen (Hout)
Erkerramen (Niet-Hout)
Erwten
Erwten (met Peulen) (Vers Gesneden)
E-Sigaretten
E-Sigaretten - Accessoires
Esparcetteplanten (Onobrychis Viciifolia)
Etherische Oliën
Ethiopisch Haver (Avena Abyssinica)
Ethiopische banaanbomen (Ensete ventricosum)
Ethiopische Mosterd
Etiketteermachines
Etiketten/Bonnen/Tickets - Voorgedrukt
Etuis voor Potloden en Pennen
Eucalyptusbomen (Eucalyptus ssp.)
Extern geheugen voor Computer/PC's/Spelcomputers/Games
Extracten/Kruiden/Smaakversterkers (Houdbaar)
Extracten/Zout/Vlees Malsmakers (Houdbaar)
Farmaceutische samenstelling – Accessoires
Farmaceutische samenstelling - Basisproducten
Farmaceutische Samenstelling – Chemicaliën
Fashion Tape
Faxapparaat - Verbruiksartikelen
Faxapparaten
Fazantenvlees - Bereid/Bewerkt
Fazantenvlees - Niet-bereid/Niet-bewerkt
Feestartikelen - Assortimenten
Feestartikelen - Overig
Feesthoedjes
Feesttenten
Feesttoeters/Bellen
Feijoabomen (Feijoa sellowiana)
Feijoa's/Ananasguaves
Fenegriekplanten (Trigonella Foenum-Graecum)
Fiddlehead Varens
Fietsaccessoires - Computers/Navigatieapparatuur
Fietsaccessoires - Gereedschap/Bandenplakkits
Fietsaccessoires - Overig
Fietsen - Anti-diefstal Apparaten
Fietsen (Elektrisch)
Fietsen (Niet-elektrisch)
Fietsonderdelen - Banden/Wielen
Fietsonderdelen - Bellen
Fietsonderdelen - Handgrepen
Fietsonderdelen - Jasbeschermers/Spatborden
Fietsonderdelen - Kettingen
Fietsonderdelen - Lampen
Fietsonderdelen - Overig
Fietsonderdelen - Pedalen
Fietsonderdelen - Remmen
Fietsonderdelen - Standaards
Fietsonderdelen - Versnellingsysteem
Fietsonderdelen - Zadels & Zadelaccessoires
Fietssport Artikelen - Assortimenten
Fietssport Artikelen - Overig
Fietsvervoer - Bagagebinders/Snelbinders
Fietsvervoer - Kinderzitjes
Fietsvervoer - Manden/Kratten/Tassen
Figuurzaagmachines
Fijnspar (Picea abies)
Film/Filmrol
Films - Digitaal
Filters (Elektrisch) voor Zwembad/Vijver/Waterpartij
Filters voor Fototoestellen
Filters/Hoezen voor Computer/PC's/Spelcomputers/Games
Financiële Diensten
Firewalls
Fitness Accessoires
Fitness Artikelen - Assortimenten
Fitness Artikelen - Onderdelen/Accessoires
Fitness Artikelen - Overig
Fitness Meetapparatuur
Fitnessapparatuur (Elektrisch)
Fitnessapparatuur (Niet-elektrisch)
Flemingiaplanten (Flemingia Macrophylla)
Flenzen
Fles/Blik Isolatoren
Fleskalabasplanten (Lagenaria Siceraria)
Fleskalebas
Flesstoppen/Schenkkurken
Flint-mais
Flip-over Borden
Flitser voor Fotostudio
Flitsers voor Camera's
Floppy Disks
Fluitketels (Niet-elektrisch)
Fluweelblad Planten (Abutilon avicennae)
Fluweelboonplanten (Mucuna Pruriens)
Fluweelpootje/Enoki
Fluweelpootjefungus (Flammulina Velutipes)
Fondueset (Niet-Elektrisch)
Fondueset (Niet-Elektrisch) - Accessoires/Onderdelen
Fonduestellen (Elektrisch)
Fonioplanten (Digitaria Exilis)
Fopmiddelen
Fopspenen/Bijtringen
Fornuizen (Kookplaat/Oven Gecombineerd)
Fotoalbums/Kubussen
Fotografie - Assortimenten
Fotografie - Onderdelen/Accessoires
Fotografie - Overig
Fotografie/Optica - Assortimenten
Fotokopieermachines
Fotolampen voor Donkere Kamer
Fotolijsten
Fotopapier
Foto's
Fotovergrotingsapparatuur
Frambozen
Frambozenplanten (Rubus idaeus)
Frankeermachines
Frankeertoestellen (Niet–elektrisch)
Fraserspar (Abies fraseri)
Freestafels
Fresia - Snijbloem
Frisbees
Frisée (Krulandijvie)
Friteuses
Frontjes voor Mobiele Telefoon
Fruit - Bereid/Bewerkt (Beperkt Houdbaar)
Fruit - Bereid/Bewerkt (Diepvries)
Fruit - Bereid/Bewerkt (Houdbaar)
Fruit - Onbewerkt/Onverwerkt (Diepvries)
Fruit - Onbewerkt/Onverwerkt (Houdbaar)
Fruit - Onbewerkt/Onverwerkt (Vers) - Mengsels
Fruit (Vers Gesneden) - Mengsels
Fruit (Vers Gesneden) - Overig
Fruit/Groenten - Mengsels Onbewerkt/Onverwerkt (Vers)
Fruit/Groenten/Noten/Zaadjes - Assortimenten
Fruit/Noten/Zaadjes Combinatie - Assortimenten
Fruit/Noten/Zaadjes Gemengd - Bereid/Bewerkt (Houdbaar)
Fuchsia / Bellenplant - Levende Plant
Gaasmat/Wapeningsgaas
Gabion
Gagelheesters (Myrica)
Galbanumplanten (Ferula gummosa)
Gama-gras (Tripsacum spp.)
Gandariabomen (Bouea macrophylla)
Ganzenvlees - Bereid/Bewerkt
Ganzenvlees - Niet-bereid/Niet-bewerkt
Garage
Garagepoorten
Gas-/Hitte-/Rookdetectors
Gasbranders
Gasbrandstoffen
Gasflessen - Onderdelen/Accessoires
Gasflessen/-bussen onder druk (leeg)
Gastro-intestinale Middelen - Assortimenten
Gastro-intestinale Middelen - Overig
Gatenplant (Monstera) - Snijgroen
Gatenzaag
Gateways
Gazania / Middaggoud - Levende Plant
Gazon Verticuteermachines/Beluchters (Aangedreven)
Gazonbeluchters (Niet-aangedreven)
Gazonvegers (Niet-aangedreven)
Gearomatiseerde Dranken - Gebruiksklaar
Gearomatiseerde Dranken - Niet-gebruiksklaar
Gebitsprothesen/Orthodontie - Reinigingsproduct
Gebitsprothesen/Orthodontie - Verzorgingsproduct
Gebitsreiniging
Gebouw Bewakingsapparatuur - Assortimenten
Gebouw Veiligheid/Toezicht/Beveiliging - Assortimenten
Gebroken Hartjes (Dicentra) - Levende Plant
Gedroogde Broodproducten (Diepvries)
Gedroogde Broodproducten (Houdbaar)
Gedrukte Boeken/Composities
Gedrukte Kaarten
Gedrukte Tijdschriften en Kranten
Geelmelkhoutbomen (Garcinia livingstonei)
Geelrode Naaldaar (Setaria Pumila)
Geelwortelplanten (Curcuma Longa)
Gehaktmolens/Grove Zeven/Pastamachines (Niet-elektrisch)
Geheugenkaart Recorders
Geheugenkaarten
Gehoorapparaten
Gehoorbescherming - Aangedreven
Gehoorbescherming - Niet-aangedreven
Gehoornde Meloenplanten (Cucumis Metuliferus)
Geiten
Geitenvlees - Bereid/Bewerkt
Geitenvlees - Niet-bereid/Niet-bewerkt
Gekleurd Guinea-gras (Panicum Coloratum)
Gekruist Raaigras (Lolium X Hybridum)
Gelbrandstoffen
Gelderse Roos (Viburnum) - Snijbloem
Geldkistjes
Gele mombinpruimennbomen (Spondias mombin)
Gele Passievruchten (Maracuja's)
Gele Pitahayaplanten (Selenicereus megalanthus)
Gele Pitahaya's (Drakenvruchten)
Gele ribesheesters (Ribes aureum)
Gele zapotebomen (Pouteria campechiana)
Geleideprofiel voor Hoekafwerking/Pleisterwerk
Geluiddemper-/Uitlaatreparatie
Geluksbamboe (Dracaena) - Snijgroen
Gember
Gemberplanten (Zingiber Officinale)
Gemengde Dranken met Alcohol
Gemengde Soorten Vlees/Gevogelte/Wild - Bereid/Bewerkt
Gemengde Vleessoorten - Niet-bereid/Niet-bewerkt
Gemengde Worsten - Bereid/Bewerkt
Geneeskundige/Orthopedische Schoenen
Geneesmiddelen
Geneesmiddelentoediening
Geneesmiddelentoediening - Accessoires
Geneesmiddelentoediening - Assortimenten
Geneesmiddelentoediening - Onderdelen
Geneesmiddelentoediening - Overig
Generatoren
Gentiaan - Levende Plant
Gentiaanplanten (Gentiana Spp.)
Gepersonaliseerde Motorkappen
Geraldton Wasbloem (Chamelaucium) - Snijbloem
Geranium (Pelargonium) - Levende Plant
Gerbera - Levende Plant
Gerbera - Snijbloem
Gereedschap voor Drukkunst
Gereedschap voor Glasbewerking (Elektrisch)
Gereedschap voor Houtbrand/Graveerkunst (Elektrisch)
Gereedschap voor Houtbrand/Graveerkunst (Niet-elektrisch)
Gereedschap voor Kaarsen-/Zeepgieten (Elektrisch)
Gereedschap voor Kaarsen-/Zeepgieten (Niet-elektrisch)
Gereedschap voor Mandenvlechtwerk (Niet-elektrisch)
Gereedschap voor Metselwerk
Gereedschap voor Papierkunst (Niet-elektrisch)
Gereedschap/Gereedschapsets voor Computers
Gereedschappen voor Wand-/Plafondbekleding - (Aangedreven)
Gereedschapskasten
Gereedschapskisten/Gereedschapskoffers
Gereedschapsslijpers (Aangedreven)
Gereedschapswagentjes
Gerst (Hordeum) - Levende Plant
Gerstplanten (Hordeum vulgare)
Geschenkverpakking
Geschenkverpakking/Accessoires
Geschenkverpakking/Accessoires - Assortimenten
Geschenkverpakking/Accessoires - Overig
Gesponnen/Geweven Garens/Draden
Gesteelde lakzwamfungus (Ganoderma Lucidum)
Gevechtsport Artikelen - Overig
Gevechtssport Artikelen - Assortimenten
Gewasbeschermingsmiddelen
Geweren
Gewervelde Dieren - Overig
Gewone Hazelaar / Hazelnoot (Corylus) - Snijgroen
Gewone Rolklaver (Lotus) - Levende Plant
Gewone Rolklaverplanten (Lotus Corniculatus)
Gewone Spurrieplanten (Spergula Arvensis)
Gewoon barbarakruid (Barbarea Vulgaris)
Gezichtsdoeken/Zakdoeken (Wegwerpartikel)
Gezichtsreiniging/Make-up Verwijderproducten (Elektrisch)
Gezichtsreiniging/Make-up Verwijderproducten (Niet-elektrisch)
Gezinsplanning - Assortimenten
Gezondheidsbehandelingen/-hulpmiddelen - Assortimenten
Gezondheidszorg - Assortimenten
Gierstplanten (Panicum Spp.)
Gieters
Ginkgo Bilobaplanten (Ginkgo Biloba)
Ginsengplanten (Panax)
Ginsengwortel
Gips-/Cementplaat
Gipskruid (Gypsophila) - Levende Plant
Gipskruid (Gypsophila) - Snijbloem
Gipsmengsels/Gipsplaatvoegen
Gladiool / Zwaardlelie - Bol/Knol
Gladiool / Zwaardlelie - Snijbloem
Glas
Glas (Gerecycled/Hernieuwbaar)
Glas (Gevormd)
Glas (Ongevormd)
Glas Reparatiekits
Glasbouwstenen
Glasbreukmelder
Glassnijders (Niet-aangedreven)
Glasvezelverlichting
Gliricidiabomen (Gliricidia Sepium)
Gloeilampen/Buizen/LED Lampen
Gloeilampfittings
Gloeilampwisselaars
Gloeispiralen
Gloeispiralen - Assortimenten
Gloxinia (Sinningia) - Levende Plant
Goji Bessen
Gojibessenplanten (Lycium Barbarum)
Gomboom (Eucalyptus) - Snijgroen
Gootsteenontstoppers (Aangedreven)
Gordijnen
Gordijnhaken
Gordijnonderdelen/-accessoires - Assortimenten
Gordijnonderdelen/-accessoires - Overig
Gordijnrails
Gordijnroedes
Goudbesbomen (Physalis peruviana)
Goudpalm (Dypsis) - Levende Plant
Goudsbloemplanten (Calendula Officinalis)
GPS Bevestigingsapparatuur
GPS-Antennes voor Auto's
GPS-Apparatuur - Mobiele Communicatie
GPS-Software - Mobiele Communicatie
GPS-Software - Mobiele Communicatie - Digitaal
Graan-/Mueslirepen
Graanproduct/Peulvruchtproduct - Assortimenten
Graanproducten - Gebruiksklaar (Beperkt Houdbaar)
Graanproducten - Gebruiksklaar (Houdbaar)
Graanproducten - Niet-gebruiksklaar (Diepvries)
Graanproducten - Niet-gebruiksklaar (Houdbaar)
Grafische Tablets
Grafkisten
Granaatappelbomen (Punica granatum)
Granaatappels
Granen/Graanproducten - Gebruiksklaar - (Beperkt Houdbaar)
Granen/Graanproducten - Gebruiksklaar - (Houdbaar)
Granen/Graanproducten - Niet-gebruiksklaar (Beperkt Houdbaar)
Granen/Graanproducten - Niet-gebruiksklaar (Diepvries)
Granen/Graanproducten - Niet-gebruiksklaar (Houdbaar)
Granen/Meel - Assortimenten
Grapefruitbomen (Citrus paradisi)
Grapefruits/Pompelmoezen (Vlaams)
Gras/Haagscharen met Lange Snijbladen
Graskantstekers/Trimmers (Niet-aangedreven)
Graslelie (Chlorophytum) - Levende Plant
Grasmaaiers (Aangedreven)
Grasmaaiers (Niet-aangedreven)
Graswalsen (Aangedreven)
Graswalsen (Niet-aangedreven)
Graszaden
Griekse alantplanten (Inula helenium)
Grill/Braadroosters (Elektrisch)
Grills (Elektrisch)
Grind/Kiezelsteentjes
Groenbemester Zaden
Groene Bonenplanten (Phaseolus Vulgaris)
Groene kardemombomen (Elettaria Cardamomum)
Groenlofplanten (Cichorium Intybus var. Foliosum)
Groenten - Bereid/Bewerkt (Beperkt Houdbaar)
Groenten - Bereid/Bewerkt (Diepvries)
Groenten - Bereid/Bewerkt (Houdbaar)
Groenten - Onbewerkt/Onverwerkt (Diepvries)
Groenten - Onbewerkt/Onverwerkt (Houdbaar)
Groenten - Onbewerkt/Onverwerkt (Vers) - Mengsels
Groenten (Vers Gesneden) - Mengsels
Groenten (Vers Gesneden) - Overig
Groenten/Fruit - Mengsels - Vers Gesneden
Groenten/Paddenstoelen
Groentesap - Gebruiksklaar (Beperkt Houdbaar)
Groentesap - Gebruiksklaar (Houdbaar)
Groentesap - Niet-gebruiksklaar (Diepvries)
Groentesap - Niet-gebruiksklaar (Houdbaar)
Grondboren (Aangedreven)
Grondboren (Niet-aangedreven)
Grondstof (Gevormd) - Overige
Grondstof (Ongevormd) - Overige
Grondverven/Primers
Grosellabomen (Phyllanthus acidus)
Grote Brandnetelplanten (Urtica dioica)
Grote Engelwortelplanten (Angelica Archangelica)
Grote Klit (Grote Klis)
Grote Klitplanten (Arctium Lappa)
Grote Kooktoestellen - Onderdelen/Accessoires
Grote Kooktoestellen - Overig
Grote Leeuwebek (Antirrhinum) - Levende Plant
Grote Leeuwebek (Antirrhinum) - Snijbloem
Grote Wastoestellen - Onderdelen/Accessoires
Grote Wastoestellen - Overig
Grove Den (Pinus sylvestris)
Guaiacbomen (Bulnesia Sarmientoi)
Guanabana's/Zuurzakken
Guanacastebomen (Enterolobium Cyclocarpum)
Guaranaplanten (Paullinia cupana)
Guarplanten (Cyamopsis Tetragonoloba)
Guatemalteekse Spar (Abies guatemalensis)
Guavebomen (Psidium guajava)
Guaves
Guayuleplanten (Parthenium argentatum)
Guinea-gras (Panicum Maximum)
Guldenroede (Solidago) - Snijbloem
Guldenroedeplanten (Agathosma)
Gutsen
Guttaperchabomen (Palaquium sp.)
Gymnastiek Artikelen - Assortimenten
Gymnastiek Artikelen - Overig
Gymnastiektoestellen
Haagsnoeiers (Aangedreven)
Haar - Accessoires
Haar - Borstels en Kammen
Haar - Crèmespoeling/Behandeling
Haar - Hulpmiddelen(Elektrisch)
Haar - Hulpmiddelen(Niet-elektrisch)
Haar - Kleurmiddelen
Haar - Krulspelden/Haarrollers
Haar - Permanent
Haar - Shampoo
Haar - Styling (Elektrisch)
Haar - Styling (Niet-elektrisch)
Haar - Vals
Haarproducten - Assortimenten
Haaruitvalbehandelingen
Haarverzorgingsproducten - Assortimenten
Haarverzorgingsproducten - Onderdelen
Haarverzorgingsproducten - Overig
Hak-, breek- & Slijpgeleiders
Haken
Hakmachines/Versnipperaars/Mulchmachines (Aangedreven)
Halskruid (Trachelium) - Snijbloem
Hamers (DHZ)
Hamers/Bijlen - Assortimenten (DHZ)
Hamers/Bijlen - Onderdelen/Accessoires
Hammam Cabine
Hand- /Kruisbogen
Handafwas - Wasmiddel
Handboormachines
Handcirkelzagen
Handdoekstangen/-haken/-ringen - Losstaand
Handdoekstangen/-haken/-ringen - Muurbevestiging
Handdrogers
Handgereedschap/Apparatuur - Overig
Handgereedschap/Apparatuur- Assortimenten
Handgrepen
Handjesgras (Cynodon Dactylon)
Handpoppen
Handschoenen
Handsfree Kits/Koptelefoons
Handsfree/Headset - Onderdelen/Accessoires
Handwerken - Accessoires
Handwerken - Bergruimte
Handwerken - Draad/Garen
Handwerken - Gereedschap (Handmatig/Machinaal)
Handwerken - Markeringsgereedschap
Handwerken - Patronen/Sjablonen
Handwerken - Sluitingen
Handwerken - Stoffen/Textiel
Handzagen - Onderdelen/Accessoires
Hanenkam (Celosia) - Levende Plant
Hanenkam (Celosia) - Snijbloem
Hangmatten
Harbin Perenbomen (Pyrus ussuriensis)
Hard Zwenkgras (Festuca Brevipila)
Harddisk Recorder
Harde Schijven
Harde/Zachte Snoepjes
Hardgekookte Eieren (Apart)
Harken
Hausa grondnootplanten (Macrotyloma geocarpum)
Haverplanten (Avena Sativa)
Hazelnootbomen (Corylus avellana)
Hazen/Konijnen
Hazenvlees - Bereid/Bewerkt
Hazenvlees - Niet-bereid/Niet-bewerkt
Heilige Lotusplanten (Nelumbo Nucifera)
Hekschermen/Borden/Hekken
Heliotroop - Levende Plant
Helium
Helmgras (Ammophila Arenaria)
Henequen Cactussen (Agave fourcroydes)
Hengelmolens
Hengels
Hengels - Accessoires
Hengelsport Artikelen - Assortimenten
Hengelsport Artikelen - Overig
Hennabomen (Lawsonia inermis)
Hennepplanten (Cannabis sativa)
Herfsttijloosplanten (Colchicum Autumnale)
Herikplanten (Sinapis Arvensis)
Hertenvlees, behalve Reevlees - Bereid/Bewerkt
Hertenvlees, behalve Reevlees - Niet-bereid/Niet-bewerkt
Heteluchtpistolen
Hijstoestellen/Lieren
Hin Choy/Chinese Spinazie
Hoekbeschermers
Hoekmeetapparaten (Aangedreven)
Hoekslijpmachines
Hoesjes voor Mobiele Telefoon
Hoezen Reservebanden
Hogedrukreiniger - Onderdelen/Accessoires
Hogedrukreinigers (Aangedreven)
Hoja Santa/Heilige Bladpeper
Hoja Santaplanten (Piper Auritum )
Hokjespeulplanten (Astragalus)
Home Audio-versterkers/Voorversterkers
Home Stereosystemen
Homeopathische Middelen - Combinatie Ingrediënten
Homeopathische Middelen - Individuele Ingrediënten
Honden
Honderdjarige Aloë Cactussen (Agave americana)
Honing (Houdbaar)
Honingpomelo's
Honingvervangers
Hoofddeksels
Hoofdkussens
Hooivorken (Tuin)
Hopklaverplanten (Medicago Lupulina)
Hopplanten (Humulus lupulus)
Horizontale Jaloezieën
Horloges
Horloges - Onderdelen/Accessoires
Horloges - Overig
Hormonale Anticonceptiva
Horren
Horren - Onderdelen/Accessoires
Hortensia (Hydrangea) - Levende Plant
Hortensia (Hydrangea) - Snijbloem
Hortensia (Hydrangea) - Snijgroen
Hosta - Levende Plant
Hotdogrollers
Houders voor Borden
Houders/Standaards voor Muziekinstrumenten
Hout (Gerecycled/Hernieuwbaar)
Hout (Gevormd)
Hout (Ongevormd)
Houtafwerking/-behandelingen/-deklagen
Houtbrand/Graveerkunst - Onderdelen/Accessoires
Houten Blaasinstrumenten (Elektrisch)
Houten Blaasinstrumenten (Niet-elektrisch)
Houten/Rubberen Hamers (DHZ)
Houtkloofmachines (Aangedreven)
Huid/Hoofdhuid Behandelingsproducten - Assortimenten
Huid/Hoofdhuidbehandelingsproducten - Overig
Huidproducten - Assortimenten
Huidverlichting
Huidverzorging - Assortimenten
Huidverzorging - Onderdelen
Huidverzorging - Overig
Huidverzorging/Vochtinbrengende Producten
Huis Textiel - Assortimenten
Huis/Kantoor - Assortimenten
Huis/Kantoor Banken (Elektrisch)
Huis/kantoor bar/toonbank/aanrecht
Huis/Kantoor Dozen/Manden
Huis/Kantoor Kasten/Vitrines - Assortimenten
Huis/Kantoor Kasten/Vitrines - Onderdelen/Accessoires
Huis/Kantoor Kasten/Vitrines - Overig
Huis/Kantoor Meubilair/Inrichting/Beddengoed - Assortimenten
Huis/Kantoor Scheidingen/Schermen
Huis/Kantoor Schrijftafels/Werkstations
Huis/Kantoor Slaapbanken
Huis/Kantoor Stoelen/Krukken (Elektrisch)
Huis/Kantoor Stoelen/Krukken (Niet-elektrisch)
Huis/Kantoor Tafels
Huis/Kantoor Tafels/Bureaus - Assortimenten
Huis/Kantoor Tafels/Bureaus - Onderdelen/Accessoires
Huis/Kantoor Tafels/Bureaus - Overig
Huis/Kantoor Textiel - Overig
Huis/Kantoor Vitrine-/uitstalkasten
Huis/Kantoor Voetsteunen
Huis/Kantoor Zitbanken (Niet-elektrisch)
Huis/Kantoor Zitmeubelen - Assortimenten
Huis/Kantoor Zitmeubelen - Onderdelen/Accessoires
Huis/Kantoor Zitmeubelen - Overig
Huis-/kantoortelefoon
Huishoud Boilers/Verwarmingsketels/Geisers
Huishoud Boilers/Verwarmingsketels/Geisers - Onderdelen/Accessoires
Huishoud Organisers/Opbergbakjes
Huishoudelijke Schoonmaakmiddelen
Huishoudelijke Schoonmaakproducten – Assortimenten
Huishoudelijke Stofzuigers
Huishoudsponzen
Huisidentificatie - Nummers/Letters
Huislook (Sempervivum) - Levende Plant
Huisvesting/Verblijfplaats voor dieren
Hulpmiddelen Invaliditeit
Hulpmiddelen tegen Vermoeidheid (DHZ)
Hulpmiddelen voor Babyvoeding - (Niet-elektrisch)
Hulpmiddelen voor Babyvoeding (Elektrisch)
Hulpmiddelen voor Meten en Geometrie
Hulpmiddelen voor Stoot- en Traptrainingen
Hulpmiddelen voor Voetverzorging/Hygiëne
Hulpmiddelen voor Wand-/Plafondbekleding - Niet-aangedreven
Hulpmiddelen voor Zwemtraining
Hulpmiddelen/Toebehoren voor Aquaria
Hulpmiddelen/Toebehoren voor Terraria
Hulst (Ilex) - Snijbloem
Hulst (Ilex) - Snijgroen
Huttentutplanten (Camelina Sativa)
Huzarenknoop (Sanvitalia) - Levende Plant
Hyacint - Bol/Knol
Hyacint - Levende Plant
Hyacint - Snijbloem
Hybride pruimenbomen(Prunus hybrids)
Hybriden van Steenvruchten
Hygiëne/Gezondheidsbescherming voor Dieren
Hygiënische en Schoonheidsverzorging Diensten
Hygrometers - Elektrisch
Hygrometers - Niet-elektrisch
Hygrometers/Psychrometers - Elektrisch
Hypericum X Inodorum (o.a. Annebel, Elstead, Excellent Flair, Rheingold) - Snijbloem
Hysop
Hysopplanten (Hyssopus Officinalis)
Iburuplanten (Digitaria Iburua)
IJs (Diepvries)
IJs (Houdbaar)
IJs-/Verwarmingszak
IJs-/Wijnemmers
IJsbereiders (Elektrisch)
IJsbergsla
IJsblokjes
IJsdrankmachines/IJsmalers (Elektrisch)
IJskruid (Dorotheanthus) - Levende Plant
IJslandse Papaver - Levende Plant
IJsmachines
IJsmalers/IJsblokjesmakers (Elektrisch)
IJsplanten (Mesembryanthemum Crystallinum)
IJzer (Gerecycled/Hernieuwbaar)
IJzer (Gevormd)
IJzer (Ongevormd)
IJzerhard (Verbena) - Levende Plant
Ijzerhardplanten (Verbena)
Ilamabomen (Annona diversifolia)
Imbubomen (Spondias Tuberosa)
Inbakerdoek/Wikkeldoek
Inbindmachines (Elektrisch)
Inbindmachines (Niet-elektrisch)
Inbussleutels
Incalelie / Peruviaanse Lelie (Alstroemeria) - Levende Plant
Incalelie / Peruviaanse Lelie (Alstroemeria) - Snijbloem
Incontinentie bij Volwassenen - Assortimenten
Incontinentie bij Volwassenen - Benodigdheden
Incontinentie bij Volwassenen - Maandverbanden
Incontinentie bij Volwassenen - Ondergoed (Geen Wegwerpartikel)
Incontinentie bij Volwassenen - Ondergoed (Wegwerpartikel)
Incontinentie bij Volwassenen - Overig
Incontinentie kinderen - Assortimenten
Incontinentie kinderen - Luiers (herbruikbaar)
Incontinentie kinderen - Luiers (wegwerp)
Incontinentie kinderen - Ondergoed (herbruikbaar)
Incontinentie kinderen - Ondergoed (Wegwerp)
Incontinentie kinderen - Overig
Incontinentie kinderen - Verband
Indiaans-rijstgras (Oryzopsis Hymenoides)
Indiase jujubebomen (Ziziphus mauritiana)
Indiase kruisbesbomen (Phyllanthus emblica)
Indiase pruimenbomen (Flacourtia indica)
Indigoplanten (Indigofera Spp.)
Indigoplanten (Indigofera tinctoria)
Indisch Bloemriet (Canna) - Levende Plant
Indisch Vlas Planten (Abroma augustum)
Indische Amandelbomen (Terminalia catappa)
Indische Limoenen
Industriële constructies
Industriële drijvende loopbruggen
Industriële Drijvers
Industriële Gassen - Overig
Industriële Nat/Droog Stofzuigers
Industriële Nat/Droog Stofzuigers - Buizen/Slangen
Industriële Nat/Droog Stofzuigers - Filters
Industriële Nat/Droog Stofzuigers - Mondstukken
Industriële pompen - elektromotoren
Industriële pompen - verbrandingsmotoren
Industriële pompen – vervangende onderdelen/accessoires
Industriële vangrails
Industriële Vloerreiniging - Aangedreven
Industriële Vloerreiniging - Accessoires
Industriële vlotdeksels/afdekkingen
Industriële vlotten
Infraroodcabine
Ingelegde Groenten
Inhaleertoestellen/Nevelapparaten/Ademhalingstoestellen (Elektrisch)
Inhaleertoestellen/Nevelapparaten/Ademhalingstoestellen (Niet-elektrisch)
Inkarnaatklaverplanten (Trifolium Incarnatum)
Inkt
Insecten
Insecten - Andere - bereid/bewerkt
Insecten - andere - Niet-bereid/Niet-bewerkt
Insecten - Gemengde soorten - bereid/bewerkt
Insecten - Gemengde soorten - Niet-bereid/Niet-bewerkt
Insecten-/Ongediertebestrijding - Assortimenten
Insecten-/Ongediertebestrijding - Barrières/Vallen
Insecten-/Ongediertebestrijding - Overig
Insectenwerende Middelen - Niet voor Persoonlijk Gebruik
Insecticiden/Pesticiden voor Tuin
Insecticiden/Pesticiden/Verdelgingsmiddelen
Inspectiecamera/Endoscoop (DIY)
Installatiediensten
Instrumentenborden/-frames
Intercoms
Intermediate Bulk Container (IBC) (Leeg)
Internet-Televisie Accessoires
Inzetstukken voor Grille
Iris - Bol/Knol
Iris / Lis / Gele Lis / Zwaardlelie - Snijbloem
Isolatie - Assortimenten
Isolatie - Isolatieplaten/Rollen/Dekens
Isolatie - Leidingbekleding
Isolatie - Losse Vulling/Sprayschuim
Isolatie - Overig
Isolatie - Steunstukken/Ankers
Isolatie - Stralingsbarrières/Hitteschermen
Isolatiepistolen (Niet aangedreven)
Italiaans Raaigras (Lollium Multiflorum)
Jaboticababomen (Myrciaria cauliflora)
Jachtgeweren
Jachthulpmiddelen – schoonmaken van prooi
Jachtsport Accessoires - Assortimenten
Jachtsport Accessoires - Overig
Jackboonplanten (Canavalia Ensiformis)
Jacuzzi/Badmassage
Jalapplanten (Ipomea purga)
Jam/Marmelade (Houdbaar)
Jam/Marmelade/Fruitbeleg (Beperkt Houdbaar)
Jambolans
Japans-bloedgras (Imperata Cylindrica)
Japanse Abrikozen
Japanse Andoorn
Japanse Anemoon / Herfstanemoon - Levende Plant
Japanse Gierstplanten (Echinochloa Frumentacea)
Japanse Haverplanten (Avena Strigosa)
Japanse mispelbomen (Eriobotrya japonica)
Japanse Mispels/Loquats
Japanse Pruimen
Japanse Wijnbesplanten (Rubus Phoenicolasius)
Jaraguagras (Hyparrhenia Rufa)
Jarretels/Kousenbanden
Jasjes/Blazers/Vesten/Hesjes
Jasmijnplanten (Jasminum officinale)
Javaanse Amandelbomen (Canarium indicum)
Jeffrey Den (Pinus jeffreyi)
Jeneverbesstruiken (Juniperus Communis)
Jengkolbomen (Archidendron jiringa)
Jerrycans en Accessoires
Jistabesstruiken (Ribes X Nidigrolaria)
Job's Tranengras (Coix Lacryma-jobi)
Jobs-tranenplanten (Coix Lacryma-Jobi)
Johannesbrood/Carob
Johannesbroodbomen (Ceratonia Siliqua)
Jojobaplanten (Simmondsia Chinensis)
Jostabessen
Juridische Diensten
Jurken
Jutestruiken (Corchorus)
Juwelendozen/-Zakjes
Kaalknopkruidplanten (Galinsoga Parviflora)
Kaaps Viooltje (Saintpaulia) - Levende Plant
Kaapse Jasmijn (Gardenia) - Levende Plant
Kaapse Malva (Anisodontea) - Levende Plant
Kaarsen
Kaartlezers
Kaartspelen (Elektrisch)
Kaartspelen (Niet-elektrisch)
Kaas (Beperkt Houdbaar)
Kaas (Diepvries)
Kaas (Houdbaar)
Kabel-/Draadtrekkers
Kabelbuisfittingen
Kabelhaspels
Kabelklemmen/-ringen/Tie Wraps
Kabelmerkers
Kabelsets/Kabelbomen
Kafferkorenplanten (Sorghum Bicolor)
Kai-Lan/Chinese Broccoli
Kai-lanplanten (Brassica Oleracea var. Alboglabra)
Kakibomen (Diospyros kaki)
Kaki's/Sharonvruchten
Kalanchoë - Levende Plant
Kalebassen
Kalenders/Planners
Kalfsvlees - Bereid/Bewerkt
Kalfsvlees - Niet-bereid/Niet-bewerkt
Kalk (DHZ)
Kalkoenenvlees - Bereid/Bewerkt
Kalkoenenvlees - Niet-bereid/Niet-bewerkt
Kalkremmers/waterontharders
Kalmerend Middel bij Insectenbeten
Kalmoesplanten (Acorus Calamus)
Kamalabomen (Mallotus philippensis)
Kamerden (Araucaria heterophylla)
Kamerjasmijn (Jasminum) - Levende Plant
Kamerverwarmingstoestellen
Kamferbomen (Cinnamomum camphora)
Kamgras (Cynosurus Cristatus)
Kampeer Koelboxen/-Tassen
Kampeer Water-/Drank Apparatuur
Kampeer WC's (Elektrisch)
Kampeer WC's (Niet-elektrisch)
Kampeerbedden/Slaapmatten
Kampeerdouches
Kampeerkasten
Kampeerkookgerei
Kampeerkooktoestellen
Kampeermeubilair/Artikelen - Assortimenten
Kampeermeubilair/Artikelen - Overig
Kampeerstoelen
Kampeertafelgerei
Kampeertafels
Kampeertentaccessoires
Kampeertenten
Kampeertenten - Assortimenten
Kampeertenten - Overig
Kampeertentuitbreidingen
Kampeeruitrusting - Verlichting
Kampeeruitrusting - Verwarming/Verlichting - Assortimenten
Kampeeruitrusting - Verwarming/Verlichting - Overig
Kampeeruitrusting - Waterverwarmers
Kampeeruitrusting Koken/Drinken/Eten - Assortimenten
Kampeeruitrusting Koken/Drinken/Eten - Onderdelen/Accessoires
Kampeeruitrusting Koken/Drinken/Eten - Overig
Kampeeruitrusting Was-/Sanitaire Voorzieningen - Assortimenten
Kampeeruitrusting Was-/Sanitaire Voorzieningen - Onderdelen/Accessoires
Kampeeruitrusting Was-/Sanitaire Voorzieningen - Overig
Kampeeruitrusting Waterzuiveringsproducten
Kamperen - Assortimenten
Kamstatice (Limonium) - Snijbloem
Kanariegras (Phalaris spp.)
Kanariezaadplanten (Phalaris Canariensis)
Kandelaars/Accessoires
Kaneelbomen (Cinnamomum Verum)
Kaneelvarens
Kanonneerplant (Pilea) - Levende Plant
Kant/Linten/Koorden/Vlechten
Kant-en-klaarmaaltijden - Direct Gebruik - Assortimenten
Kant-en-klaarmaaltijden - Direct Gebruik (Beperkt Houdbaar)
Kant-en-klaarmaaltijden - Direct Gebruik (Houdbaar)
Kant-en-klaarmaaltijden - Niet Direct Gebruik - Assortimenten
Kant-en-klaarmaaltijden - Niet Direct Gebruik (Beperkt Houdbaar)
Kant-en-klaarmaaltijden - Niet Direct Gebruik (Diepvries)
Kant-en-klaarmaaltijden - Niet Direct Gebruik (Houdbaar)
Kantoorapparaten - Assortimenten
Kantoorapparaten - Overig
Kantoorartikelen - Lijmen / Ringmappen / Nietapparatuur - Assortimenten
Kantoorartikelen - Lijmen / Ringmappen / Nietapparatuur - Overig
Kantoorartikelen - Opslag/Archivering - Assortimenten
Kantoorartikelen - Opslag/Archivering - Onderdelen/Accessoires
Kantoorartikelen - Opslag/Archivering - Overig
Kantoorartikelen - Papier/Karton/Vellen - Assortimenten
Kantoorartikelen - Papier/Karton/Vellen - Overig
Kantoorartikelen - Snijapparaten / Versnipperaars / Perforators - Assortimenten
Kantoorartikelen - Snijapparaten / Versnipperaars / Perforators - Overig
Kantoorbenodigdheden - Bevestigingsmiddelen
Kantoorbenodigdheden - Lijmen
Kantoorbenodigdheden - Nietmachines (Elektrisch)
Kantoorbenodigdheden - Nietmachines (Niet-elektrisch)
Kantoorbenodigdheden - Ordners/Mappen/Portefeuilles
Kantoorbenodigdheden - Plakbanden
Kantoorbenodigdheden - Scharen
Kantoorbenodigdheden - Verwijderproducten voor Nietjes
Kantoorbenodigdheden/Kantoorapparaten - Assortimenten
Kantoorbenodigdheden/Kantoorapparaten/Schrijfwaren - Overig
Kantoorbenodigdheden/Kantoorapparaten/Schrijfwaren/Feestartikelen - Assortimenten
Kapokbomen (Ceiba pentandra)
Kapokstruiken (Aerva Javanica)
Kappertjesstruiken (Capparis Spinosa)
Karamel-/Chocoladeappels
Kardoen
Kardoenplanten (Cynara Cardunculus)
Karwijplant
Karwijplanten (Carum Carvi)
Kassa's/Geldregisters (Elektrisch)
Kastanjebomen (Castanea sativa)
Katrollen en Riemaandrijvingen
Katten
Katten-/Hondenluiken
Kattengras (Cyperus) - Levende Plant
Kauwgom
Kavaheesters (Piper methysticum)
Kekerplanten (Cicer Arietinum)
Kelderluikdeuren
Kenafplanten (Hibiscus cannabinus)
Kentiapalm (Howea) - Levende Plant
Keramiekovens - elektrisch
Kerrieplanten (Helichrysum Italicum)
Kerrieplanten (Murraya Koenigii)
Kerstcactus (Schlumbergera) - Levende Plant
Kerstroos (Helleborus) - Levende Plant
Kerstster (Euphorbia) - Levende Plant
Kervel
Kervelplanten (Anthriscus Cerefolium)
Ketels (Elektrisch)
Kettingen/Halsbandjes
Kettingzagen (Aangedreven)
Keuken - Blendermachine
Keuken - Gecombineerde Machine
Keuken - Hakmachine
Keuken - Mixmachine
Keuken - Snijmachine
Keuken Snij-/Rasp-/Haktoestellen
Keuken Was-/Spoelmachines - Onderdelen/Accessoires
Keuken Was-/Spoelmachines - Overig
Keuken-/werkhandschoenen
Keukengerei - Assortimenten
Keukenmessen/Hakmessen
Keukenmessenslijpers (Niet-elektrisch)
Keukenopslag - Assortimenten
Keukenopslag - Onderdelen/Accessoires
Keukenopslag - Overig
Keukenopslag Rekken/Staanders/Houders/Dispensers
Keukenscharen
Keukentrapjes/Opstapjes
Keukenweegschalen (Elektrisch)
Keukenweegschalen (Niet-elektrisch)
Kevers - Bereid/bewerkt
Kevers - Onvoorbereid/Onbewerkt
Keyboards/Piano's (Elektrisch)
Keyboards/Piano's (Niet-elektrisch)
Kijkspeelgoed (Elektrisch)
Kijkspeelgoed (Niet-elektrisch)
Kikkerbillen - Bereid/Bewerkt
Kikkerbillen - Niet-bereid/Niet-bewerkt
Kikkererwten
Kikkererwten (Vers Gesneden)
Kikuyu-gras (Pennisetum Clandestinum)
Kinabomen (Cinchona)
Kinaplanten (Cinchona)
Kinderwagen/Wandelwagen/Buggy - Accessoires
Kinderwagens/Wandelwagens/Buggy's
King mandarijnenbomen (Citrus nobilis)
King of Siam Mandarijnen
Kippenvlees - Bereid/Bewerkt
Kippenvlees - Niet-bereid/Niet-bewerkt
Kit voor Alcoholverrijking door middel van Aroma
Kitpistolen (Niet-aangedreven)
Kits voor Alcoholvervaardiging
Kits voor Noodsituaties langs de Weg
Kitspuiten (Aangedreven)
Kittelbloemplanten (Clitoria Ternatea)
Kiwano's
Kiwi’s (Vers Gesneden)
Kiwifruitbomen (Actinidia deliciosa)
Kiwi's
Kleding - Assortimenten
Kleding voor Bovenlichaam - Assortimenten
Kleding voor Dieren
Kleding voor het hele Lichaam - Assortimenten
Kleding voor het Onderlichaam - Assortimenten
Kleding Vouwmachine (Elektrisch)
Kleding Vouwplank (Niet-elektrisch)
Kleding-/Opbergkasten
Kledingaccessoires - Assortimenten
Kledingroller
Kledingsieraden/Pins/Badges/Gespen
Kleefgips
Kleerhangers
Klein Keukenmateriaal - Assortimenten
Klein Keukenmateriaal - Overig
Kleine Bevernel
Kleine Honingklaverplanten (Melilotus Indicus)
Kleine Huishoudapparaten - Overig
Kleine Kooktoestellen - Onderdelen/Accessoires
Kleine Kooktoestellen - Overig
Kleine veenbesplanten (Vaccinium oxycoccos)
Klemmen
Klerenpersen
Kleurbeschermend middel
Kleurversnellende Producten
Klimaatregelaars - Draagbaar
Klimaatregelingsapparatuur - Multifunctioneel - Draagbaar
Klimop (Hedera) - Levende Plant
Klinknagelmachines
Klinknagels
Klokbilzekruidplanten (Scopolia Carniolica)
Klokken
Klokken - Onderdelen
Klokmimosaplanten (Dichrostachys Cinerea)
Klokradio's
Klopboormachines
Klysma's/Spoelingen
Knaagdieren
Knalbonbons (Crackers)
Kniebeschermers
Knippabomen (Meliococcus Bijgatus)
Knoflook
Knoflookplanten (Allium sativum)
Knolcapucien
Knolcapucienplanten (Tropaeolum Tuberosum)
Knolcyperusplanten (Cyperus Esculentus)
Knolrapen (Meirapen)
Knolribzaad/Knolkervel
Knolselderij
Knolvenkel (subspecies azoricum)
Knoopkruidplanten (Centaurea)
Kodo-gierst (Paspalum Scrobiculatum)
Koel/Vriestoestellen - Onderdelen/Accessoires
Koel/Vriestoestellen - Overig
Koeling/Verwarming Combinaties
Koelkasten
Koelmiddelen voor Airconditioning
Koffers/Tassen/Hoezen voor Muziekinstrumenten
Koffie - Capsules/Pads
Koffie - Gemalen Bonen
Koffie - Hele Bonen
Koffie - Oplos/Instant
Koffie - Vloeibaar/Gebruiksklaar
Koffie - Vloeibaar/Niet-gebruiksklaar
Koffie/Thee/Vervangingsmiddelen - Assortimenten
Koffiebranders
Koffieheesters (Coffea)
Koffiemolens (Elektrisch)
Koffieplant (Coffea) - Levende Plant
Koffievervangingsmiddel - Capsules/Pads
Koffievervangingsmiddel - Gemalen/Infusie
Koffievervangingsmiddel - Oplos/Instant
Koffievervangingsmiddel - Vloeibaar/Gebruiksklaar
Kokerbromelia (Aechmea) - Levende plant
Kokerbromelia / Bromelia (Guzmania) - Levende Plant
Kokosnootpalmbomen (Cocos nucifera)
Kokospalm / Klapperboom (Cocos) - Levende Plant
Kokumbomen (Garcinia indica)
Kolokwintplanten (Citrullus Colocynthis)
Kolomboormachines
Komatsunaplanten (Brassica Perviridis)
Komijnplanten (Cuminum Cyminum)
Komkommer (Cucumis) - Snijgroen
Komkommerkruid/Bernagie
Komkommerplanten (Cucumis Sativus)
Komkommers
Komkommers (Vers Gesneden)
Kommen (Niet Wegwerp)
Kommen voor Voedselbereiding
Konijnenvlees - Bereid/Bewerkt
Konijnenvlees - Niet-bereid/Niet-bewerkt
Koninginnekruid / Leverkruid (Eupatorium) - Snijgroen
Koningsoesterzwam/Eryngii
Koningsvarens
Konjakplanten (Amorphophallus Konjac)
Kookgerei/Bakgerei - Assortimenten
Kookgerei/Bakgerei - Onderdelen/Accessoires
Kookgerei/Bakgerei - Overig
Kookplaten/Kookstellen
Kooktoestellen - Assortimenten
Kookwekkers (Elektrisch)
Kookwekkers (Niet-elektrisch)
Kookwijnen
Kool / Sierkool (Brassica) - Levende Plant
Kool / Sierkool (Brassica) - Snijgroen
Kooldioxide
Koolraapplanten (Brassica Napobrassica)
Koolrabi
Koolrabiplanten (Brassica Oleracea var. Gongylodes)
Koolrapen (Rutabagas)
Koolsoorten (Vers Gesneden)
Koolstofvezel (Gevormd)
Koolzaadplanten (Brassica Napus)
Koper (Gerecycled/Hernieuwbaar)
Koper (Gevormd)
Koper (Ongevormd)
Koperen Muziekinstrument Accessoires (Niet-elektrisch)
Koperen Muziekinstrumenten (Elektrisch)
Koperen Muziekinstrumenten (Niet-elektrisch)
Koplamparmaturen
Koppelingsstukken voor Aanhangwagen
Koptelefoons
Koptelefoons voor Computer/PC's/Spelcomputers/Games
Koraal/Zeeanemonen
Koraalbomen (Erythrina Spp.)
Koreaanse Zilverspar (Abies koreana)
Koriander
Korianderplanten (Coriandrum Sativum)
Korte Snoeischaren (Takjes/Bloemen)
Kousebandplanten (Vigna Unguiculata subsp. Sesquipedalis)
Kousenband/Aspergebonen
Kraaienpootgras (Dactyloctenium Aegyptium)
Kraaiheiplanten (Empetrum nigrum)
Kraakbesheesters (Vaccinium membranaceum)
Kranen
Kranen - Onderdelen/Accessoires
Krasverwijderaars
Krentenbomen (Amelanchier)
Krokus - Bol/Knol
Kromme Komkommers
Kropaar (Dactylis Glomerata)
Kropsla (Vers Gesneden)
Kropsla/Botersla
Kropslaplanten (Lactuca Sativa var. Capitata)
Krotonbomen (Croton tiglium)
Kruiden (Vers Gesneden)
Kruiden Pruimtabak/Snuiftabak - Geen tabak
Kruiden/Conserveringsmiddelen/Extracten - Assortimenten
Kruiden/Specerijen (Beperkt Houdbaar)
Kruiden/Specerijen (Diepvries)
Kruiden/Specerijen (Houdbaar)
Kruiden/Specerijen/Extracten - Assortimenten
Kruidenmengsels (Verse Kruidenplanten)
Kruidensigaretten - Geen tabak
Kruidnagelbomen (Syzygium Aromaticum)
Kruimeldief
Kruipbraamstruiken(Rubus Chamaemorus)
Kruisbes (Ribes Uva-Crispa)
Kruisbessen
Kruisdisteloesterzwamfungus (Pleurotus Eryngii)
Kruiwagens - Aangedreven
Kruiwagens - Niet-aangedreven
Krulpeterselie
Krulslaplanten (Lactuca Sativa var. Crispa)
Kumquatbomen (Citrus japonica)
Kumquats
Kunst/Ambacht - Assortimenten
Kunstbloemen/-planten/-bomen
Kunstgras
Kunstkerstboom (Elektrisch)
Kunstkerstboom (Niet-elektrisch)
Kunstkerstkrans en Slinger (Elektrisch)
Kunstkerstkrans en Slinger (Niet-elektrisch)
Kunstmatige Omhulsels
Kunststoffen (Gerecycled/Hernieuwbaar)
Kunststoffen (Gevormd)
Kunststoffen (Ongevormd)
Kunzeastruiken (Kunzea)
Kurkentrekkers/Flesopeners (Elektrisch)
Kurrat
Kurratplanten (Allium kurrat)
Kussenhoezen
Kussenslopen
Kuwinibomen (Mangifera odorata)
KVM-Switch
Kwallen
Kwartelvlees - Bereid/Bewerkt
Kwartelvlees - Niet-bereid/Niet-bewerkt
Kwartjesplant (Aspidistra) - Snijgroen
Kweek (Elymus repens)
Kweepeerbomen (Cydonia oblonga)
Kweeperen
Laarzen - Algemeen Gebruik
Labdanumstruiken (Cistus ladanifer)
Lablabplanten (Lablab Purpureus)
Lacatan banaanstruiken (Musa acuminata × M. balbisiana - AA Group - Lacatan)
Lachgas (Distikstofoxide)
Ladder Onderdelen/Accessoires
Ladders/Opstapjes
Lademat/Contactpapier
Ladenkasten/Laden
Lagers/Bussen
Lakken
Lama-/Alpacavlees - Bereid/Bewerkt
Lama-/Alpacavlees - Niet-bereid/Niet-bewerkt
Lamellendeuvels
Lamellenfrezen
Laminaatzagen – elektrisch
Lamineermachines - verbruiksmaterialen
Lamineermachines (Elektrisch)
Lampenkappen
Lampepoetsersgras / Borstelveergras (Pennisetum) - Levende Plant
Lampionplant (Physalis) - Snijgroen
Lampstandaards/Voetstukken
Lamsoor/Zeelavendel/Zeeaster
Lamsvlees - Bereid/Bewerkt
Lamsvlees - Niet-bereid/Niet-bewerkt
Landslak - Bereid/Bewerkt
Landslak - Niet-bereid/Niet-bewerkt
Lange Peperplanten (Piper Longum)
Langsatbomen (Lansium domesticum)
Laosplanten (Alpinia Galanga)
Lasapparaten met Vlamboog
Lasbranders/Soldeerlampen
Lasbranders/Soldeerlampen - Lasstaven/Lasdraden/Soldeer
Lasbranders/Soldeerlampen - Onderdelen/Accessoires
Lashelmen/Helmen – Aangedreven
Lashelmen/Helmen - Niet-aangedreven
Lasmaskers/Gezichtsbeschermkappen
Lathyrusplanten (Lathyrus Sativus)
Latten / Regels
Latundan of appel banaanstruiken (Musa acuminata × M. balbisiana (AAB Group) Silk)
Latwerk
Laurier
Laurierplanten (Laurus Nobilis)
Lavas/Maggiplant
Lavendelplanten (Lavandula Augustifolia)
Lavsplanten (Levisticum Officinale)
Laxeermiddelen
Led strips en Vervangende onderdelen / accessoires
Ledumplanten (Ledum groenlandicum)
Leefgebied c.q. onderkomen
Leersia-gras (Leersia Hexandra)
Leidingboosters
Leidingen/Buizen/Goten voor Bekabeling/Bedrading
Leidingontstoppers
Lelie - Bol/Knol
Lelie (Lilium) - Levende Plant
Lelie (Lilium) - Snijgroen
Lelietjes-van-dalenplenten (Convallaria Majalis)
Lente-uitjes
Lente-uitjesplanten (Allium cepa var. cepa)
Lepelplant (Spathiphyllum) - Levende Plant
Leucadendron - Snijgroen
Levantknoflookplanten (Allium ampeloprasum)
Levende Planten - Assortimenten
Levende Planten - Overig
Levensmiddelen/Drank Verwarmingstoestellen (Niet-elektrisch)
Levensmiddelen/Dranken/Rookwaren - Assortimenten
Libellen - Niet-bereid/Niet-bewerkt
Lichaamsbeschermers
Lichaamshaar Bleek-/Maskeermiddelen
Lichaamsmassage/Spierstimulatoren - Assortimenten
Lichaamsmassage/Spierstimulatoren - Onderdelen
Lichaamsmassage/Spierstimulatoren - Overig
Lichaamsreiniging - Assortimenten
Lichaamsreiniging - Overig
Lichaamsverzorgingsproducten - Assortimenten
Licht-/Bewegings-/Geluidssensoren
Lichteffecten op Basis van Geluid
Lichtkettingen/-buizen
Lichtmeters - Elektrisch
Lichtschachten
Liefdegras (Eragrostis spp.)
Lieren/Accessoires van Lieren - Assortimenten
Lieren/Accessoires van Lieren - Overig
Liften/Takels/Hefbomen
Lijm/Kleefstof
Lijmpistolen - Aangedreven
Lijnen/Halsbanden/Harnassen voor Huisdieren (Niet-elektrisch)
Lijsterbesbomen (Sorbus domestica)
Likeuren
Lila Tayers
Limabonen/Boterbonen
Limaboonplanten (Phaseolus Lunatus)
Limequats
Limetten
Limetten bomen (Citrus limetta)
Limoenbomen (Citrus aurantifolia)
Limpo-gras (Hemarthria Altissima)
Lindebomen (Tilia)
Lindheimer's Kaars / Prachtkaars (Gaura) - Levende Plant
Lingzhi's/Reishi's
Linzen
Linzeplanten (Lens Culinaris)
Lipbalsems
Lisianthus (Eustoma) - Snijbloem
Liverseed-gras (Urochloa Panicoides)
Lobbenpompen
Lobelia - Levende Plant
Loekoentoegras (Ischaemum spp.)
Loganbesheesters (Rubus x loganobaccus)
Loganbessen
Lokmiddelen/Lokvogels/Roepinstrumenten
Lollo Bionda
Lollo Rosso
Longanbomen (Dimocarpus longan)
Longans (Drakenogen)
Loodjes
Losse Onderdelen
Losse/Meervoudige Slabladeren - Overig
Losse/Meervoudige Slabladeren (Vers Gesneden)
Losstaande Lampen
Loten / Kraskaarten
Lotonis bainesiiplanten (Lotononis Bainesii)
Lotuswortel
Low-noise Signaalconverters (LNB)
Lubricatie van de intieme delen
Lucht Yamplanten (Dioscorea Bulbifera)
Lucht-/Textielverfrissers - Assortimenten
Lucht-/Textielverfrissers - Overig
Luchtbevochtigingsapparaten - Draagbaar
Luchtbevochtigingsapparaten - Vast
Luchtbuksen
Luchtcompressoren - Draagbaar
Luchtcompressoren - Vastgemonteerd
Luchtfilter Reiniger
Luchthoorns/Misthoorns
Luchtionisators - Draagbaar
Luchtkanalen - Assortimenten
Luchtkanalen - Onderdelen en Accessoires
Luchtkanalen/Luchtkanalen Fittingen
Luchtkoelers - Draagbaar
Luchtleidingen/-kanalen
Luchtmeetapparatuur
Luchtontvochtiger - Draagbaar (Niet-elektrisch)
Luchtontvochtigingsapparaat - Draagbaar (elektrisch)
Luchtontvochtigingsapparaten - Vast
Luchtvaartuig
Luchtverfrissers (Aangedreven)
Luchtverfrissers (Niet-aangedreven)
Luchtverwarmingstoestellen - Draagbaar
Luchtvrachtcontainers (Leeg)
Luchtzuiveringsapparatuur - Draagbaar
Luchtzuiveringsinstallaties/Ionisators - Vast
Luciferplantje / Mexicaanse Heide (Cuphea) - Levende Plant
Lucumabomen (Pouteria lucuma)
Ludwigia - Levende Plant
Luffa
Luffaplanten (Luffa)
Lulo/Naranjilla
Luloplanten (Solanum Quitoense)
Lupine - Levende Plant
Lupineplanten (Lupinus Spp.)
Lycheebomen (Litchi chinensis)
Lychees
Maagbitters/Alcoholische Siropen
Maagdenpalmplanten (vinca)
Maagwortelplanten (Curcuma Zedoaria)
Maatbekers/-lepels/-kommen voor voedingsmiddelen
Mabolobomen (Diospyros discolor)
Macadamiabomen (Macadamia ternifolia)
Machines voor Brievenvouwen/Insteken/Verzegelen
Machines voor Koolzuurhoudende Dranken
Machines voor Warme Dranken
Madeliefje (Bellis) - Levende Plant
Madronabomen (Arbutus menziesii)
Magnetrons
Maisplanten (Zea Mays subsp. Mays)
Ma-kiangbomen (Cleistocalyx operculatus var. paniala)
Mallen voor Kaarsen-/Zeepgieten
Mamey Sapota
Mamey Sapotebomen (Pouteria sapota)
Manchetknopen
Mandarijnen - Mediterrane Types
Mandarijnen - Overige Hybride Types
Mandarijnenbomen (Citrus x reticulata)
Manden/Benches/Kussens voor Huisdieren
Mandenvlechtwerk - Accessoires
Mandenvlechtwerk - Materialen
Mandevilla / Dipladenia - Levende Plant
Mangistans
Mangobomen (Mangifera indica)
Mangoesteenbomen (Garcinia mangostana)
Mango's
Manilla Tamarindebomen (Pithecellobium Dulce)
Mannetjesvarens (Dryopteris Filix-Mas)
Mansoorplanten (Asarum Europaeum)
Margarine (Beperkt Houdbaar)
Margarine (Diepvries)
Margarine (Houdbaar)
Margriet (Leucanthemum) - Levende Plant
Mariadistelplanten (Silybum Marianum)
Marjolein/Majoraan
Marjoraanplanten (Origanum Majorana)
Markeerkrijt/Kalklijner
Markeerstift
Marulabomen (Sclerocarya birrea)
Massagedouches
Mastiekbomen (Pistacia lentiscus)
Materiaal (Gerecycled/Hernieuwbaar) - Overig
Materiaal voor Beeldhouwers/Pottenbakkers
Materiaal voor Glasbewerking/Emailleerkunst/Marqueterie
Materiaal voor Kaarsen-/Zeepgieten
Materiaalvellen voor Gezondheidsbehandelingen en -Hulpmiddelen
Materialen voor Schuimgieten
Matrassen
Mattenkloppers
Mauritius-Hennep Planten (Furcraea foetida)
May-Changbomen (Litsea Cubeba)
Mayonaise/Mayonaisevervangers (Beperkt Houdbaar)
Mayonaise/Mayonaisevervangers (Diepvries)
Mayonaise/Mayonaisevervangers (Houdbaar)
Mechanische Anticonceptiva - Assortimenten
Mechanische Anticonceptiva - Overig
Medaillons/Hangers/Sieradenbedels
Medinilla - Levende Plant
Medische Diensten
Medische Hulpmiddelen
Meekrapplanten (Rubia tinctorum)
Meel - Graanproducten/Peulvruchten (Houdbaar)
Meetapparatuur voor Levensmiddelen - Assortimenten
Meetapparatuur voor Levensmiddelen - Overig
Meetlatten (DHZ)
Meetlinten (DHZ)
Meetwielen
Megafoons
Meidoornheesters (Crataegus)
Meisjesogen (Coreopsis)- Levende Plant
Meldeplanten (Atriplex Spp.)
Meldeplanten (Atriplex)
Melindjoeplanten (Gnetum Gnemon)
Melk (Beperkt Houdbaar)
Melk (Diepvries)
Melk (Houdbaar)
Melk/Boter/Room/Yoghurt/Kaas/Eieren/Vervangingsmiddelen - Assortimenten
Meloenen (Vers Gesneden)
Membraanpompen
Membranen voor Dakbedekking
Messen (Elektrisch)
Messen/Zakmessen - Niet Aangedreven (Hobby/Uitrusting)
Messen/Zakmessen - Niet Aangedreven Vervangingsonderdelen/Accessoires
Messen/Zakmessen losse mesjes - Niet Aangedreven (Hobby/Uitrusting)
Messenslijpers (Elektrisch)
Metaaldetectoren
Metaalscharen - Bladmetaal (Niet-aangedreven)
Metalen Componenten (Afmeting/Structuur)
Metronomen/Stemapparaten (Elektrisch)
Metronomen/Stemapparaten (Niet-elektrisch)
Metselmortel
Meubelovertrekken/Bescherming - Afneembaar
Meubelpoten
Meubilair Zwenkwieltjes/Kussentjes/Schuifsystemen
Mexicaanse Dwergpalm (Chamaedorea) - Levende Plant
Mexicaanse korianderplanten (Eryngium Foetidum)
Mexicaanse Limetten
Mexicaanse Margrietplanten (Tagetes Erecta)
Mexicaanse Zonnebloembomen (Tithonia Diversifolia)
Mexican Diners (Elektrisch)
Mezzanineladders/Zolderladders
Mibunaplanten (Brassica Rapa Japonica)
Microfoons
Microgroenten (Vers Gesneden)
Micrometers
Microscopen
Middelen tegen Diarree
Middelen tegen Maagzuur/Indigestie/winderigheid
Middelen tegen Misselijkheid
Middelen voor de keel
Mierikswortelen
Milieudiensten
Militair - Rantsoenen
Militair - Speciaal Aangedreven Gereedschap/Apparatuur
Militair - Speciaal Handgereedschap/Apparatuur
Mineraal-/Bron-/Tafelwater
Minerale Schuurmiddelen
Minikassen/Mini-Kweekbakken/Glazen kappen
Mini-Kiwi's/Kiwibessen
Minneolabomen (Citrus x tangelo)
Minneola's/Andere Tangelo's
Mirabelbomen (Prunus domestica ssp. Insititia)
Mirabelle-Pruimen
Mirteplanten (Myrtus)
Mispelbomen (Mespilus germanica)
Mispels
Mixer/Trilplaat
Mizuna
Mizunaplanten (Brassica Rapa Subsp. Nipposinica)
Mobiel Opslagmedium voor Foto's
Mobiele Telefoons/Smartphones
Modems
Moederkorenschimmels (Claviceps Purpurea)
Moederkruid / Wormkruid (Tanacetum) - Snijbloem
Moerasanemoonplanten (Houttuynia Cordata)
Moerasbeemdgras (Poa Palustris)
Moeraskruisbesstruik (Ribes Hirtellum)
Moerasspireaplanten (Filipendula Ulmaria)
Moerbeibomen (Morus)
Moerbouten/Draadstaven
Moeren
Moersleutels - Ratelverlengstukken/Handvaten
Moersleutels/Ringsleutels/Steeksleutels
Moersleutels/Ringsleutels/Steeksleutels - Assortimenten
Moersleutels/Ringsleutels/Steeksleutels - Onderdelen/Accessoires
Moersleutels/Ringsleutels/Steeksleutels - Sets
Moersplijter
Mokers
Mokken/Kopjes (Niet Wegwerp)
Molens/Vruchtenpersen/IJsmalers (Niet-elektrisch)
Mondbehandelingen
Mondbeschermers
Mondhygiëne - Assortimenten
MondHygiëne - Onderdelen
Mondhygiëne - Opladers/Units voor Elektrische Tandenborstel
Mondhygiëne - Overig
Mondverzorging - Accessoires
Mondverzorging - Hulpmiddelen(Elektrisch)
Mondverzorging - Hulpmiddelen(Niet-elektrisch)
Monitoren/Beeldschermen
Monitors voor Computer/PC's/Spelcomputers/Games
Monkeypotbomen (Lecythis ollaria)
Monniksbaard
Monnikskapplanten (Aconitum)
Monnikspeperbomen (Vitex Agnus-Castus)
Monoculair/Telescopen
Montagewagens/kruipwagens voor Autoreparatie
Montbretia (Crocosmia) - Snijgroen
Mop Emmer Set
Moppen
Morieljefungus (Morchella Esculenta)
Morieljes
Moringabomen (Moringa oleifera)
Mosterd (Beperkt Houdbaar)
Mosterd (Diepvries)
Mosterd (Houdbaar)
Mosterdkool
Motorfietsen
Motorontvettingsmiddelen/Verontreinigingsbeperkende Middelen
Motoroptimalisatiemodule voor Aanhangers/Slepen
Motorvoertuigen - Accentverlichting
Motorvoertuigen - Accu Accessoires
Motorvoertuigen - Accu's
Motorvoertuigen - Achteruitrijdlichten
Motorvoertuigen - Aftappluggen
Motorvoertuigen - Antivries-/Koelmiddelen
Motorvoertuigen - Applicatoren/Borstels
Motorvoertuigen - Artikelen voor Olieverversing - Assortimenten
Motorvoertuigen - Artikelen voor Olieverversing - Overig
Motorvoertuigen - Asbakken
Motorvoertuigen - Assortimenten voor Stoelen
Motorvoertuigen - Bandenpompen
Motorvoertuigen - Bedekking/Bescherming - Overig
Motorvoertuigen - Bescherming voor Kabels en Slangen
Motorvoertuigen - Beschermingshoezen/-bakjes voor Binnenlading
Motorvoertuigen - Binnenaccessoires - Combinatieonderdelen
Motorvoertuigen - Binnenaccessoires - Decoratief - Assortimenten
Motorvoertuigen - Binnenaccessoires - Decoratief - Overig
Motorvoertuigen - Boenschijven/Polijstmachines
Motorvoertuigen - Bonnet Spoilers
Motorvoertuigen - Brandblussers
Motorvoertuigen - Bullbars/Pushbars
Motorvoertuigen - Cabrioletdaken - Onderdelen/Accessoires
Motorvoertuigen - Caravanspiegels
Motorvoertuigen - Carrosseriereparatie - Assortimenten
Motorvoertuigen - Carrosseriereparatie - Overig
Motorvoertuigen - Chemische Bandenvullers
Motorvoertuigen - Chemische Producten voor Buitenkant - Assortimenten
Motorvoertuigen - Chemische Producten voor Buitenkant - Overig
Motorvoertuigen - Consoles
Motorvoertuigen - Contactdozen/Oogjes
Motorvoertuigen - dakkoffers
Motorvoertuigen - Decoratieve Accessoires/Gereedschappen - Overig
Motorvoertuigen - Decoratieve Emblemen
Motorvoertuigen - Decoratieve Verlichting - Assortimenten
Motorvoertuigen - Decoratieve Verlichting - Overig
Motorvoertuigen - Deurbeschermers
Motorvoertuigen - Elektrisch - Assortimenten
Motorvoertuigen - Elektrisch - Onderdelen/Accessoires
Motorvoertuigen - Elektrisch - Overig
Motorvoertuigen - Filteraccessoires
Motorvoertuigen - Filterkits/Accessoires
Motorvoertuigen - Filters - Assortimenten
Motorvoertuigen - Filters - Overig
Motorvoertuigen - Flexibele Buis/Gevlochten Kabel
Motorvoertuigen - Hellingen/Liften
Motorvoertuigen - Hoofd-/Nekkussens
Motorvoertuigen - Houders voor Belastingplaatjes
Motorvoertuigen - IJskrabbers
Motorvoertuigen - Imperiaals/Dakdragers
Motorvoertuigen - Instrumenten en Meetsystemen
Motorvoertuigen - Kaartleeslampen
Motorvoertuigen - Kleerhangers
Motorvoertuigen - Knoppen/Handgrepen voor Versnellingspook
Motorvoertuigen - Koel-/Verwarminrichting
Motorvoertuigen - Kogelkoppen voor Aanhangwagenkoppeling
Motorvoertuigen - Kompassen
Motorvoertuigen - Kop-/Fleshouders
Motorvoertuigen - Koplampen
Motorvoertuigen - Koppelstukken/Kits voor Versnellingspook
Motorvoertuigen - Laadbakuitbreidingen/Bumperdragers
Motorvoertuigen - Lading Vastsnoer- en Bevestigingsmiddelen
Motorvoertuigen - Lakbeschermingsfolies
Motorvoertuigen - Lakverdunners/Drogingsvertragers
Motorvoertuigen - Lampenbescherming
Motorvoertuigen - Lichten/Lampjes - Assortimenten
Motorvoertuigen - Lichten/Lampjes - Overig
Motorvoertuigen - Lieren
Motorvoertuigen - Luchtcompressoren
Motorvoertuigen - Luchtfilters
Motorvoertuigen - Luchtinlaten
Motorvoertuigen - Luchtverfrissers (Aangedreven)
Motorvoertuigen - Luchtverfrissers (Niet-aangedreven)
Motorvoertuigen - Markeerlichten
Motorvoertuigen - Meetinstrumenten Binnen
Motorvoertuigen - Mistlampen
Motorvoertuigen - Nivelleerapparatuur
Motorvoertuigen - Noodverlichting/Waarschuwingslichten
Motorvoertuigen - Oliefiltersleutels
Motorvoertuigen - Olieleidingen/Accessoires - Assortimenten
Motorvoertuigen - Olieleidingen/Accessoires - Overig
Motorvoertuigen - Oliematten
Motorvoertuigen - Oliemengers
Motorvoertuigen - Onderdelen voor Sierlijsten/Sierstrippen
Motorvoertuigen - Onderdelen/Accessoires voor Stoelen
Motorvoertuigen - Opbergdozen/-bakken/-manden (Binnenruimte)
Motorvoertuigen - Opbergruimte Binnen - Overig
Motorvoertuigen - Opbouw op Trekstang/Kogelkop
Motorvoertuigen – Oprijplaten en Accessoires voor Oprijplaten
Motorvoertuigen - Opstaphulpen
Motorvoertuigen - Overtrekken voor Hoofdsteunen/Hoofdsteunkits
Motorvoertuigen - Pedaalbeschermers/Sets
Motorvoertuigen - Profielen voor Lichten/Lampen
Motorvoertuigen - Profielen/Bekledingen voor Zijruiten
Motorvoertuigen - Reflecterende Tape
Motorvoertuigen - Reflectoren
Motorvoertuigen - Reiniger voor Elektrische Onderdelen
Motorvoertuigen - Reserve Vloerbekleding
Motorvoertuigen - Reservelampen
Motorvoertuigen - Reservelenzen
Motorvoertuigen - Rijlichten
Motorvoertuigen - Rubber Afdichtingen
Motorvoertuigen - Ruit Verzorgingsproducten
Motorvoertuigen - Ruitenwisserarmen
Motorvoertuigen - Ruitenwisserbuizen
Motorvoertuigen - Ruitenwisservloeistof
Motorvoertuigen - Schakelaars
Motorvoertuigen - Sidebars/Running Boards
Motorvoertuigen - Sigarettenaanstekers/Adapters
Motorvoertuigen - Sleepogen
Motorvoertuigen - Sleeptouw/-beugel/-stang
Motorvoertuigen - Sleutelhouders
Motorvoertuigen - Slijppasta/Poetsmiddelen/Krasverwijderaars
Motorvoertuigen - Snack/Drankbakjes
Motorvoertuigen - Spatborden/Spoilers
Motorvoertuigen - Spiegels
Motorvoertuigen - Startonderbrekers
Motorvoertuigen - Stoelen
Motorvoertuigen - Stoelkussens
Motorvoertuigen - Stoelovertrekken
Motorvoertuigen - Stroboscoopverlichting
Motorvoertuigen - Thermometers
Motorvoertuigen - Toeters/Claxons
Motorvoertuigen - Transmissiefilters
Motorvoertuigen - Transportapparaten - Onderdelen/Accessoires
Motorvoertuigen - Transportapparaten - Overig
Motorvoertuigen - Treeplaten
Motorvoertuigen - Trekhaak Treeplanken
Motorvoertuigen - Trekhaakadapters
Motorvoertuigen - Trekhaakbeschermers
Motorvoertuigen - Trekhaakset
Motorvoertuigen - Trekhaakuitbreidingen
Motorvoertuigen - Trekhaakzekeringen
Motorvoertuigen - Trekhaken
Motorvoertuigen - Trekstangen
Motorvoertuigen - Uurwerken
Motorvoertuigen - Veiligheid - Assortimenten
Motorvoertuigen - Veiligheid - Onderdelen/Accessoires
Motorvoertuigen - Veiligheid - Overig
Motorvoertuigen - Veiligheidskettingen/-kabels voor Slepen
Motorvoertuigen - Ventilatieroosters
Motorvoertuigen - Ventilators
Motorvoertuigen – vloeistoffilters
Motorvoertuigen - Vloerbekleding - Overig
Motorvoertuigen - Vloermatten
Motorvoertuigen - Vuilniszakken
Motorvoertuigen - Waarschuwingsdriehoeken
Motorvoertuigen - Waarschuwingsvlaggen/-vlaggenstokken
Motorvoertuigen - Was-/Reinigingssystemen (Aangedreven)
Motorvoertuigen - Wielblokken
Motorvoertuigen - Zekeringen
Motorvoertuigen - Zoeklichten
Motorvoertuigen - Zonnedaken/Schuifdaken
Motorvoertuigen Deurtrapjes/Voetplatformen
Mousserende wijn
Mozaiekplant (Fittonia) - Levende Plant
Mozindabomen (Treculia africana)
MP3 Docking Stations
Muisdoorn (Ruscus) - Snijgroen
Muismatten/Muissteunen
Mulch / Bodembedekkers
Multifunctioneel Keukengereedschap
Multifunctionele Kantoormachine
Multifunctionele Wellness Cabine
Multi-kooktoestellen
Multiplex/Spaanplaat/OSB-plaat
Mungboonplanten (Vigna Mungo)
Mungboonplanten (Vigna Radiata)
Munitie voor Vuurwapens
Munt
Muntautomaat Regeleenheid
Munten
Muntplanten (Mentha Spp.)
Muskaatpompoen
Muskaatpompoenplanten (Cucurbita Moschata)
Muskietengras (Bouteloua spp.)
Muskusokraplanten (Abelmoschus Moschatus)
Muur-/Plafondbedekking - Accessoires
Muur-/Plafondbedekking - Assortimenten
Muur-/Plafondbedekking - Overig
Muurbedekking - Platen/Panelen
Muurbedekking - Rollen
Muurbedekking - Tegels
Muurdekstenen
Muurfrezen (Aangedreven)
Muurplaten (Elektrisch)
Muziek - Digitaal
Muziekinstrument Hulpmiddelen (Elektrisch)
Muziekinstrumenten - Overige Accessoires
Muziekinstrumenten/Accessoires - Assortimenten
Muzikaal Speelgoed - Overig
Muzikaal Speelgoed (Elektrisch)
Muzikaal Speelgoed (Niet-elektrisch)
Naai/Breimachines (Elektrisch)
Naai/Breimachines (Niet-elektrisch)
Naaldaar (Setaria spp.)
Nachtjaponnen/Nachthemden
Nachtkleding - Assortimenten
Nagels - Accessoires (Elektrisch)
Nagels - Accessoires (Niet-elektrisch)
Nagels - Behandelingen
Nagels - Cosmetica
Nagels - Hulpmiddelen(Elektrisch)
Nagels - Hulpmiddelen(Niet-elektrisch)
Nagels - Reinigingsmiddelen/Cosmetica Verwijderproducten
Nagels - Vals
Nagels/Pinnen
Nagelsets/Verzinkboren
Name Mapuey
Name Mapueyplanten (Dioscorea Trifida)
Nandoevlees - Bereid/Bewerkt
Nandoevlees - Niet-bereid/Niet-bewerkt
Nangkabomen (Artocarpus heterophyllus)
Nangka's
Narcis - Bol/Knol
Narcis - Levende Plant
Narcis - Snijbloem
Narduskruidplanten (Nardostachys Jatamansi)
Nashi Perenbomen (Pyrus pyrifolia)
Nashi-Peren
Natalgras (Melinis Repens)
Natuurlijke Omhulsels
Nautische Navigatie - Radarsystemen
Nautische Navigatie Hardware
Nautische Navigatiesoftware
Navelklem
Navigatieapparatuur voor Auto's
Nectarinebomen (Prunus persica var nucipersica)
Nectarines
Neonotoniaplanten (Glycine Wightii)
Netmeloenen
Netwerk Access Points
Netwerkhubs/USB Hubs
Netwerkinterfacekaarten
Netwerkrouters
Netwerkswitches
Neusstrips/Sprays
Nibbelscharen/Knabbelscharen - Metaal (Aangedreven)
Nierboonplanten (Phaseolus Vulgaris)
Niet-bedrukte Borden
Niethamer - Niet-aangedreven
Nietjes/Nagelpistool - Niet-aangedreven
Nietpistolen (Aangedreven)
Nieuw-Zeelandse Peperbomen (Pseudowintera Colorata)
Nieuw-Zeelandse Spinazie
Nieuw-Zeelandse spinazieplanten (Tetragonia Tetragonioides)
Nijlgras (Acroceras Macrum)
Njangsabomen (Ricinodendron Heudelotii)
Nonibomen (Morinda citrifolia)
Nootmuskaatbomen (Myristica Fragrans)
Nordmann Spar (Abies nordmanniana)
Noten/Zaadjes - Bereid/Bewerkt (In Pel/Schil)
Noten/Zaadjes - Bereid/Bewerkt (Uit Pel/Schil)
Noten/Zaadjes - Onbewerkt/Onverwerkt (In Pel/Schil)
Noten/Zaadjes - Onbewerkt/Onverwerkt (Vers)
Notitieboekjes/adresboeken
Nummerplaatframes
Nummerplaten - Decoraties
Oca
Ocaplanten (Oxalis Tuberosa)
Ochtendjassen
Oepasbomen (Antiaris Africana)
Oesterzwamfungus (Pleurotus Ostreatus)
Oesterzwammen
Okra
Okraplanten (Abelmoschus Esculentus)
Oliën (Ongevormd)
Oliepalmbomen (Elaeis Guineensis)
Olieverversing Kits/Accessoires
Olifantsgras (Pennisetum Purpureum)
Olifantsknoflook
Olifantsoor (Alocasia) - Levende Plant
Olifantsoorplanten (Colocasia Esculenta)
Olifantspoot (Nolina) - Levende Plant
Olijfbomen (Olea Europea)
Olijfwilgbomen (Elaeagnus multiflora)
Olijven (Beperkt Houdbaar)
Olijven (Houdbaar)
Omheiningsnetten/Gaas
Omheiningspalen
Omheiningsstutten/Ankers
Onderbroeken/Slipjes/Boxershorts
Onderdelen van Aanhangwagen
Onderdelen van Lieren
Onderdelen voor Fotokopieermachines
Onderdelen voor Schrijfmachine
Onderdelen voor Schuiframen (Hout)
Onderdelen voor Schuiframen (Niet-Hout)
Onderdelen/Accessoires voor Aansluitkranen - Water en Gas
Onderdelen/Accessoires voor Aansluitstukken/Koppelingen - Water, Gas, CV
Onderdelen/Accessoires voor Centrale Verwarming
Onderdelen/Accessoires voor Dia's
Onderdelen/Accessoires voor Fotoalbums
Onderdelen/Hulpstukken voor Afvoerpijpen
Onderdelen/Hulpstukken voor Trappen
Ondergoed - Assortimenten
Ondergoed voor het hele Lichaam
Ondergrondse Klaverplanten (Trifolium Subterraneum)
Onderhemden/Onderjurken
Onderhoud/Reparatie - Overig
Onderhouds- / Reparatiediensten
Ondersteunende Component van een Medisch Hulpmiddel
Ondersteunende Component van een Veterinair Medisch Hulpmiddel
Ongediertebestrijdingsmiddelen
Ongesorteerde Eieren in Schaal
Ongewervelde Dieren - Overig
Ongewervelde Waterdieren - Bereid/Bewerkt (Beperkt Houdbaar)
Ongewervelde Waterdieren - Bereid/Bewerkt (Diepvries)
Ongewervelde Waterdieren - Bereid/Bewerkt (Houdbaar)
Ongewervelde Waterdieren - Niet-bereid/Niet-bewerkt (Beperkt Houdbaar)
Ongewervelde Waterdieren - Niet-bereid/Niet-bewerkt (Diepvries)
Ongewervelde Waterdieren - Niet-bereid/Niet-bewerkt (Houdbaar)
Ongewervelde Waterdieren/Vis/Schaal-/Schelpdieren Mix - Bereid/Bewerkt (Beperkt Houdbaar)
Ongewervelde Waterdieren/Vis/Schaal-/Schelpdieren Mix - Bereid/Bewerkt (Diepvries)
Ongewervelde Waterdieren/Vis/Schaal-/Schelpdieren Mix - Bereid/Bewerkt (Houdbaar)
Ongewervelde Waterdieren/Vis/Schaal-/Schelpdieren Mix - Niet-bereid/Niet-bewerkt (Beperkt Houdbaar)
Ongewervelde Waterdieren/Vis/Schaal-/Schelpdieren Mix - Niet-bereid/Niet-bewerkt (Diepvries)
Ongewervelde Waterdieren/Vis/Schaal-/Schelpdieren Mix - Niet-bereid/Niet-bewerkt (Houdbaar)
Onkruidverbranders (Aangedreven)
Onkruidverdelger
Ontharingsproducten - Assortimenten
Ontharingsproducten - Onderdelen
Ontharingsproducten - Overig
Ontkalkers
Ontkalkers (DHZ)
Ontsmettingsmiddelen
Ontstekingsbougies
Ontstekingsbougies - Assortimenten
Ontstekingsbougies - Overig
Ontwikkelings/Educatief Speelgoed - Assortimenten
Ontwikkelings/Educatief Speelgoed - Overig
Ontwormingspreparaten
Oogpreparaten
Oor-/Neusverzorging
Oorbellen/Piercing Sieraden
Oorpreparaten
Op Afstand Bestuurbare Voertuigen
Op Afstand Bestuurbare Voertuigen - Onderdelen en Toebehoren
Op Zuivel Gebaseerde Dranken - Gebruiksklaar (Beperkt Houdbaar)
Op Zuivel Gebaseerde Dranken - Gebruiksklaar (Houdbaar)
Op Zuivel Gebaseerde Dranken - Niet-gebruiksklaar (Houdbaar)
Op Zuivelvervangers Gebaseerde Dranken - Gebruiksklaar (Beperkt Houdbaar)
Op Zuivelvervangers Gebaseerde Dranken - Gebruiksklaar (Houdbaar)
Op Zuivelvervangers Gebaseerde Dranken - Niet-gebruiksklaar (Houdbaar)
Opbergdozen/Draagtassen voor Computer/PC's/Spelcomputers/Games
Opbergrails/Houders
Opblaasbare Zitmeubelen
Opblaasbedden/Waterbedden
Opdienbestek (Niet Wegwerp)
Open Haard Behandelingen/Reinigingsmiddelen
Open Haarden - Brandstofopslag
Open Haarden - Hulpmiddelen
Open Haarden - Roosters
Open Haarden - Schermen
Open haarden/Schoorsteenmantels
Openbare brandalarmen
Openers
Openingssystemen voor Poort-/Garagedeur
Openingssystemen voor Poort-/Garagedeur - Onderdelen/Accessoires
Opladers
Opneembare Media - Assortimenten
Opneembare Media - Overig
Oppervlaktebewerkend Gereedschap
Oppervlaktebewerkend Gereedschap - Verbruiksmaterialen
Oppervlakteverzorging - Assortimenten
Oppervlakteverzorging - Overig
Oppervlakteverzorging/Bescherming
Oppottafel
Opslag Barrels/Tonnen/Vaten (Leeg)
Opslag Cilindrische Vaten (Leeg)
Opslag Flessen (Leeg)
Opslag Tuinslang - Mobiel
Opslag Tuinslang - Vast
Opslag van Dia's
Opslag van Gereedschap - Assortimenten
Opslag van Gereedschap - Overig
Opslag van Smeermiddelen/Beschermende Middelen - Assortimenten
Opslag/Transport Bakken (Leeg)
Opslag/Transport Dozen (Leeg)
Opslag/Transport Kratten (Leeg)
Opslag/Transport Tanks (Leeg)
Opstrijkbare randstrook
Optica - Assortimenten
Optica - Onderdelen/Accessoires
Optica - Overig
Optische schijf / CD / DVD lezers
Optische Schrijven - Lezen/Schrijven
Opvangbakken
Opvulstukjes/Afstandsplaten
Opwarmlades
Opzetranden voor Pallets
Orale toediening van glucose en zoutoplossingen/Elektrolytbalans
Orangelo's
Oranjebloesem (Garnering van Voedsel)
Orchidee (Cymbidium) - Levende Plant
Orchidee (Cymbidium) - Snijbloem
Orchidee (Dendrobium) - Levende Plant
Orchidee / Viooltjesorchidee (Miltonia) - Levende Plant
Orchis - Levende Plant
Oregano
Origanoplanten (Origanum Vulgare)
Orleaanbomen (Bixa Orellana)
Ornamenten / Sierobjecten (Niet-aangedreven)
Ornamenten /Sierobjecten (Aangedreven)
Ornamenten/Houtwerk/Traponderdelen - Overig
Oscillerende Multitools
Ovens
Overalls/Jumpsuits/Bodysuits
Overhangende pompen
Overheadprojectors
Overhemden/Bloezen/Poloshirts/T-Shirts
Overig Calla (Zantedeschia) - Snijbloem
Overig Hertshooi (Hypericum) - Snijbloem
Overig Lamsoor / Statice / Zeelavendel (Limonium) - Snijbloem
Overig Lelie (Lilium) - Snijbloem
Overig Ranonkel / Boterbloem / Waterranonkel - Snijbloem
Overige Anjer (Dianthus) - Snijbloem
Overige Annona's
Overige Armaturen
Overige Astilbe / Spirea / Pluimspirea - Snijgroen
Overige Bar- en Wijnaccessoires
Overige Hybriden van Zacht Fruit
Overige klaverplanten (Trifolium)
Overige Levende Planten - Grassen
Overige Levende Planten - Kruiden
Overige Levende Planten - Varens
Overige Levende Planten - Vetplanten / Cactussen
Overige Levende Planten - Waterplanten
Overige Meloenen
Overige Nachtschadegewassen (Vers Gesneden)
Overige Pompoen / Kalebas (Cucurbita) - Snijgroen
Overige Wasbloem (Chamelaucium) - Snijbloem
Overige Wilde Paddenstoelen
Overlevingsdekens/Slaapzakken voor Noodgevallen
Overspanningonderdrukkers/-beveiligers
Overtrekken voor Voertuigen
Paalgatboren (Aangedreven)
Paalgatboren (Niet-aangedreven)
Paardeboonplanten (Vicia Faba var. Equina)
Paarden/Ezels
Paardenbloem
Paardenbloemplanten (Taraxacum)
Paardenvlees - Bereid/Bewerkt
Paardenvlees - Niet-bereid/Niet-bewerkt
Paarse Morgenster
Paarse Morgensterplanten (Tragopogon Porrifolius)
Paarse Passievruchten
Paascactus (Rhipsalidopsis) - Levende Plant
Paddenstoelen (Vers Gesneden)
Paellamakers
Pagodes (Tuin)
Paksoi
Paksoiplanten (Brassica Chinensis)
Palen/Roedes
Pallets
Palmhart
Palmlelieplanten (Yucca)
Palmyra palmbomen (Borassus)
Pampasgras (Cortaderia) - Levende Plant
Pandanbomen (Pandanus Utilis)
Panelen/Platen voor Dakbedekking
Pannenkoek-/Donutmakers
Panty's
Papaja’s (Vers Gesneden)
Papajabomen (Carica papaya)
Papaja's
Papalo/Boliviaanse Koriander
Papedabomen (Citrus papeda)
Papier en Karton (Gerecycled/Hernieuwbaar)
Papier en Karton (Gevormd)
Papier/Karton - Ongedrukt
Papieren Handdoekjes
Papierfilters
Papiersnijmachines
Papierversnipperaars (Elektrisch)
Papierversnipperaars (Niet-elektrisch)
Paprikaplanten (Capsicum Annuum)
Paprika's (incl. Pepers) - Mengsels (Vers)
Paprika's (incl. Pepers) (Vers Gesneden)
Parachutes
Paradijskorrelplanten (Aframomum Melegueta)
Paradijsnootbomen (Lecythis zabucajo)
Paradijsvogelbloem (Strelitzia) - Snijbloem
Paradijsvogelbloem (Strelitzia) - Snijgroen
Paragras (Brachiaria Mutica)
Paraguayobomen (Prunus persica var. Platycarpa)
Paranotenbomen (Bertholletia excelsa)
Paraplu's
Parasietbehandeling voor Dieren
Parasolden (Pinus pinea)
Parasolvoeten
Parelgierstplanten (Pennisetum Glaucum)
Parelhoenvlees - Bereid/Bewerkt
Parelhoenvlees - Niet-bereid/Niet-bewerkt
Parfums
Parkeerbeschermers
Parkeerbeugel
Parkiabomen (Parkia Biglobosa)
Party Drankfonteinen (Elektrisch)
Partytenten
Passer/Kompas (DHZ)
Passievruchtbomen (Passiflora edulis)
Passievruchten (Vers Gesneden)
Pasta/Noedels - Assortimenten
Pasta/Noedels - Gebruiksklaar (Beperkt Houdbaar)
Pasta/Noedels - Gebruiksklaar (Houdbaar)
Pasta/Noedels - Niet-gebruiksklaar (Beperkt Houdbaar)
Pasta/Noedels - Niet-gebruiksklaar (Diepvries)
Pasta/Noedels - Niet-gebruiksklaar (Houdbaar)
Pastakooktoestellen
Pastelstiften/Houtskool/Kleurpotloden voor Kunstenaars
Pastinaakplanten (Pastinaca Sativa)
Pastinaken
Patchoulistruiken (Pogostemon Cablin)
Paté (Beperkt Houdbaar)
Paté (Diepvries)
Paté (Houdbaar)
Patiodeuren
Pattypanplanten (Cucurbita Melopepo)
Pawpawheesters (Asimina)
Pecannootbomen (Carya illinoinensis)
Peelings/Maskers
Penetratie Accessoires (Elektrisch)
Penetratie Accessoires (Niet-elektrisch)
Pennen
Penselen/Spatels/Applicatoren voor Kunstenaars
Peperomia - Levende Plant
Peperplanten (Piper Nigrum)
Pepinoplanten (Solanum Muricatum)
Pepino's
Peren
Perenbomen (Pyrus communis)
Perforators (Elektrisch)
Perforators (Niet-elektrisch)
Peristaltische/rollenpompen
Persen/Decoratiespuiten voor Voeding (Niet-elektrisch)
Personal Computers - All-in-One
Personal Computers - Desktop/Internet Terminal
Personal Computers - Draagbaar
Personal Computers - Tablets/E-readers
Personal Data Assistant (PDA)/Organiser Pen
Persoonlijke Accessoires - Assortimenten
Persoonlijke Agenda's (Niet-elektrisch)
Persoonlijke Beschermingsmiddelen - Assortimenten
Persoonlijke Beschermingsmiddelen - Onderdelen/Accessoires
Persoonlijke Beschermingsmiddelen - Overig
Persoonlijke Digitale Assistenten (PDA's)
Persoonlijke Hulpmiddelen - Assortimenten
Persoonlijke Hulpmiddelen - Overig
Persoonlijke Insectenwerende middelen
Persoonlijke Omroepapparaten
Persoonlijke tassen
Persoonlijke Veiligheidslichten
Persoonlijke Veiligheidsuitrusting - Assortimenten
Persoonlijke Ventilator - Handventilator
Persoonlijke Ventilator - Waaier
Persoonlijke Verwarming/Massage (Elektrisch)
Persoonlijke Verwarming/Massage (Niet-elektrisch)
Peruaanse Ganzevoetplanten (Chenopodium Pallidicaule)
Perubalsembomen (Myroxylon balsamum)
Peruviaanse peperbomen (Schinus Molle)
Perzikbomen (Prunus persica)
Perziken
Perzische Klaverplanten (Trifolium Resupinatum)
Perzische limoenbomen (Citrus latifolia)
Pessaria/Cervixkapjes
Pesticiden voor Tuin - Assortimenten
Pesticiden voor Tuin - Overig
Petehboonbomen (Parkia Speciosa)
Peterselieplanten (Petroselinum Crispum)
Petticoats/Onderrokken/Slips
Petunia - Levende Plant
Peultjes
Phaceliaplanten (Phacelia Tanacetifolia)
Philodendron - Levende Plant
Physalis (Kaapse Kruisbessen)
Pijlbladklaverplanten (Trifolium Vesiculosum)
Pijlen
Pijlrietgras (Arundo Donax)
Pijlwortelplanten (Maranta Arundinacea)
Pijnbomen (Pinus pinea)
Pijnstiller - Assortimenten
Pijnstiller - Overig
Pijnstiller (Elektrisch)
Pijnstiller voor Artritis/Reuma/Spierpijn
Pijnstiller voor Hoofdpijn/Migraine
Pijp blokkeerapparatuur
Pijp-/Buissnijders - Niet-aangedreven
Pijpbuigmachines
Pijpen/Buizen - Water, Gas, CV
Pijpkassia
Pijpsansevieria - Levende Plant
Pijpsnijders (Aangedreven)
Pikhouwelen
Pimentplanten (Pimenta Dioica)
Pimpernelplanten (Sanguisorba Spp.)
Pinata's
Pincet (DHZ)
Pindaplanten (Arachis hypogaea)
Pioen / Pioenroos (Paeonia) - Levende Plant
Pioen / Pioenroos (Paeonia) - Snijbloem
Piper Excelsumbomen (Piper Excelsum)
Pipiche
Pistachebomen (Pistacia vera)
Pitahaya’s (Vers Gesneden)
Pitayaplanten (Stenocereus)
Pittosporum - Snijbloem
Pittosporum - Snijgroen
Pitvruchten (Vers Gesneden)
Pizzamakers
Plafondbedekking - Platen/Tegels
Plafondbedekking - Verlaagd Plafond Systemen
Plamuur/Bouwplaatmessen
Planken / Stellingen
Plannings- en Organisatiehulpmiddelen - Assortimenten
Plannings- en Organisatiehulpmiddelen - Onderdelen/Accessoires
Plannings- en Organisatiehulpmiddelen - Overig
Plant/Bodem Mest/Voedingsmiddelen
Plantaardige Middelen
Plantaardige Zuivelspread (Beperkt Houdbaar)
Plantaardige Zuivelspread (Diepvries)
Plantaardige Zuivelspread (Houdbaar)
Plantaardige/Homeopathische Middelen - Assortimenten
Plantaardige/Homeopathische Middelen - Overig
Plantagebanaanstruiken (Musa x paradisiaca - AAB)
Planten - Assortimenten
Plantenbakken/Bloempotten - Gevuld
Plantenbakken/Bloempotten - Leeg
Plantenbakken/Bloempotten - Onderdelen/Accessoires
Plantengroeiregulatoren
Plantensteunen/Plantengeleiders
Plantentunnels
Plat handjesgras (Eleusine Indica)
Plateauwagentjes
Platte Paprika's (Tomaatpaprika's)
Platte Serveerschalen
Pleistertroffels/Plakspanen
Pleisterwerk/Stucco
Plinten voor Campers/Caravans
Plinten/Kroonlijsten/Accessoires voor plinten
Plisségordijnen
Pluimgierst (Panicum Virgatum)
Plumcots
Plunjerpompen
Pneumatische pompen
Pochets/Zakdoeken
Poelietrekker - Aangedreven
Poelietrekker (Niet-aangedreven)
Poetsdoeken/Poetslappen voor de Werkplaats
Polijstmachines voor Details
Polijstmengsel
Polytrias-gras (Polytrias Armaura)
Pomelo's/Pompelmoezen (Nederlands)
Pompelmoesbomen (Citrus maxima)
Pompen (Aangedreven)
Pompen (Niet-aangedreven)
Pompen voor Water-/Gasvoorziening
Pompoen / Kalebas / Sierkalebas (Cucurbita Pepo) - Snijgroen
Pompoenen
Pompoenen – Eetbare Schil (Vers Gesneden)
Pompoenen – Niet-eetbare Schil (Vers Gesneden)
Ponsen
Poolse tarweplanten (Triticum Polonicum)
Poorten (Aangedreven)
Poorten (Niet-aangedreven)
Pootjes/Steunen voor Aanhangwagen
Popcorn (Houdbaar)
Popcornmakers
Poppen Gebouwen/Omgevingen
Poppen/Handpoppen/Pluchen Speelgoed - Overig
Poppen/Pluchen Speelgoed (Elektrisch)
Poppen/Pluchen Speelgoed (Niet-elektrisch)
Poppenhoofden voor Knippen (Elektrisch)
Poppenhoofden voor Knippen (Niet-elektrisch)
Poppenkasten
Poppenkleding
Poppenmeubilair
Portefeuilles/Portemonnees/Reisdocumentenetuis
Postdiensten
Postelein
Postelein (Portulaca) - Levende Plant
Posteleinplanten (Portulaca Oleracea)
Posters/Prenten
Posters/Spiegels/Lijsten - Assortimenten
Posters/Spiegels/Lijsten - Overig
Postkaarten
Postzegels
Potloden
Potloden/Kleurkrijt (DHZ)
Potten/Pannen/Wokken/Braadpannen - Assortimenten
Pottenbakkerswielen (Aangedreven)
Pottenbakkerswielen (Niet-aangedreven)
Prei
Preiplanten (Allium Porrum)
Prepaid Kaarten/Cadeaukaarten/Vouchers
Prepaid Vouchers/Kaarten voor Vaste Communicatie
Presentatieborden (Elektrisch)
Presentatieborden (Niet-elektrisch)
Pre-shave/Scheerschuim/Scheermiddel
Preventieve Middelen tegen Reisziekte - Geneeskundig
Preventieve Middelen tegen Reisziekte - Niet-geneeskundig
Priemen
Priemen/Ponsen/Nagelsets - Assortimenten
Prikkeldraad Omheining
Primaten
Primers/Middelen voor Oppervlaktebehandeling voor Kunstenaars
Primula / Sleutelbloem - Levende Plant
Prinsessenknolplanten (Ullucus Tuberosus)
Printer Accessoires
Printers
Producten tegen Genitale Irritatie
Producten tegen Reisziekte - Assortimenten
Producten tegen Reisziekte - Overig
Producten ter Verzorging na Ontharing
Producten voor het Verwijderen/Behandelen van Gif
Producten voor Lichaamsreiniging
Producten voor Spierstimulatie (Elektrisch)
Producten/Maaltijden op basis van Deeg - Assortimenten
Producten/Maaltijden op basis van Deeg - Gebruiksklaar (Beperkt Houdbaar)
Producten/Maaltijden op basis van Deeg - Gebruiksklaar (Houdbaar)
Producten/Maaltijden op basis van Deeg - Niet-gebruiksklaar (Beperkt Houdbaar)
Producten/Maaltijden op basis van Deeg - Niet-gebruiksklaar (Diepvries)
Producten/Maaltijden op basis van Deeg - Niet-gebruiksklaar (Houdbaar)
Producten/Maaltijden op basis van Eieren - Niet-gebruiksklaar (Beperkt Houdbaar)
Producten/Maaltijden op basis van Eieren - Niet-gebruiksklaar (Diepvries)
Producten/Maaltijden op basis van Eieren - Niet-gebruiksklaar (Houdbaar)
Producten/Maaltijden op basis van Graan - Assortimenten
Producten/Maaltijden op basis van Graan - Gebruiksklaar (Beperkt Houdbaar)
Producten/Maaltijden op basis van Graan - Gebruiksklaar (Houdbaar)
Producten/Maaltijden op basis van Graan - Niet-gebruiksklaar (Diepvries)
Producten/Maaltijden op basis van Graan - Niet-gebruiksklaar (Houdbaar)
Producten/Maaltijden op basis van Graan - Niet-gebruiksklaar)
Producten/Maaltijden op basis van Groenten - Assortimenten
Producten/Maaltijden op basis van Groenten - Gebruiksklaar (Beperkt Houdbaar)
Producten/Maaltijden op basis van Groenten - Gebruiksklaar (Houdbaar)
Producten/Maaltijden op basis van Groenten - Niet-gebruiksklaar (Beperkt Houdbaar)
Producten/Maaltijden op basis van Groenten - Niet-gebruiksklaar (Diepvries)
Producten/Maaltijden op basis van Groenten - Niet-gebruiksklaar (Houdbaar)
Producten/Maaltijden op basis van Zuivelproducten - Niet-gebruiksklaar (Diepvries)
Producten/Maaltijden op basis van Zuivelproducten - Niet-gebruiksklaar (Houdbaar)
Producten/Maaltijden op basis van Zuivelproducten/Eieren - Assortimenten
Producten/Maaltijden op basis van Zuivelproducten/Eieren - Gebruiksklaar (Beperkt Houdbaar)
Producten/Maaltijden op basis van Zuivelproducten/Eieren - Gebruiksklaar (Houdbaar)
Profielen/Decoratieve Elementen/Traponderdelen - Assortimenten
Profielzoekers/-Detectoren/-Sensoren
Progressieve holtepompen
Projectiesystemen
Projectietafels
Pronkbonen/Snijbonen
Pronkboonplanten (Phaseolus Coccineus)
Pronkerwtplanten (Lathyrus Odoratus)
Prosopisbomen (Prosopis Spp.)
Proteïnerepen
Pruim Cherrytomaten
Pruimen
Pruimenbomen (Prunus domestica)
Pruimtomaten
Psoriasis/Eczema/Droge Huid Behandelingen
Psylliumplanten (Plantago Ovata)
Pucks
Puerariaplanten (Pueraria Spp.)
Puntarelle
Puntarelleplanten (Cichorium Intybus Gr. Catalugna)
Puntenslijpers (Elektrisch)
Puntenslijpers (Niet-elektrisch)
Puntpaprika's
Purperklokje (Heuchera) - Levende Plant
Purple mombrilbomen (Spondias purpurea)
Puzzels (Elektrisch)
Puzzels (Niet-elektrisch)
Pyjamabroeken Lang en Kort
Pyranometers/Solarimeters - Elektrisch
Quinoaplanten (Chenopodium Quinoa)
Raam Balanceerinrichtingen
Raam- en Decoratiefolie
Raamdecoratie - Onderdelen/Accessoires
Raamknoppen
Raamlijsten
Raamluiken
Raamluikmotoren
Raamonderdelen/Accessoires - Assortimenten
Raamonderdelen/Accessoires - Overig
Raamsloten/-grendels
Raamsystemen/Dubbele Ramen (Gelamineerd Hout)
Raamsystemen/Dubbele Ramen (Hout)
Raamsystemen/Dubbele Ramen (Niet Hout)
Raamuitzetter / raamopener
Raamwisser (Elektrisch)
Raapstelen
Rabarber
Rabarberplanten (Rheum Rhaponticum)
Rackets
Racketsport Artikelen - Assortimenten
Racketsport Artikelen - Overig
Racketsporten - Onderdelen/Accessoires
Racletapparaat (Elektrisch)
Radardetectors voor Auto
Radiaalzagen
Radiator Reparatiekits
Radiators
Radicchio Rosso
Radijsjes
Radijsplanten (Raphanus Sativus)
Radiocommunicatie Toestellen
Radio's/Walkietalkies
Raffiapalmen (Raphia farinifera)
Rambaibomen (Baccaurea motleyana)
Ramboetans
Rambutanbomen (Nephelium lappaceum)
Ramen - Overig
Ramieplanten/Chinees Gras (Boehmeria nivea)
Rammenassen
Randafwerkingen
Randapparatuur voor Computers/PC's/Spelcomputers/Games - Assortimenten
Randapparatuur voor Computers/PC's/Spelcomputers/Games - Onderdelen/Accessoires
Randapparatuur voor Computers/PC's/Spelcomputers/Games - Overig
Ranonkel - Snijbloem
Ranonkel / Boterbloem (Ranunculus) - Levende Plant
Raspen
Raspen (Elektrisch)
Ravensarebomen (Cryptocarya agathophylla)
Recht/Matrijzenslijpmachines
Reciprozagen
Rectale Medicijnen
Reddingsboten/Reddingsboeien/Drijfkussens
Reddingsgordels/Reddingsvesten/Reddingspakken
Reeschaven - Draagbaar
Reevlees - Bereid/Bewerkt
Reevlees - Niet-bereid/Niet-bewerkt
Regenmeters - Elektrisch
Regenmeters - Niet-elektrisch
Reine Claude Pruimen
Reine Claudebomen (Prunus domestica ssp. Insititia)
Reiniging/Luchtverfrissers - Accessoires - Assortimenten
Reiniging/Luchtverfrissers - Accessoires - Overig
Reiniging/Luchtverfrissers - Onderdelen/Accessoires
Reinigings-/Onderhoudsproducten voor Schoenen
Reinigingsdoekjes voor Telefoon
Reinigingsmiddelen - Assortimenten
Reisdiensten
Reiswiegen/Reismanden
Rekenmachines/Valutaomzetters (Elektrisch)
Rekken
Relais/Contactors
Relingen/Leuningen/Terrasbouw - Assortimenten
Relingen/Leuningen/Terrasbouw - Overig
Rem-/Knipperlichten
Rembesturingen
Remblok/Remvoering
Remmen van Aanhangwagen
Remmenreinigers
Remschijf
Remschijfhuis
Remschijfset
Remtrommel/Remtrommel Onderdeel
Rendier-/Kariboevlees - Bereid/Bewerkt
Rendier-/Kariboevlees - Niet-bereid/Niet-bewerkt
Reparatiekits voor Lekke Band
Reparatieset voor Gips-/Cementplaat
Reptielen
Reserve Ruitenwisserbladen
Reumatiekplantje (Plectranthus) - Levende Plant
Reuze Pompoenplanten (Cucurbita Maxima)
Reuze Taroplanten (Alocasia Macrorrhizos)
Reuzengranadillabomen (Passiflora quadrangularis)
Reuzengranadilla's/Grote Markoesa's
Reuzenzilverspar (Abies grandis)
Revolvers/Pistolen
Rhapis - Levende Plant
Rhodes-gras (Chloris Gayana)
Ridderspoor (Delphinium) - Levende Plant
Ridderspoor (Delphinium) - Snijbloem
Riemen/Bretels/Sjerpen
Riemen/Holsters/Buidels voor Gereedschap
Rietzwenkgras (Schedonorus Arundinaceus)
Rijst- en Granenkokers/Stoomkokers
Rijstboonplanten (Vigna Umbellata)
Rijstgrasplanten (Paspalum Scrobiculatum)
Rijstplanten (Oryza Sativa)
Rijstveldkruidplanten (Limnophila Aromatica)
Ringen
Ringen/Pakkingringen
Ringtonen - Digitaal
Riooldeksels
Rioolveren - Niet-aangedreven
Robotstofzuigers
Rode aalbesstruiken (Ribes Rubrum)
Rode banaanstruiken (Musa acuminata - AAA var. Rubra)
Rode Bananen
Rode bieten
Rode Bietplanten (Beta Vulgaris Subsp. Vulgaris var. Conditiva)
Rode Hanenkopplanten (Hedysarum Coronarium)
Rode Klaverplanten (Trifolium Pratense)
Rode Kool
Rode kraakbesheesters (Vaccinium parvifolium)
Rode Pitahaya's (Drakenvruchten)
Rode Zilverspar (Abies magnifica)
Rode Zonnehoed (Echinacea) - Levende Plant
Rode Zonnehoedplanten (Echinacea Purpurea)
Rode-havergras (Themeda Triandra)
Rode-koolplanten (Brassica Oleracea var. Capitata F. Rubra)
Roggeplanten (Secale cereale)
Rokken
Rolgordijnen
Roljaloezieën
Rollen voor Dakbedekking
Rollenbok
Rollenspel - Huishouden/Tuinieren/DHZ Speelgoed
Rollenspel - Keukenspeelgoed
Rollenspel - Winkel/Kantoor/Bedrijf Speelgoed
Romaineslaplanten (Lactuca Sativa var. Romana)
Romanesco Bloemkool
Romanescoplanten (Brassica Oleracea Convar. Botrytis var. Botrytis)
Ronde Cherrytomaten
Ronde Tomaten
Roodlof
Roodlofplanten (Cichorium Intybus var. Foliosum)
Roodvlezige Drakenvruchtenplanten (Hylocereus costaricensis)
Roodzwenkgras (Festuca Rubra)
Rooibosplanten (Aspalathus linearis)
Rookaccessoires
Rookkappen/Ademhalingstoestellen
Room (Beperkt Houdbaar)
Room (Diepvries)
Room (Houdbaar)
Roomse Kamilleplanten (Chamaemelum Nobile)
Roomse Kervel
Roomse Kervelplanten (Myrrhis Odorata)
Roos - Levende Plant
Roos - Snijbloem
Roos - Snijgroen
Roselleplanten (Hibiscus sabdariffa var. altissima)
Roselleplanten (Hibiscus sabdariffa)
Rotanpalmen (Calamus rotang)
Roterende Multitools
Roze peperbomen (Schinus Terebinthifolia)
Rozemarijn
Rozemarijnplanten (Rosmarinus Officinalis)
Rozenplanten (Rosa)
Rubberbomen (Hevea brasiliensis)
Rucola
Rucolaplanten (Eruca Sativa)
Rugzakken/Reistassen
Ruige Rupsklaverplanten (Medicago Polymorpha)
Ruitenwisserbladen
Ruitenwisserbuizen/-slangen
Ruitenwisserkappen
Ruitenwissermondstukken
Ruitenwissermotors
Ruitenwissermotors (Motorkernen)
Ruitenwisseronderdelen - Assortimenten
Ruitenwisseronderdelen - Overig
Ruitenwisserpompen
Ruitenwissers/Ruitenwisseronderdelen - Assortimenten
Ruitenwissers/Ruitenwisseronderdelen - Overig
Runderen
Rundvlees - Bereid/Bewerkt
Rundvlees - Niet-bereid/Niet-bewerkt
Russische Paardenbloemplanten (Taraxacum kok-saghyz)
Sabi-gras (Urochloa Mosambicensis)
Saffloer (Carthamus) - Snijgroen
Saffloerplanten (Carthamus Tinctorius)
Saffraankrokusplanten (Crocus Sativus)
Sagopalmbomen (Metroxylon Spp.)
Salakbomen (Salacca edulis)
Salakken (Slangenfruit)
Salamanderbomen (Antidesma bunius)
Salambomen (Eugenia Polyantha)
Salie
Salviaplanten (Salvia Officinalis)
Sandwich-/Wafelmakers
Sandwiches/Gevulde Broodjes/Wraps - Assortimenten
Sandwiches/Gevulde Broodjes/Wraps (Beperkt Houdbaar)
Sandwiches/Gevulde Broodjes/Wraps (Diepvries)
Sanitair/Sanitaire Voorzieningen - Assortimenten
Sanitair/Sanitaire Voorzieningen - Onderdelen/Accessoires
Sanitair/Verwarming Ventilatie/Airconditioning - Assortimenten
Sanitaire Meubels voor Baby's - Assortimenten
Sanitaire Meubels voor Baby's - Onderdelen
Sanitaire Meubels voor Baby's - Overig
Santolbomen (Sandoricum koetjape)
Santonicaplanten (Artemisia Cina)
Sapodilla
Sapodillabomen (Manilkara zapota)
Sapota (Vers Gesneden)
Sareptamosterd (Amsoi)
Sareptamosterdplanten (Brassica Juncea)
Saskatoon Bessen
Sassafrasplanten (Sassafras Albidum)
Satelliet Antenne Systemen
Satellietinstallatie-Kabels
Satsuma Mandarijnen
Satsumabomen (Citrus reticulata 'Satsuma')
Saunacabine
Sauna-Uitrusting - Onderdelen/Accessoires
Sauzen - Koken (Beperkt Houdbaar)
Sauzen - Koken (Diepvries)
Sauzen - Koken (Houdbaar)
Sauzen/Spreads/Dipsausjes/Smaakmakers - Assortimenten
Savadoreaanse Hennep Cactussen (Agave letonae)
Savooiekool (Groene kool)
Savooiekoolplanten (Brassica Oleracea var. Sabauda)
Scammoniaplanten (Convolvulus Scammonia)
Scanners
Schaafbanken - Vastgemonteerd
Schaafbanken/Vandikteschaafbanken - Draagbaar
Schaafmachines
Schaal-/Schelpdieren - Assortimenten
Schaal-/Schelpdieren - Bereid/Bewerkt (Beperkt Houdbaar)
Schaal-/Schelpdieren - Bereid/Bewerkt (Diepvries)
Schaal-/Schelpdieren - Bereid/Bewerkt (Houdbaar)
Schaal-/Schelpdieren - Niet-bereid/Niet-bewerkt (Beperkt Houdbaar)
Schaal-/Schelpdieren - Niet-bereid/Niet-bewerkt (Diepvries)
Schaal-/Schelpdieren - Niet-bereid/Niet-bewerkt (Houdbaar)
Schaaldieren
Schaambomen (Sesbania Spp.)
Schakelaars
Schapen
Schapenbesheesters (Viburnum lentago)
Schapenvlees - Bereid/Bewerkt
Schapenvlees - Niet-bereid/Niet-bewerkt
Schaven
Schaven/Schaafbanken/Vijlen/Raspen - Assortimenten
Scheefbloemplanten (Iberis)
Scheeraccessoires
Scheerapparaten (Elektrisch)
Scheermesjes
Scheermesjes (Niet-elektrisch)
Scheidingspanelen voor Urinoir
Scherm met Identificatie van de oproeper
Schermsport Artikelen (Elektrisch)
Schermsport Artikelen (Niet-elektrisch)
Scherpslijpmachines (Niet-aangedreven)
Scheuten
Schiethamers (Aangedreven)
Schietsportartikelen - Assortimenten
Schietsportartikelen - Overig
Schijfremafdichtingen
Schijfschuurmachines
Schijfschuurmachines / Gipsplaatschuurmachines - Draagbaar
Schilder/Tekenbenodigdheden voor Kunstenaars - Assortimenten
Schilder/Tekenbenodigdheden voor Kunstenaars - Overig
Schilderijen
Schildersafdekpapier/-folie
Schildersezels
Schilderspaletten
Schildvoetbladplanten (Podophyllum Peltatum)
Schimmelverdelger
Schimmelverwijderaars
Schisandra chinensisheesters (Schisandra chinensis)
Schisandrabessen
Schoenen - Algemeen Gebruik
Schoenen - Onderdelen/Accessoires
Schoenen Accessoires - Assortimenten
Schoenen Inzetstukken
Schoenen voor Binnen Gebruik - Gedeeltelijk Gesloten Bovenkant
Schoenen voor Binnen Gebruik - Volledig Gesloten Bovenkant
Schoenkleur/Verf
Schoenpoets-/Schoenreinigingsmiddelen
Schoffelmachines/Grondwoelers/Hakfrezen (Aangedreven)
Schoffels
Schoonheid/Persoonlijke Verzorging/Hygiëne - Assortimenten
Schoonheids-/Cosmetica Accessoires voor Poppen
Schoonmaak-/Hygiënemiddelen - Assortimenten
Schoonmaakapparatuur - Onderdelen/Accessoires
Schoonmaakapparatuur - Overig
Schoonmaakdiensten
Schoonmaakdoekjes
Schoonmaakhulpmiddelen Accessoires
Schoonmaakproducten - Assortimenten
Schoonmaakproducten - Overig
Schoonmaakproducten voor Audio/Video Apparaten
Schoonmaakproducten voor Computer/PC's/Spelcomputers/Games
Schoonmaakproducten voor Muziekinstrumenten
Schoorsteenkap/Regenkap
Schoppen/Spaden
Schorseneerplanten (Scorzonera Hispanica)
Schorseneren
Schottenpompen
Schraapmessen
Schriften
Schrijf/Teken Benodigdheden/Hulpmiddelen - Assortimenten
Schrijf/Teken Benodigdheden/Hulpmiddelen - Overig
Schrijfbenodigdheden - Onderdelen
Schrijfmachines (Elektrisch)
Schrijfmachines (Niet-elektrisch)
Schrikdraad/Draadloze Omheining
Schroefdraadsnijmachines voor Pijpen - Niet-aangedreven
Schroefpistolen
Schroefpompen
Schroeven
Schroevendraaier - Sets
Schroevendraaiers - Niet-aangedreven
Schroevendraaiers - Onderdelen/Accessoires
Schroevendraaiers - Overig
Schroevendraaiers (Aangedreven)
Schroeventrekkers
Schuifdak Zonnekleppen
Schuifmaten (DHZ)
Schuimsnijders - Aangedreven
Schuldbekentenis
Schuurkussentjes/Staalwol
Schuurlinnen
Schuurmachines voor Afwerking
Schuurmiddelen - Assortimenten
Schuurmiddelen - Onderdelen/Accessoires
Schuurmiddelen - Overig
Schuurpapier
Schuurrollers (Aangedreven)
Schuurtjes
Scooter (Niet-aangedreven)
Segmentoverstijgende Classificatie - Assortimenten
Seizoensdecoraties (Elektrisch)
Seizoensdecoraties (Niet-elektrisch)
Selderijkruid (Apium Graveolens)
Selederijplanten (Apium Graveolens)
Semafoon
Senegalese Palissanderbomen (Pterocarpus erinaceus)
Sennaplanten (Senna alexandrina)
Septische Tanks
Seradelleplanten (Ornithopus Sativus)
Sering (Syringa) - Snijbloem
Sering (Syringa) - Snijgroen
Serpentines/Papieren Slingers
Serres
Serveergerei - Assortimenten
Serveergerei - Overig
Serveerkannen/-kruiken/-karaffen
Serveerwagentjes (Verwarmd)
Servers
Servetringen
Servische Spar (Picea omorika)
Sesamplanten (Sesamum Indicum)
Set Glazen
Set-top Boxen/Mediaboxen
Sheabomen (Vitellaria paradoxa)
Shiitakefungus (Lentinula Edodes)
Shiitake's
Shisoplanten (Perilla Frutescens)
Shuttles
Siamese Tulp (Curcuma) - Levende Plant
Sichuan peperplanten (Zanthoxylum)
Sieraden - Assortimenten
Sieraden - Onderdelen
Sieraden - Overig
Sieradenvervaardiging - Accessoires
Sieradenvervaardiging - Materialen
Sierasperge (Asparagus Setaceus) - Snijgroen
Sierasperge (Asparagus Umbellatus) - Snijgroen
Sierkussens
Siervelgen
Sifons/Putten/Douchegoten
Sifons/Putten/Douchegoten - Onderdelen/Accessoires
Sigaren
Sigaretten
Signaalversterkers
Sikkels/Zeisen
SIM-Kaarten/SIM-Kaart Adapters voor Mobiele Telefoon
Sinaasappelbomen (Citrus sinensis)
Sinaasappels
Sint-Janskruid / Mansbloed (Hypericum) - Snijbloem
Sint-Janskruidplanten (Hypericum Perforatum)
Siratroplanten (Phaseolus Atropurpureus)
Siroop/Suikerstroop/Melasse (Houdbaar)
Sisalcactussen (Agave sisalane)
Sjaals/Stropdassen/Dassen
Sjalotplanten (Allium ascalonicum)
Sjalotten
Skateboard Artikelen - Onderdelen/Accessoires
Skateboard/Sportscooter Artikelen - Assortimenten
Skateboard/Sportscooter Artikelen - Overig
Skateboards (Niet-elektrisch)
Ski's/Skiboards/Snowboards
Slaap/Stressverminderende Middelen - Assortimenten
Slaap/Stressverminderende Middelen - Overig
Slaapbolplanten (Papaver Somniferum)
Slaapbomen (Albizia Spp.)
Slaapmiddelen
Slaapmutsen
Slaapzakken
Slabbetjes
Slaghouten/Sticks/Knuppels
Slaghouten/Sticks/Knuppels - Overig
Slaginstrumenten (Elektrisch)
Slaginstrumenten (Niet-elektrisch)
Slagmoersleutels
Slagschroevendraaiers
Slangaansluitstukken
Slangehoutplanten (Rauvolfia Serpentina)
Slangklemmen
Slasauzen//Dipsausjes (Beperkt Houdbaar)
Slasauzen/Dipsausjes (Houdbaar)
Sleedoornbomen (Prunus spinosa)
Sleeën
Sleep/Trekhaak - Assortimenten (Elektrisch)
Sleepkabel/Trekhaak - Assortimenten
Sleepkabel/Trekhaak - Overig
Sleepkabel/Trekhaak - Overig (Elektrisch)
Sleeplichten
Sleeponderdelen - Heavy Duty
Sleutelhangeralarm
Sleutelhangers
Sleutels
Slijmappelbomen (Aegle marmelos)
Slijp-, Breek- & maalmachines (niet-aangedreven)
Slimme Deurbel
Sloophamer
Sloten/Stuurwielvergrendelingen/Pedaalvergrendelingen
Slow Cookers
Sluitingen
Sluitringen
Smart Home/Domotica apparatuur - Slimme stekker/contactdoos
Smartwatches
Smeerbeleg gebaseerd op Noten of Chocolade (Houdbaar)
Smeermiddelen - Assortimenten
Smeermiddelen/Beschermende Middelen - Assortimenten
Smeeroliën/Vloeistoffen
Smeerproducten - Assortimenten
Smeervetten
Smeerwas
Smokers
Snaarinstrumenten (Elektrisch)
Snaarinstrumenten (Niet-elektrisch)
Snacks - Assortimenten
Snacks - Overig
Sneeuwbal (Viburnum) - Snijgroen
Sneeuwbanaanbomen (Ensete glaucum)
Sneeuwbes (Symphoricarpos) - Snijgroen
Sneeuwruimers (Aangedreven)
Snelkokers
Snijbietplanten (Beta Vulgaris Subsp. Vulgaris var. Cicla)
Snijbloemen - Overig
Snijgereedschap
Snijgroen - Assortimenten
Snijgroen - Overig
Snijplanken
Snijplaten/matrijzen (Niet-aangedreven)
Snoeischaar (Aangedreven)
Snoeischaren met Lange Steel (Takken)
Socotra Aloeplanten (Aloe perryi)
Soedangras (Sorghum × Drummondii)
Soep Additieven (Beperkt Houdbaar)
Soep Additieven (Diepvries)
Soep Additieven (Houdbaar)
Soepen - Bereid - Assortimenten
Soepen - Bereid (Beperkt Houdbaar)
Soepen - Bereid (Diepvries)
Soepen - Bereid (Houdbaar)
Software voor Mobiele Telefoon
Software voor Mobiele Telefoon - Digitaal
Soja-/Rijstmelkmachines
Sojaplanten (Glycine Max)
Sokken
Soldaatjeplanten (Orchis Militaris)
Soldeerapparaten
Soldeertoorts
Sopropo
Sopropoplanten (Momordica Charantia)
Spaanse Margriet (Osteospermum) - Levende Plant
Spanningsrails
Spanningsregelaars/-omvormers
Spanschroeven
Spatborden/Spatbordverbreders
Spatels/Scheplepels/Soeplepels
Spatlappen
Speciale Voertuigen
Speciekuipen/Bouwemmers/Mortelkuipen/Mengbakken
Speelgoed Bouwblokken (Niet-elektrisch)
Speelgoed Bouwblokken Elektrisch)
Speelgoed Modelbouw (Elektrisch)
Speelgoed Modelbouw (Niet-elektrisch)
Speelgoed voor Dieren (Elektrisch)
Speelgoed voor Dieren (Niet-elektrisch)
Speelgoed/Spelletjes - Assortimenten
Speelgoed/Spelletjes - Overig
Speelgoedcomputer - Accessoires
Speelgoedcomputers
Speelgoedtekenborden - Accessoires
Speelgoedvervaardiging Accessoires
Speelgoedvoertuigen - Berijdbaar - Accessoires
Speelgoedvoertuigen - Berijdbaar - Overig
Speelgoedvoertuigen - Berijdbaar (Elektrisch)
Speelgoedvoertuigen - Berijdbaar (Niet-elektrisch)
Speelgoedvoertuigen - Niet-berijdbaar - Assortimenten
Speelgoedvoertuigen - Niet-berijdbaar - Overig
Speelgoedvoertuigen - Niet-berijdbaar (Elektrisch)
Speelgoedvoertuigen - Niet-berijdbaar (Niet-elektrisch)
Speeltoestellen en -zwembaden voor Buiten
Speergras (Heteropogon Contortus)
Spelcomputer - Accessoires
Spelcomputer - Draagbaar
Spelcomputer - Niet-Draagbaar
Spelcomputer - Onderdelen
Spellen voor Binnen of Buiten
Spellen/Speeltoestellen voor Buiten - Overig
Speltplanten (Triticum Spelta)
Spermiciden
Sperziebonen/Boterbonen
Spiegels
Spiegels voor Persoonlijke Verzorging
Spijker-/Niet-/Bevestigingsgereedschap - Onderdelen/Accessoires
Spijkertrekkers
Spin-/Weefkunst - Onderdelen/Accessoires
Spin-/Weefmachines (Elektrisch)
Spin-/Weefmachines (Niet-elektrisch)
Spinazie
Spinazie (Vers Gesneden)
Spinazieplanten (Spinacia Oleracea)
Spinnen/Schorpioenen
Spitskool
Spitskoolplanten (Brassica Oleracea var. Capitata F. Conica)
Splitters
Sponsen
Spoorweguitrusting
Sporen - Overig
Sport Beschermingsartikelen - Assortimenten
Sport Beschermingsartikelen - Overig
Sport- en Pleziervaartuigen - Onderdelen/Accessoires (Niet-elektrisch)
Sport- en Pleziervaartuigen (Niet-elektrisch)
Sport Scorebenodigdheden (Elektrisch)
Sportartikelen - Accessoires - Assortimenten
Sportartikelen - Accessoires - Overig
Sportartikelen - Assortimenten
Sportartikelen - Bowlingkegels/Kegels/Stumps
Sportartikelen - Doelen/Netten - Accessoires
Sportartikelen - Doelen/Netten/Omheiningen
Sportartikelen - Lopen
Sportartikelen - Markeerapparaten
Sportartikelen - Matten/Tapijten
Sportartikelen - Opbergrekken/Standaards
Sportartikelen - Scorebenodigdheden (Niet-elektrisch)
Sportartikelen - Springen
Sportartikelen - Tassen/Koffers/Hoezen
Sportartikelen - Werpen
Sportballen
Sportballen/Pucks/Shuttles/Frisbees/Boemerangs - Assortimenten
Sportballen/Pucks/Shuttles/Frisbees/Boemerangs - Overig
Sportdranken - Isotoon/Verrijkt met Mineralen (Gebruiksklaar)
Sportdranken - Isotoon/Verrijkt met Mineralen (Niet-gebruiksklaar)
Sportkleding - Assortimenten
Sportkleding - Dassen en Halsdoeken
Sportkleding - Handschoenen
Sportkleding - Hoofddeksels
Sportkleding - Kleding voor Bovenlichaam
Sportkleding - Kleding voor het hele Lichaam
Sportkleding - Kleding voor het Onderlichaam
Sportkleding - Kousen en Sokken
Sportkleding - Overig
Sportkleding - Riemen
Sportkleding - Spelden/Gespen
Sportschoenen - Algemeen Gebruik
Sportschoenen - Speciaal Gebruik
Sportscooters (Elektrisch)
Sporttafels
Sporttafels - Overig
Sprinkhanen/Krekels - Bereid/Bewerkt
Sprinkhanen/Krekels - Niet-bereid/Niet-bewerkt
Sproeiers/Sprayers/Benevelaars (Handbediend)
Sproeiers/Verstuivers/Benevelaars (Elektrisch)
Sproeiers/Verstuivers/Benevelaars (Slang Uiteinde)
Spruitkool (Spruitjes)
Spruitkoolplanten (Brassica Oleracea var. Gemmifera)
Spuitlakapparatuur - Onderdelen/Accessoires
Spuitpistolen (Aangedreven)
Staal (Gerecycled/Hernieuwbaar)
Staal (Gevormd)
Staal (Ongevormd)
Staalborstels
Staartpeperplanten (Piper Cubeba)
Stabilisé
Stampers (Aangedreven)
Stamslaplanten (Lactuca Sativa var. Angustana)
Standaards/Beugels/Steunen voor Audio/Video Apparaten
Standaards/Houders voor Tuinzakken
Startmotor
Statief (Verlichting)
St-Augustine-gras (Stenotaphrum Secundatum)
Steen-/Houtfineer voor Gevelbekleding
Steenbreek (Saxifraga) - Levende Plant
Steengrillen (Elektrisch)
Steenvruchten (Vers Gesneden)
Steenzaad (Lithodora) - Levende Plant
Stekkers
Stellages/Steigers
Stencils
Stenen/blokken/bakstenen
Stengel- of bosuiplanten (Allium fistulosum)
Stengelgroenten (Vers Gesneden)
Stengels van de Zoete Aardappel
Stengelsla (Vers Gesneden)
Steranijsplanten (Illicium Verum)
Sterilisatoren/Heelkundige Alcohol
Sterke Drank
Sterke-armschaafbanken - Vastgemonteerd
Steunen/Draagbeugels
Steviaplanten (Stevia Rebaudiana)
Stikstof
Stille Wijn
Stinkende-mangobomen (Mangifera foetida)
Stoffen voor Vervaardiging van Beton
Stoffen/Textiel Hand-/theedoeken
Stoffen/Textiel Tafellinnen
Stoffenbeschermers
Stofzuigerbuizen/Stofzuigerslangen
Stofzuigerfilters
Stofzuigermondstukken
Stofzuigerzakken
Stoomovens
Stoomreinigers
Stoomstrijkijzers
Stoot/Trek Speelgoed (Elektrisch)
Stoot/Trek Speelgoed (Niet-elektrisch)
Stootijzers
Stopcontacten/Wandcontactdozen
Stopverf/afdichtkit
Stormdeur - Onderdelen
Stormdeuren - Combinatie Panelen/Glas
Stormramen
Stormschuilplaats
Straatstenen
Stralingsbeschermers voor Mobiele Telefoon
Strandkleding/Cover-Ups
Strawberry Guavabomen (Psidium cattleianum)
Stressverminderende/Kalmerende Middelen
Strijkborden
Strijkconcentraten/Stijfsel
Strijkijzers (Aangedreven)
Strijkplanken (Niet-aangedreven)
Strijkplanken Onderdelen/Accessoires
Strobloem (Helichrysum) - Levende Plant
Strooizout/Antivries Producten
Stroomonderbrekers
Strophantus Kombeplanten (Strophantus Kombe)
Struiken/Bomen - Overig
Struikmargriet (Argyranthemum) - Levende Plant
Struikwindeplanten (Smilax)
Struisgras (Agrostis spp.)
Struisvogelvlees - Bereid/Bewerkt
Struisvogelvlees - Niet-bereid/Niet-bewerkt
Strychninebomen (Strychnos Nux-Vomica)
Stuurwielen
Stuurwielovertrekken
Styloplanten (Stylosanthes Spp.)
Styraxbomen (Styrax benzoin)
Suiker/Kunstmatige Zoetstof (Houdbaar)
Suikerappels/Zoetzakken
Suikerbietenplanten (Beta Vulgaris subsp.Vulgaris var. Altissima )
Suikererwten (Sugar Snaps)
Suikererwtplanten (Pisum Sativum var. Saccharatum)
Suikerij/Groenlof
Suikermais
Suikermeloenplanten (Cucumis Melo var. Reticulatus)
Suikerriet (Vers Gesneden)
Suikerriet (Vers)
Suikerrietplanten (Saccharum Officinarum)
Suikers/ Kunstmatige Zoetstoffen - Assortimenten
Suikersorghumplanten (Sorghum Saccharatum)
Suikerspinmachines
Suikerwortelplanten (Sium Sisarum)
Sukadebomen (Citrus medica)
Sukadecitroenen (Cederappels)
Sumakbomen (Rhus Coriaria)
Sweaters/Pullovers
Sweeties
Switchboxen
Syrische wijnruitstruiken (Peganum Harmala)
Taart/Gebak Decoratiematerialen/Accessoires (Niet-Eetbaar)
Taarten/Gebakjes - Zoet (Beperkt Houdbaar)
Taarten/Gebakjes - Zoet (Diepvries)
Taarten/Gebakjes - Zoet (Houdbaar)
Taarten/Gebakjes/Pizza's/Quiches - Hartig (Beperkt Houdbaar)
Taarten/Gebakjes/Pizza's/Quiches - Hartig (Diepvries)
Taarten/Gebakjes/Pizza's/Quiches - Hartig (Houdbaar)
Tabak - Los
Tabak - Vast
Tabaksplanten (Lobelia Inflata)
Tabakswaren - Pruimtabak/Snuiftabak
Tabakswaren/Cannabis/Kruiden/Rookaccessoires - Assortimenten
Tafelbestek (Niet Wegwerp)
Tafeldruiven
Tafeldruivenplanten (Vitis sp.)
Tafelgerei - Assortimenten
Tafelgerei Accessoires - Assortimenten
Tafelgerei Accessoires - Overig
Tafelgerei Accessoires (Wegwerp)
Tafelkleden/Servetten (Wegwerp)
Tafels met draaiend blad
Tafelslijpmachines (Aangedreven)
Tafelspelen - Overig
Tafelspelen (Elektrisch)
Tafelspelen (Niet-elektrisch)
Tafelzagen - Draagbaar
Tafelzagen - Vastgemonteerd
Tajines (Elektrisch)
Tamarillobomen (Cyphomandra betacea)
Tamarillo's (Boomtomaten)
Tamarinde
Tamarindebomen (Tamarindus indica)
Tampoibomen (Baccaurea macrocarpa)
Tandwielpompen
Tandzaad (Bidens) - Levende Plant
Tangen
Tangen/Grijpers Vervangingsonderdelen/Accesoires
Tangen/Pincetten/Hamers/Stampers/Kwasten
Tangenset
Tangerine Mandarijnen
Tangerinebomen (Citrus tangerina)
Tangors
Tanks/Bakken/Spoelen voor Donkere Kamer
Tanniaplanten (Xanthosoma Sagittifolium)
Tap/Matrijs Sets
Tape (DHZ)
Tape Drives/Tape Streamers
Tappen (Niet-aangedreven)
Taraplanten (Caesalpinia Spinosa)
Taroplanten (Colocasia Antiquorum)
Taro's
Tarweplanten (Triticum spp.)
Tasmaanse peperbomen (Drimys Lanceolata)
Tassen/Koffers/Dozen/Etuis voor Audio/Video Apparaten
Tassen/Koffers/Paraplu's - Assortimenten
Tassen/Koffers/Paraplu's - Overig
Tassen/Toolboxen voor Gereedschap
Tatoeages/Plakkers/Zelfklevende Sieraden - Tijdelijk
Tatsoi
Tatsoiplanten (Brassica Narinosa)
Tavabomen (Pometia pinnata)
Taybesheesters (Rubus Tayberry hybrids)
Teffplanten (Eragrostis Tef)
Tegelsnijders (Niet-aangedreven)
Tekenborden voor Kunstenaars
Tekenhaken (DHZ)
Telecommunicatiediensten
Telecommunicatiekabels
Telefooncentrales
Telefoonhouders
Televisie Combinaties
Televisie Ontvangst/Installatie - Accessoires
Televisie Ontvangst/Installatie - Assortimenten
Televisieshows - Digitaal
Televisietoestellen
Televisietoestellen - Assortimenten
Televisietoestellen - Draagbaar
Televisietoestellen - Onderdelen/Accessoires
Televisietoestellen - Overig
Teltower Rapen
Temoe-koentjieplanten (Boesenbergia Rotunda)
Tentverwarmingstoestellen
Teparyboonplanten (Phaseolus Acutifolius)
Termieten - Niet-bereid/Niet-bewerkt
Terpentijnbomen (Pistacia terebinthus)
Terras Balustrade Onderdelen
Terras Balustrade Systemen - Composiet
Terrasaccessoires
Terrasbodem - Composiet
Terrasoverkapping
Terrasverwarmers (Elektrisch)
Terrasverwarmers (Niet-elektrisch)
Terugslagklep Onderdelen/Accessoires
Terugslagklep Testapparatuur
Terugslagkleppen
Teunisbloemplanten (Oenothera Fruticosa)
Textielverfrissers
Thee - Capsules/Pads
Thee - Instant
Thee - Theezakjes/Los
Thee - Vloeibaar/Gebruiksklaar
Thee - Vloeibaar/Niet-gebruiksklaar
Thee/Koffie Bestek (Niet Wegwerp)
Thee/Koffie/Chocolademelk - Accessoires
Thee/Koffie/Chocolademelk - Assortimenten
Theebomen (Leptospermum)
Theebomen (Melaleuca sp.)
Theeheesters (Camellia sinensis)
Theepotten/Cafetières
Therapeutische Kousen
Thermische Lekdetector
Thermometers
Thermometers voor Levensmiddelen
Thermostaten
Thijmplanten (Thymus Vulgaris)
Thuis Audio Cassettedecks
Thuis Audio CD-Decks
Thuis Audio Effect Apparatuur
Thuis Audio Jukeboxen
Thuis Audio Karaokesystemen
Thuis Audio Losse Luidsprekers
Thuis Audio Luidsprekersystemen
Thuis Audio MD-Decks
Thuis Audio Ontvangers/Tuners/Radio's
Thuis Audio/Video Mixers
Thuis Audioapparatuur - Assortimenten
Thuis Audioapparatuur - Onderdelen/Accessoires
Thuis Audioapparatuur - Overig
Thuisbioscoop Systemen
Thuisdiagnostica - Accessoires
Thuisdiagnostica - Assortimenten
Tijdelijke Classificatie
Tijdelijke Logiesdiensten
Tijdschriften en Kranten - Assortimenten
Tijgerorchidee (Oncidium) - Levende Plant
Tijm
Tillandsia (Bromelia) - Levende Plant
Timer/Besturing voor Bewatering
Timmerhout (Hard Hout)
Timmerhout (Zacht Hout)
Timmerhout/Houten Panelen/Gips - Assortimenten
Timmerhout/Houten Panelen/Gips - Overig
Timoteegras (Phleum Pratense)
Tindolaplanten (Coccinia Grandis)
Tjampedakbomen (Artocarpus integer)
Toastovens
Toebehoren voor Dieren - Assortimenten
Toebehoren voor Dieren - Overig
Toedienings-/Toevoerinrichtingen (Aangedreven)
Toegangscontrole Veiligheidssystemen
Toegangsrooster/ Mattenkader
Toestellen voor Mobiele Communicatie/Diensten - Assortimenten
Toestellen voor Mobiele Communicatie/Diensten - Onderdelen
Toestellen voor Mobiele Communicatie/Diensten - Overig
Toestellen voor Vaste Communicatie - Accessoires
Toestellen voor Vaste Communicatie - Assortimenten
Toestellen voor Vaste Communicatie - Overig
Toetsenborden
Toilet/Bidet - complete set
Toilet/Bidet Frames
Toilet/Bidet Frontplaat
Toilet/Bidet/Urinoir Onderdelen/Accessoires
Toiletbenodigdheden
Toilettassen/Beauty Cases
Toiletten
Tollen/Jojo's
Tomaten - Mengsels (Vers)
Tomaten (Vers Gesneden)
Tomatenketchup/Ketchupvervangers (Beperkt Houdbaar)
Tomatenketchup/Ketchupvervangers (Diepvries)
Tomatenketchup/Ketchupvervangers (Houdbaar)
Tomatenplanten (Solanum Lycopersicum)
Tomatilloplanten (Physalis Philadelphica)
Tomatillo's
Toners/Adstringerende Middelen
Tonkaboonbomen (Dipteryx Odorata)
Topinamboeren (Aardperen)
Touw/koord
Touwen/Kettingen/Kabels
Training/Controle Hulpmiddelen/Toebehoren voor Dieren (Elektrisch)
Training/Controle Hulpmiddelen/Toebehoren voor Huisdieren (Niet-elektrisch)
Traktaties voor dieren (Aanvullende Eetbare Producten) (Beperkt Houdbaar)
Traktaties voor dieren (Aanvullende Eetbare Producten) (Houdbaar)
Traktaties voor Huisdieren (Aanvullende Eetbare Producten) (Diepvries)
Transmissievloeistof
Transmissievloeistof - Assortimenten
Transmissievloeistof - Overig
Transparant Thermoplast
Transparanten/Acetaatzijde
Transpiratiewerende producten/Deodorants
Transponders
Transportdiensten
Trapleuningen
Trappalen
Trappen - Geprefabriceerd
Trechters (DHZ)
Trechters voor Levensmiddelen
Trekking/Bergsport Artikelen
Trekking/Bergsport Artikelen - Overig
Trillingsdempers
Trolleys
Trommelversnipperaars/Stobberooiers (Aangedreven)
Trompetlelie (Lilium) - Snijbloem
Trosgierst (Setaria Italica)
Trosgierst (Setaria) - Snijgroen
Trosraaigras (× Schedolium Loliaceum)
Truffelfungus (Tuber Aestivum)
Truffels
Ttriticaleplanten (Triticosecale)
Tuin Afvalsystemen - Onderdelen/Accessoires
Tuin Afvalsystemen - Overig
Tuin Analyseapparatuur - Onderdelen/Accessoires
Tuin Analyseapparatuur - Overige
Tuin Bewateringsapparatuur - Assortimenten
Tuin Bewateringsapparatuur Onderdelen
Tuin Bewateringsapparatuur Overig
Tuin Dierafschrikmiddelen/Dierafweermiddelen - Elektrisch
Tuin Dierafschrikmiddelen/Dierafweermiddelen - Niet-elektrisch
Tuin Handgereedschap - Assortimenten
Tuin Handgereedschap - Onderdelen/Accessoires
Tuin Handgereedschap - Overig
Tuin Knielkussens/Zitjes
Tuin Kook-/Verwarmingstoestellen - Assortimenten
Tuin Kook/Verwarmingstoestellen - Onderdelen/Accessoires
Tuin Kook-/Verwarmingstoestellen - Overig
Tuin Legplanken/Werkbladen
Tuin Omheining - Assortimenten
Tuin Omheining - Overig
Tuin Omheining Accessoires
Tuin Opslagbox
Tuin Schommelstoelen en banken
Tuin Sofa's - ligbedden
Tuin Stofzuigers/Blazers
Tuin Uitstalkasten/Etagères
Tuin Verbrandingsovens
Tuin Voetsteunen
Tuin Wateropslagbenodigdheden
Tuin Waterpartijen
Tuin Zonnedaken/Zeildoeken
Tuin Zwembaden/Vijvers/Waterpartijen - Assortimenten
Tuin Zwembaden/Vijvers/Waterpartijen - Overig
Tuin/Waterpartij Decoratie
Tuinaarde/-mest - Overige
Tuinaarde/Potgrond
Tuinbanken
Tuinbonen
Tuinboonplanten (Vicia Faba var. Major)
Tuinerwtplanten (Pisum Sativum)
Tuingereedschap - Accessoires
Tuingereedschap - Assortimenten
Tuingereedschap - Overig
Tuinhuisjes/Kassen - Assortimenten
Tuinhuisjes/Kassen - Onderdelen/Accessoires
Tuinhuisjes/Kassen - Overig
Tuinhuisjes/Pergola's/Priëlen
Tuinkers
Tuinkersplanten (Lepidium Sativum)
Tuinmeubelen - Assortimenten
Tuinmeubelen - Onderdelen/Accessoires
Tuinmeubelen - Overig
TuinParaplu's/Parasols
Tuinranden/opsluitbanden
Tuinslangen
Tuinstoelen
Tuintafels
Tuintegels
Tuintractors
Tuinverlichting - Onderdelen/Accessoires
Tuinverlichting - Overig
Tuinwagens (Aangedreven)
Tuinwagens (Niet-aangedreven)
Tuinzakken
Tulp - Bol/Knol
Tulp - Levende Plant
Tulp - Snijbloem
Turkse Oregano
Turkse Oregano (Origanum Onites)
Tussen lagerpompen
Tussenlagen
Tweenaaldige Pinyon Den (Pinus edulis)
Ubeplanten (Dioscorea Alata)
Udjong Atupbomen (Baeckea Frutescens)
Ugli's
Uien
Uienplanten (Allium cepa)
Uitbreidingsborden/-kaarten
Uitgangsmateriaal
Uitlaatfilter Reiniger
Uitnodigingskaartjes/-briefjes
Uitrusting voor Vaartuigen (Niet-aangedreven) - Assortimenten
Uitrusting voor Vaartuigen (Niet-aangedreven) - Overig
Universele Afstandsbedieningen
Universele Elektrische Timers/Controllers
Universele Televisiemeubels
Urenaplanten (Urena lobata)
Urinoirs
Urnen
USB Audio Interfaces
USB Internet Stick
USB Sticks
UTV's/Quad's
UV Reinigers voor Zwembad/Vijver/Waterpartij
Vaatwasmachine - Additieven
Vaatwasmachine - Afwaszout
Vaatwasmachine - Spoelmiddel
Vaatwasmachine - Verfrissers
Vaatwasmachine - Wasmiddel
Vaatwasmachines
Vacuümmachines (Elektrisch)
Valeriaanplanten (Valeriana Officinalis)
Valse Christusdoornbomen (Gleditsia Triacanthos)
Valse Sagopalm (Cycas) - Levende Plant
Valse Wimpers
Vanda - Levende Plant
Vanda - Snijbloem
Vanillebladplanten (Achlys Triphylla)
Vanilleplanten (Vanilla Planifolia)
Varens (Vers Gesneden)
Varkensvlees - Bereid/Bewerkt
Varkensvlees - Niet-bereid/Niet-bewerkt
Vaste Brandstoffen
Vazen
Veenbramen/Kruipbramen
Veiligheid/Toezicht/Beveiliging - Assortimenten
Veiligheid/Toezicht/Beveiliging voor Baby's - Assortimenten
Veiligheid/Toezicht/Beveiliging voor Baby's - Onderdelen
Veiligheid/Toezicht/Beveiliging voor Baby's - Overig
Veiligheids-/Beschermende Overschoenen
Veiligheids-/Beschermende Schoenen
Veiligheids-/Beschermingslaarzen
Veiligheidsbrillen/Stofbrillen
Veiligheidsdeuren/Veiligheidspoorten
Veiligheidsfakkels/Signalen
Veiligheidsgordelbeschermers
Veiligheidsgordels/Verlengstukken
Veiligheidskleppen/Vacuümbrekers
Veiligheidslichten
Veiligheidslint voor Versperringen
Veiligheidsnetten/Gordijnen/Afsluitingen
Veiligheidsproduct voor Weer/Natuurrampen - Assortimenten
Veiligheidsproducten voor Computer/PC's/Spelcomputers/Games
Veldbeemdgras (Poa Pratensis)
Veldboonplanten (Macroptilium Lathyroides)
Veldboonplanten (Vicia Faba subsp. Minor)
Velderwtplanten (Pisum Sativum Subsp. Arvense)
Veldsla
Veldslaplanten (Valerianella Locusta)
Velgen
Venkel
Venkelplanten (Foeniculum Vulgare)
Vensterbanken
Ventilators - Draagbaar
Ventilators - Extractieapparaat
Ventilators - Plafond
Ventilators - Venster
Venus Vliegenval (Dionaea) - Levende Plant
Venusschoentje (Paphiopedilum) - Levende Plant
Verdampingsmeters - Elektrisch
Verdeelborden/-kasten
Verdovingsgeweren
Veren
Verf - Assortimenten
Verf - Overig
Verf-/Kleurstofzeven
Verf/Vernis Verwijderproducten/Schoonmaakmiddelen
Verfadditieven
Verfapparatuur - Accessoires
Verfapparatuur - Niet-aangedreven
Verfapparatuur - Onderdelen
Verfbremstruiken (Genista tinctoria)
Verfinstrumenten - Aangedreven
Verfkwasten/-rollers/-applicatoren
Verfpistolen
Vergrootglazen
Vergruizers
Verkleedkleding Accessoires (Elektrisch)
Verkleedkleding Accessoires (Niet-elektrisch)
Verkleedpakken
Verkleedpakken en Accessoires - Assortimenten
Verkleedpakken en Accessoires - Overig
Verkoelende Gezichts-/Lichaamsbenevelaars
Verkoopautomaat
Verkoudheid/Hoest Middelen
Verlengsnoeren/Stroomkabels
Verlichting - Vast
Verlichting Onderkant Wagen
Verlichting/Reflectors van Aanhangwagen
Verontreinigde/Beschadigde Eieren in Schaal
Verpakkings- / Opslagdiensten
Verpakkingsmateriaal
Verrekijkers
Verstekzagen - Draagbaar
Verstelbare Bedden (Elektrisch)
Verstelbare Bedden (Niet-elektrisch)
Versterkers
Versterkte Wijn
Verticaal hangende pompen
Verticale Jaloezieën
Vervangingsmiddel voor Kaas (Beperkt Houdbaar)
Vervangingsmiddel voor Kaas (Diepvries)
Vervangingsmiddel voor Kaas (Houdbaar)
Vervangingsmiddel voor Yoghurt (Diepvries)
Vervangingsproducten voor Melk (Beperkt Houdbaar)
Vervangingsproducten voor Melk (Diepvries)
Vervangingsproducten voor Melk (Houdbaar)
Vervangingsproducten voor Room (Beperkt Houdbaar)
Vervangingsproducten voor Room (Diepvries)
Vervangingsproducten voor Room (Houdbaar)
Vervangingsproducten voor Yoghurt (Beperkt Houdbaar)
Vervangingsproducten voor Yoghurt (Houdbaar)
Verven
Verven voor Speciale Doeleinden
Verven/Kleurstoffen voor Kunstenaars
Vervoermiddelen voor Huisdieren
Verwarmingsinstallatie - Assortimenten
Verwarmingskabel/Verwarmingstape
Verwarmingssysteem Besturingen
Verwarmingstoestellen - Onderdelen/Accessoires
Verwarmingstoestellen - Overig
Verwarmingstoestellen (Tuin)
Verwijderproducten voor Plakpasta/Lijm
Verwisselbare Lenzen
Verwisselbare Schijven
Verzendbuizen/Verzenddozen
Verzendmaterialen/Postverwerking/Accessoires - Assortimenten
Verzendmaterialen/Postverwerking/Accessoires - Overig
Verzorging van Dieren - Hulpmiddelen
Verzorging voor Dieren - Assortimenten
Verzorging/Behandeling van Zintuigen - Assortimenten
Verzorging/Behandeling van Zintuigen - Overig
Verzorging/Voedingsmiddelen voor dieren - Assortimenten
Verzorgingsmiddelen/Reparatiekits voor Kampeertenten
Verzorgingsproducten voor Brillen
Verzorgingsproducten voor Brillen - Accessoires
Verzorgingsproductenvoor Contactlenzen
Veterinaire Diensten
Veterinaire Geneesmiddelen
Veterinaire Medische Hulpmiddelen
Vetivergras (Chrysopogon Zizanioides)
Vetkruid / Hemelsleutel / Muurpeper / Tripmadam (Sedum) - Levende Plant
Vetplanten (Vers Gesneden)
Vetspuiten (Aangedreven)
Video (Niet Films) - Digitaal
Video Adapters
Video Editor
Video Hard Disc Recorders
Video Opname/Weergave - Assortimenten
Video Opname/Weergave - Onderdelen/Accessoires
Video Spelers/Recorders
Video Splitters/Verdelers
Videocassettes - Opneembaar
Videocassettes - Voorbespeeld
Vietnamese korianderplanten (Persicaria Odorata)
Vijgebomen (Ficus carica)
Vijgen
Vijlen
Vijver/Waterpartij Beluchters
Vijver/Waterpartij Warmeluchtverstuivers
Vingergierstplanten (Eleusine Coracana)
Vingergras (Digitaria spp.)
Vingergras / Gierst (Panicum) - Snijgroen
Vingerhoedskruidplanten (Digitalis Purpurea)
Vingerplant (Fatsia) - Snijgroen
Vingersboom (Schefflera) - Levende Plant
Vinyl - Voorbespeeld
Violenplanten (Viola)
Violier (Matthiola) - Snijbloem
Violier (Matthiola) - Snijgroen
Viooltje / Viool - Levende Plant
Viooltjesplanten (Viola Tricolor)
Virginische Jeneverbesbomen (Juniperus Virginiana)
Vis - Bereid/Bewerkt (Beperkt Houdbaar)
Vis - Bereid/Bewerkt (Diepvries)
Vis - Bereid/Bewerkt (Houdbaar)
Vis - Niet-bereid/Niet-bewerkt (Beperkt Houdbaar)
Vis - Niet-bereid/Niet-bewerkt (Diepvries)
Vis - Niet-bereid/Niet-bewerkt (Houdbaar)
Vishaken
Vislijn/Visgaren
Visnetten
Vissen
Visvervangers - Assortimenten
Visvervangers - Met Dierlijke Ingrediënten (Beperkt houdbaar)
Visvervangers - Met Dierlijke Ingrediënten (Diepvries)
Visvervangers - Met Dierlijke Ingrediënten (Houdbaar)
Visvervangers - Zonder Dierlijke Ingrediënten (Beperkt houdbaar)
Visvervangers - Zonder Dierlijke Ingrediënten (Diepvries)
Visvervangers - Zonder Dierlijke Ingrediënten (Houdbaar)
Viszoekers
Vitaminen/Mineralen
Vitaminen/Mineralen/Voedingssupplementen - Assortimenten
Vlakschuurmachines
Vlambloem / Phlox - Levende Plant
Vlambloem / Phlox - Snijbloem
Vlasplanten (Linum usitatissimum)
Vleesmolens/Gehaktmolens (Elektrisch)
Vleespennen/Sticks
Vleestomaten
Vleesvervangers - Assortimenten
Vleesvervangers - Met Dierlijke Ingrediënten (Beperkt houdbaar)
Vleesvervangers - Met Dierlijke Ingrediënten (Diepvries)
Vleesvervangers - Met Dierlijke Ingrediënten (Houdbaar)
Vleesvervangers - Zonder Dierlijke Ingrediënten (Beperkt houdbaar)
Vleesvervangers - Zonder Dierlijke Ingrediënten (Diepvries)
Vleesvervangers - Zonder Dierlijke Ingrediënten (Houdbaar)
Vlekverwijderaars
Vleugelbonen (Goabonen)
Vleugelboonplanten (Psophocarpus Tetragonolobus)
Vliegen - Niet-bereid/Niet-bewerkt
Vlieger/Parachute Artikelen - Assortimenten
Vlieger/Parachute Artikelen - Onderdelen/Accessoires
Vlieger/Parachute Artikelen - Overig
Vliegers
Vlierbesheesters (Sambucus)
Vlierbessen
Vlijtig Liesje / Springzaad (Impatiens) - Levende Plant
Vlinderorchidee (Phalaenopsis) - Levende Plant
Vlinderorchidee / Orchidee (Phalaenopsis) - Snijbloem
Vlinders/Motten - Bereid/bewerkt
Vlinders/Nachtvlinders - Niet-bereid/Niet-bewerkt
Vloeibare Bouillon/Beenderen (Beperkt Houdbaar)
Vloeibare Bouillon/Beenderen (Diepvries)
Vloeibare Bouillon/Beenderen (Houdbaar)
Vloeibare Brandstof Flessen/Bussen (Leeg)
Vloeibare Brandstoffen
Vloeistofpistolen
Vloerconstructies
Vloerluik
Vloermateriaal - Accessoires
Vloermateriaal - Assortimenten
Vloermateriaal - Keramische/Porseleinen Tegels
Vloermateriaal - Kurk/Bamboe
Vloermateriaal - Lamelparket
Vloermateriaal - Laminaat
Vloermateriaal - Massief Hout
Vloermateriaal - Onderlaag
Vloermateriaal - Overig
Vloermateriaal - Steen/Marmer
Vloermateriaal - Tapijt
Vloermateriaal - Vinyl/Rubber/Linoleum
Vloertapijten/Matten – Verwijderbaar
Vloerverwarmingssystemen
Vochtige Doekjes
Vochtigheidsmeter
Voederbietplanten (Beta Vulgaris Subsp. Vulgaris var. Crassa)
Voedererwtplanten (Pisum Sativum var. Arvense)
Voederwikkeplanten (Vicia Sativa)
Voedingen voor Computers
Voedingsmiddelen voor dieren (Beperkt Houdbaar)
Voedingsmiddelen voor dieren (Diepvries)
Voedingsmiddelen voor dieren (Houdbaar)
Voedingsmiddelen/Dranken voor dieren - Assortimenten
Voedingssupplementen
Voedingssupplementen voor Dieren
Voedingssupplementen voor Dieren - Assortimenten
Voedingssupplementen voor Dieren - Overig
Voedseladditieven
Voedselrekken/Displays
Voegmortel
Voer- en Drinkbakken voor Dieren
Voertuig Tracking Systemen
Voet/Been Verzorging/Behandeling - Assortimenten
Voet/Been Verzorging/Behandeling - Overig
Vogelmelk (Ornithogalum) - Snijbloem
Vogels
Voltmeters/Multimeters
Voorbedrukte Borden
Voorbehandelingsmiddelen voor Bouwstoffen
Voorbespeelde Media - Assortimenten
Voorbespeelde Media - Overig
Voorjaarsadonisplanten (Adonis Vernalis)
Voorruit Zonnekleppen
Voorruitontwaseming Reparatiekits
Voorruitzonneschermen
Vormgips
Vormpjes voor Levensmiddelen
Vossenbesheesters (Vaccinium vitis-idaea)
Vossenbessen/Rode Bosbessen
Vouwgordijnen
Vriesea (Bromelia) - Levende Plant
Vrije Gewichten/Handhalters
Vrouwelijke Hygiëne - Accessoires
Vrouwelijke Hygiëne - Assortimenten
Vrouwelijke Hygiëne - Cups
Vrouwelijke Hygiëne - Inlegkruisjes
Vrouwelijke Hygiëne - Maandverbanden
Vrouwelijke Hygiëne - Overig
Vrouwelijke Hygiëne - Tampons
Vrouwenmantel / Leeuwenklauw (Alchemilla) - Snijbloem
Vruchten- en Kruideninfusies/-tisanes - Capsules/Pads
Vruchten- en Kruideninfusies/-tisanes - Instant
Vruchten- en Kruideninfusies/-tisanes - Theezakjes/Los
Vruchten- en Kruideninfusies/-tisanes - Vloeibaar/Gebruiksklaar
Vruchten- en Kruideninfusies/-tisanes - Vloeibaar/Niet-gebruiksklaar
Vruchtenpersen (Elektrisch)
Vruchtensap - Gebruiksklaar (Beperkt Houdbaar)
Vruchtensap - Gebruiksklaar (Houdbaar)
Vruchtensap - Niet-gebruiksklaar (Diepvries)
Vruchtensap - Niet-gebruiksklaar (Houdbaar)
Vuile oortjes (Angelonia) - Levende Plant
Vuilnisbakken voor Buiten
Vulmateriaal
Vuurwapens - Onderdelen/Accessoires
Vuurwerk
Vuurwerkplanten (Dictamnus Albus)
Waaierpalm (Livistona) - Levende Plant
Wachtrij afscheidingen/ afzetlintpalen
Walvissen/Dolfijnen/Bruinvissen
Wampeebomen (Clausena lansium)
Wandbekleding – Sierobjecten
Wapitivlees - Bereid/Bewerkt
Wapitivlees - Niet-bereid/Niet-bewerkt
Waringin / Treurvijg (Ficus) - Levende Plant
Warmhoudplaten (Elektrisch)
Wasabiplanten (Eutrema Japonicum)
Wasautomaten
Wasbakken
Wasdrogers
Wasdrogers (niet-aangedreven)
Wasmanden
Wasmiddelen
Wasmiddelversterkers/Bleekmiddelen
Wasophang hulpmiddelen
Waspalmbomen (Ceroxylon quindiuense)
Waspompoenplanten (Benincasa Hispida)
Wasproducten - Assortimenten
Wasproducten - Overig
Wastafel onderstellen
Wastafel/Onderkast Combinaties
Wastafelbenodigdheden
Wasverzachters/Conditioners
Wasverzorgingstoestellen - Onderdelen/Accessoires
Wasverzorgingstoestellen - Overig
Waszakken
Water applebomen (Syzygium aqueum)
Water/Bodem Analyseapparatuur (Elektrisch)
Water/Bodem Analyseapparatuur (Niet-elektrisch)
Water-/Drankapparatuur - Assortimenten
Water-/Drankapparatuur - Overig
Water-/Gasvoorziening - Assortimenten
Waterautomaten - Tafelmodel
Waterautomaten - Vrijstaand
Waterbehandelingen (DHZ)
Waterbuffelvlees - Bereid/Bewerkt
Waterbuffelvlees - Niet-bereid/Niet-bewerkt
Watercacao (Pachira) - Levende Plant
Waterdichtmakende Sprays/Impregneermiddelen
Waterfilters/Waterfilter Patronen
Waterfiltratie Machines/Systemen
Waterkastanjeplanten (Eleocharis Dulcis)
Waterkastanjes (Vers)
Waterkers
Waterkersplanten (Nasturtium Officinale)
Waterlelie / Witte Waterlelie (Nymphaea) - Levende Plant
Watermeloenen
Watermeloenplanten (Citrullus Lunatus)
Watermeters
Wateropslag/-behandeling - Assortimenten
Wateropslag/-behandeling - Onderdelen/Accessoires
Waterpassen
Waterpassen met Laser
Waterpeperplanten (Persicaria Hydropiper)
Waterplanten - Bereid/Bewerkt (Beperkt Houdbaar)
Waterplanten - Bereid/Bewerkt (Diepvries)
Waterplanten - Bereid/Bewerkt (Houdbaar)
Waterplanten - Niet-bereid/Niet-bewerkt (Beperkt Houdbaar)
Waterplanten - Niet-bereid/Niet-bewerkt (Diepvries)
Waterplanten - Niet-bereid/Niet-bewerkt (Houdbaar)
Waterreservoirs voor Toilet/Urinoir
Waterspeelgoed voor Bad/Zwembad
Waterspinazie/Ong Choy/Kangkung
Waterspinazieplanten (Ipomoea Aquatica)
Watertanks
Watertestkits
Waterverwarmer zonder Reservoir
Waterverzachters
Waterverzachters (DHZ)
Waterverzachters Onderdelen/Accessoires
Waterzagen/Tegelsnijders/Glassnijders
Watten Producten
WC-Brillen
WC-papier
WC-Schoonmaakproducten
Webcams
Weegbreeplanten (Plantago Lanceolata)
Weekdieren
Weerstation - Assortimenten
Weerstation - Elektrisch
Weerstation - Niet-elektrisch
Weerstation - Onderdelen/Accessoires
Weerstation - Overig
Wegwerp Draagtassen
Wegwerp Scheermesjes (Niet-elektrisch)
Wegwerpdozen voor Levensmiddelen
Wegwerpkookgerei
Wegwerptafelgerei/Wegwerptafelbekleding
Wegwerpverpakkingen Levensmiddelen - Assortimenten
Wegwerpverpakkingen Levensmiddelen - Overig
Wegwerpverpakkingsfolie voor Levensmiddelen
Wegwerpzakjes voor Levensmiddelen
Weichselbomen (Prunus Mahaleb)
Wekkers
Welriekende Ganzevoetplanten (Chenopodium Ambrosioides)
Welzijn/Hygiëne voor Dieren - Assortimenten
Welzijn/Hygiëne voor Dieren - Overig
Wenskaartdisplays
Wenskaarten/Uitnodigingen
Wenskaarten/Uitnodigingen - Assortimenten
Wenskaarten/Uitnodigingen - Overig
Werkbank/Werktafel - Onderdelen/Accessoires
Werkbanken
Werkbladen
Werkplaatshulpmiddelen - Onderdelen/Accessoires
Werkplaatshulpmiddelen - Overig
Westerse Levensboom (Thuja Occidentalis)
Wetenschappelijk Speelgoed (Elektrisch)
Wetenschappelijk Speelgoed (Niet-elektrisch)
Wetenschappelijke en Technologische Diensten
Wieldoppen
Wielen/velgen
Wierook
Wierookbomen (Boswelia)
Wierookhouders/Wierookbranders en accessoires
Wiggen
Wijnaccessoires
Wijndruifplanten (Vitis vinifera)
Wijnkoelers
Wijnpalmbomen (Jubaea)
Wijnruitplanten (Ruta Graveolens)
Wild Zwijn Vlees - Bereid/Bewerkt
Wild Zwijn Vlees - Niet-bereid/Niet-bewerkt
Wilde appelbomen (Malus sylvestris)
Wilde Appels
Wilde Bosbessen
Wilde Cichorei
Wilde Cichoreiplanten (Cichorium Intybus var. Sativum)
Wilde citroenbomen (Poncirus trifolata)
Wilde lijsterbesbomen (Sorbus aucuparia)
Wilde Paddenstoelenfungus
Wilde Perziken (Paraquayos)
Wilde Rijstplanten (Zizania Aquatica)
Wilg (Salix) - Snijgroen
Windmeters - Elektrisch
Windmeters - Niet-elektrisch
Windwijzers/Windvanen
Winkeldisplay/-vitrine
Wintermeloenen of Andere Suikermeloenen
Wintermeloenplanten (Cucumis Melo var. Inodorus)
Wintersport Artikelen - Assortimenten
Wintersport Artikelen - Onderdelen/Accessoires
Wintersport Artikelen - Overig
Wisselbloem (Lantana) - Levende Plant
Wissers
Witlof (Witloof)
Witlofplanten (Cichorium Intybus var. Foliosum)
Witte Esdoornbomen (Acer Saccharum)
Witte Heggerankplanten (Bryonia Alba)
Witte Honingklaver (Melilotus Albus)
Witte Klaverplanten (Trifolium Repens)
Witte Kool
Witte Mimosabomen (Leucaena Leucocephala)
Witte Mosterdplanten (Sinapis Alba)
Witte Raapplanten (Brassica Rapa Subsp. Rapa)
Witte Ramanasplanten (Raphanus Sativus var. Longipinnatus)
Witte Rapen
Witte Sapota
Witte Tayers
Witte zapotebomen (Casimiroa edulis)
Witte-koolplanten (Brassica Oleracea var. Capitata)
Witvlezige drakenvruchtplanten (Hylocereus undatus)
Woks (Elektrisch)
Wolfskersplanten (Atropa Belladonna)
Wolfspootplanten (Lycopus Europaeus)
Wolverleiplanten (Arnica montana)
Wonderbomen (Ricinus Communis)
Wormen
Worsten van Kalfsvlees - Bereid/Bewerkt
Worsten van Kalkoenvlees - Bereid/Bewerkt
Worsten van Kippenvlees - Bereid/Bewerkt
Worsten van Lams-/Schapenvlees - Bereid/Bewerkt
Worsten van Rundvlees - Bereid/Bewerkt
Worsten van Varkensvlees - Bereid/Bewerkt
Wortelen
Wortelpeterselie
Wortelplanten (Daucus Carota)
Wortels/Knollen (Vers Gesneden)
Wrat/Likdoorn/Eeltplek Behandelingen
XPS Bouwplaten en Tegelelementen
Xylopia aethiopicaplanten (Xylopia Aethiopica)
Ya Peren (Chinese Peren)
Ya perenbomen (Pyrus bretschneideri)
Yaconplanten (Smallanthus Sonchifolius)
Yamboon
Yamboonplanten (Pachyrhizus Erosus)
Yamknollen
Yamplanten (Dioscorea Esculenta)
Yehebplanten (Cordeauxia Edulis)
Yerba Mateplanten (Ilex paraguariensis)
Ylang-Ylangbomen (Cananga Odorata)
Yoghurt (Beperkt Houdbaar)
Yoghurt (Diepvries)
Yoghurt (Houdbaar)
Yoghurtmakers
Yohimbebomen (Pausinystalia Johimbe)
Yucca - Levende Plant
Zaadbakjes
Zaagbladen - Niet-aangedreven
Zaagbokken/Schragen
Zaailingen - Gebruiksklaar
Zachtboard Platen
Zachtfruit/Kleinfruit - Mengsels
Zaden - Overig
Zagen - Niet-aangedreven
Zakenformulieren - Voorgedrukt
Zamio / Zamioculcas - Levende Plant
Zand (DHZ)
Zandhaver (Leymus spp.)
Zandkunst Benodigdheden
Zandstraalmachines
Zandzakken/Overstromingsbeveiliging
Zantedeschia/Calla - Bol/Knol
Zeealsemplanten (Artemisia Maritima)
Zeekool
Zeekraal
Zeesterren/Zee-egels
Zee-uiplanten(Urginea Maritima)
Zeevruchtenvervangers - Assortimenten
Zeevruchtenvervangers - Met Dierlijke Ingrediënten (Beperkt Houdbaar)
Zeevruchtenvervangers - Met Dierlijke Ingrediënten (Diepvries)
Zeevruchtenvervangers - Met Dierlijke Ingrediënten (Houdbaar)
Zeevruchtenvervangers - Zonder Dierlijke Ingrediënten (Beperkt houdbaar)
Zeevruchtenvervangers - Zonder Dierlijke Ingrediënten (Diepvries)
Zeevruchtenvervangers - Zonder Dierlijke Ingrediënten (Houdbaar)
Zekeringen
Zelfklevende Memo/Papierblokhouders
Zelfverdedigingssprays
Zeven (Tuin)
Zeven/Ziften/Vergieten
Zevenbomen (Juniperus Sabina)
Zijruit Zonnekleppen
Zilte Groenten - Overig
Zilte Groenten (Vers Gesneden)
Zilverkruiskruid (Senecio) - Levende Plant
Zilverstruikje (Calocephalus) - Levende Plant
Zip/Jazz Schijven
Zitzakken/Poefs/Lounge Stoelen
Ziziphus mucronatabomen (Ziziphus Mucronata)
Zoet Smeerbeleg - Assortimenten
Zoete Aardappelen
Zoete Aardappelplanten (Ipomoea Batatas)
Zoete Bakkerij Producten - Assortimenten
Zoete Granadillabomen (Passiflora ligularis)
Zoete Granadilla's
Zoete Kersen
Zoete kersenbomen (Prunus avium)
Zoete limoenbomen (Citrus limettioides)
Zoete Maisplanten (Zea Mays Subsp. Saccharata)
Zoete puntpaprika's
Zoethoutplanten (Glycyrrhiza Glabra)
Zoetwaren Producten - Assortimenten
Zoetwaren/Kunstmatige Zoetstof - Assortimenten
Zoetzak/Suikerappelbomen (Annona squamosa)
Zomeralsemplanten (Artemisia Annua)
Zomerpompoen (Cucurbita Maxima) - Snijgroen
Zon/Dromenvangers/Windklokkenspel
Zonbeschermende Producten
Zonnebank
Zonnebesplanten (Solanum Retroflexum)
Zonnebloem (Helianthus) - Levende Plant
Zonnebloem (Helianthus) - Snijbloem
Zonnebloemplanten (Helianthus Annuus)
Zonnebrillen - Klaar voor Gebruik
Zonne-energie Set
Zonneschermen - Elektrisch
Zonneschermen - Niet-elektrisch
Zonneschijnautograaf - Elektrisch
Zout-/Peper-/Kruidenmolens (Niet-elektrisch)
Zout-/Pepervaten
Zoute Stengels/Mini Pretzels
Zoysia-gras (Zoysia spp.)
Zuid-Afrikaanse Margriet (Euryops) - Levende Plant
Zuiderwindlelie (Ornithogalum) - Levende Plant
Zuigerpompen
Zuignappen/Zuigvoeten
Zuigtoestellen (Elektrisch)
Zuigtoestellen (Niet-elektrisch)
Zuilen
Zuivelspread (Beperkt Houdbaar)
Zuivelspread (Diepvries)
Zuivelspread (Houdbaar)
Zure Blimbingen
Zure Kersen
Zure kersenbomen (Prunus cerasus)
Zure sinaasappelbomen (Citrus aurantium)
Zuring
Zuringplanten (Rumex Acetosa)
Zuringplanten (Rumex sp.)
Zuurzak/Guanabanabomen (Annona muricata)
Zwaaihaak
Zwaailichten met Sirene
Zwaardboonplanten (Canavalia Gladiata)
Zwaardvaren (Nephrolepsis) - Levende Plant
Zwanenplant (Gomphocarpus) - Snijgroen
Zwangerschap Huidverzorging/Vochtinbrengende Producten
Zwangerschapsband
Zware Wapens
Zware Wapens - Munitie
Zware Wapens - Onderdelen en Accessoires
Zwarte Bessen
Zwarte komijnplanten (Nigella Sativa)
Zwarte Mosterdplanten (Brassica Nigra)
Zwarte nachtschadeplanten (Solanum Nigrum)
Zwarte Rammenasplanten (Raphanus Sativus var. Niger)
Zwarte Sapota
Zwarte zapotebomen (Diospyros digyna)
Zwartebesstruiken (Ribes Nigrum)
Zwartmoeskervelplanten (Smyrnium Olusatrum)
Zwartoogbonen
```



#### Language Options

The `language` field can contain the following values:

```plaintext
Abchazisch
Afaan Oromo
Afar
Afrikaans
Akan
Albanees
Amhaars
Arabisch
Aragonees
Armeens
Assamees
Avaars
Avestisch
Aymara
Azerbeidzjaans
Bambara
Basjkiers
Bengaals
Birmaans / Birmees
Bosnisch
Bretons
Bulgaars
Catalaans
Chamorro
Chinees
Cornisch
Deens
Divehi
Duits
Dzongkha
Engels
Esperanto
Estisch
Fijisch
Fins
Frans
Fula
Galicisch
Georgisch
Grieks
Groenlands
Guaraní
Haïtiaans Creools
Hebreeuws
Hongaars
Iers
Ijslands
Indonesisch
Italiaans
Japans
Kannada
Kasjmiri
Kerkslavisch
Koerdisch
Koreaans
Kroatisch
Laotiaans
Latijn
Lets
Limburgs
Litouws
Luba-Katanga
Luganda
Luxemburgs
Macedonisch
Malayalam
Maleis
Maltees
Mongools
Nauruaans
Ndonga
Nederlands
Nepalees
Nynorsk
Occitaans
Oekraïens
Pali
Perzisch
Plateaumalagasi
Pools
Portugees
Reto-Romaans
Roemeens
Russisch
Samoaans
Schots-Gaelisch
Servisch
Sloveens
Slowaaks
Soendanees
Spaans
Swahili
Tadzjieks
Tagalog
Thais
Tibetaans
Tigrinya
Tsjechisch
Turks
Twi
Venda
Vietnamees
Waals
Welsh
Westerlauwers Fries
Wit-Russisch
Zhuang
Zoeloe
Zuid-Sotho
Zweeds
```

#### Target Market Country Options

The `targetMarketCountry` field can contain the following values:

```plaintext
Afghanistan
Aland-eilanden
Albanië
Algerije
Amerikaans Samoa
Andorra
Angola
Anguilla
Antarctica
Antigua en Barbuda
Argentinië
Armenië
Aruba
Australië
Azerbeidzjan
Bahamas
Bahrein
Bangladesh
Barbados
België
Belize
Benin
Bermuda
Bhutan
Bolivia (Plurinationale Staat)
Bonaire, Sint Eustatius en Saba
Bosnië-Herzegovina
Botswana
Bouvet Island
Brazilië
Brits-Indisch oceaan gebied
Brunei Darussalam
Bulgarije
Burkina Faso
Burundi
Cabo Verde
Cambodja
Canada
Centraal Afrikaanse Republiek
Chili
China
Cocos (Keeling) eilanden
Colombia
Comoren
Congo
Congo (de Democratische Republiek)
Cook eilanden
Costa Rica
Cuba
Curacao
Cyprus
Denemarken
Djibouti
Dominica
Dominicaanse Republiek
Duitsland
Ecuador
Egypte
El Salvador
Equatoriaal-Guinea
Eritrea
Estland
Ethiopië
Europese Unie
Faeröer
Falklandeilanden (de) [Malvinas]
Fiji
Filippijnen
Finland
Frankrijk
Franse zuidelijke gebieden
Frans-Guyana
Frans-Polynesië
Gabon
Gambia
Georgië
Ghana
Gibraltar
Global Market
Grenada
Griekenland
Groenland
Grootstedelijk Frankrijk
Guadeloupe
Guam
Guatemala
Guernsey
Guinea
Guinee-Bissau
Guyana
Haïti
Heard en McDonald Eilanden
Honduras
Hong Kong
Hongarije
Ierland
IJsland
Indië
Indonesië
Irak
Iran (Islamitische Republiek)
Isle of Man
Israël
Italië
Ivoorkust
Jamaica
Japan
Jemen
Jersey
Jordanië
Kaaiman Eilanden
Kameroen
Kazachstan
Kenia
Kersteiland
Kirgizië
Kiribati
Kleine afgelegen eilanden van de Verenigde Staten
Koeweit
Korea (de Democratische Volksrepubliek)
Korea (de Republiek)
Kroatië
Lao Democratische Volksrepubliek
Lesotho
Letland
Libanon
Liberia
Libië
Liechtenstein
Litouwen
Luxemburg
Maagdeneilanden (Brits)
Macao
Macedonië (de Voormalige Joegoslavische Republiek)
Madagascar
Maladiven
Malawi
Maleisië
Mali
Malta
Marokko
Marshall eilanden
Martinique
Mauritanië
Mauritius
Mayotte
Mexico
Micronesië (Federale Staten van)
Moldavië (de Republiek)
Monaco
Mongolië
Montenegro
Montserrat
Mozambique
Myanmar
Namibië
Nauru
Nederland
Nepal
Nicaragua
Niet EU
Nieuw Zeeland
Nieuw-Caledonië
Niger
Nigeria
Niue
Noordelijke Mariana eilanden
Noorwegen
Norfolk Island
Oeganda
Oekraïne
Oezbekistan
Oman
Ontwikkelingslanden ondersteuning
Oostenrijk
Pakistan
Palau
Palestina, staat
Panama
Papoea-Nieuw-Guinea
Paraguay
Peru
Pitcairn
Polen
Portugal
Puerto Rico
Qatar
Réunion
Roemenië
Russische Federatie
Rwanda
Saint Barthélemy
Saint Kitts en Nevis
Saint Lucia
Saint Martin (Franse gedeelte)
Saint Vincent en de Grenadines
Saint-Pierre en Miquelon
Samoa
San Marino
Sao Tome en Principe
Saoedi-Arabië
Senegal
Servië
Seychellen
Sierra Leone
Singapore
Sint Maarten (Nederlandse deel)
Sint-Helena
Slovenië
Slowakije
Soedan
Soedan
Solomon eilanden
Somalië
Spanje
Sri Lanka
Suriname
Svalbard en Jan Mayen
Swaziland
Syrische Arabische Republiek
Tadzjikistan
Taiwan (provincie China)
Tanzania, Verenigde Republiek van
Thailand
Timor-Leste
Togo
Tokelau
Tonga
Trinidad en Tobago
Tsjaad
Tsjechië
Tunesië
Turkije
Turkmenistan
Turks- en Caicoseilanden
Tuvalu
Uruguay
Vanuatu
Vaticaanstad
Venezuela (Bolivariaanse Republiek)
Verenigd Koninkrijk
Verenigde Arabische Emiraten
Verenigde Staten van Amerika
Vietnam
Virgin Islands / Maagden eilanden (US)
Wallis en Futuna
Westelijke Sahara*
Wit-Rusland
Zambia
Zimbabwe
Zuid Soedan
Zuid-Afrika
Zuid-Georgië en de Zuid-Sandwicheilanden
Zweden
Zwitserland
```

#### Measure Unit Options

```plaintext
(Boog)graden (hoekeenheid)
Aantal
Aantal cellen
Aantal internationale eenheden (IE)
Aantal paren
Ampère
Ampère uur
Angström
Anti-XA eenheid
Assortiment
Atomaire massa-eenheid (u/ame/amu)
Bar (eenheid voor druk)
Base box
Batch
Beeldpunten per inch (Dots per inch; dpi)
Bit per seconde
Blocnote
Boek
Britse warmte-eenheid (BTU, British thermal unit)
Bruto kilogram
Byte
Candela per vierkante meter
Centigram
Centiliter
Centimeter
Centimeter per seconde
Centimeter Per Uur
Dagen
Decibel
Decigram
Deciliter
Decimeter
Dimensioneringsfactor (Sizing factor)
Dosis
Dozijn
Draagvermogen
Duizend Liter
Duizend stuks
Eetlepel
Femtoliter
"Gallon (VK)	"
Gallon (VS)
Gebruik
Gigabyte
Graadmeter
Graden Celsius
Gram
Gram per kubieke centimeter
Gram per liter
Gram per uur
Gram per vierkante meter
Half dozijn
Hectoliter
Hertz
Inches
"Internationale Eenheden per kilogram (IE/kg)	"
Joule
Kaart
Kelvin
Kilobyte
Kilocalorie (internationale tabel)
Kilogram
Kilogram per vierkante meter
Kilometer
Kilometer per uur
Kilowatt
Kilowatt / uur
Kilowattuur
Kit
Kopje (VS)
Kubieke centimeter
Kubieke decimeter
Kubieke inch
Kubieke meter
Kubieke meter per uur
Kubieke millimeter
Lineaire meter
Link
Liter
"Liter / dag	"
Liter per uur
Lumen
Lumen per Watt
Lux
Maand
Meest waarschijnlijke nummer ('Most probable number')
Megabyte
"Megahertz	"
Megawatt
"Megawattuur (1000 kWh)	"
Meter
Meter per seconde
Metrisch karaat
Microgram
Microliter
Micrometer
Micromol
Mijl per minuut
"Miljoen Internationale Eenheid (NIE)	"
Milliampère uur
Milligram
Milliliter
Millimeter
Millimeter per seconde
Minuut (tijdseenheid)
Nanogram
Netto kilogram
Oertinctuur (droog materiaal)
Ohm
Ons
Ons per vierkante yard
Paar
Paardenkracht
Pagina - hardcopy
"Peck (Droog, VS)	"
per liter (/L)
per milliliter (/mL)
pH (zuurgraad)
Picometer
Picowatt
"Pint (VK)	"
Pixel
Pixels per centimeter
Pond (0.45359237 kg)
Portie
Potential Renal Solute Load
Procent
Quart, Droog VS
"Retinol Activiteit Equivalenten	"
Rol
Schepel (UK; in het Engels 'Bushel')
"Schepel (VS, in het Engels 'Bushel')	"
Seconde (tijdseenheid)
Set
Slagen per minuut
SQ-E (aantal allergenen)
Standaardatmosfeer
Startstroom
Stère
Stuks
Stuks (piece)
Tablet
Tanden Per Inch
Terabyte
Theelepel
"Ton (metrisch)	"
Uur
Vat VS
Vel
Vierkante centimeter
Vierkante decimeter
Vierkante meter
Vierkante meter/seconde
Vierkante millimeter
Vierkante voet
Vloeibare ons ('Fluid ounce', VK)
Vloeibare ons ('Fluid ounce', VS)
Voet
Voet per uur
Volt
Vracht
Watt
Wattuur
Week
Yard
Yard per minuut
"Yard per uur	"
```

### Leveraging GTIN-13 on E-Commerce Platforms

With the GTIN-13 codes generated through our API, businesses can efficiently list their products on platforms like Bol.com and Amazon, ensuring global reach and compliance with e-commerce standards. This streamlined approach facilitates quicker product uploads, enhanced market visibility, and adherence to international retail requirements.

## Conclusion

The GTIN-13 API for E-Commerce Integration offers a pivotal solution for businesses looking to expand their presence on major e-commerce platforms. As this project evolves, we remain committed to enhancing its capabilities and support for our users. For further assistance, please refer to our documentation or contact our support team.

Thank you for considering our GTIN-13 API for your e-commerce integration needs. We look forward to supporting your business's growth and success online.