---
tags:
  - op/test
date: 2026-04-17
---
# 1. Server - via API - UI

## Test 0 - predefined queries

### Main nodes (UI)

```Sparql
SELECT ?node ?label ?location
WHERE {
  ?node <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.wikidata.org/entity/Q108163> .
  ?node <http://www.wikidata.org/entity/P1476> ?label .
  OPTIONAL { ?node <http://www.wikidata.org/entity/P131> ?location }
}
ORDER BY ?label
LIMIT 30
```

> Clarify Q108163, P1476> Miquel

#### Results
```json
[
  {
    "node": "A Tocar Del Cementiri De Sant Romà D'abella",
    "label": "A Tocar Del Cementiri De Sant Romà D'abella",
    "location": "Spain"
  },
  {
    "node": "A Tocar Del Cementiri De Sant Romà D'abella",
    "label": "A Tocar Del Cementiri De Sant Romà D'abella",
    "location": "Lleida"
  },
  {
    "node": "A Tocar Del Cementiri De Sant Romà D'abella",
    "label": "A Tocar Del Cementiri De Sant Romà D'abella",
    "location": "Sant Romà d'Abella"
  },
  {
    "node": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "label": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "location": "Catalunya"
  },
  {
    "node": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "label": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "location": "Spain"
  },
  {
    "node": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "label": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "location": "Barcelona"
  },
  {
    "node": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "label": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "location": "Sant Feliu de Llobregat"
  },
  {
    "node": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "label": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "location": "Baix Llobregat"
  },
  {
    "node": "Aljub Al Soleràs",
    "label": "Aljub Al Soleràs",
    "location": "Spain"
  },
  {
    "node": "Aljub Al Soleràs",
    "label": "Aljub Al Soleràs",
    "location": "Lleida"
  },
  {
    "node": "Aljub Al Soleràs",
    "label": "Aljub Al Soleràs",
    "location": "El Soleràs"
  },
  {
    "node": "Antic Camí De Llanera",
    "label": "Antic Camí De Llanera",
    "location": "Llobera"
  },
  {
    "node": "Aqüeducte del Collet",
    "label": "Aqüeducte del Collet",
    "location": "Barcelona"
  },
  {
    "node": "Aqüeducte del Collet",
    "label": "Aqüeducte del Collet",
    "location": "Guardiola de Berguedà"
  },
  {
    "node": "Aulivar Del Civit",
    "label": "Aulivar Del Civit",
    "location": "Spain"
  },
  {
    "node": "Aulivar Del Civit",
    "label": "Aulivar Del Civit",
    "location": "Lleida"
  },
  {
    "node": "Aulivar Del Civit",
    "label": "Aulivar Del Civit",
    "location": "El Cogul"
  },
  {
    "node": "Aulivarets De Vespella De Gaià",
    "label": "Aulivarets De Vespella De Gaià",
    "location": "Spain"
  },
  {
    "node": "Aulivarets De Vespella De Gaià",
    "label": "Aulivarets De Vespella De Gaià",
    "location": "Vespella de Gaià"
  },
  {
    "node": "Aumaec",
    "label": "Aumaec",
    "location": null
  },
  {
    "node": "Avenc De La Figuerota. Puig Francàs",
    "label": "Avenc De La Figuerota. Puig Francàs",
    "location": "Tarragona"
  },
  {
    "node": "Avenc De La Figuerota. Puig Francàs",
    "label": "Avenc De La Figuerota. Puig Francàs",
    "location": "Spain"
  },
  {
    "node": "Avenc De La Figuerota. Puig Francàs",
    "label": "Avenc De La Figuerota. Puig Francàs",
    "location": "El Montmell"
  },
  {
    "node": "Bancal Del Panser",
    "label": "Bancal Del Panser",
    "location": "Spain"
  },
  {
    "node": "Bancal Del Panser",
    "label": "Bancal Del Panser",
    "location": "Lleida"
  },
  {
    "node": "Bancal Del Panser",
    "label": "Bancal Del Panser",
    "location": "El Cogul"
  },
  {
    "node": "Bancal de l'Anton",
    "label": "Bancal de l'Anton",
    "location": "Spain"
  },
  {
    "node": "Bancal de l'Anton",
    "label": "Bancal de l'Anton",
    "location": "Lleida"
  },
  {
    "node": "Bancal de l'Anton",
    "label": "Bancal de l'Anton",
    "location": "El Cogul"
  },
  {
    "node": "Banyadé: Solana Del Pas Del Pi",
    "label": "Banyadé: Solana Del Pas Del Pi",
    "location": "Spain"
  }
]
```

> node y label show the same information also in the UI

### Main nodes (Server)

```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT ?node WHERE { ?node a <http://www.wikidata.org/entity/Q108163> . } LIMIT 30",
    "format": "json"
  }'
```

#### Results:
```json
STATUS: 500
Internal Server Error
```

### People (UI)
```Sparql
SELECT ?node ?label ?birth ?death
WHERE {
  ?node <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.wikidata.org/entity/Q5> .
  ?node <http://www.wikidata.org/entity/P1476> ?label .
  OPTIONAL { ?node <http://www.wikidata.org/entity/P569> ?birth }
  OPTIONAL { ?node <http://www.wikidata.org/entity/P570> ?death }
}
ORDER BY ?label
LIMIT 30
```

#### Results
First try:
```
Error: Request failed with status code 500
```
Second: 
```json
[
  {
    "node": "Aalto, William",
    "label": "Aalto, William",
    "birth": "1915-07-30T00:00:00Z",
    "death": "1958-06-11T00:00:00Z"
  },
  {
    "node": "Aalto, Yrjo Johan",
    "label": "Aalto, Yrjo Johan",
    "birth": null,
    "death": null
  },
  {
    "node": "Abadia, Juan",
    "label": "Abadia, Juan",
    "birth": null,
    "death": null
  },
  {
    "node": "Abadia, Lucien",
    "label": "Abadia, Lucien",
    "birth": null,
    "death": null
  },
  {
    "node": "Abadie De Pascaou, Pierre-Gaston-Jean",
    "label": "Abadie De Pascaou, Pierre-Gaston-Jean",
    "birth": null,
    "death": null
  },
  {
    "node": "Abbelse, François",
    "label": "Abbelse, François",
    "birth": "1914-01-01",
    "death": null
  },
  {
    "node": "Abberville, Pierre",
    "label": "Abberville, Pierre",
    "birth": null,
    "death": null
  },
  {
    "node": "Abbey, Albert Alfr",
    "label": "Abbey, Albert Alfr",
    "birth": null,
    "death": null
  },
  {
    "node": "Abderrahmani, Alí",
    "label": "Abderrahmani, Alí",
    "birth": "1903-01-25T00:00:00Z",
    "death": null
  },
  {
    "node": "Abdmer, Ramoni",
    "label": "Abdmer, Ramoni",
    "birth": null,
    "death": null
  },
  {
    "node": "Abdrensen, Alf",
    "label": "Abdrensen, Alf",
    "birth": null,
    "death": null
  },
  {
    "node": "Abello, Giuseppe",
    "label": "Abello, Giuseppe",
    "birth": "1906-12-10T00:00:00Z",
    "death": null
  },
  {
    "node": "Abello, Victor",
    "label": "Abello, Victor",
    "birth": "1908-01-01T00:00:00Z",
    "death": null
  },
  {
    "node": "Abramczuk, Jan",
    "label": "Abramczuk, Jan",
    "birth": "1912-01-01",
    "death": null
  },
  {
    "node": "Abramczyk, Mordka",
    "label": "Abramczyk, Mordka",
    "birth": "1911-08-05",
    "death": null
  },
  {
    "node": "Abramofsky, Bernard",
    "label": "Abramofsky, Bernard",
    "birth": null,
    "death": null
  },
  {
    "node": "Abramovicz, Daniel",
    "label": "Abramovicz, Daniel",
    "birth": "1911-12-24T00:00:00Z",
    "death": "1938-01-01T00:00:00Z"
  },
  {
    "node": "Abramovicz, Julius",
    "label": "Abramovicz, Julius",
    "birth": "1915-01-01T00:00:00Z",
    "death": null
  },
  {
    "node": "Abribas",
    "label": "Abribas",
    "birth": null,
    "death": null
  },
  {
    "node": "Abribat, Georges",
    "label": "Abribat, Georges",
    "birth": null,
    "death": null
  },
  {
    "node": "Abril Burgos, Miguel",
    "label": "Abril Burgos, Miguel",
    "birth": null,
    "death": null
  },
  {
    "node": "Acedo Luna, Ventura",
    "label": "Acedo Luna, Ventura",
    "birth": null,
    "death": null
  },
  {
    "node": "Acero Hoda, Diego",
    "label": "Acero Hoda, Diego",
    "birth": "1912-10-22T00:00:00Z",
    "death": null
  },
  {
    "node": "Acero, Juan",
    "label": "Acero, Juan",
    "birth": null,
    "death": null
  },
  {
    "node": "Achard, Jean",
    "label": "Achard, Jean",
    "birth": "1912-09-22T00:00:00Z",
    "death": null
  },
  {
    "node": "Acher, Henri",
    "label": "Acher, Henri",
    "birth": "1904-02-26T00:00:00Z",
    "death": null
  },
  {
    "node": "Acherbon, Herman",
    "label": "Acherbon, Herman",
    "birth": null,
    "death": null
  },
  {
    "node": "Acosta Ortiz, Bartolome",
    "label": "Acosta Ortiz, Bartolome",
    "birth": null,
    "death": null
  },
  {
    "node": "Acosta Pérez, Alberto",
    "label": "Acosta Pérez, Alberto",
    "birth": "1910-08-07T00:00:00Z",
    "death": null
  },
  {
    "node": "Acosta Sánchez, Francisco",
    "label": "Acosta Sánchez, Francisco",
    "birth": null,
    "death": null
  }
]
```

> Same label = node ❓
> Some present Null - is this from the original database or is the data lost? ☝️ > Miquel
> 

### People (Server)

```Sparql
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT ?node ?label ?birth ?death WHERE { ?node <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.wikidata.org/entity/Q5> . ?node <http://www.wikidata.org/entity/P1476> ?label . OPTIONAL { ?node <http://www.wikidata.org/entity/P569> ?birth } OPTIONAL { ?node <http://www.wikidata.org/entity/P570> ?death } } ORDER BY ?label LIMIT 30",
    "format": "json"
  }'
```

#### Results:
```json
STATUS: 500
Internal Server Error
```


### Mass graves (UI)
```Sparql
SELECT ?node ?label ?location
WHERE {
  ?node <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.wikidata.org/entity/Q108163> .
  ?node <http://www.wikidata.org/entity/P1476> ?label .
  OPTIONAL { ?node <http://www.wikidata.org/entity/P131> ?location }
}
ORDER BY ?label
LIMIT 30
```

#### Response with limit
```json
[
  {
    "node": "A Tocar Del Cementiri De Sant Romà D'abella",
    "label": "A Tocar Del Cementiri De Sant Romà D'abella",
    "location": "Spain"
  },
  {
    "node": "A Tocar Del Cementiri De Sant Romà D'abella",
    "label": "A Tocar Del Cementiri De Sant Romà D'abella",
    "location": "Lleida"
  },
  {
    "node": "A Tocar Del Cementiri De Sant Romà D'abella",
    "label": "A Tocar Del Cementiri De Sant Romà D'abella",
    "location": "Sant Romà d'Abella"
  },
  {
    "node": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "label": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "location": "Catalunya"
  },
  {
    "node": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "label": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "location": "Spain"
  },
  {
    "node": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "label": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "location": "Barcelona"
  },
  {
    "node": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "label": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "location": "Sant Feliu de Llobregat"
  },
  {
    "node": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "label": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "location": "Baix Llobregat"
  },
  {
    "node": "Aljub Al Soleràs",
    "label": "Aljub Al Soleràs",
    "location": "Spain"
  },
  {
    "node": "Aljub Al Soleràs",
    "label": "Aljub Al Soleràs",
    "location": "Lleida"
  },
  {
    "node": "Aljub Al Soleràs",
    "label": "Aljub Al Soleràs",
    "location": "El Soleràs"
  },
  {
    "node": "Antic Camí De Llanera",
    "label": "Antic Camí De Llanera",
    "location": "Llobera"
  },
  {
    "node": "Aqüeducte del Collet",
    "label": "Aqüeducte del Collet",
    "location": "Barcelona"
  },
  {
    "node": "Aqüeducte del Collet",
    "label": "Aqüeducte del Collet",
    "location": "Guardiola de Berguedà"
  },
  {
    "node": "Aulivar Del Civit",
    "label": "Aulivar Del Civit",
    "location": "Spain"
  },
  {
    "node": "Aulivar Del Civit",
    "label": "Aulivar Del Civit",
    "location": "Lleida"
  },
  {
    "node": "Aulivar Del Civit",
    "label": "Aulivar Del Civit",
    "location": "El Cogul"
  },
  {
    "node": "Aulivarets De Vespella De Gaià",
    "label": "Aulivarets De Vespella De Gaià",
    "location": "Spain"
  },
  {
    "node": "Aulivarets De Vespella De Gaià",
    "label": "Aulivarets De Vespella De Gaià",
    "location": "Vespella de Gaià"
  },
  {
    "node": "Aumaec",
    "label": "Aumaec",
    "location": null
  },
  {
    "node": "Avenc De La Figuerota. Puig Francàs",
    "label": "Avenc De La Figuerota. Puig Francàs",
    "location": "Tarragona"
  },
  {
    "node": "Avenc De La Figuerota. Puig Francàs",
    "label": "Avenc De La Figuerota. Puig Francàs",
    "location": "Spain"
  },
  {
    "node": "Avenc De La Figuerota. Puig Francàs",
    "label": "Avenc De La Figuerota. Puig Francàs",
    "location": "El Montmell"
  },
  {
    "node": "Bancal Del Panser",
    "label": "Bancal Del Panser",
    "location": "Spain"
  },
  {
    "node": "Bancal Del Panser",
    "label": "Bancal Del Panser",
    "location": "Lleida"
  },
  {
    "node": "Bancal Del Panser",
    "label": "Bancal Del Panser",
    "location": "El Cogul"
  },
  {
    "node": "Bancal de l'Anton",
    "label": "Bancal de l'Anton",
    "location": "Spain"
  },
  {
    "node": "Bancal de l'Anton",
    "label": "Bancal de l'Anton",
    "location": "Lleida"
  },
  {
    "node": "Bancal de l'Anton",
    "label": "Bancal de l'Anton",
    "location": "El Cogul"
  },
  {
    "node": "Banyadé: Solana Del Pas Del Pi",
    "label": "Banyadé: Solana Del Pas Del Pi",
    "location": "Spain"
  }
]
```

Response without limit
```json
[
  {
    "node": "A Tocar Del Cementiri De Sant Romà D'abella",
    "label": "A Tocar Del Cementiri De Sant Romà D'abella",
    "location": "Spain"
  },
  {
    "node": "A Tocar Del Cementiri De Sant Romà D'abella",
    "label": "A Tocar Del Cementiri De Sant Romà D'abella",
    "location": "Lleida"
  },
  {
    "node": "A Tocar Del Cementiri De Sant Romà D'abella",
    "label": "A Tocar Del Cementiri De Sant Romà D'abella",
    "location": "Sant Romà d'Abella"
  },
  {
    "node": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "label": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "location": "Catalunya"
  },
  {
    "node": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "label": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "location": "Spain"
  },
  {
    "node": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "label": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "location": "Barcelona"
  },
  {
    "node": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "label": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "location": "Sant Feliu de Llobregat"
  },
  {
    "node": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "label": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "location": "Baix Llobregat"
  },
  {
    "node": "Aljub Al Soleràs",
    "label": "Aljub Al Soleràs",
    "location": "Spain"
  },
  {
    "node": "Aljub Al Soleràs",
    "label": "Aljub Al Soleràs",
    "location": "Lleida"
  },
  {
    "node": "Aljub Al Soleràs",
    "label": "Aljub Al Soleràs",
    "location": "El Soleràs"
  },
  {
    "node": "Antic Camí De Llanera",
    "label": "Antic Camí De Llanera",
    "location": "Llobera"
  },
  {
    "node": "Aqüeducte del Collet",
    "label": "Aqüeducte del Collet",
    "location": "Barcelona"
  },
  {
    "node": "Aqüeducte del Collet",
    "label": "Aqüeducte del Collet",
    "location": "Guardiola de Berguedà"
  },
  {
    "node": "Aulivar Del Civit",
    "label": "Aulivar Del Civit",
    "location": "Spain"
  },
  {
    "node": "Aulivar Del Civit",
    "label": "Aulivar Del Civit",
    "location": "Lleida"
  },
  {
    "node": "Aulivar Del Civit",
    "label": "Aulivar Del Civit",
    "location": "El Cogul"
  },
  {
    "node": "Aulivarets De Vespella De Gaià",
    "label": "Aulivarets De Vespella De Gaià",
    "location": "Spain"
  },
  {
    "node": "Aulivarets De Vespella De Gaià",
    "label": "Aulivarets De Vespella De Gaià",
    "location": "Vespella de Gaià"
  },
  {
    "node": "Aumaec",
    "label": "Aumaec",
    "location": null
  },
  {
    "node": "Avenc De La Figuerota. Puig Francàs",
    "label": "Avenc De La Figuerota. Puig Francàs",
    "location": "Tarragona"
  },
  {
    "node": "Avenc De La Figuerota. Puig Francàs",
    "label": "Avenc De La Figuerota. Puig Francàs",
    "location": "Spain"
  },
  {
    "node": "Avenc De La Figuerota. Puig Francàs",
    "label": "Avenc De La Figuerota. Puig Francàs",
    "location": "El Montmell"
  },
  {
    "node": "Bancal Del Panser",
    "label": "Bancal Del Panser",
    "location": "Spain"
  },
  {
    "node": "Bancal Del Panser",
    "label": "Bancal Del Panser",
    "location": "Lleida"
  },
  {
    "node": "Bancal Del Panser",
    "label": "Bancal Del Panser",
    "location": "El Cogul"
  },
  {
    "node": "Bancal de l'Anton",
    "label": "Bancal de l'Anton",
    "location": "Spain"
  },
  {
    "node": "Bancal de l'Anton",
    "label": "Bancal de l'Anton",
    "location": "Lleida"
  },
  {
    "node": "Bancal de l'Anton",
    "label": "Bancal de l'Anton",
    "location": "El Cogul"
  },
  {
    "node": "Banyadé: Solana Del Pas Del Pi",
    "label": "Banyadé: Solana Del Pas Del Pi",
    "location": "Spain"
  },
  {
    "node": "Banyadé: Solana Del Pas Del Pi",
    "label": "Banyadé: Solana Del Pas Del Pi",
    "location": "Conca de Dalt"
  },
  {
    "node": "Barranc De Torrenova",
    "label": "Barranc De Torrenova",
    "location": "Vilalba dels Arcs"
  },
  {
    "node": "Barranc de la Call",
    "label": "Barranc de la Call",
    "location": "Spain"
  },
  {
    "node": "Barranc de la Call",
    "label": "Barranc de la Call",
    "location": "Isona i Conca Dellà"
  },
  {
    "node": "Bordes De Cabrils",
    "label": "Bordes De Cabrils",
    "location": "Spain"
  },
  {
    "node": "Bordes De Cabrils",
    "label": "Bordes De Cabrils",
    "location": "Lleida"
  },
  {
    "node": "Bordes De Cabrils",
    "label": "Bordes De Cabrils",
    "location": "Farrera"
  },
  {
    "node": "Bordes De Tressó",
    "label": "Bordes De Tressó",
    "location": "Spain"
  },
  {
    "node": "Bordes De Tressó",
    "label": "Bordes De Tressó",
    "location": "Lleida"
  },
  {
    "node": "Bordes De Tressó",
    "label": "Bordes De Tressó",
    "location": "Farrera"
  },
  {
    "node": "Bosc I Trinxeres Del Coll De Ban",
    "label": "Bosc I Trinxeres Del Coll De Ban",
    "location": "Bassella"
  },
  {
    "node": "Ca La Maxina (Torregassa)",
    "label": "Ca La Maxina (Torregassa)",
    "location": "Tarragona"
  },
  {
    "node": "Ca La Maxina (Torregassa)",
    "label": "Ca La Maxina (Torregassa)",
    "location": "Spain"
  },
  {
    "node": "Ca La Maxina (Torregassa)",
    "label": "Ca La Maxina (Torregassa)",
    "location": "Sant Jaume dels Domenys"
  },
  {
    "node": "Cabana De L'agnès",
    "label": "Cabana De L'agnès",
    "location": "Spain"
  },
  {
    "node": "Cabana De L'agnès",
    "label": "Cabana De L'agnès",
    "location": "Lleida"
  },
  {
    "node": "Cabana De L'agnès",
    "label": "Cabana De L'agnès",
    "location": "L'Albagés"
  },
  {
    "node": "Cal Corretger",
    "label": "Cal Corretger",
    "location": "Spain"
  },
  {
    "node": "Cal Corretger",
    "label": "Cal Corretger",
    "location": "Santa Susanna"
  },
  {
    "node": "Cal Trepat",
    "label": "Cal Trepat",
    "location": "Spain"
  },
  {
    "node": "Cal Trepat",
    "label": "Cal Trepat",
    "location": "Lleida"
  },
  {
    "node": "Cal Trepat",
    "label": "Cal Trepat",
    "location": "Tàrrega"
  },
  {
    "node": "Camp De La Pona",
    "label": "Camp De La Pona",
    "location": "Spain"
  },
  {
    "node": "Camp De La Pona",
    "label": "Camp De La Pona",
    "location": "Lleida"
  },
  {
    "node": "Camp De La Pona",
    "label": "Camp De La Pona",
    "location": "Montellà i Martinet"
  },
  {
    "node": "Camp De Treball Núm. 2 De L’hospitalet De L’infant.",
    "label": "Camp De Treball Núm. 2 De L’hospitalet De L’infant.",
    "location": "Spain"
  },
  {
    "node": "Camp De Treball Núm. 2 De L’hospitalet De L’infant.",
    "label": "Camp De Treball Núm. 2 De L’hospitalet De L’infant.",
    "location": "Vandellòs I L'hospitalet De L'infant"
  },
  {
    "node": "Camp Dels Morts De La Casagolda",
    "label": "Camp Dels Morts De La Casagolda",
    "location": "Spain"
  },
  {
    "node": "Camp Dels Morts De La Casagolda",
    "label": "Camp Dels Morts De La Casagolda",
    "location": "Lleida"
  },
  {
    "node": "Camp Dels Morts De La Casagolda",
    "label": "Camp Dels Morts De La Casagolda",
    "location": "Castellar de la Ribera"
  },
  {
    "node": "Camp Malacara",
    "label": "Camp Malacara",
    "location": "Spain"
  },
  {
    "node": "Camp Malacara",
    "label": "Camp Malacara",
    "location": "Lleida"
  },
  {
    "node": "Camp Malacara",
    "label": "Camp Malacara",
    "location": "Tarrés"
  },
  {
    "node": "Camí De L'Hort D'En Tona - Bòbila Del Sogas",
    "label": "Camí De L'Hort D'En Tona - Bòbila Del Sogas",
    "location": "Spain"
  },
  {
    "node": "Camí De L'Hort D'En Tona - Bòbila Del Sogas",
    "label": "Camí De L'Hort D'En Tona - Bòbila Del Sogas",
    "location": "Vilafranca del Penedès"
  },
  {
    "node": "Camí De La Font De Conill. Cabra Del Camp",
    "label": "Camí De La Font De Conill. Cabra Del Camp",
    "location": "Tarragona"
  },
  {
    "node": "Camí De La Font De Conill. Cabra Del Camp",
    "label": "Camí De La Font De Conill. Cabra Del Camp",
    "location": "Spain"
  },
  {
    "node": "Camí De La Font De Conill. Cabra Del Camp",
    "label": "Camí De La Font De Conill. Cabra Del Camp",
    "location": "Cabra del Camp"
  },
  {
    "node": "Camí De Les Eres (Cometes).",
    "label": "Camí De Les Eres (Cometes).",
    "location": "Tarragona"
  },
  {
    "node": "Camí De Les Eres (Cometes).",
    "label": "Camí De Les Eres (Cometes).",
    "location": "Spain"
  },
  {
    "node": "Camí De Les Eres (Cometes).",
    "label": "Camí De Les Eres (Cometes).",
    "location": "Corbera d'Ebre"
  },
  {
    "node": "Camí Fondo De Torres De Segre (Pala De La Gemma)",
    "label": "Camí Fondo De Torres De Segre (Pala De La Gemma)",
    "location": "Soses"
  },
  {
    "node": "Camí Nou Del Mas De Galofre",
    "label": "Camí Nou Del Mas De Galofre",
    "location": "Tarragona"
  },
  {
    "node": "Camí Nou Del Mas De Galofre",
    "label": "Camí Nou Del Mas De Galofre",
    "location": "Spain"
  },
  {
    "node": "Camí Nou Del Mas De Galofre",
    "label": "Camí Nou Del Mas De Galofre",
    "location": "L'Albiol"
  },
  {
    "node": "Camí Vell De Falset",
    "label": "Camí Vell De Falset",
    "location": "Spain"
  },
  {
    "node": "Camí Vell De Falset",
    "label": "Camí Vell De Falset",
    "location": "Gratallops"
  },
  {
    "node": "Camí Vell De La Pobla De Massaluca",
    "label": "Camí Vell De La Pobla De Massaluca",
    "location": "Tarragona"
  },
  {
    "node": "Camí Vell De La Pobla De Massaluca",
    "label": "Camí Vell De La Pobla De Massaluca",
    "location": "Spain"
  },
  {
    "node": "Camí Vell De La Pobla De Massaluca",
    "label": "Camí Vell De La Pobla De Massaluca",
    "location": "Vilalba dels Arcs"
  },
  {
    "node": "Camí de les Monges (II)",
    "label": "Camí de les Monges (II)",
    "location": "Spain"
  },
  {
    "node": "Camí de les Monges (II)",
    "label": "Camí de les Monges (II)",
    "location": "Barcelona"
  },
  {
    "node": "Camí de les Monges (II)",
    "label": "Camí de les Monges (II)",
    "location": "Ullastrell"
  },
  {
    "node": "Can Carous",
    "label": "Can Carous",
    "location": "Spain"
  },
  {
    "node": "Can Carous",
    "label": "Can Carous",
    "location": "Barcelona"
  },
  {
    "node": "Can Carous",
    "label": "Can Carous",
    "location": "Gurb"
  },
  {
    "node": "Can Carreres",
    "label": "Can Carreres",
    "location": "Spain"
  },
  {
    "node": "Can Carreres",
    "label": "Can Carreres",
    "location": "Rubí"
  },
  {
    "node": "Can Maçana",
    "label": "Can Maçana",
    "location": "Barcelona"
  },
  {
    "node": "Can Maçana",
    "label": "Can Maçana",
    "location": "El Bruc"
  },
  {
    "node": "Cantallops (vinyes a tocar de la N-340)",
    "label": "Cantallops (vinyes a tocar de la N-340)",
    "location": "Spain"
  },
  {
    "node": "Cantallops (vinyes a tocar de la N-340)",
    "label": "Cantallops (vinyes a tocar de la N-340)",
    "location": "Barcelona"
  },
  {
    "node": "Cantallops (vinyes a tocar de la N-340)",
    "label": "Cantallops (vinyes a tocar de la N-340)",
    "location": "Subirats"
  },
  {
    "node": "Carbonelles",
    "label": "Carbonelles",
    "location": "Spain"
  },
  {
    "node": "Carbonelles",
    "label": "Carbonelles",
    "location": "Lleida"
  },
  {
    "node": "Carbonelles",
    "label": "Carbonelles",
    "location": "Torrebesses"
  },
  {
    "node": "Casa Blanca, creu de ferro de Bellprat",
    "label": "Casa Blanca, creu de ferro de Bellprat",
    "location": "Spain"
  },
  {
    "node": "Casa Blanca, creu de ferro de Bellprat",
    "label": "Casa Blanca, creu de ferro de Bellprat",
    "location": "Barcelona"
  },
  {
    "node": "Casa Blanca, creu de ferro de Bellprat",
    "label": "Casa Blanca, creu de ferro de Bellprat",
    "location": "Bellprat"
  },
  {
    "node": "Casanova De Clarà",
    "label": "Casanova De Clarà",
    "location": "Spain"
  },
  {
    "node": "Casanova De Clarà",
    "label": "Casanova De Clarà",
    "location": "Lleida"
  },
  {
    "node": "Casanova De Clarà",
    "label": "Casanova De Clarà",
    "location": "Castellar de la Ribera"
  },
  {
    "node": "Caseta D'en Codolà",
    "label": "Caseta D'en Codolà",
    "location": "Spain"
  },
  {
    "node": "Caseta D'en Codolà",
    "label": "Caseta D'en Codolà",
    "location": "Girona"
  },
  {
    "node": "Caseta D'en Codolà",
    "label": "Caseta D'en Codolà",
    "location": "Cassà de la Selva"
  },
  {
    "node": "Caseta De Peons Ferroviaris",
    "label": "Caseta De Peons Ferroviaris",
    "location": "Tarragona"
  },
  {
    "node": "Caseta De Peons Ferroviaris",
    "label": "Caseta De Peons Ferroviaris",
    "location": "Spain"
  },
  {
    "node": "Caseta De Peons Ferroviaris",
    "label": "Caseta De Peons Ferroviaris",
    "location": "Móra la Nova"
  },
  {
    "node": "Caseta de peons caminers de Guialmons. Les Piles",
    "label": "Caseta de peons caminers de Guialmons. Les Piles",
    "location": "Spain"
  },
  {
    "node": "Caseta de peons caminers de Guialmons. Les Piles",
    "label": "Caseta de peons caminers de Guialmons. Les Piles",
    "location": "Guialmons"
  },
  {
    "node": "Cementeri de Montardit d'Enviny",
    "label": "Cementeri de Montardit d'Enviny",
    "location": "Spain"
  },
  {
    "node": "Cementeri de Montardit d'Enviny",
    "label": "Cementeri de Montardit d'Enviny",
    "location": "Sort"
  },
  {
    "node": "Cementir",
    "label": "Cementir",
    "location": null
  },
  {
    "node": "Cementiri  Vell de Vimbodí. Soldats de la 13a Brigada Internacional.",
    "label": "Cementiri  Vell de Vimbodí. Soldats de la 13a Brigada Internacional.",
    "location": "Spain"
  },
  {
    "node": "Cementiri  Vell de Vimbodí. Soldats de la 13a Brigada Internacional.",
    "label": "Cementiri  Vell de Vimbodí. Soldats de la 13a Brigada Internacional.",
    "location": "Vimbodí i Poblet"
  },
  {
    "node": "Cementiri Ampolla",
    "label": "Cementiri Ampolla",
    "location": "Spain"
  },
  {
    "node": "Cementiri Ampolla",
    "label": "Cementiri Ampolla",
    "location": "L'Ampolla"
  },
  {
    "node": "Cementiri Antic D'almacelles",
    "label": "Cementiri Antic D'almacelles",
    "location": "Spain"
  },
  {
    "node": "Cementiri Antic D'almacelles",
    "label": "Cementiri Antic D'almacelles",
    "location": "Lleida"
  },
  {
    "node": "Cementiri Antic D'almacelles",
    "label": "Cementiri Antic D'almacelles",
    "location": "Almacelles"
  },
  {
    "node": "Cementiri Balaguer. Fossa Dels 19",
    "label": "Cementiri Balaguer. Fossa Dels 19",
    "location": "Balaguer"
  },
  {
    "node": "Cementiri Bellmunt Del Priorat",
    "label": "Cementiri Bellmunt Del Priorat",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri Bellmunt Del Priorat",
    "label": "Cementiri Bellmunt Del Priorat",
    "location": "Spain"
  },
  {
    "node": "Cementiri Bellmunt Del Priorat",
    "label": "Cementiri Bellmunt Del Priorat",
    "location": "Bellmunt del Priorat"
  },
  {
    "node": "Cementiri D'Arenys De Mar",
    "label": "Cementiri D'Arenys De Mar",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'Arenys De Mar",
    "label": "Cementiri D'Arenys De Mar",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri D'Arenys De Mar",
    "label": "Cementiri D'Arenys De Mar",
    "location": "Arenys de Mar"
  },
  {
    "node": "Cementiri D'Arenys De Munt",
    "label": "Cementiri D'Arenys De Munt",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'Arenys De Munt",
    "label": "Cementiri D'Arenys De Munt",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri D'Arenys De Munt",
    "label": "Cementiri D'Arenys De Munt",
    "location": "Arenys de Munt"
  },
  {
    "node": "Cementiri D'Es Bòrdes",
    "label": "Cementiri D'Es Bòrdes",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'Es Bòrdes",
    "label": "Cementiri D'Es Bòrdes",
    "location": "Es Bòrdes"
  },
  {
    "node": "Cementiri D'Estaràs",
    "label": "Cementiri D'Estaràs",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'Estaràs",
    "label": "Cementiri D'Estaràs",
    "location": "Lleida"
  },
  {
    "node": "Cementiri D'Estaràs",
    "label": "Cementiri D'Estaràs",
    "location": "Estaràs"
  },
  {
    "node": "Cementiri D'alcanó",
    "label": "Cementiri D'alcanó",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'alcanó",
    "label": "Cementiri D'alcanó",
    "location": "Lleida"
  },
  {
    "node": "Cementiri D'alcanó",
    "label": "Cementiri D'alcanó",
    "location": "Alcanó"
  },
  {
    "node": "Cementiri D'alcover. Ossera",
    "label": "Cementiri D'alcover. Ossera",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri D'alcover. Ossera",
    "label": "Cementiri D'alcover. Ossera",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'alcover. Ossera",
    "label": "Cementiri D'alcover. Ossera",
    "location": "Alcover"
  },
  {
    "node": "Cementiri D'alentorn. Enterrament De Vicente Boquera",
    "label": "Cementiri D'alentorn. Enterrament De Vicente Boquera",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'alentorn. Enterrament De Vicente Boquera",
    "label": "Cementiri D'alentorn. Enterrament De Vicente Boquera",
    "location": "Alentorn"
  },
  {
    "node": "Cementiri D'almenar",
    "label": "Cementiri D'almenar",
    "location": "Almenar"
  },
  {
    "node": "Cementiri D'alta-riba",
    "label": "Cementiri D'alta-riba",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'alta-riba",
    "label": "Cementiri D'alta-riba",
    "location": "Estaràs"
  },
  {
    "node": "Cementiri D'altron",
    "label": "Cementiri D'altron",
    "location": "Catalunya"
  },
  {
    "node": "Cementiri D'altron",
    "label": "Cementiri D'altron",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'altron",
    "label": "Cementiri D'altron",
    "location": "Lleida"
  },
  {
    "node": "Cementiri D'altron",
    "label": "Cementiri D'altron",
    "location": "Pallars Sobirà"
  },
  {
    "node": "Cementiri D'altron",
    "label": "Cementiri D'altron",
    "location": "Altron"
  },
  {
    "node": "Cementiri D'alòs De Balaguer. Sepultura De Juan Campoy Sánchez",
    "label": "Cementiri D'alòs De Balaguer. Sepultura De Juan Campoy Sánchez",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'alòs De Balaguer. Sepultura De Juan Campoy Sánchez",
    "label": "Cementiri D'alòs De Balaguer. Sepultura De Juan Campoy Sánchez",
    "location": "Lleida"
  },
  {
    "node": "Cementiri D'alòs De Balaguer. Sepultura De Juan Campoy Sánchez",
    "label": "Cementiri D'alòs De Balaguer. Sepultura De Juan Campoy Sánchez",
    "location": "Alòs de Balaguer"
  },
  {
    "node": "Cementiri D'amer. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri D'amer. Traslladada Al Valle De Los Caídos",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'amer. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri D'amer. Traslladada Al Valle De Los Caídos",
    "location": "Girona"
  },
  {
    "node": "Cementiri D'amer. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri D'amer. Traslladada Al Valle De Los Caídos",
    "location": "Amer"
  },
  {
    "node": "Cementiri D'anglesola",
    "label": "Cementiri D'anglesola",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'anglesola",
    "label": "Cementiri D'anglesola",
    "location": "Lleida"
  },
  {
    "node": "Cementiri D'anglesola",
    "label": "Cementiri D'anglesola",
    "location": "Anglesola"
  },
  {
    "node": "Cementiri D'escós",
    "label": "Cementiri D'escós",
    "location": "Escós"
  },
  {
    "node": "Cementiri D'esparreguera. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri D'esparreguera. Traslladada Al Valle De Los Caídos",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'esparreguera. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri D'esparreguera. Traslladada Al Valle De Los Caídos",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri D'esparreguera. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri D'esparreguera. Traslladada Al Valle De Los Caídos",
    "location": "Esparreguera"
  },
  {
    "node": "Cementiri D'esterri De Cardós",
    "label": "Cementiri D'esterri De Cardós",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'esterri De Cardós",
    "label": "Cementiri D'esterri De Cardós",
    "location": "Lleida"
  },
  {
    "node": "Cementiri D'esterri De Cardós",
    "label": "Cementiri D'esterri De Cardós",
    "location": "Esterri de Cardós"
  },
  {
    "node": "Cementiri D'herba-Savina",
    "label": "Cementiri D'herba-Savina",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'herba-Savina",
    "label": "Cementiri D'herba-Savina",
    "location": "Lleida"
  },
  {
    "node": "Cementiri D'herba-Savina",
    "label": "Cementiri D'herba-Savina",
    "location": "Conca de Dalt"
  },
  {
    "node": "Cementiri D'horta De Sant Joan. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri D'horta De Sant Joan. Traslladada Al Valle De Los Caídos.",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri D'horta De Sant Joan. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri D'horta De Sant Joan. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'horta De Sant Joan. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri D'horta De Sant Joan. Traslladada Al Valle De Los Caídos.",
    "location": "Horta de Sant Joan"
  },
  {
    "node": "Cementiri D'igualada",
    "label": "Cementiri D'igualada",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'igualada",
    "label": "Cementiri D'igualada",
    "location": "Igualada"
  },
  {
    "node": "Cementiri D'ivars D'urgell",
    "label": "Cementiri D'ivars D'urgell",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'ivars D'urgell",
    "label": "Cementiri D'ivars D'urgell",
    "location": "Lleida"
  },
  {
    "node": "Cementiri D'unha",
    "label": "Cementiri D'unha",
    "location": "Lleida"
  },
  {
    "node": "Cementiri D'unha",
    "label": "Cementiri D'unha",
    "location": "Naut Aran"
  },
  {
    "node": "Cementiri De Banyeres Del Penedès",
    "label": "Cementiri De Banyeres Del Penedès",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Banyeres Del Penedès",
    "label": "Cementiri De Banyeres Del Penedès",
    "location": "Banyeres del Penedès"
  },
  {
    "node": "Cementiri De Barcelona (sense Determinar). Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Barcelona (sense Determinar). Traslladada Al Valle De Los Caídos.",
    "location": "Catalunya"
  },
  {
    "node": "Cementiri De Barcelona (sense Determinar). Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Barcelona (sense Determinar). Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Barcelona (sense Determinar). Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Barcelona (sense Determinar). Traslladada Al Valle De Los Caídos.",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Barcelona (sense Determinar). Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Barcelona (sense Determinar). Traslladada Al Valle De Los Caídos.",
    "location": "Barcelonès"
  },
  {
    "node": "Cementiri De Bassella",
    "label": "Cementiri De Bassella",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Bassella",
    "label": "Cementiri De Bassella",
    "location": "Bassella"
  },
  {
    "node": "Cementiri De Bellprat",
    "label": "Cementiri De Bellprat",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Bellprat",
    "label": "Cementiri De Bellprat",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Bellprat",
    "label": "Cementiri De Bellprat",
    "location": "Bellprat"
  },
  {
    "node": "Cementiri De Bellpuig",
    "label": "Cementiri De Bellpuig",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Bellpuig",
    "label": "Cementiri De Bellpuig",
    "location": "Bellpuig"
  },
  {
    "node": "Cementiri De Bonastre",
    "label": "Cementiri De Bonastre",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De Bonastre",
    "label": "Cementiri De Bonastre",
    "location": "Catalunya"
  },
  {
    "node": "Cementiri De Bonastre",
    "label": "Cementiri De Bonastre",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Bonastre",
    "label": "Cementiri De Bonastre",
    "location": "Bonastre"
  },
  {
    "node": "Cementiri De Bonastre",
    "label": "Cementiri De Bonastre",
    "location": "Baix Penedès"
  },
  {
    "node": "Cementiri De Bot. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Bot. Traslladada Al Valle De Cuelgamuros",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De Bot. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Bot. Traslladada Al Valle De Cuelgamuros",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Bot. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Bot. Traslladada Al Valle De Cuelgamuros",
    "location": "Bot"
  },
  {
    "node": "Cementiri De Bovera",
    "label": "Cementiri De Bovera",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Bovera",
    "label": "Cementiri De Bovera",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Bovera",
    "label": "Cementiri De Bovera",
    "location": "Bovera"
  },
  {
    "node": "Cementiri De Cabrera De Mar",
    "label": "Cementiri De Cabrera De Mar",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Cabrera De Mar",
    "label": "Cementiri De Cabrera De Mar",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Cabrera De Mar",
    "label": "Cementiri De Cabrera De Mar",
    "location": "Cabrera de Mar"
  },
  {
    "node": "Cementiri De Cabó (Camp De Treball)",
    "label": "Cementiri De Cabó (Camp De Treball)",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Cabó (Camp De Treball)",
    "label": "Cementiri De Cabó (Camp De Treball)",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Cabó (Camp De Treball)",
    "label": "Cementiri De Cabó (Camp De Treball)",
    "location": "Cabó"
  },
  {
    "node": "Cementiri De Calaf",
    "label": "Cementiri De Calaf",
    "location": "Catalunya"
  },
  {
    "node": "Cementiri De Calaf",
    "label": "Cementiri De Calaf",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Calaf",
    "label": "Cementiri De Calaf",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Calaf",
    "label": "Cementiri De Calaf",
    "location": "Calaf"
  },
  {
    "node": "Cementiri De Calaf",
    "label": "Cementiri De Calaf",
    "location": "Anoia"
  },
  {
    "node": "Cementiri De Caldes D'Estrac",
    "label": "Cementiri De Caldes D'Estrac",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Caldes D'Estrac",
    "label": "Cementiri De Caldes D'Estrac",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Caldes D'Estrac",
    "label": "Cementiri De Caldes D'Estrac",
    "location": "Caldes d'Estrac"
  },
  {
    "node": "Cementiri De Camarasa",
    "label": "Cementiri De Camarasa",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Camarasa",
    "label": "Cementiri De Camarasa",
    "location": "Camarasa"
  },
  {
    "node": "Cementiri De Castellbisbal",
    "label": "Cementiri De Castellbisbal",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Castellbisbal",
    "label": "Cementiri De Castellbisbal",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Castellbisbal",
    "label": "Cementiri De Castellbisbal",
    "location": "Castellbisbal"
  },
  {
    "node": "Cementiri De Castellciutat",
    "label": "Cementiri De Castellciutat",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Castellciutat",
    "label": "Cementiri De Castellciutat",
    "location": "Castellciutat"
  },
  {
    "node": "Cementiri De Castellfollit De La Roca. Traslladada A Cuelgamuros",
    "label": "Cementiri De Castellfollit De La Roca. Traslladada A Cuelgamuros",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Castellfollit De La Roca. Traslladada A Cuelgamuros",
    "label": "Cementiri De Castellfollit De La Roca. Traslladada A Cuelgamuros",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Castellfollit De La Roca. Traslladada A Cuelgamuros",
    "label": "Cementiri De Castellfollit De La Roca. Traslladada A Cuelgamuros",
    "location": "Castellfollit de la Roca"
  },
  {
    "node": "Cementiri De Castellgalí",
    "label": "Cementiri De Castellgalí",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Castellgalí",
    "label": "Cementiri De Castellgalí",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Castellgalí",
    "label": "Cementiri De Castellgalí",
    "location": "Castellgalí"
  },
  {
    "node": "Cementiri De Castellolí",
    "label": "Cementiri De Castellolí",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Castellolí",
    "label": "Cementiri De Castellolí",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Castellolí",
    "label": "Cementiri De Castellolí",
    "location": "Castellolí"
  },
  {
    "node": "Cementiri De Castellserà",
    "label": "Cementiri De Castellserà",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Castellserà",
    "label": "Cementiri De Castellserà",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Castellserà",
    "label": "Cementiri De Castellserà",
    "location": "Castellserà"
  },
  {
    "node": "Cementiri De Celrà. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Celrà. Traslladada Al Valle De Cuelgamuros",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Celrà. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Celrà. Traslladada Al Valle De Cuelgamuros",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Celrà. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Celrà. Traslladada Al Valle De Cuelgamuros",
    "location": "Celrà"
  },
  {
    "node": "Cementiri De Cerdanyola Del Vallès, Fossa Dels Anarquistes",
    "label": "Cementiri De Cerdanyola Del Vallès, Fossa Dels Anarquistes",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Cerdanyola Del Vallès, Fossa Dels Anarquistes",
    "label": "Cementiri De Cerdanyola Del Vallès, Fossa Dels Anarquistes",
    "location": "Cerdanyola del Vallès"
  },
  {
    "node": "Cementiri De Comabella",
    "label": "Cementiri De Comabella",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Comabella",
    "label": "Cementiri De Comabella",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Comabella",
    "label": "Cementiri De Comabella",
    "location": "Sant Guim de la Plana"
  },
  {
    "node": "Cementiri De Concabella",
    "label": "Cementiri De Concabella",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Concabella",
    "label": "Cementiri De Concabella",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Concabella",
    "label": "Cementiri De Concabella",
    "location": "Els Plans de Sió"
  },
  {
    "node": "Cementiri De Dosrius",
    "label": "Cementiri De Dosrius",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Dosrius",
    "label": "Cementiri De Dosrius",
    "location": "Dosrius"
  },
  {
    "node": "Cementiri De Falset",
    "label": "Cementiri De Falset",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De Falset",
    "label": "Cementiri De Falset",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Falset",
    "label": "Cementiri De Falset",
    "location": "Falset"
  },
  {
    "node": "Cementiri De Figueres. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Figueres. Traslladada Al Valle De Los Caídos",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Figueres. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Figueres. Traslladada Al Valle De Los Caídos",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Figueres. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Figueres. Traslladada Al Valle De Los Caídos",
    "location": "Figueres"
  },
  {
    "node": "Cementiri De Flix. Repressió A La Reraguarda",
    "label": "Cementiri De Flix. Repressió A La Reraguarda",
    "location": "Flix"
  },
  {
    "node": "Cementiri De Flix. Soldats Morts A L'hospital Militar.",
    "label": "Cementiri De Flix. Soldats Morts A L'hospital Militar.",
    "location": "Flix"
  },
  {
    "node": "Cementiri De Flix. Víctimes De Bombardeig.",
    "label": "Cementiri De Flix. Víctimes De Bombardeig.",
    "location": "Flix"
  },
  {
    "node": "Cementiri De Florejacs Ii",
    "label": "Cementiri De Florejacs Ii",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Florejacs Ii",
    "label": "Cementiri De Florejacs Ii",
    "location": "Torrefeta"
  },
  {
    "node": "Cementiri De Fontanet",
    "label": "Cementiri De Fontanet",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Fontanet",
    "label": "Cementiri De Fontanet",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Fontanet",
    "label": "Cementiri De Fontanet",
    "location": "Torà"
  },
  {
    "node": "Cementiri De Garrigoles. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Garrigoles. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Garrigoles. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Garrigoles. Traslladada Al Valle De Los Caídos.",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Garrigoles. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Garrigoles. Traslladada Al Valle De Los Caídos.",
    "location": "Garrigoles"
  },
  {
    "node": "Cementiri De Garrigàs",
    "label": "Cementiri De Garrigàs",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Garrigàs",
    "label": "Cementiri De Garrigàs",
    "location": "Garrigàs"
  },
  {
    "node": "Cementiri De L'ametlla De Mar I Voltant De La Masia Ponts",
    "label": "Cementiri De L'ametlla De Mar I Voltant De La Masia Ponts",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De L'ametlla De Mar I Voltant De La Masia Ponts",
    "label": "Cementiri De L'ametlla De Mar I Voltant De La Masia Ponts",
    "location": "Catalunya"
  },
  {
    "node": "Cementiri De L'ametlla De Mar I Voltant De La Masia Ponts",
    "label": "Cementiri De L'ametlla De Mar I Voltant De La Masia Ponts",
    "location": "Spain"
  },
  {
    "node": "Cementiri De L'ametlla De Mar I Voltant De La Masia Ponts",
    "label": "Cementiri De L'ametlla De Mar I Voltant De La Masia Ponts",
    "location": "Baix Ebre"
  },
  {
    "node": "Cementiri De L'ametlla De Mar I Voltant De La Masia Ponts",
    "label": "Cementiri De L'ametlla De Mar I Voltant De La Masia Ponts",
    "location": "L'Ametlla de Mar"
  },
  {
    "node": "Cementiri De La Doma De La Garriga",
    "label": "Cementiri De La Doma De La Garriga",
    "location": "La Garriga"
  },
  {
    "node": "Cementiri De La Granadella. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De La Granadella. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De La Granadella. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De La Granadella. Traslladada Al Valle De Los Caídos.",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De La Granadella. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De La Granadella. Traslladada Al Valle De Los Caídos.",
    "location": "La Granadella"
  },
  {
    "node": "Cementiri De La Guingueta D'àneu",
    "label": "Cementiri De La Guingueta D'àneu",
    "location": "La Guingueta d'Àneu"
  },
  {
    "node": "Cementiri De La Pobla De Mafumet",
    "label": "Cementiri De La Pobla De Mafumet",
    "location": "Spain"
  },
  {
    "node": "Cementiri De La Pobla De Mafumet",
    "label": "Cementiri De La Pobla De Mafumet",
    "location": "La Pobla de Mafumet"
  },
  {
    "node": "Cementiri De La Secuita. Repressió De Reraguarda.",
    "label": "Cementiri De La Secuita. Repressió De Reraguarda.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De La Secuita. Repressió De Reraguarda.",
    "label": "Cementiri De La Secuita. Repressió De Reraguarda.",
    "location": "La Secuita"
  },
  {
    "node": "Cementiri De La Selva Del Camp. Civils Morts A L'Hospital Intercomarcal.",
    "label": "Cementiri De La Selva Del Camp. Civils Morts A L'Hospital Intercomarcal.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De La Selva Del Camp. Civils Morts A L'Hospital Intercomarcal.",
    "label": "Cementiri De La Selva Del Camp. Civils Morts A L'Hospital Intercomarcal.",
    "location": "La Selva del Camp"
  },
  {
    "node": "Cementiri De La Seu D'Urgell. Civils Reinhumats El 1937",
    "label": "Cementiri De La Seu D'Urgell. Civils Reinhumats El 1937",
    "location": "Spain"
  },
  {
    "node": "Cementiri De La Seu D'Urgell. Civils Reinhumats El 1937",
    "label": "Cementiri De La Seu D'Urgell. Civils Reinhumats El 1937",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De La Seu D'Urgell. Civils Reinhumats El 1937",
    "label": "Cementiri De La Seu D'Urgell. Civils Reinhumats El 1937",
    "location": "La Seu d'Urgell"
  },
  {
    "node": "Cementiri De La Seu D'Urgell. Soldats Morts A L'Hospital Del X Cos D'Exèrcit",
    "label": "Cementiri De La Seu D'Urgell. Soldats Morts A L'Hospital Del X Cos D'Exèrcit",
    "location": "Spain"
  },
  {
    "node": "Cementiri De La Seu D'Urgell. Soldats Morts A L'Hospital Del X Cos D'Exèrcit",
    "label": "Cementiri De La Seu D'Urgell. Soldats Morts A L'Hospital Del X Cos D'Exèrcit",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De La Seu D'Urgell. Soldats Morts A L'Hospital Del X Cos D'Exèrcit",
    "label": "Cementiri De La Seu D'Urgell. Soldats Morts A L'Hospital Del X Cos D'Exèrcit",
    "location": "La Seu d'Urgell"
  },
  {
    "node": "Cementiri De La Tallada D'empordà. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De La Tallada D'empordà. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De La Tallada D'empordà. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De La Tallada D'empordà. Traslladada Al Valle De Los Caídos.",
    "location": "Girona"
  },
  {
    "node": "Cementiri De La Tallada D'empordà. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De La Tallada D'empordà. Traslladada Al Valle De Los Caídos.",
    "location": "La Tallada d'Empordà"
  },
  {
    "node": "Cementiri De La Torre De Claramunt",
    "label": "Cementiri De La Torre De Claramunt",
    "location": "Spain"
  },
  {
    "node": "Cementiri De La Torre De Claramunt",
    "label": "Cementiri De La Torre De Claramunt",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De La Torre De Claramunt",
    "label": "Cementiri De La Torre De Claramunt",
    "location": "La Torre De Claramunt"
  },
  {
    "node": "Cementiri De La Torre De L'Espanyol",
    "label": "Cementiri De La Torre De L'Espanyol",
    "location": "Spain"
  },
  {
    "node": "Cementiri De La Torre De L'Espanyol",
    "label": "Cementiri De La Torre De L'Espanyol",
    "location": "La Torre de l'Espanyol"
  },
  {
    "node": "Cementiri De Les Oluges II",
    "label": "Cementiri De Les Oluges II",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Les Oluges II",
    "label": "Cementiri De Les Oluges II",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Les Oluges II",
    "label": "Cementiri De Les Oluges II",
    "location": "Les Oluges"
  },
  {
    "node": "Cementiri De Les Pallargues",
    "label": "Cementiri De Les Pallargues",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Les Pallargues",
    "label": "Cementiri De Les Pallargues",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Les Pallargues",
    "label": "Cementiri De Les Pallargues",
    "location": "Els Plans de Sió"
  },
  {
    "node": "Cementiri De Linyola",
    "label": "Cementiri De Linyola",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Linyola",
    "label": "Cementiri De Linyola",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Linyola",
    "label": "Cementiri De Linyola",
    "location": "Linyola"
  },
  {
    "node": "Cementiri De Llagunes",
    "label": "Cementiri De Llagunes",
    "location": "Llagunes"
  },
  {
    "node": "Cementiri De Llavorsi (III)",
    "label": "Cementiri De Llavorsi (III)",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Llavorsi (III)",
    "label": "Cementiri De Llavorsi (III)",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Llavorsi (III)",
    "label": "Cementiri De Llavorsi (III)",
    "location": "Llavorsí"
  },
  {
    "node": "Cementiri De Lleida. Departament De Sant Josep. Víctimes De La Violència Revolucionària",
    "label": "Cementiri De Lleida. Departament De Sant Josep. Víctimes De La Violència Revolucionària",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Lleida. Departament De Sant Josep. Víctimes De La Violència Revolucionària",
    "label": "Cementiri De Lleida. Departament De Sant Josep. Víctimes De La Violència Revolucionària",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Lleida. Víctimes De La Repressió Franquista",
    "label": "Cementiri De Lleida. Víctimes De La Repressió Franquista",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Lleida. Víctimes De La Repressió Franquista",
    "label": "Cementiri De Lleida. Víctimes De La Repressió Franquista",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Lloret De Mar. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Lloret De Mar. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Lloret De Mar. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Lloret De Mar. Traslladada Al Valle De Los Caídos.",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Lloret De Mar. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Lloret De Mar. Traslladada Al Valle De Los Caídos.",
    "location": "Lloret de Mar"
  },
  {
    "node": "Cementiri De Maials",
    "label": "Cementiri De Maials",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Maials",
    "label": "Cementiri De Maials",
    "location": "Maials"
  },
  {
    "node": "Cementiri De Manresa",
    "label": "Cementiri De Manresa",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Manresa",
    "label": "Cementiri De Manresa",
    "location": "Manresa"
  },
  {
    "node": "Cementiri De Martorell. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Martorell. Traslladada Al Valle De Los Caídos",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Martorell. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Martorell. Traslladada Al Valle De Los Caídos",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Martorell. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Martorell. Traslladada Al Valle De Los Caídos",
    "location": "Martorell"
  },
  {
    "node": "Cementiri De Masdenverge",
    "label": "Cementiri De Masdenverge",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Masdenverge",
    "label": "Cementiri De Masdenverge",
    "location": "Masdenverge"
  },
  {
    "node": "Cementiri De Monistrol De Montserrat. Fossa De Soldats Republicans",
    "label": "Cementiri De Monistrol De Montserrat. Fossa De Soldats Republicans",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Monistrol De Montserrat. Fossa De Soldats Republicans",
    "label": "Cementiri De Monistrol De Montserrat. Fossa De Soldats Republicans",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Monistrol De Montserrat. Fossa De Soldats Republicans",
    "label": "Cementiri De Monistrol De Montserrat. Fossa De Soldats Republicans",
    "location": "Monistrol de Montserrat"
  },
  {
    "node": "Cementiri De Monistrol De Montserrat. Víctimes De La Violència A La Rereguarda",
    "label": "Cementiri De Monistrol De Montserrat. Víctimes De La Violència A La Rereguarda",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Monistrol De Montserrat. Víctimes De La Violència A La Rereguarda",
    "label": "Cementiri De Monistrol De Montserrat. Víctimes De La Violència A La Rereguarda",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Monistrol De Montserrat. Víctimes De La Violència A La Rereguarda",
    "label": "Cementiri De Monistrol De Montserrat. Víctimes De La Violència A La Rereguarda",
    "location": "Monistrol de Montserrat"
  },
  {
    "node": "Cementiri De Mont-roig",
    "label": "Cementiri De Mont-roig",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Mont-roig",
    "label": "Cementiri De Mont-roig",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Mont-roig",
    "label": "Cementiri De Mont-roig",
    "location": "Els Plans de Sió"
  },
  {
    "node": "Cementiri De Montblanc. Fossa De Soldats Republicans",
    "label": "Cementiri De Montblanc. Fossa De Soldats Republicans",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De Montblanc. Fossa De Soldats Republicans",
    "label": "Cementiri De Montblanc. Fossa De Soldats Republicans",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Montblanc. Fossa De Soldats Republicans",
    "label": "Cementiri De Montblanc. Fossa De Soldats Republicans",
    "location": "Montblanc"
  },
  {
    "node": "Cementiri De Montferrer (Camp De Treball)",
    "label": "Cementiri De Montferrer (Camp De Treball)",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Montferrer (Camp De Treball)",
    "label": "Cementiri De Montferrer (Camp De Treball)",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Montferrer (Camp De Treball)",
    "label": "Cementiri De Montferrer (Camp De Treball)",
    "location": "Montferrer i Castellbò"
  },
  {
    "node": "Cementiri De Montgai",
    "label": "Cementiri De Montgai",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Montgai",
    "label": "Cementiri De Montgai",
    "location": "Montgai"
  },
  {
    "node": "Cementiri De Montjuïc. Fossar De La Pedrera",
    "label": "Cementiri De Montjuïc. Fossar De La Pedrera",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Montjuïc. Fossar De La Pedrera",
    "label": "Cementiri De Montjuïc. Fossar De La Pedrera",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Móra D'ebre",
    "label": "Cementiri De Móra D'ebre",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Móra D'ebre",
    "label": "Cementiri De Móra D'ebre",
    "location": "Móra d'Ebre"
  },
  {
    "node": "Cementiri De Pardines. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Pardines. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Pardines. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Pardines. Traslladada Al Valle De Los Caídos.",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Pardines. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Pardines. Traslladada Al Valle De Los Caídos.",
    "location": "Pardines"
  },
  {
    "node": "Cementiri De Poboleda",
    "label": "Cementiri De Poboleda",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Poboleda",
    "label": "Cementiri De Poboleda",
    "location": "Poboleda"
  },
  {
    "node": "Cementiri De Ponts. Repressió A La Rereguarda.",
    "label": "Cementiri De Ponts. Repressió A La Rereguarda.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Ponts. Repressió A La Rereguarda.",
    "label": "Cementiri De Ponts. Repressió A La Rereguarda.",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Ponts. Repressió A La Rereguarda.",
    "label": "Cementiri De Ponts. Repressió A La Rereguarda.",
    "location": "Ponts"
  },
  {
    "node": "Cementiri De Prats De Rei",
    "label": "Cementiri De Prats De Rei",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Prats De Rei",
    "label": "Cementiri De Prats De Rei",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Prats De Rei",
    "label": "Cementiri De Prats De Rei",
    "location": "Els Prats de Rei"
  },
  {
    "node": "Cementiri De Preixens",
    "label": "Cementiri De Preixens",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Preixens",
    "label": "Cementiri De Preixens",
    "location": "Preixens"
  },
  {
    "node": "Cementiri De Puigdelfí. Fossa De Soldats Republicans.",
    "label": "Cementiri De Puigdelfí. Fossa De Soldats Republicans.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Puigdelfí. Fossa De Soldats Republicans.",
    "label": "Cementiri De Puigdelfí. Fossa De Soldats Republicans.",
    "location": "Puigdelfí"
  },
  {
    "node": "Cementiri De Queixans. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Queixans. Traslladada Al Valle De Los Caídos",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Queixans. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Queixans. Traslladada Al Valle De Los Caídos",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Queixans. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Queixans. Traslladada Al Valle De Los Caídos",
    "location": "Fontanals de Cerdanya"
  },
  {
    "node": "Cementiri De Reus. Cipriano Martos",
    "label": "Cementiri De Reus. Cipriano Martos",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Reus. Cipriano Martos",
    "label": "Cementiri De Reus. Cipriano Martos",
    "location": "Reus"
  },
  {
    "node": "Cementiri De Reus. Fossa Històrica 5.",
    "label": "Cementiri De Reus. Fossa Històrica 5.",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De Reus. Fossa Històrica 5.",
    "label": "Cementiri De Reus. Fossa Històrica 5.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Reus. Fossa Històrica 5.",
    "label": "Cementiri De Reus. Fossa Històrica 5.",
    "location": "Reus"
  },
  {
    "node": "Cementiri De Reus. Soldats Republicans I Civils.",
    "label": "Cementiri De Reus. Soldats Republicans I Civils.",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De Reus. Soldats Republicans I Civils.",
    "label": "Cementiri De Reus. Soldats Republicans I Civils.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Reus. Soldats Republicans I Civils.",
    "label": "Cementiri De Reus. Soldats Republicans I Civils.",
    "location": "Reus"
  },
  {
    "node": "Cementiri De Rialp (I)",
    "label": "Cementiri De Rialp (I)",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Rialp (I)",
    "label": "Cementiri De Rialp (I)",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Rialp (I)",
    "label": "Cementiri De Rialp (I)",
    "location": "Rialp"
  },
  {
    "node": "Cementiri De Riner",
    "label": "Cementiri De Riner",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Riner",
    "label": "Cementiri De Riner",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Riner",
    "label": "Cementiri De Riner",
    "location": "Riner"
  },
  {
    "node": "Cementiri De Ripoll. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Ripoll. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Ripoll. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Ripoll. Traslladada Al Valle De Los Caídos.",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Ripoll. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Ripoll. Traslladada Al Valle De Los Caídos.",
    "location": "Ripoll"
  },
  {
    "node": "Cementiri De Rocafort De Queralt. Fossa Dels Soldats Franquistes",
    "label": "Cementiri De Rocafort De Queralt. Fossa Dels Soldats Franquistes",
    "location": "Rocafort de Queralt"
  },
  {
    "node": "Cementiri De Rocafort De Queralt. Fossa Dels Soldats Franquistes",
    "label": "Cementiri De Rocafort De Queralt. Fossa Dels Soldats Franquistes",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Roda De Ter",
    "label": "Cementiri De Roda De Ter",
    "location": "Catalunya"
  },
  {
    "node": "Cementiri De Roda De Ter",
    "label": "Cementiri De Roda De Ter",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Roda De Ter",
    "label": "Cementiri De Roda De Ter",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Roda De Ter",
    "label": "Cementiri De Roda De Ter",
    "location": "Roda de Ter"
  },
  {
    "node": "Cementiri De Roda De Ter",
    "label": "Cementiri De Roda De Ter",
    "location": "Osona"
  },
  {
    "node": "Cementiri De Sant Boi De Llobregat. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Boi De Llobregat. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Boi De Llobregat. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Boi De Llobregat. Traslladada Al Valle De Los Caídos.",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Sant Boi De Llobregat. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Boi De Llobregat. Traslladada Al Valle De Los Caídos.",
    "location": "Sant Boi de Llobregat"
  },
  {
    "node": "Cementiri De Sant Domí",
    "label": "Cementiri De Sant Domí",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Domí",
    "label": "Cementiri De Sant Domí",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Sant Domí",
    "label": "Cementiri De Sant Domí",
    "location": "Sant Guim de Freixenet"
  },
  {
    "node": "Cementiri De Sant Feliu De Codines. Fossa De Guillermo Ganuza",
    "label": "Cementiri De Sant Feliu De Codines. Fossa De Guillermo Ganuza",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Sant Feliu De Codines. Fossa De Guillermo Ganuza",
    "label": "Cementiri De Sant Feliu De Codines. Fossa De Guillermo Ganuza",
    "location": "Sant Feliu de Codines"
  },
  {
    "node": "Cementiri De Sant Feliu De Guíxols. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Feliu De Guíxols. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Feliu De Guíxols. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Feliu De Guíxols. Traslladada Al Valle De Los Caídos.",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Sant Feliu De Guíxols. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Feliu De Guíxols. Traslladada Al Valle De Los Caídos.",
    "location": "Sant Feliu de Guíxols"
  },
  {
    "node": "Cementiri De Sant Feliu De Llobregat. Mausoleu Dels 14 Del Canyet",
    "label": "Cementiri De Sant Feliu De Llobregat. Mausoleu Dels 14 Del Canyet",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Feliu De Llobregat. Mausoleu Dels 14 Del Canyet",
    "label": "Cementiri De Sant Feliu De Llobregat. Mausoleu Dels 14 Del Canyet",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Sant Feliu De Llobregat. Mausoleu Dels 14 Del Canyet",
    "label": "Cementiri De Sant Feliu De Llobregat. Mausoleu Dels 14 Del Canyet",
    "location": "Sant Feliu de Llobregat"
  },
  {
    "node": "Cementiri De Sant Gregori. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Sant Gregori. Traslladada Al Valle De Cuelgamuros",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Gregori. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Sant Gregori. Traslladada Al Valle De Cuelgamuros",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Sant Gregori. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Sant Gregori. Traslladada Al Valle De Cuelgamuros",
    "location": "Sant Gregori"
  },
  {
    "node": "Cementiri De Sant Hilari Sacalm",
    "label": "Cementiri De Sant Hilari Sacalm",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Hilari Sacalm",
    "label": "Cementiri De Sant Hilari Sacalm",
    "location": "Sant Hilari Sacalm"
  },
  {
    "node": "Cementiri De Sant Joan De Vilatorrada",
    "label": "Cementiri De Sant Joan De Vilatorrada",
    "location": "Sant Joan de Vilatorrada"
  },
  {
    "node": "Cementiri De Sant Joan Despí",
    "label": "Cementiri De Sant Joan Despí",
    "location": "Catalunya"
  },
  {
    "node": "Cementiri De Sant Joan Despí",
    "label": "Cementiri De Sant Joan Despí",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Joan Despí",
    "label": "Cementiri De Sant Joan Despí",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Sant Joan Despí",
    "label": "Cementiri De Sant Joan Despí",
    "location": "Sant Joan Despí"
  },
  {
    "node": "Cementiri De Sant Joan Despí",
    "label": "Cementiri De Sant Joan Despí",
    "location": "Baix Llobregat"
  },
  {
    "node": "Cementiri De Sant Llorenç De Morunys",
    "label": "Cementiri De Sant Llorenç De Morunys",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Llorenç De Morunys",
    "label": "Cementiri De Sant Llorenç De Morunys",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Sant Llorenç De Morunys",
    "label": "Cementiri De Sant Llorenç De Morunys",
    "location": "Sant Llorenç de Morunys"
  },
  {
    "node": "Cementiri De Sant Martí De Merlès",
    "label": "Cementiri De Sant Martí De Merlès",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Sant Martí De Merlès",
    "label": "Cementiri De Sant Martí De Merlès",
    "location": "Sant Martí de Merlès"
  },
  {
    "node": "Cementiri De Sant Martí Del Brull",
    "label": "Cementiri De Sant Martí Del Brull",
    "location": "El Brull"
  },
  {
    "node": "Cementiri De Sant Miquel De Campmajor. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Miquel De Campmajor. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Miquel De Campmajor. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Miquel De Campmajor. Traslladada Al Valle De Los Caídos.",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Sant Miquel De Campmajor. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Miquel De Campmajor. Traslladada Al Valle De Los Caídos.",
    "location": "Sant Miquel de Campmajor"
  },
  {
    "node": "Cementiri De Sant Pere De Ribes",
    "label": "Cementiri De Sant Pere De Ribes",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Pere De Ribes",
    "label": "Cementiri De Sant Pere De Ribes",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Sant Pere De Ribes",
    "label": "Cementiri De Sant Pere De Ribes",
    "location": "Sant Pere de Ribes"
  },
  {
    "node": "Cementiri De Sant Quintí De Mediona",
    "label": "Cementiri De Sant Quintí De Mediona",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Quintí De Mediona",
    "label": "Cementiri De Sant Quintí De Mediona",
    "location": "Sant Quintí de Mediona"
  },
  {
    "node": "Cementiri De Sant Quintí De Mediona. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Quintí De Mediona. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Quintí De Mediona. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Quintí De Mediona. Traslladada Al Valle De Los Caídos.",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Sant Quintí De Mediona. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Quintí De Mediona. Traslladada Al Valle De Los Caídos.",
    "location": "Sant Quintí de Mediona"
  },
  {
    "node": "Cementiri De Sant Sebastià. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Sebastià. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Sebastià. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Sebastià. Traslladada Al Valle De Los Caídos.",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Sant Sebastià. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Sebastià. Traslladada Al Valle De Los Caídos.",
    "location": "Sitges"
  },
  {
    "node": "Cementiri De Santa Bàrbara",
    "label": "Cementiri De Santa Bàrbara",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Santa Bàrbara",
    "label": "Cementiri De Santa Bàrbara",
    "location": "Santa Bàrbara"
  },
  {
    "node": "Cementiri De Santa Coloma De Farners",
    "label": "Cementiri De Santa Coloma De Farners",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Santa Coloma De Farners",
    "label": "Cementiri De Santa Coloma De Farners",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Santa Coloma De Farners",
    "label": "Cementiri De Santa Coloma De Farners",
    "location": "Santa Coloma de Farners"
  },
  {
    "node": "Cementiri De Santa Susanna",
    "label": "Cementiri De Santa Susanna",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Santa Susanna",
    "label": "Cementiri De Santa Susanna",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Santa Susanna",
    "label": "Cementiri De Santa Susanna",
    "location": "Riner"
  },
  {
    "node": "Cementiri De Sarrià De Ter. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Sarrià De Ter. Traslladada Al Valle De Cuelgamuros",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sarrià De Ter. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Sarrià De Ter. Traslladada Al Valle De Cuelgamuros",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Sarrià De Ter. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Sarrià De Ter. Traslladada Al Valle De Cuelgamuros",
    "location": "Sarrià de Ter"
  },
  {
    "node": "Cementiri De Sedó",
    "label": "Cementiri De Sedó",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sedó",
    "label": "Cementiri De Sedó",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Sedó",
    "label": "Cementiri De Sedó",
    "location": "Torrefeta i Florejacs"
  },
  {
    "node": "Cementiri De Sedó II",
    "label": "Cementiri De Sedó II",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sedó II",
    "label": "Cementiri De Sedó II",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Sedó II",
    "label": "Cementiri De Sedó II",
    "location": "Torrefeta"
  },
  {
    "node": "Cementiri De Sils",
    "label": "Cementiri De Sils",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sils",
    "label": "Cementiri De Sils",
    "location": "Sils"
  },
  {
    "node": "Cementiri De Sisteró Pelagalls II",
    "label": "Cementiri De Sisteró Pelagalls II",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sisteró Pelagalls II",
    "label": "Cementiri De Sisteró Pelagalls II",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Sisteró Pelagalls II",
    "label": "Cementiri De Sisteró Pelagalls II",
    "location": "Els Plans de Sió"
  },
  {
    "node": "Cementiri De Tarragona. Fossa 1 Repressió Franquista.",
    "label": "Cementiri De Tarragona. Fossa 1 Repressió Franquista.",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De Tarragona. Fossa 1 Repressió Franquista.",
    "label": "Cementiri De Tarragona. Fossa 1 Repressió Franquista.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Tarragona. Fossa 2 Repressió Franquista",
    "label": "Cementiri De Tarragona. Fossa 2 Repressió Franquista",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De Tarragona. Fossa 2 Repressió Franquista",
    "label": "Cementiri De Tarragona. Fossa 2 Repressió Franquista",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Tarragona. Fossa Del Cementiri Neutre. Víctimes De La Repressió Franquista.",
    "label": "Cementiri De Tarragona. Fossa Del Cementiri Neutre. Víctimes De La Repressió Franquista.",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De Tarragona. Fossa Del Cementiri Neutre. Víctimes De La Repressió Franquista.",
    "label": "Cementiri De Tarragona. Fossa Del Cementiri Neutre. Víctimes De La Repressió Franquista.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Tarroja De Segarra",
    "label": "Cementiri De Tarroja De Segarra",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Tarroja De Segarra",
    "label": "Cementiri De Tarroja De Segarra",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Tarroja De Segarra",
    "label": "Cementiri De Tarroja De Segarra",
    "location": "Tarroja de Segarra"
  },
  {
    "node": "Cementiri De Tarrés",
    "label": "Cementiri De Tarrés",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Tarrés",
    "label": "Cementiri De Tarrés",
    "location": "Tarrés"
  },
  {
    "node": "Cementiri De Terrades. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Terrades. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Terrades. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Terrades. Traslladada Al Valle De Los Caídos.",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Terrades. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Terrades. Traslladada Al Valle De Los Caídos.",
    "location": "Terrades"
  },
  {
    "node": "Cementiri De Torrebesses",
    "label": "Cementiri De Torrebesses",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Torrebesses",
    "label": "Cementiri De Torrebesses",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Torrebesses",
    "label": "Cementiri De Torrebesses",
    "location": "Torrebesses"
  },
  {
    "node": "Cementiri De Torà",
    "label": "Cementiri De Torà",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Torà",
    "label": "Cementiri De Torà",
    "location": "Torà"
  },
  {
    "node": "Cementiri De Toses. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Toses. Traslladada Al Valle De Los Caídos",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Toses. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Toses. Traslladada Al Valle De Los Caídos",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Toses. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Toses. Traslladada Al Valle De Los Caídos",
    "location": "Toses"
  },
  {
    "node": "Cementiri De Tírvia",
    "label": "Cementiri De Tírvia",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Tírvia",
    "label": "Cementiri De Tírvia",
    "location": "Tírvia"
  },
  {
    "node": "Cementiri De Vallverd",
    "label": "Cementiri De Vallverd",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Vallverd",
    "label": "Cementiri De Vallverd",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Vallverd",
    "label": "Cementiri De Vallverd",
    "location": "Ivars D'Urgell"
  },
  {
    "node": "Cementiri De Vila-Rodona. Repressió A La Reraguarda",
    "label": "Cementiri De Vila-Rodona. Repressió A La Reraguarda",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De Vila-Rodona. Repressió A La Reraguarda",
    "label": "Cementiri De Vila-Rodona. Repressió A La Reraguarda",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Vila-Rodona. Repressió A La Reraguarda",
    "label": "Cementiri De Vila-Rodona. Repressió A La Reraguarda",
    "location": "Vila-rodona"
  },
  {
    "node": "Cementiri De Vilac",
    "label": "Cementiri De Vilac",
    "location": "Vielha e Mijaran"
  },
  {
    "node": "Cementiri De Vilademuls. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Vilademuls. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Vilademuls. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Vilademuls. Traslladada Al Valle De Los Caídos.",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Vilademuls. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Vilademuls. Traslladada Al Valle De Los Caídos.",
    "location": "Vilademuls"
  },
  {
    "node": "Cementiri De Viladrau. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Viladrau. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Viladrau. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Viladrau. Traslladada Al Valle De Los Caídos.",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Viladrau. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Viladrau. Traslladada Al Valle De Los Caídos.",
    "location": "Viladrau"
  },
  {
    "node": "Cementiri De Vilafranca Del Penedès",
    "label": "Cementiri De Vilafranca Del Penedès",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Vilafranca Del Penedès",
    "label": "Cementiri De Vilafranca Del Penedès",
    "location": "Vilafranca del Penedès"
  },
  {
    "node": "Cementiri De Vilalba Dels Arcs. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Vilalba Dels Arcs. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Vilalba Dels Arcs. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Vilalba Dels Arcs. Traslladada Al Valle De Los Caídos.",
    "location": "Vilalba dels Arcs"
  },
  {
    "node": "Cementiri De Vilamur",
    "label": "Cementiri De Vilamur",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Vilamur",
    "label": "Cementiri De Vilamur",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Vilamur",
    "label": "Cementiri De Vilamur",
    "location": "Vilamur"
  },
  {
    "node": "Cementiri De Vilanova De Bellpuig",
    "label": "Cementiri De Vilanova De Bellpuig",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Vilanova De Bellpuig",
    "label": "Cementiri De Vilanova De Bellpuig",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Vilanova De Bellpuig",
    "label": "Cementiri De Vilanova De Bellpuig",
    "location": "Vilanova De Bellpuig"
  },
  {
    "node": "Cementiri Del Catllar. Repressió De Reraguarda.",
    "label": "Cementiri Del Catllar. Repressió De Reraguarda.",
    "location": "Spain"
  },
  {
    "node": "Cementiri Del Catllar. Repressió De Reraguarda.",
    "label": "Cementiri Del Catllar. Repressió De Reraguarda.",
    "location": "El Catllar"
  },
  {
    "node": "Cementiri Del Catllar. Soldat De L'exèrcit Popular De La República",
    "label": "Cementiri Del Catllar. Soldat De L'exèrcit Popular De La República",
    "location": "Spain"
  },
  {
    "node": "Cementiri Del Catllar. Soldat De L'exèrcit Popular De La República",
    "label": "Cementiri Del Catllar. Soldat De L'exèrcit Popular De La República",
    "location": "El Catllar"
  },
  {
    "node": "Cementiri Del Llor",
    "label": "Cementiri Del Llor",
    "location": "Spain"
  },
  {
    "node": "Cementiri Del Llor",
    "label": "Cementiri Del Llor",
    "location": "Lleida"
  },
  {
    "node": "Cementiri Del Llor",
    "label": "Cementiri Del Llor",
    "location": "Torrefeta"
  },
  {
    "node": "Cementiri Del Palau D'Anglesola",
    "label": "Cementiri Del Palau D'Anglesola",
    "location": "Spain"
  },
  {
    "node": "Cementiri Del Palau D'Anglesola",
    "label": "Cementiri Del Palau D'Anglesola",
    "location": "Lleida"
  },
  {
    "node": "Cementiri Del Palau D'Anglesola",
    "label": "Cementiri Del Palau D'Anglesola",
    "location": "El Palau D'Anglesola"
  },
  {
    "node": "Cementiri Del Perelló",
    "label": "Cementiri Del Perelló",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri Del Perelló",
    "label": "Cementiri Del Perelló",
    "location": "Catalunya"
  },
  {
    "node": "Cementiri Del Perelló",
    "label": "Cementiri Del Perelló",
    "location": "Spain"
  },
  {
    "node": "Cementiri Del Perelló",
    "label": "Cementiri Del Perelló",
    "location": "Baix Ebre"
  },
  {
    "node": "Cementiri Del Perelló",
    "label": "Cementiri Del Perelló",
    "location": "El Perelló"
  },
  {
    "node": "Cementiri Del Talladell",
    "label": "Cementiri Del Talladell",
    "location": "Spain"
  },
  {
    "node": "Cementiri Del Talladell",
    "label": "Cementiri Del Talladell",
    "location": "Tàrrega"
  },
  {
    "node": "Cementiri Dels Guiamets",
    "label": "Cementiri Dels Guiamets",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri Dels Guiamets",
    "label": "Cementiri Dels Guiamets",
    "location": "Spain"
  },
  {
    "node": "Cementiri Dels Guiamets",
    "label": "Cementiri Dels Guiamets",
    "location": "Els Guiamets"
  },
  {
    "node": "Cementiri Dels Reguers",
    "label": "Cementiri Dels Reguers",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri Dels Reguers",
    "label": "Cementiri Dels Reguers",
    "location": "Spain"
  },
  {
    "node": "Cementiri Dels Reguers",
    "label": "Cementiri Dels Reguers",
    "location": "Tortosa"
  },
  {
    "node": "Cementiri Dels Reguers II",
    "label": "Cementiri Dels Reguers II",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri Dels Reguers II",
    "label": "Cementiri Dels Reguers II",
    "location": "Spain"
  },
  {
    "node": "Cementiri Dels Reguers II",
    "label": "Cementiri Dels Reguers II",
    "location": "Els Reguers"
  },
  {
    "node": "Cementiri El Molar",
    "label": "Cementiri El Molar",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri El Molar",
    "label": "Cementiri El Molar",
    "location": "Spain"
  },
  {
    "node": "Cementiri El Molar",
    "label": "Cementiri El Molar",
    "location": "El Molar"
  },
  {
    "node": "Cementiri Nou del Soleràs",
    "label": "Cementiri Nou del Soleràs",
    "location": "Spain"
  },
  {
    "node": "Cementiri Nou del Soleràs",
    "label": "Cementiri Nou del Soleràs",
    "location": "El Soleràs"
  },
  {
    "node": "Cementiri Roní (I)",
    "label": "Cementiri Roní (I)",
    "location": "Spain"
  },
  {
    "node": "Cementiri Roní (I)",
    "label": "Cementiri Roní (I)",
    "location": "Lleida"
  },
  {
    "node": "Cementiri Roní (I)",
    "label": "Cementiri Roní (I)",
    "location": "Rialp"
  },
  {
    "node": "Cementiri Sant Sadurní D'Anoia. Soldats Franquistes",
    "label": "Cementiri Sant Sadurní D'Anoia. Soldats Franquistes",
    "location": "Spain"
  },
  {
    "node": "Cementiri Sant Sadurní D'Anoia. Soldats Franquistes",
    "label": "Cementiri Sant Sadurní D'Anoia. Soldats Franquistes",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri Sant Sadurní D'Anoia. Soldats Franquistes",
    "label": "Cementiri Sant Sadurní D'Anoia. Soldats Franquistes",
    "location": "Sant Sadurní d'Anoia"
  },
  {
    "node": "Cementiri Vell D'Abrera",
    "label": "Cementiri Vell D'Abrera",
    "location": "Spain"
  },
  {
    "node": "Cementiri Vell D'Abrera",
    "label": "Cementiri Vell D'Abrera",
    "location": "Abrera"
  },
  {
    "node": "Cementiri Vell D'albinyana",
    "label": "Cementiri Vell D'albinyana",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri Vell D'albinyana",
    "label": "Cementiri Vell D'albinyana",
    "location": "Catalunya"
  },
  {
    "node": "Cementiri Vell D'albinyana",
    "label": "Cementiri Vell D'albinyana",
    "location": "Spain"
  },
  {
    "node": "Cementiri Vell D'albinyana",
    "label": "Cementiri Vell D'albinyana",
    "location": "Albinyana"
  },
  {
    "node": "Cementiri Vell D'albinyana",
    "label": "Cementiri Vell D'albinyana",
    "location": "Baix Penedès"
  },
  {
    "node": "Cementiri Vell Del Soleràs",
    "label": "Cementiri Vell Del Soleràs",
    "location": "Catalunya"
  },
  {
    "node": "Cementiri Vell Del Soleràs",
    "label": "Cementiri Vell Del Soleràs",
    "location": "Spain"
  },
  {
    "node": "Cementiri Vell Del Soleràs",
    "label": "Cementiri Vell Del Soleràs",
    "location": "Lleida"
  },
  {
    "node": "Cementiri Vell Del Soleràs",
    "label": "Cementiri Vell Del Soleràs",
    "location": "El Soleràs"
  },
  {
    "node": "Cementiri Vell Del Soleràs",
    "label": "Cementiri Vell Del Soleràs",
    "location": "Garrigues"
  },
  {
    "node": "Cementiri d'Ainet de Besan",
    "label": "Cementiri d'Ainet de Besan",
    "location": "Spain"
  },
  {
    "node": "Cementiri d'Ainet de Besan",
    "label": "Cementiri d'Ainet de Besan",
    "location": "Alins"
  },
  {
    "node": "Cementiri d'Alins",
    "label": "Cementiri d'Alins",
    "location": "Spain"
  },
  {
    "node": "Cementiri d'Alins",
    "label": "Cementiri d'Alins",
    "location": "Lleida"
  },
  {
    "node": "Cementiri d'Alins",
    "label": "Cementiri d'Alins",
    "location": "Alins"
  },
  {
    "node": "Cementiri d'Alta-Riba II",
    "label": "Cementiri d'Alta-Riba II",
    "location": "Estaràs"
  },
  {
    "node": "Cementiri d'Altafulla. Fossa de soldats republicans",
    "label": "Cementiri d'Altafulla. Fossa de soldats republicans",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri d'Altafulla. Fossa de soldats republicans",
    "label": "Cementiri d'Altafulla. Fossa de soldats republicans",
    "location": "Spain"
  },
  {
    "node": "Cementiri d'Altafulla. Fossa de soldats republicans",
    "label": "Cementiri d'Altafulla. Fossa de soldats republicans",
    "location": "Altafulla"
  },
  {
    "node": "Cementiri d'Alòs de Balaguer. Tomba de Josep Gou Marsà",
    "label": "Cementiri d'Alòs de Balaguer. Tomba de Josep Gou Marsà",
    "location": "Spain"
  },
  {
    "node": "Cementiri d'Alòs de Balaguer. Tomba de Josep Gou Marsà",
    "label": "Cementiri d'Alòs de Balaguer. Tomba de Josep Gou Marsà",
    "location": "Lleida"
  },
  {
    "node": "Cementiri d'Alòs de Balaguer. Tomba de Josep Gou Marsà",
    "label": "Cementiri d'Alòs de Balaguer. Tomba de Josep Gou Marsà",
    "location": "Alòs de Balaguer"
  },
  {
    "node": "Cementiri d'Ogern. Víctimes del Camp de Treball núm. 5 del SIM",
    "label": "Cementiri d'Ogern. Víctimes del Camp de Treball núm. 5 del SIM",
    "location": "Ogern"
  },
  {
    "node": "Cementiri d'Ulldemolins",
    "label": "Cementiri d'Ulldemolins",
    "location": "Ulldemolins"
  },
  {
    "node": "Cementiri d'Àreu",
    "label": "Cementiri d'Àreu",
    "location": null
  },
  {
    "node": "Cementiri de Biure de Gaià. Fossa d'un soldat republicà.",
    "label": "Cementiri de Biure de Gaià. Fossa d'un soldat republicà.",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Biure de Gaià. Fossa d'un soldat republicà.",
    "label": "Cementiri de Biure de Gaià. Fossa d'un soldat republicà.",
    "location": "Biure de Gaià"
  },
  {
    "node": "Cementiri de Bolvir. Traslladada al Valle de los Caídos",
    "label": "Cementiri de Bolvir. Traslladada al Valle de los Caídos",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Bolvir. Traslladada al Valle de los Caídos",
    "label": "Cementiri de Bolvir. Traslladada al Valle de los Caídos",
    "location": "Girona"
  },
  {
    "node": "Cementiri de Bolvir. Traslladada al Valle de los Caídos",
    "label": "Cementiri de Bolvir. Traslladada al Valle de los Caídos",
    "location": "Bolvir"
  },
  {
    "node": "Cementiri de Capçanes",
    "label": "Cementiri de Capçanes",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Capçanes",
    "label": "Cementiri de Capçanes",
    "location": "Capçanes"
  },
  {
    "node": "Cementiri de Castellnou de Bages",
    "label": "Cementiri de Castellnou de Bages",
    "location": "Castellnou de Bages"
  },
  {
    "node": "Cementiri de Collbató",
    "label": "Cementiri de Collbató",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de Collbató",
    "label": "Cementiri de Collbató",
    "location": "Collbató"
  },
  {
    "node": "Cementiri de Cornellà de Llobregat. Traslladada al Valle de los Caídos",
    "label": "Cementiri de Cornellà de Llobregat. Traslladada al Valle de los Caídos",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Cornellà de Llobregat. Traslladada al Valle de los Caídos",
    "label": "Cementiri de Cornellà de Llobregat. Traslladada al Valle de los Caídos",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de Cornellà de Llobregat. Traslladada al Valle de los Caídos",
    "label": "Cementiri de Cornellà de Llobregat. Traslladada al Valle de los Caídos",
    "location": "Cornellà de Llobregat"
  },
  {
    "node": "Cementiri de Cornudella de Montsant",
    "label": "Cementiri de Cornudella de Montsant",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri de Cornudella de Montsant",
    "label": "Cementiri de Cornudella de Montsant",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Cornudella de Montsant",
    "label": "Cementiri de Cornudella de Montsant",
    "location": "Cornudella de Montsant"
  },
  {
    "node": "Cementiri de Darmós",
    "label": "Cementiri de Darmós",
    "location": "Darmós"
  },
  {
    "node": "Cementiri de Girona",
    "label": "Cementiri de Girona",
    "location": "Girona"
  },
  {
    "node": "Cementiri de Gra",
    "label": "Cementiri de Gra",
    "location": "Torrefeta"
  },
  {
    "node": "Cementiri de Guissona II",
    "label": "Cementiri de Guissona II",
    "location": "Guissona"
  },
  {
    "node": "Cementiri de Lleida. Departament de Sant Miquel. Traslladada al Valle de Cuelgamuros",
    "label": "Cementiri de Lleida. Departament de Sant Miquel. Traslladada al Valle de Cuelgamuros",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Lleida. Departament de Sant Miquel. Traslladada al Valle de Cuelgamuros",
    "label": "Cementiri de Lleida. Departament de Sant Miquel. Traslladada al Valle de Cuelgamuros",
    "location": "Lleida"
  },
  {
    "node": "Cementiri de Llessui",
    "label": "Cementiri de Llessui",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Llessui",
    "label": "Cementiri de Llessui",
    "location": "Llessui"
  },
  {
    "node": "Cementiri de Marçà",
    "label": "Cementiri de Marçà",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Marçà",
    "label": "Cementiri de Marçà",
    "location": "Marçà"
  },
  {
    "node": "Cementiri de Moià",
    "label": "Cementiri de Moià",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Moià",
    "label": "Cementiri de Moià",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de Moià",
    "label": "Cementiri de Moià",
    "location": "Moià"
  },
  {
    "node": "Cementiri de Montjuïc. Víctimes de bombardeig de la Barceloneta",
    "label": "Cementiri de Montjuïc. Víctimes de bombardeig de la Barceloneta",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Montjuïc. Víctimes de bombardeig de la Barceloneta",
    "label": "Cementiri de Montjuïc. Víctimes de bombardeig de la Barceloneta",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de Montmaneu",
    "label": "Cementiri de Montmaneu",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Montmaneu",
    "label": "Cementiri de Montmaneu",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de Montmaneu",
    "label": "Cementiri de Montmaneu",
    "location": "Montmaneu"
  },
  {
    "node": "Cementiri de Polinyà",
    "label": "Cementiri de Polinyà",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Polinyà",
    "label": "Cementiri de Polinyà",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de Polinyà",
    "label": "Cementiri de Polinyà",
    "location": "Polinyà"
  },
  {
    "node": "Cementiri de Pontons",
    "label": "Cementiri de Pontons",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Pontons",
    "label": "Cementiri de Pontons",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de Pontons",
    "label": "Cementiri de Pontons",
    "location": "Pontons"
  },
  {
    "node": "Cementiri de Pradell de la Teixeta",
    "label": "Cementiri de Pradell de la Teixeta",
    "location": "Pradell de la Teixeta"
  },
  {
    "node": "Cementiri de Prades. Soldats del Cos d’Exèrcit Marroquí",
    "label": "Cementiri de Prades. Soldats del Cos d’Exèrcit Marroquí",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri de Prades. Soldats del Cos d’Exèrcit Marroquí",
    "label": "Cementiri de Prades. Soldats del Cos d’Exèrcit Marroquí",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Prades. Soldats del Cos d’Exèrcit Marroquí",
    "label": "Cementiri de Prades. Soldats del Cos d’Exèrcit Marroquí",
    "location": "Prades"
  },
  {
    "node": "Cementiri de Rocafort de Queralt. Fossa de soldats republicans.",
    "label": "Cementiri de Rocafort de Queralt. Fossa de soldats republicans.",
    "location": "Rocafort de Queralt"
  },
  {
    "node": "Cementiri de Rocafort de Queralt. Fossa de soldats republicans.",
    "label": "Cementiri de Rocafort de Queralt. Fossa de soldats republicans.",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Sant Guim de Freixenet",
    "label": "Cementiri de Sant Guim de Freixenet",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Sant Guim de Freixenet",
    "label": "Cementiri de Sant Guim de Freixenet",
    "location": "Sant Guim de Freixenet"
  },
  {
    "node": "Cementiri de Sant Guim de Freixenet II",
    "label": "Cementiri de Sant Guim de Freixenet II",
    "location": "Sant Guim de Freixenet"
  },
  {
    "node": "Cementiri de Sant Julià de Ramis. Traslladada al Valle de Cuelgamuros",
    "label": "Cementiri de Sant Julià de Ramis. Traslladada al Valle de Cuelgamuros",
    "location": "Sant Julià de Ramis"
  },
  {
    "node": "Cementiri de Sant Martí de Tous",
    "label": "Cementiri de Sant Martí de Tous",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Sant Martí de Tous",
    "label": "Cementiri de Sant Martí de Tous",
    "location": "Sant Martí de Tous"
  },
  {
    "node": "Cementiri de Sant Mateu de Bages",
    "label": "Cementiri de Sant Mateu de Bages",
    "location": "Sant Mateu de Bages"
  },
  {
    "node": "Cementiri de Sant Pere de Riudebitlles. Traslladada al Valle de los Caídos",
    "label": "Cementiri de Sant Pere de Riudebitlles. Traslladada al Valle de los Caídos",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Sant Pere de Riudebitlles. Traslladada al Valle de los Caídos",
    "label": "Cementiri de Sant Pere de Riudebitlles. Traslladada al Valle de los Caídos",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de Sant Pere de Riudebitlles. Traslladada al Valle de los Caídos",
    "label": "Cementiri de Sant Pere de Riudebitlles. Traslladada al Valle de los Caídos",
    "location": "Sant Pere de Riudebitlles"
  },
  {
    "node": "Cementiri de Tarragona. Repressió de rereguarda",
    "label": "Cementiri de Tarragona. Repressió de rereguarda",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri de Tarragona. Repressió de rereguarda",
    "label": "Cementiri de Tarragona. Repressió de rereguarda",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Torregrossa",
    "label": "Cementiri de Torregrossa",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Torregrossa",
    "label": "Cementiri de Torregrossa",
    "location": "Torregrossa"
  },
  {
    "node": "Cementiri de Torrelles de Foix",
    "label": "Cementiri de Torrelles de Foix",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Torrelles de Foix",
    "label": "Cementiri de Torrelles de Foix",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de Torrelles de Foix",
    "label": "Cementiri de Torrelles de Foix",
    "location": "Torrelles de Foix"
  },
  {
    "node": "Cementiri de Torroja del Priorat",
    "label": "Cementiri de Torroja del Priorat",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Torroja del Priorat",
    "label": "Cementiri de Torroja del Priorat",
    "location": "Torroja del Priorat"
  },
  {
    "node": "Cementiri de Tàrrega",
    "label": "Cementiri de Tàrrega",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Tàrrega",
    "label": "Cementiri de Tàrrega",
    "location": "Lleida"
  },
  {
    "node": "Cementiri de Tàrrega",
    "label": "Cementiri de Tàrrega",
    "location": "Tàrrega"
  },
  {
    "node": "Cementiri de l'Albi",
    "label": "Cementiri de l'Albi",
    "location": "Spain"
  },
  {
    "node": "Cementiri de l'Albi",
    "label": "Cementiri de l'Albi",
    "location": "L'Albi"
  },
  {
    "node": "Cementiri de l'Espluga de Francolí. Soldats procedents de l’Hospital Militar de les Masies",
    "label": "Cementiri de l'Espluga de Francolí. Soldats procedents de l’Hospital Militar de les Masies",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri de l'Espluga de Francolí. Soldats procedents de l’Hospital Militar de les Masies",
    "label": "Cementiri de l'Espluga de Francolí. Soldats procedents de l’Hospital Militar de les Masies",
    "location": "Spain"
  },
  {
    "node": "Cementiri de l'Espluga de Francolí. Soldats procedents de l’Hospital Militar de les Masies",
    "label": "Cementiri de l'Espluga de Francolí. Soldats procedents de l’Hospital Militar de les Masies",
    "location": "L'Espluga de Francolí"
  },
  {
    "node": "Cementiri de la Gornal. Soldats republicans",
    "label": "Cementiri de la Gornal. Soldats republicans",
    "location": "Spain"
  },
  {
    "node": "Cementiri de la Gornal. Soldats republicans",
    "label": "Cementiri de la Gornal. Soldats republicans",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de la Gornal. Soldats republicans",
    "label": "Cementiri de la Gornal. Soldats republicans",
    "location": "Castellet i la Gornal"
  },
  {
    "node": "Cementiri de la Guixera de Sort",
    "label": "Cementiri de la Guixera de Sort",
    "location": "Spain"
  },
  {
    "node": "Cementiri de la Guixera de Sort",
    "label": "Cementiri de la Guixera de Sort",
    "location": "Lleida"
  },
  {
    "node": "Cementiri de la Guixera de Sort",
    "label": "Cementiri de la Guixera de Sort",
    "location": "Sort"
  },
  {
    "node": "Cementiri de la Palma d'Ebre. Soldats republicans i civils",
    "label": "Cementiri de la Palma d'Ebre. Soldats republicans i civils",
    "location": "La Palma d'Ebre"
  },
  {
    "node": "Cementiri de la Pobla de Claramunt",
    "label": "Cementiri de la Pobla de Claramunt",
    "location": "Spain"
  },
  {
    "node": "Cementiri de la Pobla de Claramunt",
    "label": "Cementiri de la Pobla de Claramunt",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de la Pobla de Claramunt",
    "label": "Cementiri de la Pobla de Claramunt",
    "location": "La Pobla de Claramunt"
  },
  {
    "node": "Cementiri de la Pobla de Cérvoles",
    "label": "Cementiri de la Pobla de Cérvoles",
    "location": "Spain"
  },
  {
    "node": "Cementiri de la Pobla de Cérvoles",
    "label": "Cementiri de la Pobla de Cérvoles",
    "location": "La Pobla de Cérvoles"
  },
  {
    "node": "Cementiri de la Pobla de Segur. Panteó de víctimes de la rereguarda",
    "label": "Cementiri de la Pobla de Segur. Panteó de víctimes de la rereguarda",
    "location": "La Pobla de Segur"
  },
  {
    "node": "Cementiri de la Seu d'Urgell. Inhumats en fossa de beneficiència",
    "label": "Cementiri de la Seu d'Urgell. Inhumats en fossa de beneficiència",
    "location": "Spain"
  },
  {
    "node": "Cementiri de la Seu d'Urgell. Inhumats en fossa de beneficiència",
    "label": "Cementiri de la Seu d'Urgell. Inhumats en fossa de beneficiència",
    "location": "Lleida"
  },
  {
    "node": "Cementiri de la Seu d'Urgell. Inhumats en fossa de beneficiència",
    "label": "Cementiri de la Seu d'Urgell. Inhumats en fossa de beneficiència",
    "location": "La Seu d'Urgell"
  },
  {
    "node": "Cementiri del Cogul",
    "label": "Cementiri del Cogul",
    "location": "Spain"
  },
  {
    "node": "Cementiri del Cogul",
    "label": "Cementiri del Cogul",
    "location": "El Cogul"
  },
  {
    "node": "Cementiri del Masroig",
    "label": "Cementiri del Masroig",
    "location": "El Masroig"
  },
  {
    "node": "Cementiri del Pinell de Brai",
    "label": "Cementiri del Pinell de Brai",
    "location": "El Pinell de Brai"
  },
  {
    "node": "Cementiri del Vilosell",
    "label": "Cementiri del Vilosell",
    "location": "Spain"
  },
  {
    "node": "Cementiri del Vilosell",
    "label": "Cementiri del Vilosell",
    "location": "El Vilosell"
  },
  {
    "node": "Cinglo Alt - rodalies de la masia de Bonrepòs",
    "label": "Cinglo Alt - rodalies de la masia de Bonrepòs",
    "location": "Spain"
  },
  {
    "node": "Cinglo Alt - rodalies de la masia de Bonrepòs",
    "label": "Cinglo Alt - rodalies de la masia de Bonrepòs",
    "location": "Gavet de la Conca"
  },
  {
    "node": "Closa De Fonolleres",
    "label": "Closa De Fonolleres",
    "location": "Spain"
  },
  {
    "node": "Closa De Fonolleres",
    "label": "Closa De Fonolleres",
    "location": "Tàrrega"
  },
  {
    "node": "Codinera De La Casa Tapioles",
    "label": "Codinera De La Casa Tapioles",
    "location": "Spain"
  },
  {
    "node": "Codinera De La Casa Tapioles",
    "label": "Codinera De La Casa Tapioles",
    "location": "Lleida"
  },
  {
    "node": "Codinera De La Casa Tapioles",
    "label": "Codinera De La Casa Tapioles",
    "location": "Altès"
  },
  {
    "node": "Coll De Leix - Gargallera 2",
    "label": "Coll De Leix - Gargallera 2",
    "location": "Spain"
  },
  {
    "node": "Coll De Leix - Gargallera 2",
    "label": "Coll De Leix - Gargallera 2",
    "location": "Montferrer i Castellbò"
  },
  {
    "node": "Coma De La Carretera D'Alcanó",
    "label": "Coma De La Carretera D'Alcanó",
    "location": "Spain"
  },
  {
    "node": "Coma De La Carretera D'Alcanó",
    "label": "Coma De La Carretera D'Alcanó",
    "location": "Granyena de les Garrigues"
  },
  {
    "node": "Cometes I. Poble Vell",
    "label": "Cometes I. Poble Vell",
    "location": "Tarragona"
  },
  {
    "node": "Cometes I. Poble Vell",
    "label": "Cometes I. Poble Vell",
    "location": "Spain"
  },
  {
    "node": "Cometes I. Poble Vell",
    "label": "Cometes I. Poble Vell",
    "location": "Corbera d'Ebre"
  },
  {
    "node": "Cometes II. Poble Vell",
    "label": "Cometes II. Poble Vell",
    "location": "Tarragona"
  },
  {
    "node": "Cometes II. Poble Vell",
    "label": "Cometes II. Poble Vell",
    "location": "Spain"
  },
  {
    "node": "Cometes II. Poble Vell",
    "label": "Cometes II. Poble Vell",
    "location": "Corbera d'Ebre"
  },
  {
    "node": "Corba del Salt",
    "label": "Corba del Salt",
    "location": "Spain"
  },
  {
    "node": "Corba del Salt",
    "label": "Corba del Salt",
    "location": "Lleida"
  },
  {
    "node": "Corba del Salt",
    "label": "Corba del Salt",
    "location": "Alt Àneu"
  },
  {
    "node": "Costa Del Mas Dels Quadros",
    "label": "Costa Del Mas Dels Quadros",
    "location": "Spain"
  },
  {
    "node": "Costa Del Mas Dels Quadros",
    "label": "Costa Del Mas Dels Quadros",
    "location": "Lleida"
  },
  {
    "node": "Costa Del Mas Dels Quadros",
    "label": "Costa Del Mas Dels Quadros",
    "location": "Llobera"
  },
  {
    "node": "Costa Negra: La Socarrada",
    "label": "Costa Negra: La Socarrada",
    "location": "Rialp"
  },
  {
    "node": "Cota 705 - Punta Alta",
    "label": "Cota 705 - Punta Alta",
    "location": "Tarragona"
  },
  {
    "node": "Cota 705 - Punta Alta",
    "label": "Cota 705 - Punta Alta",
    "location": "Spain"
  },
  {
    "node": "Cota 705 - Punta Alta",
    "label": "Cota 705 - Punta Alta",
    "location": "El Pinell de Brai"
  },
  {
    "node": "Devesa Del Baiget",
    "label": "Devesa Del Baiget",
    "location": "Spain"
  },
  {
    "node": "Devesa Del Baiget",
    "label": "Devesa Del Baiget",
    "location": "Lleida"
  },
  {
    "node": "Devesa Del Baiget",
    "label": "Devesa Del Baiget",
    "location": "Cervià de les Garrigues"
  },
  {
    "node": "Domenges",
    "label": "Domenges",
    "location": "Tarragona"
  },
  {
    "node": "Domenges",
    "label": "Domenges",
    "location": "Spain"
  },
  {
    "node": "Domenges",
    "label": "Domenges",
    "location": "Gandesa"
  },
  {
    "node": "El Rovellar",
    "label": "El Rovellar",
    "location": "Tarragona"
  },
  {
    "node": "El Rovellar",
    "label": "El Rovellar",
    "location": "Spain"
  },
  {
    "node": "El Rovellar",
    "label": "El Rovellar",
    "location": "La Palma d'Ebre"
  },
  {
    "node": "Els Guascos",
    "label": "Els Guascos",
    "location": "Spain"
  },
  {
    "node": "Els Guascos",
    "label": "Els Guascos",
    "location": "Lleida"
  },
  {
    "node": "Els Guascos",
    "label": "Els Guascos",
    "location": "Tarrés"
  },
  {
    "node": "Els Omells De Na Gaia",
    "label": "Els Omells De Na Gaia",
    "location": "Spain"
  },
  {
    "node": "Els Omells De Na Gaia",
    "label": "Els Omells De Na Gaia",
    "location": "Els Omells de na Gaia"
  },
  {
    "node": "Els Prats. Fossa Del Punt De Socors De Cabra Del Camp",
    "label": "Els Prats. Fossa Del Punt De Socors De Cabra Del Camp",
    "location": "Cabra del Camp"
  },
  {
    "node": "Els Verats",
    "label": "Els Verats",
    "location": "Tarragona"
  },
  {
    "node": "Els Verats",
    "label": "Els Verats",
    "location": "Spain"
  },
  {
    "node": "Els Verats",
    "label": "Els Verats",
    "location": "La Palma d'Ebre"
  },
  {
    "node": "Era Del Castell",
    "label": "Era Del Castell",
    "location": "Spain"
  },
  {
    "node": "Era Del Castell",
    "label": "Era Del Castell",
    "location": "Lleida"
  },
  {
    "node": "Era Del Castell",
    "label": "Era Del Castell",
    "location": "El Cogul"
  },
  {
    "node": "Eretes Noves - Boscos",
    "label": "Eretes Noves - Boscos",
    "location": "Spain"
  },
  {
    "node": "Eretes Noves - Boscos",
    "label": "Eretes Noves - Boscos",
    "location": "La Torre de l'Espanyol"
  },
  {
    "node": "Ermita De La Consolació",
    "label": "Ermita De La Consolació",
    "location": "Spain"
  },
  {
    "node": "Ermita De La Consolació",
    "label": "Ermita De La Consolació",
    "location": "Torroja del Priorat"
  },
  {
    "node": "Es Colomines: Tredos",
    "label": "Es Colomines: Tredos",
    "location": "Spain"
  },
  {
    "node": "Es Colomines: Tredos",
    "label": "Es Colomines: Tredos",
    "location": "Naut Aran"
  },
  {
    "node": "Església De La Granja Sant Vicenç Ferrer",
    "label": "Església De La Granja Sant Vicenç Ferrer",
    "location": "Spain"
  },
  {
    "node": "Església De La Granja Sant Vicenç Ferrer",
    "label": "Església De La Granja Sant Vicenç Ferrer",
    "location": "Penelles"
  },
  {
    "node": "Espai De La Tabacalera",
    "label": "Espai De La Tabacalera",
    "location": "Tarragona"
  },
  {
    "node": "Espai De La Tabacalera",
    "label": "Espai De La Tabacalera",
    "location": "Catalunya"
  },
  {
    "node": "Espai De La Tabacalera",
    "label": "Espai De La Tabacalera",
    "location": "Spain"
  },
  {
    "node": "Espai De La Tabacalera",
    "label": "Espai De La Tabacalera",
    "location": "Tarragonès"
  },
  {
    "node": "Estació De Flix",
    "label": "Estació De Flix",
    "location": "Tarragona"
  },
  {
    "node": "Estació De Flix",
    "label": "Estació De Flix",
    "location": "Catalunya"
  },
  {
    "node": "Estació De Flix",
    "label": "Estació De Flix",
    "location": "Spain"
  },
  {
    "node": "Estació De Flix",
    "label": "Estació De Flix",
    "location": "Ribera d'Ebre"
  },
  {
    "node": "Estació De Flix",
    "label": "Estació De Flix",
    "location": "Flix"
  },
  {
    "node": "Exterior Cementiri Gandesa",
    "label": "Exterior Cementiri Gandesa",
    "location": "Tarragona"
  },
  {
    "node": "Exterior Cementiri Gandesa",
    "label": "Exterior Cementiri Gandesa",
    "location": "Spain"
  },
  {
    "node": "Exterior Cementiri Gandesa",
    "label": "Exterior Cementiri Gandesa",
    "location": "Gandesa"
  },
  {
    "node": "Exterior Del Cementiri De Balaguer. Fossa De Soldats Marroquins",
    "label": "Exterior Del Cementiri De Balaguer. Fossa De Soldats Marroquins",
    "location": "Spain"
  },
  {
    "node": "Exterior Del Cementiri De Balaguer. Fossa De Soldats Marroquins",
    "label": "Exterior Del Cementiri De Balaguer. Fossa De Soldats Marroquins",
    "location": "Lleida"
  },
  {
    "node": "Exterior Del Cementiri De Balaguer. Fossa De Soldats Marroquins",
    "label": "Exterior Del Cementiri De Balaguer. Fossa De Soldats Marroquins",
    "location": "Balaguer"
  },
  {
    "node": "Extramurs Del Cementiri De Gratallops",
    "label": "Extramurs Del Cementiri De Gratallops",
    "location": "Spain"
  },
  {
    "node": "Extramurs Del Cementiri De Gratallops",
    "label": "Extramurs Del Cementiri De Gratallops",
    "location": "Gratallops"
  },
  {
    "node": "Fondo del Bosc Glaçat",
    "label": "Fondo del Bosc Glaçat",
    "location": "Spain"
  },
  {
    "node": "Fondo del Bosc Glaçat",
    "label": "Fondo del Bosc Glaçat",
    "location": "Barcelona"
  },
  {
    "node": "Fondo del Bosc Glaçat",
    "label": "Fondo del Bosc Glaçat",
    "location": "Olesa de Bonesvalls"
  },
  {
    "node": "Font Del Fortet",
    "label": "Font Del Fortet",
    "location": "Spain"
  },
  {
    "node": "Font Del Fortet",
    "label": "Font Del Fortet",
    "location": "Capafonts"
  },
  {
    "node": "Fora Del Cementiri D'Ars",
    "label": "Fora Del Cementiri D'Ars",
    "location": "Spain"
  },
  {
    "node": "Fora Del Cementiri D'Ars",
    "label": "Fora Del Cementiri D'Ars",
    "location": "Lleida"
  },
  {
    "node": "Fora Del Cementiri D'Ars",
    "label": "Fora Del Cementiri D'Ars",
    "location": "Les Valls de Valira"
  },
  {
    "node": "Forn De Calç Del Camp Del Muntaner",
    "label": "Forn De Calç Del Camp Del Muntaner",
    "location": "Spain"
  },
  {
    "node": "Forn De Calç Del Camp Del Muntaner",
    "label": "Forn De Calç Del Camp Del Muntaner",
    "location": "Barcelona"
  },
  {
    "node": "Forn De Calç Del Camp Del Muntaner",
    "label": "Forn De Calç Del Camp Del Muntaner",
    "location": "Olesa de Bonesvalls"
  },
  {
    "node": "Fosa de Prades",
    "label": "Fosa de Prades",
    "location": "Spain"
  },
  {
    "node": "Fossa Comuna Amb Cossos De Soldats Recollits Al Terme. Cementiri De La Granadella",
    "label": "Fossa Comuna Amb Cossos De Soldats Recollits Al Terme. Cementiri De La Granadella",
    "location": "Spain"
  },
  {
    "node": "Fossa Comuna Amb Cossos De Soldats Recollits Al Terme. Cementiri De La Granadella",
    "label": "Fossa Comuna Amb Cossos De Soldats Recollits Al Terme. Cementiri De La Granadella",
    "location": "Lleida"
  },
  {
    "node": "Fossa Comuna Amb Cossos De Soldats Recollits Al Terme. Cementiri De La Granadella",
    "label": "Fossa Comuna Amb Cossos De Soldats Recollits Al Terme. Cementiri De La Granadella",
    "location": "La Granadella"
  },
  {
    "node": "Fossa D'altadill I",
    "label": "Fossa D'altadill I",
    "location": "Spain"
  },
  {
    "node": "Fossa D'altadill I",
    "label": "Fossa D'altadill I",
    "location": "Lleida"
  },
  {
    "node": "Fossa D'altadill I",
    "label": "Fossa D'altadill I",
    "location": "Sant Guim de Freixenet"
  },
  {
    "node": "Fossa D'altadill Ii",
    "label": "Fossa D'altadill Ii",
    "location": "Spain"
  },
  {
    "node": "Fossa D'altadill Ii",
    "label": "Fossa D'altadill Ii",
    "location": "Lleida"
  },
  {
    "node": "Fossa D'altadill Ii",
    "label": "Fossa D'altadill Ii",
    "location": "Sant Guim de Freixenet"
  },
  {
    "node": "Fossa D'altadill Iii",
    "label": "Fossa D'altadill Iii",
    "location": "Spain"
  },
  {
    "node": "Fossa D'altadill Iii",
    "label": "Fossa D'altadill Iii",
    "location": "Lleida"
  },
  {
    "node": "Fossa D'altadill Iii",
    "label": "Fossa D'altadill Iii",
    "location": "Sant Guim de Freixenet"
  },
  {
    "node": "Fossa De Civils Del Cementiri De Llorenç Del Penedès",
    "label": "Fossa De Civils Del Cementiri De Llorenç Del Penedès",
    "location": "Tarragona"
  },
  {
    "node": "Fossa De Civils Del Cementiri De Llorenç Del Penedès",
    "label": "Fossa De Civils Del Cementiri De Llorenç Del Penedès",
    "location": "Spain"
  },
  {
    "node": "Fossa De Civils Del Cementiri De Llorenç Del Penedès",
    "label": "Fossa De Civils Del Cementiri De Llorenç Del Penedès",
    "location": "Llorenç del Penedès"
  },
  {
    "node": "Fossa Del Cementiri Vell De Mont-roig",
    "label": "Fossa Del Cementiri Vell De Mont-roig",
    "location": "Spain"
  },
  {
    "node": "Fossa Del Cementiri Vell De Mont-roig",
    "label": "Fossa Del Cementiri Vell De Mont-roig",
    "location": "Lleida"
  },
  {
    "node": "Fossa Del Cementiri Vell De Mont-roig",
    "label": "Fossa Del Cementiri Vell De Mont-roig",
    "location": "Els Plans de Sió"
  },
  {
    "node": "Fossa Dels Brigadistes",
    "label": "Fossa Dels Brigadistes",
    "location": "Spain"
  },
  {
    "node": "Fossa Dels Brigadistes",
    "label": "Fossa Dels Brigadistes",
    "location": "Lleida"
  },
  {
    "node": "Fossa Dels Brigadistes",
    "label": "Fossa Dels Brigadistes",
    "location": "Bellaguarda"
  },
  {
    "node": "Fossa Dels Italians Del Cementiri De L'albi",
    "label": "Fossa Dels Italians Del Cementiri De L'albi",
    "location": "Spain"
  },
  {
    "node": "Fossa Dels Italians Del Cementiri De L'albi",
    "label": "Fossa Dels Italians Del Cementiri De L'albi",
    "location": "Lleida"
  },
  {
    "node": "Fossa Dels Italians Del Cementiri De L'albi",
    "label": "Fossa Dels Italians Del Cementiri De L'albi",
    "location": "L'Albi"
  },
  {
    "node": "Fossa Dels Rebels Italians. Cementiri Dels Caputxins De Mataró",
    "label": "Fossa Dels Rebels Italians. Cementiri Dels Caputxins De Mataró",
    "location": "Spain"
  },
  {
    "node": "Fossa Dels Rebels Italians. Cementiri Dels Caputxins De Mataró",
    "label": "Fossa Dels Rebels Italians. Cementiri Dels Caputxins De Mataró",
    "location": "Barcelona"
  },
  {
    "node": "Fossa Dels Rebels Italians. Cementiri Dels Caputxins De Mataró",
    "label": "Fossa Dels Rebels Italians. Cementiri Dels Caputxins De Mataró",
    "location": "Mataró"
  },
  {
    "node": "Fossa Militar Del Cementiri De Balaguer",
    "label": "Fossa Militar Del Cementiri De Balaguer",
    "location": "Spain"
  },
  {
    "node": "Fossa Militar Del Cementiri De Balaguer",
    "label": "Fossa Militar Del Cementiri De Balaguer",
    "location": "Balaguer"
  },
  {
    "node": "Fossa de Mas Suau",
    "label": "Fossa de Mas Suau",
    "location": "Les Oluges"
  },
  {
    "node": "Fossa de l'era de Cal Casat (Ferran)",
    "label": "Fossa de l'era de Cal Casat (Ferran)",
    "location": "Estaràs"
  },
  {
    "node": "Fossa de l'era de la Maria Antònia (Ferran)",
    "label": "Fossa de l'era de la Maria Antònia (Ferran)",
    "location": "Estaràs"
  },
  {
    "node": "Fossa de l'ermita de la Mare de Déu de Santes Masses",
    "label": "Fossa de l'ermita de la Mare de Déu de Santes Masses",
    "location": "Torrefeta"
  },
  {
    "node": "Fossa de la Costa de l'Aguda",
    "label": "Fossa de la Costa de l'Aguda",
    "location": "Torà"
  },
  {
    "node": "Fossa del Mas de Can Ranxet (Portell)",
    "label": "Fossa del Mas de Can Ranxet (Portell)",
    "location": "Sant Ramon"
  },
  {
    "node": "Fossa del cementiri de Vilabella",
    "label": "Fossa del cementiri de Vilabella",
    "location": "Tarragona"
  },
  {
    "node": "Fossa del cementiri de Vilabella",
    "label": "Fossa del cementiri de Vilabella",
    "location": "Vilabella"
  },
  {
    "node": "Fossa dels germans Inglés Andreu. Cementiri de Tarrés",
    "label": "Fossa dels germans Inglés Andreu. Cementiri de Tarrés",
    "location": "Spain"
  },
  {
    "node": "Fossa dels germans Inglés Andreu. Cementiri de Tarrés",
    "label": "Fossa dels germans Inglés Andreu. Cementiri de Tarrés",
    "location": "Lleida"
  },
  {
    "node": "Fossa dels germans Inglés Andreu. Cementiri de Tarrés",
    "label": "Fossa dels germans Inglés Andreu. Cementiri de Tarrés",
    "location": "Tarrés"
  },
  {
    "node": "Fosses 4 I 5 Del Cementiri De Terrassa",
    "label": "Fosses 4 I 5 Del Cementiri De Terrassa",
    "location": "Spain"
  },
  {
    "node": "Fosses 4 I 5 Del Cementiri De Terrassa",
    "label": "Fosses 4 I 5 Del Cementiri De Terrassa",
    "location": "Barcelona"
  },
  {
    "node": "Fosses 4 I 5 Del Cementiri De Terrassa",
    "label": "Fosses 4 I 5 Del Cementiri De Terrassa",
    "location": "Terrassa"
  },
  {
    "node": "Fosses De Maquis Al Cementiri De Camprodon",
    "label": "Fosses De Maquis Al Cementiri De Camprodon",
    "location": "Spain"
  },
  {
    "node": "Fosses De Maquis Al Cementiri De Camprodon",
    "label": "Fosses De Maquis Al Cementiri De Camprodon",
    "location": "Girona"
  },
  {
    "node": "Fosses De Maquis Al Cementiri De Camprodon",
    "label": "Fosses De Maquis Al Cementiri De Camprodon",
    "location": "Camprodon"
  },
  {
    "node": "Fosses del Riu de l'Oró",
    "label": "Fosses del Riu de l'Oró",
    "location": "Spain"
  },
  {
    "node": "Fosses del Riu de l'Oró",
    "label": "Fosses del Riu de l'Oró",
    "location": "Lleida"
  },
  {
    "node": "Fosses del Riu de l'Oró",
    "label": "Fosses del Riu de l'Oró",
    "location": "Cervià de les Garrigues"
  },
  {
    "node": "Fuses: Sant Marti De Canals",
    "label": "Fuses: Sant Marti De Canals",
    "location": "Spain"
  },
  {
    "node": "Fuses: Sant Marti De Canals",
    "label": "Fuses: Sant Marti De Canals",
    "location": "Lleida"
  },
  {
    "node": "Fuses: Sant Marti De Canals",
    "label": "Fuses: Sant Marti De Canals",
    "location": "Conca de Dalt"
  },
  {
    "node": "Galobardes",
    "label": "Galobardes",
    "location": "Spain"
  },
  {
    "node": "Galobardes",
    "label": "Galobardes",
    "location": "Barcelona"
  },
  {
    "node": "Galobardes",
    "label": "Galobardes",
    "location": "Prats De Lluçanès"
  },
  {
    "node": "Garriga Del Maleneta - Racó Del Boteret",
    "label": "Garriga Del Maleneta - Racó Del Boteret",
    "location": "Tarragona"
  },
  {
    "node": "Garriga Del Maleneta - Racó Del Boteret",
    "label": "Garriga Del Maleneta - Racó Del Boteret",
    "location": "Ulldemolins"
  },
  {
    "node": "Ginestrets - Cota 356",
    "label": "Ginestrets - Cota 356",
    "location": "Tarragona"
  },
  {
    "node": "Ginestrets - Cota 356",
    "label": "Ginestrets - Cota 356",
    "location": "Spain"
  },
  {
    "node": "Ginestrets - Cota 356",
    "label": "Ginestrets - Cota 356",
    "location": "Corbera d'Ebre"
  },
  {
    "node": "Guixera La Reductora",
    "label": "Guixera La Reductora",
    "location": "Spain"
  },
  {
    "node": "Guixera La Reductora",
    "label": "Guixera La Reductora",
    "location": "Òdena"
  },
  {
    "node": "Hospital De Sang De Casa Torriella",
    "label": "Hospital De Sang De Casa Torriella",
    "location": "Spain"
  },
  {
    "node": "Hospital De Sang De Casa Torriella",
    "label": "Hospital De Sang De Casa Torriella",
    "location": "Lleida"
  },
  {
    "node": "Hospital De Sang De Casa Torriella",
    "label": "Hospital De Sang De Casa Torriella",
    "location": "Montanissell"
  },
  {
    "node": "Inhumacions a l'interior i a l'exterior del cementiri de Rodonyà",
    "label": "Inhumacions a l'interior i a l'exterior del cementiri de Rodonyà",
    "location": "Tarragona"
  },
  {
    "node": "Inhumacions a l'interior i a l'exterior del cementiri de Rodonyà",
    "label": "Inhumacions a l'interior i a l'exterior del cementiri de Rodonyà",
    "location": "Rodonyà"
  },
  {
    "node": "Inhumació Al Camí Ral A Llavaneres",
    "label": "Inhumació Al Camí Ral A Llavaneres",
    "location": "Spain"
  },
  {
    "node": "Inhumació Al Camí Ral A Llavaneres",
    "label": "Inhumació Al Camí Ral A Llavaneres",
    "location": "Sant Andreu de Llavaneres"
  },
  {
    "node": "L'escrita",
    "label": "L'escrita",
    "location": "Spain"
  },
  {
    "node": "L'escrita",
    "label": "L'escrita",
    "location": "Lleida"
  },
  {
    "node": "L'escrita",
    "label": "L'escrita",
    "location": "La Guingueta d'Àneu"
  },
  {
    "node": "La Boverola Pei",
    "label": "La Boverola Pei",
    "location": "Spain"
  },
  {
    "node": "La Boverola Pei",
    "label": "La Boverola Pei",
    "location": "Lleida"
  },
  {
    "node": "La Boverola Pei",
    "label": "La Boverola Pei",
    "location": "La Granadella"
  },
  {
    "node": "La Cadolla",
    "label": "La Cadolla",
    "location": "Spain"
  },
  {
    "node": "La Cadolla",
    "label": "La Cadolla",
    "location": "Almatret"
  },
  {
    "node": "La Carrerada",
    "label": "La Carrerada",
    "location": "Sant Romà d'Abella"
  },
  {
    "node": "La Casella De Can Soteras",
    "label": "La Casella De Can Soteras",
    "location": "Spain"
  },
  {
    "node": "La Casella De Can Soteras",
    "label": "La Casella De Can Soteras",
    "location": "Castellolí"
  },
  {
    "node": "La Cogulla. Cota 1062",
    "label": "La Cogulla. Cota 1062",
    "location": "Tarragona"
  },
  {
    "node": "La Cogulla. Cota 1062",
    "label": "La Cogulla. Cota 1062",
    "location": "Spain"
  },
  {
    "node": "La Cogulla. Cota 1062",
    "label": "La Cogulla. Cota 1062",
    "location": "La Morera de Montsant"
  },
  {
    "node": "La Figuera",
    "label": "La Figuera",
    "location": "Tarragona"
  },
  {
    "node": "La Figuera",
    "label": "La Figuera",
    "location": "Catalunya"
  },
  {
    "node": "La Figuera",
    "label": "La Figuera",
    "location": "Spain"
  },
  {
    "node": "La Figuera",
    "label": "La Figuera",
    "location": "Priorat"
  },
  {
    "node": "La Figuera",
    "label": "La Figuera",
    "location": "La Figuera"
  },
  {
    "node": "La Griera",
    "label": "La Griera",
    "location": "Spain"
  },
  {
    "node": "La Griera",
    "label": "La Griera",
    "location": "Gurb"
  },
  {
    "node": "La Plana del Mas Soler",
    "label": "La Plana del Mas Soler",
    "location": "Tarragona"
  },
  {
    "node": "La Plana del Mas Soler",
    "label": "La Plana del Mas Soler",
    "location": "Spain"
  },
  {
    "node": "La Plana del Mas Soler",
    "label": "La Plana del Mas Soler",
    "location": "Tivissa"
  },
  {
    "node": "La Saira",
    "label": "La Saira",
    "location": "Spain"
  },
  {
    "node": "La Saira",
    "label": "La Saira",
    "location": "Lleida"
  },
  {
    "node": "La Saira",
    "label": "La Saira",
    "location": "Almacelles"
  },
  {
    "node": "La Serra | Camí de la Masia",
    "label": "La Serra | Camí de la Masia",
    "location": "Spain"
  },
  {
    "node": "La Serra | Camí de la Masia",
    "label": "La Serra | Camí de la Masia",
    "location": "Lleida"
  },
  {
    "node": "La Serra | Camí de la Masia",
    "label": "La Serra | Camí de la Masia",
    "location": "Baldomar"
  },
  {
    "node": "La Serreta",
    "label": "La Serreta",
    "location": "Lleida"
  },
  {
    "node": "La Serreta",
    "label": "La Serreta",
    "location": "La Baronia de Rialb"
  },
  {
    "node": "La Sort Del Quimet De Prats",
    "label": "La Sort Del Quimet De Prats",
    "location": "Spain"
  },
  {
    "node": "La Sort Del Quimet De Prats",
    "label": "La Sort Del Quimet De Prats",
    "location": "Lleida"
  },
  {
    "node": "La Sort Del Quimet De Prats",
    "label": "La Sort Del Quimet De Prats",
    "location": "La Granadella"
  },
  {
    "node": "La Teulera",
    "label": "La Teulera",
    "location": "Spain"
  },
  {
    "node": "La Teulera",
    "label": "La Teulera",
    "location": "Lleida"
  },
  {
    "node": "La Teulera",
    "label": "La Teulera",
    "location": "Vilanova De Meià"
  },
  {
    "node": "La Venta (l'Hostal de la Serra)",
    "label": "La Venta (l'Hostal de la Serra)",
    "location": "Margalef"
  },
  {
    "node": "La Voltera. La Febró",
    "label": "La Voltera. La Febró",
    "location": "Spain"
  },
  {
    "node": "La Voltera. La Febró",
    "label": "La Voltera. La Febró",
    "location": "La Febró - Prades"
  },
  {
    "node": "La serra Fosca",
    "label": "La serra Fosca",
    "location": "Spain"
  },
  {
    "node": "La serra Fosca",
    "label": "La serra Fosca",
    "location": "Lleida"
  },
  {
    "node": "La serra Fosca",
    "label": "La serra Fosca",
    "location": "L'Albagés"
  },
  {
    "node": "Les Basses",
    "label": "Les Basses",
    "location": "Spain"
  },
  {
    "node": "Les Basses",
    "label": "Les Basses",
    "location": "Vinaixa"
  },
  {
    "node": "Les Cadolles - Les Comitjanes",
    "label": "Les Cadolles - Les Comitjanes",
    "location": "Spain"
  },
  {
    "node": "Les Cadolles - Les Comitjanes",
    "label": "Les Cadolles - Les Comitjanes",
    "location": "La Palma d'Ebre"
  },
  {
    "node": "Les Collades: Bosc De Tres Comuns",
    "label": "Les Collades: Bosc De Tres Comuns",
    "location": "Spain"
  },
  {
    "node": "Les Collades: Bosc De Tres Comuns",
    "label": "Les Collades: Bosc De Tres Comuns",
    "location": "Lleida"
  },
  {
    "node": "Les Collades: Bosc De Tres Comuns",
    "label": "Les Collades: Bosc De Tres Comuns",
    "location": "Rialp"
  },
  {
    "node": "Les Deveses De Prades. Soldats Republicans",
    "label": "Les Deveses De Prades. Soldats Republicans",
    "location": "Spain"
  },
  {
    "node": "Les Deveses De Prades. Soldats Republicans",
    "label": "Les Deveses De Prades. Soldats Republicans",
    "location": "Prades"
  },
  {
    "node": "Les Guixeres De Sort",
    "label": "Les Guixeres De Sort",
    "location": "Spain"
  },
  {
    "node": "Les Guixeres De Sort",
    "label": "Les Guixeres De Sort",
    "location": "Sort"
  },
  {
    "node": "Les Planes - Vall De Jacob",
    "label": "Les Planes - Vall De Jacob",
    "location": "Tarragona"
  },
  {
    "node": "Les Planes - Vall De Jacob",
    "label": "Les Planes - Vall De Jacob",
    "location": "Catalunya"
  },
  {
    "node": "Les Planes - Vall De Jacob",
    "label": "Les Planes - Vall De Jacob",
    "location": "Spain"
  },
  {
    "node": "Les Planes - Vall De Jacob",
    "label": "Les Planes - Vall De Jacob",
    "location": "Ribera d'Ebre"
  },
  {
    "node": "Les Planes - Vall De Jacob",
    "label": "Les Planes - Vall De Jacob",
    "location": "Ascó"
  },
  {
    "node": "Les Pobles, Mont-Roig Del Camp",
    "label": "Les Pobles, Mont-Roig Del Camp",
    "location": "Tarragona"
  },
  {
    "node": "Les Pobles, Mont-Roig Del Camp",
    "label": "Les Pobles, Mont-Roig Del Camp",
    "location": "Spain"
  },
  {
    "node": "Les Pobles, Mont-Roig Del Camp",
    "label": "Les Pobles, Mont-Roig Del Camp",
    "location": "Mont-roig del Camp"
  },
  {
    "node": "Les Solanes",
    "label": "Les Solanes",
    "location": "Spain"
  },
  {
    "node": "Les Solanes",
    "label": "Les Solanes",
    "location": "Móra d'Ebre"
  },
  {
    "node": "Les Trufes",
    "label": "Les Trufes",
    "location": "Spain"
  },
  {
    "node": "Les Trufes",
    "label": "Les Trufes",
    "location": "Batea"
  },
  {
    "node": "Lo Coll",
    "label": "Lo Coll",
    "location": "Spain"
  },
  {
    "node": "Lo Coll",
    "label": "Lo Coll",
    "location": "Lleida"
  },
  {
    "node": "Lo Coll",
    "label": "Lo Coll",
    "location": "La Granadella"
  },
  {
    "node": "Lo Forat De La Gandaia",
    "label": "Lo Forat De La Gandaia",
    "location": "Tarragona"
  },
  {
    "node": "Lo Forat De La Gandaia",
    "label": "Lo Forat De La Gandaia",
    "location": "Catalunya"
  },
  {
    "node": "Lo Forat De La Gandaia",
    "label": "Lo Forat De La Gandaia",
    "location": "Spain"
  },
  {
    "node": "Lo Forat De La Gandaia",
    "label": "Lo Forat De La Gandaia",
    "location": "Priorat"
  },
  {
    "node": "Lo Forat De La Gandaia",
    "label": "Lo Forat De La Gandaia",
    "location": "La Morera de Montsant"
  },
  {
    "node": "Lo Molló",
    "label": "Lo Molló",
    "location": "Tarragona"
  },
  {
    "node": "Lo Molló",
    "label": "Lo Molló",
    "location": "Catalunya"
  },
  {
    "node": "Lo Molló",
    "label": "Lo Molló",
    "location": "Spain"
  },
  {
    "node": "Lo Molló",
    "label": "Lo Molló",
    "location": "Terra Alta"
  },
  {
    "node": "Lo Molló",
    "label": "Lo Molló",
    "location": "La Pobla de Massaluca"
  },
  {
    "node": "Lo Solanell: Hortoneda",
    "label": "Lo Solanell: Hortoneda",
    "location": "Spain"
  },
  {
    "node": "Lo Solanell: Hortoneda",
    "label": "Lo Solanell: Hortoneda",
    "location": "Lleida"
  },
  {
    "node": "Lo Solanell: Hortoneda",
    "label": "Lo Solanell: Hortoneda",
    "location": "Conca de Dalt"
  },
  {
    "node": "Los Caus",
    "label": "Los Caus",
    "location": "Spain"
  },
  {
    "node": "Los Caus",
    "label": "Los Caus",
    "location": "Lleida"
  },
  {
    "node": "Los Caus",
    "label": "Los Caus",
    "location": "El Cogul"
  },
  {
    "node": "Los Esplans del Corona",
    "label": "Los Esplans del Corona",
    "location": "Spain"
  },
  {
    "node": "Los Esplans del Corona",
    "label": "Los Esplans del Corona",
    "location": "Lleida"
  },
  {
    "node": "Los Esplans del Corona",
    "label": "Los Esplans del Corona",
    "location": "El Soleràs"
  },
  {
    "node": "Los Raïmats",
    "label": "Los Raïmats",
    "location": "Tarragona"
  },
  {
    "node": "Los Raïmats",
    "label": "Los Raïmats",
    "location": "Spain"
  },
  {
    "node": "Los Raïmats",
    "label": "Los Raïmats",
    "location": "La Fatarella"
  },
  {
    "node": "Mallolis",
    "label": "Mallolis",
    "location": "Spain"
  },
  {
    "node": "Mallolis",
    "label": "Mallolis",
    "location": "Lleida"
  },
  {
    "node": "Mallolis",
    "label": "Mallolis",
    "location": "Farrera"
  },
  {
    "node": "Maqui Al Cementiri De L'església Dels Constantins",
    "label": "Maqui Al Cementiri De L'església Dels Constantins",
    "location": "Spain"
  },
  {
    "node": "Maqui Al Cementiri De L'església Dels Constantins",
    "label": "Maqui Al Cementiri De L'església Dels Constantins",
    "location": "Girona"
  },
  {
    "node": "Maqui Al Cementiri De L'església Dels Constantins",
    "label": "Maqui Al Cementiri De L'església Dels Constantins",
    "location": "Constantins"
  },
  {
    "node": "Maquis Al Cementiri De L'església De Castanyet",
    "label": "Maquis Al Cementiri De L'església De Castanyet",
    "location": "Girona"
  },
  {
    "node": "Maquis Al Cementiri De L'església De Castanyet",
    "label": "Maquis Al Cementiri De L'església De Castanyet",
    "location": "Castanyet"
  },
  {
    "node": "Mare de Déu de les Ares",
    "label": "Mare de Déu de les Ares",
    "location": "Spain"
  },
  {
    "node": "Mare de Déu de les Ares",
    "label": "Mare de Déu de les Ares",
    "location": "Alt Àneu"
  },
  {
    "node": "Mas D'en Rafel",
    "label": "Mas D'en Rafel",
    "location": null
  },
  {
    "node": "Mas De Barbaretes",
    "label": "Mas De Barbaretes",
    "location": "Tarragona"
  },
  {
    "node": "Mas De Barbaretes",
    "label": "Mas De Barbaretes",
    "location": "Spain"
  },
  {
    "node": "Mas De Barbaretes",
    "label": "Mas De Barbaretes",
    "location": "La Fatarella"
  },
  {
    "node": "Mas De L'alfredo",
    "label": "Mas De L'alfredo",
    "location": "Spain"
  },
  {
    "node": "Mas De L'alfredo",
    "label": "Mas De L'alfredo",
    "location": "Lleida"
  },
  {
    "node": "Mas De L'alfredo",
    "label": "Mas De L'alfredo",
    "location": "L'Albagés"
  },
  {
    "node": "Mas De La Bernarda",
    "label": "Mas De La Bernarda",
    "location": "Spain"
  },
  {
    "node": "Mas De La Bernarda",
    "label": "Mas De La Bernarda",
    "location": "Llardecans"
  },
  {
    "node": "Mas De La Pila",
    "label": "Mas De La Pila",
    "location": "Tarragona"
  },
  {
    "node": "Mas De La Pila",
    "label": "Mas De La Pila",
    "location": "Spain"
  },
  {
    "node": "Mas De La Pila",
    "label": "Mas De La Pila",
    "location": "Corbera d'Ebre"
  },
  {
    "node": "Mas De Les Aluges. Partida De Sant Miquel",
    "label": "Mas De Les Aluges. Partida De Sant Miquel",
    "location": "Spain"
  },
  {
    "node": "Mas De Les Aluges. Partida De Sant Miquel",
    "label": "Mas De Les Aluges. Partida De Sant Miquel",
    "location": "Vespella de Gaià"
  },
  {
    "node": "Mas De Prades",
    "label": "Mas De Prades",
    "location": "Ascó"
  },
  {
    "node": "Mas Del Geser",
    "label": "Mas Del Geser",
    "location": "Tarragona"
  },
  {
    "node": "Mas Del Geser",
    "label": "Mas Del Geser",
    "location": "Spain"
  },
  {
    "node": "Mas Del Geser",
    "label": "Mas Del Geser",
    "location": "Corbera d'Ebre"
  },
  {
    "node": "Mas Del Puig",
    "label": "Mas Del Puig",
    "location": "Torelló"
  },
  {
    "node": "Mas Dels Mitgers",
    "label": "Mas Dels Mitgers",
    "location": "Spain"
  },
  {
    "node": "Mas Dels Mitgers",
    "label": "Mas Dels Mitgers",
    "location": "Lleida"
  },
  {
    "node": "Mas Dels Mitgers",
    "label": "Mas Dels Mitgers",
    "location": "La Granadella"
  },
  {
    "node": "Mas D’en Blai",
    "label": "Mas D’en Blai",
    "location": "Vilalba dels Arcs"
  },
  {
    "node": "Mas Torrenova - Parc Eòlic Bon Vent",
    "label": "Mas Torrenova - Parc Eòlic Bon Vent",
    "location": "Tarragona"
  },
  {
    "node": "Mas Torrenova - Parc Eòlic Bon Vent",
    "label": "Mas Torrenova - Parc Eòlic Bon Vent",
    "location": "Spain"
  },
  {
    "node": "Mas Torrenova - Parc Eòlic Bon Vent",
    "label": "Mas Torrenova - Parc Eòlic Bon Vent",
    "location": "Corbera d'Ebre"
  },
  {
    "node": "Mas de Puigvistós de Prats de Lluçanès",
    "label": "Mas de Puigvistós de Prats de Lluçanès",
    "location": "Barcelona"
  },
  {
    "node": "Mas de Puigvistós de Prats de Lluçanès",
    "label": "Mas de Puigvistós de Prats de Lluçanès",
    "location": "Prats De Lluçanès"
  },
  {
    "node": "Mas del Primo",
    "label": "Mas del Primo",
    "location": "Tarragona"
  },
  {
    "node": "Mas del Primo",
    "label": "Mas del Primo",
    "location": "Spain"
  },
  {
    "node": "Mas del Primo",
    "label": "Mas del Primo",
    "location": "Caseres"
  },
  {
    "node": "Mas del Sant",
    "label": "Mas del Sant",
    "location": "Spain"
  },
  {
    "node": "Mas del Sant",
    "label": "Mas del Sant",
    "location": "Benissanet"
  },
  {
    "node": "Mas d’en Blanc",
    "label": "Mas d’en Blanc",
    "location": "Tarragona"
  },
  {
    "node": "Mas d’en Blanc",
    "label": "Mas d’en Blanc",
    "location": "Spain"
  },
  {
    "node": "Mas d’en Blanc",
    "label": "Mas d’en Blanc",
    "location": "Vespella de Gaià"
  },
  {
    "node": "Mas d’en Grau - Comes d'en Bonet",
    "label": "Mas d’en Grau - Comes d'en Bonet",
    "location": "Tarragona"
  },
  {
    "node": "Mas d’en Grau - Comes d'en Bonet",
    "label": "Mas d’en Grau - Comes d'en Bonet",
    "location": "Corbera d'Ebre"
  },
  {
    "node": "Masia Can Rovira",
    "label": "Masia Can Rovira",
    "location": "Spain"
  },
  {
    "node": "Masia Can Rovira",
    "label": "Masia Can Rovira",
    "location": "Barcelona"
  },
  {
    "node": "Masia Can Rovira",
    "label": "Masia Can Rovira",
    "location": "Gurb"
  },
  {
    "node": "Masia De Sanromà",
    "label": "Masia De Sanromà",
    "location": "Tarragona"
  },
  {
    "node": "Masia De Sanromà",
    "label": "Masia De Sanromà",
    "location": "Spain"
  },
  {
    "node": "Masia De Sanromà",
    "label": "Masia De Sanromà",
    "location": "Bellvei"
  },
  {
    "node": "Masia Subirana",
    "label": "Masia Subirana",
    "location": "Spain"
  },
  {
    "node": "Masia Subirana",
    "label": "Masia Subirana",
    "location": "Barcelona"
  },
  {
    "node": "Masia Subirana",
    "label": "Masia Subirana",
    "location": "Sant Julià de Cerdanyola"
  },
  {
    "node": "Mausoleu De Les Víctimes De La Repressió A La Rereguarda. Cementiri De Solivella",
    "label": "Mausoleu De Les Víctimes De La Repressió A La Rereguarda. Cementiri De Solivella",
    "location": "Tarragona"
  },
  {
    "node": "Mausoleu De Les Víctimes De La Repressió A La Rereguarda. Cementiri De Solivella",
    "label": "Mausoleu De Les Víctimes De La Repressió A La Rereguarda. Cementiri De Solivella",
    "location": "Solivella"
  },
  {
    "node": "Mausoleu dels montcadencs víctimes de la violència a la rereguarda. Cementiri de Montcada i Reixac",
    "label": "Mausoleu dels montcadencs víctimes de la violència a la rereguarda. Cementiri de Montcada i Reixac",
    "location": "Spain"
  },
  {
    "node": "Mausoleu dels montcadencs víctimes de la violència a la rereguarda. Cementiri de Montcada i Reixac",
    "label": "Mausoleu dels montcadencs víctimes de la violència a la rereguarda. Cementiri de Montcada i Reixac",
    "location": "Barcelona"
  },
  {
    "node": "Mausoleu dels montcadencs víctimes de la violència a la rereguarda. Cementiri de Montcada i Reixac",
    "label": "Mausoleu dels montcadencs víctimes de la violència a la rereguarda. Cementiri de Montcada i Reixac",
    "location": "Montcada i Reixac"
  },
  {
    "node": "Molina De Josepet",
    "label": "Molina De Josepet",
    "location": "Spain"
  },
  {
    "node": "Molina De Josepet",
    "label": "Molina De Josepet",
    "location": "Rialp"
  },
  {
    "node": "Muntanya De La Fembra Morta",
    "label": "Muntanya De La Fembra Morta",
    "location": "Spain"
  },
  {
    "node": "Muntanya De La Fembra Morta",
    "label": "Muntanya De La Fembra Morta",
    "location": "Castellolí"
  },
  {
    "node": "Nínxol Isidre Formentí Turet. Cementiri de Juncosa",
    "label": "Nínxol Isidre Formentí Turet. Cementiri de Juncosa",
    "location": "Juncosa"
  },
  {
    "node": "Nínxol de Magdalena Girth al cementiri de Sant Feliu de Guíxols",
    "label": "Nínxol de Magdalena Girth al cementiri de Sant Feliu de Guíxols",
    "location": "Spain"
  },
  {
    "node": "Nínxol de Magdalena Girth al cementiri de Sant Feliu de Guíxols",
    "label": "Nínxol de Magdalena Girth al cementiri de Sant Feliu de Guíxols",
    "location": "Girona"
  },
  {
    "node": "Nínxol de Magdalena Girth al cementiri de Sant Feliu de Guíxols",
    "label": "Nínxol de Magdalena Girth al cementiri de Sant Feliu de Guíxols",
    "location": "Sant Feliu de Guíxols"
  },
  {
    "node": "Nínxol de Marcos Goñi Almándoz",
    "label": "Nínxol de Marcos Goñi Almándoz",
    "location": "Spain"
  },
  {
    "node": "Nínxol de Marcos Goñi Almándoz",
    "label": "Nínxol de Marcos Goñi Almándoz",
    "location": "Barcelona"
  },
  {
    "node": "Nínxol de Marcos Goñi Almándoz",
    "label": "Nínxol de Marcos Goñi Almándoz",
    "location": "Montcada i Reixac"
  },
  {
    "node": "Nínxol del cementiri dels Arcs",
    "label": "Nínxol del cementiri dels Arcs",
    "location": "Spain"
  },
  {
    "node": "Nínxol del cementiri dels Arcs",
    "label": "Nínxol del cementiri dels Arcs",
    "location": "Lleida"
  },
  {
    "node": "Nínxol del cementiri dels Arcs",
    "label": "Nínxol del cementiri dels Arcs",
    "location": "Bellvís"
  },
  {
    "node": "Nínxols de Brigadistes Internacionals al cementiri de Sant Feliu de Guíxols",
    "label": "Nínxols de Brigadistes Internacionals al cementiri de Sant Feliu de Guíxols",
    "location": "Spain"
  },
  {
    "node": "Nínxols de Brigadistes Internacionals al cementiri de Sant Feliu de Guíxols",
    "label": "Nínxols de Brigadistes Internacionals al cementiri de Sant Feliu de Guíxols",
    "location": "Girona"
  },
  {
    "node": "Nínxols de Brigadistes Internacionals al cementiri de Sant Feliu de Guíxols",
    "label": "Nínxols de Brigadistes Internacionals al cementiri de Sant Feliu de Guíxols",
    "location": "Sant Feliu de Guíxols"
  },
  {
    "node": "Nínxols de Brigadistes del cementiri de Tàrrega",
    "label": "Nínxols de Brigadistes del cementiri de Tàrrega",
    "location": "Spain"
  },
  {
    "node": "Nínxols de Brigadistes del cementiri de Tàrrega",
    "label": "Nínxols de Brigadistes del cementiri de Tàrrega",
    "location": "Lleida"
  },
  {
    "node": "Nínxols de Brigadistes del cementiri de Tàrrega",
    "label": "Nínxols de Brigadistes del cementiri de Tàrrega",
    "location": "Tàrrega"
  },
  {
    "node": "Oliola: Al voltant de la població",
    "label": "Oliola: Al voltant de la població",
    "location": "Spain"
  },
  {
    "node": "Oliola: Al voltant de la població",
    "label": "Oliola: Al voltant de la població",
    "location": "Oliola"
  },
  {
    "node": "Panteó dels militars de la Mestrança d'Artilleria",
    "label": "Panteó dels militars de la Mestrança d'Artilleria",
    "location": "Montcada i Reixac"
  },
  {
    "node": "Partida De La Cova (Malladeta)",
    "label": "Partida De La Cova (Malladeta)",
    "location": "Tarragona"
  },
  {
    "node": "Partida De La Cova (Malladeta)",
    "label": "Partida De La Cova (Malladeta)",
    "location": "Spain"
  },
  {
    "node": "Partida De La Cova (Malladeta)",
    "label": "Partida De La Cova (Malladeta)",
    "location": "El Perelló"
  },
  {
    "node": "Partida De Les Espadelles - Balma",
    "label": "Partida De Les Espadelles - Balma",
    "location": "Spain"
  },
  {
    "node": "Partida De Les Espadelles - Balma",
    "label": "Partida De Les Espadelles - Balma",
    "location": "Margalef"
  },
  {
    "node": "Partida Del Mataret",
    "label": "Partida Del Mataret",
    "location": "Spain"
  },
  {
    "node": "Partida Del Mataret",
    "label": "Partida Del Mataret",
    "location": "L'Ampolla"
  },
  {
    "node": "Partida Del Negral De Bellvís",
    "label": "Partida Del Negral De Bellvís",
    "location": "Spain"
  },
  {
    "node": "Partida Del Negral De Bellvís",
    "label": "Partida Del Negral De Bellvís",
    "location": "Lleida"
  },
  {
    "node": "Partida Del Negral De Bellvís",
    "label": "Partida Del Negral De Bellvís",
    "location": "Bellvís"
  },
  {
    "node": "Partida La Costa",
    "label": "Partida La Costa",
    "location": "Spain"
  },
  {
    "node": "Partida La Costa",
    "label": "Partida La Costa",
    "location": "la Bisbal de Montsant"
  },
  {
    "node": "Partida Les Àligues - Joveres",
    "label": "Partida Les Àligues - Joveres",
    "location": "Spain"
  },
  {
    "node": "Partida Les Àligues - Joveres",
    "label": "Partida Les Àligues - Joveres",
    "location": "la Bisbal de Montsant"
  },
  {
    "node": "Partida Pla de Junquet - Coma",
    "label": "Partida Pla de Junquet - Coma",
    "location": "la Bisbal de Montsant"
  },
  {
    "node": "Partida de Salanques",
    "label": "Partida de Salanques",
    "location": "Tarragona"
  },
  {
    "node": "Partida de Salanques",
    "label": "Partida de Salanques",
    "location": "Spain"
  },
  {
    "node": "Partida de Salanques",
    "label": "Partida de Salanques",
    "location": "Poboleda"
  },
  {
    "node": "Partida dels Prats a Mont-roig del Camp",
    "label": "Partida dels Prats a Mont-roig del Camp",
    "location": "Tarragona"
  },
  {
    "node": "Partida dels Prats a Mont-roig del Camp",
    "label": "Partida dels Prats a Mont-roig del Camp",
    "location": "Spain"
  },
  {
    "node": "Partida dels Prats a Mont-roig del Camp",
    "label": "Partida dels Prats a Mont-roig del Camp",
    "location": "Mont-roig del Camp"
  },
  {
    "node": "Peixera d'Aspa",
    "label": "Peixera d'Aspa",
    "location": "Spain"
  },
  {
    "node": "Peixera d'Aspa",
    "label": "Peixera d'Aspa",
    "location": "Lleida"
  },
  {
    "node": "Peixera d'Aspa",
    "label": "Peixera d'Aspa",
    "location": "El Cogul"
  },
  {
    "node": "Pineda A Prop Del Camp Dels Morts",
    "label": "Pineda A Prop Del Camp Dels Morts",
    "location": "Spain"
  },
  {
    "node": "Pineda A Prop Del Camp Dels Morts",
    "label": "Pineda A Prop Del Camp Dels Morts",
    "location": "Lleida"
  },
  {
    "node": "Pineda A Prop Del Camp Dels Morts",
    "label": "Pineda A Prop Del Camp Dels Morts",
    "location": "Castellar de la Ribera"
  },
  {
    "node": "Pla Moran",
    "label": "Pla Moran",
    "location": "Pradell de la Teixeta"
  },
  {
    "node": "Pla de Bassar. Partida del mas Blanc",
    "label": "Pla de Bassar. Partida del mas Blanc",
    "location": "Tarragona"
  },
  {
    "node": "Pla de Bassar. Partida del mas Blanc",
    "label": "Pla de Bassar. Partida del mas Blanc",
    "location": "Spain"
  },
  {
    "node": "Pla de Bassar. Partida del mas Blanc",
    "label": "Pla de Bassar. Partida del mas Blanc",
    "location": "L'Albiol"
  },
  {
    "node": "Pla dels Panteons. Cementiri de Mataró",
    "label": "Pla dels Panteons. Cementiri de Mataró",
    "location": "Spain"
  },
  {
    "node": "Pla dels Panteons. Cementiri de Mataró",
    "label": "Pla dels Panteons. Cementiri de Mataró",
    "location": "Barcelona"
  },
  {
    "node": "Pla dels Panteons. Cementiri de Mataró",
    "label": "Pla dels Panteons. Cementiri de Mataró",
    "location": "Mataró"
  },
  {
    "node": "Plandiranes: Figuerola D'orcau",
    "label": "Plandiranes: Figuerola D'orcau",
    "location": "Spain"
  },
  {
    "node": "Plandiranes: Figuerola D'orcau",
    "label": "Plandiranes: Figuerola D'orcau",
    "location": "Lleida"
  },
  {
    "node": "Plandiranes: Figuerola D'orcau",
    "label": "Plandiranes: Figuerola D'orcau",
    "location": "Isona i Conca Dellà"
  },
  {
    "node": "Planell De Campirme",
    "label": "Planell De Campirme",
    "location": "Spain"
  },
  {
    "node": "Planell De Campirme",
    "label": "Planell De Campirme",
    "location": "Llavorsí"
  },
  {
    "node": "Plans De Rafel",
    "label": "Plans De Rafel",
    "location": "Spain"
  },
  {
    "node": "Plans De Rafel",
    "label": "Plans De Rafel",
    "location": "Batea"
  },
  {
    "node": "Pleta Barrada",
    "label": "Pleta Barrada",
    "location": "Spain"
  },
  {
    "node": "Pleta Barrada",
    "label": "Pleta Barrada",
    "location": "Gimenells i el Pla de la Font"
  },
  {
    "node": "Poliespotiu del Soleràs",
    "label": "Poliespotiu del Soleràs",
    "location": "Spain"
  },
  {
    "node": "Poliespotiu del Soleràs",
    "label": "Poliespotiu del Soleràs",
    "location": "Lleida"
  },
  {
    "node": "Poliespotiu del Soleràs",
    "label": "Poliespotiu del Soleràs",
    "location": "El Soleràs"
  },
  {
    "node": "Pont D'adrall",
    "label": "Pont D'adrall",
    "location": "Spain"
  },
  {
    "node": "Pont D'adrall",
    "label": "Pont D'adrall",
    "location": "Adrall"
  },
  {
    "node": "Pont De La Borda Dels Rengars",
    "label": "Pont De La Borda Dels Rengars",
    "location": "Spain"
  },
  {
    "node": "Pont De La Borda Dels Rengars",
    "label": "Pont De La Borda Dels Rengars",
    "location": "Lleida"
  },
  {
    "node": "Pont De La Borda Dels Rengars",
    "label": "Pont De La Borda Dels Rengars",
    "location": "La Guingueta d'Àneu"
  },
  {
    "node": "Pont de Guils",
    "label": "Pont de Guils",
    "location": "Lleida"
  },
  {
    "node": "Pont de Guils",
    "label": "Pont de Guils",
    "location": "Castellàs"
  },
  {
    "node": "Pont de Montellà",
    "label": "Pont de Montellà",
    "location": "Spain"
  },
  {
    "node": "Pont de Montellà",
    "label": "Pont de Montellà",
    "location": "Martinet"
  },
  {
    "node": "Pou De Pich I Aguilera",
    "label": "Pou De Pich I Aguilera",
    "location": "Tarragona"
  },
  {
    "node": "Pou De Pich I Aguilera",
    "label": "Pou De Pich I Aguilera",
    "location": "Spain"
  },
  {
    "node": "Pou De Pich I Aguilera",
    "label": "Pou De Pich I Aguilera",
    "location": "Reus"
  },
  {
    "node": "Pou Del Baró",
    "label": "Pou Del Baró",
    "location": "Tarragona"
  },
  {
    "node": "Pou Del Baró",
    "label": "Pou Del Baró",
    "location": "Catalunya"
  },
  {
    "node": "Pou Del Baró",
    "label": "Pou Del Baró",
    "location": "Spain"
  },
  {
    "node": "Pou Del Baró",
    "label": "Pou Del Baró",
    "location": "Terra Alta"
  },
  {
    "node": "Pou Del Baró",
    "label": "Pou Del Baró",
    "location": "Gandesa"
  },
  {
    "node": "Prat De Sant Clem",
    "label": "Prat De Sant Clem",
    "location": "La Torre de Capdella"
  },
  {
    "node": "Prat De Ton D'iguan / Prat De Giranto",
    "label": "Prat De Ton D'iguan / Prat De Giranto",
    "location": "Spain"
  },
  {
    "node": "Prat De Ton D'iguan / Prat De Giranto",
    "label": "Prat De Ton D'iguan / Prat De Giranto",
    "location": "Alt Àneu"
  },
  {
    "node": "Prat del Cerni",
    "label": "Prat del Cerni",
    "location": "Spain"
  },
  {
    "node": "Prat del Cerni",
    "label": "Prat del Cerni",
    "location": "Sant Romà d'Abella"
  },
  {
    "node": "Propietat D'en Josep Roy. Traslladada Al Valle De Los Caídos.",
    "label": "Propietat D'en Josep Roy. Traslladada Al Valle De Los Caídos.",
    "location": "Rialp"
  },
  {
    "node": "Punta de la Sinyora",
    "label": "Punta de la Sinyora",
    "location": "Juncosa"
  },
  {
    "node": "Punta del Sacarrenyo",
    "label": "Punta del Sacarrenyo",
    "location": "Spain"
  },
  {
    "node": "Punta del Sacarrenyo",
    "label": "Punta del Sacarrenyo",
    "location": "Lleida"
  },
  {
    "node": "Punta del Sacarrenyo",
    "label": "Punta del Sacarrenyo",
    "location": "El Cogul"
  },
  {
    "node": "Punta dels Sabaters",
    "label": "Punta dels Sabaters",
    "location": "Spain"
  },
  {
    "node": "Punta dels Sabaters",
    "label": "Punta dels Sabaters",
    "location": "Lleida"
  },
  {
    "node": "Punta dels Sabaters",
    "label": "Punta dels Sabaters",
    "location": "La Granadella"
  },
  {
    "node": "Pàndols - Ermita De Santa Magdalena",
    "label": "Pàndols - Ermita De Santa Magdalena",
    "location": "Tarragona"
  },
  {
    "node": "Pàndols - Ermita De Santa Magdalena",
    "label": "Pàndols - Ermita De Santa Magdalena",
    "location": "Spain"
  },
  {
    "node": "Pàndols - Ermita De Santa Magdalena",
    "label": "Pàndols - Ermita De Santa Magdalena",
    "location": "El Pinell de Brai"
  },
  {
    "node": "Pàndols/Cota 698",
    "label": "Pàndols/Cota 698",
    "location": "Spain"
  },
  {
    "node": "Pàndols/Cota 698",
    "label": "Pàndols/Cota 698",
    "location": "El Pinell de Brai"
  },
  {
    "node": "Quatre Camins",
    "label": "Quatre Camins",
    "location": "Spain"
  },
  {
    "node": "Quatre Camins",
    "label": "Quatre Camins",
    "location": "Ascó"
  },
  {
    "node": "Rabós, Prop Del Coll De Banyuls",
    "label": "Rabós, Prop Del Coll De Banyuls",
    "location": "Spain"
  },
  {
    "node": "Rabós, Prop Del Coll De Banyuls",
    "label": "Rabós, Prop Del Coll De Banyuls",
    "location": "Rabós"
  },
  {
    "node": "Racó Dels Italians Del Cementiri Del Cogul",
    "label": "Racó Dels Italians Del Cementiri Del Cogul",
    "location": "Spain"
  },
  {
    "node": "Racó Dels Italians Del Cementiri Del Cogul",
    "label": "Racó Dels Italians Del Cementiri Del Cogul",
    "location": "Lleida"
  },
  {
    "node": "Racó Dels Italians Del Cementiri Del Cogul",
    "label": "Racó Dels Italians Del Cementiri Del Cogul",
    "location": "El Cogul"
  },
  {
    "node": "Racó del Quico",
    "label": "Racó del Quico",
    "location": "Spain"
  },
  {
    "node": "Racó del Quico",
    "label": "Racó del Quico",
    "location": "Lleida"
  },
  {
    "node": "Racó del Quico",
    "label": "Racó del Quico",
    "location": "Granyena de les Garrigues"
  },
  {
    "node": "Rams",
    "label": "Rams",
    "location": "Spain"
  },
  {
    "node": "Rams",
    "label": "Rams",
    "location": "Lleida"
  },
  {
    "node": "Rams",
    "label": "Rams",
    "location": "Vilanova De Meià"
  },
  {
    "node": "Ribamala",
    "label": "Ribamala",
    "location": "Spain"
  },
  {
    "node": "Ribamala",
    "label": "Ribamala",
    "location": "Girona"
  },
  {
    "node": "Ribamala",
    "label": "Ribamala",
    "location": "Sant Joan de les Abadesses"
  },
  {
    "node": "Riu De Turons: Masos De Sant Marti",
    "label": "Riu De Turons: Masos De Sant Marti",
    "location": "Isona i Conca Dellà"
  },
  {
    "node": "Rocalladre: Era De La Garriga D'en Marian",
    "label": "Rocalladre: Era De La Garriga D'en Marian",
    "location": "Spain"
  },
  {
    "node": "Rocalladre: Era De La Garriga D'en Marian",
    "label": "Rocalladre: Era De La Garriga D'en Marian",
    "location": "Ulldemolins"
  },
  {
    "node": "Sant Pau: Camí D'accés A L'ermita",
    "label": "Sant Pau: Camí D'accés A L'ermita",
    "location": "Tarragona"
  },
  {
    "node": "Sant Pau: Camí D'accés A L'ermita",
    "label": "Sant Pau: Camí D'accés A L'ermita",
    "location": "Catalunya"
  },
  {
    "node": "Sant Pau: Camí D'accés A L'ermita",
    "label": "Sant Pau: Camí D'accés A L'ermita",
    "location": "Spain"
  },
  {
    "node": "Sant Pau: Camí D'accés A L'ermita",
    "label": "Sant Pau: Camí D'accés A L'ermita",
    "location": "Cabacés"
  },
  {
    "node": "Sant Pau: Camí D'accés A L'ermita",
    "label": "Sant Pau: Camí D'accés A L'ermita",
    "location": "Priorat"
  },
  {
    "node": "Sant Pere Màrtir",
    "label": "Sant Pere Màrtir",
    "location": "Spain"
  },
  {
    "node": "Sant Pere Màrtir",
    "label": "Sant Pere Màrtir",
    "location": "Barcelona"
  },
  {
    "node": "Sant Pere Màrtir",
    "label": "Sant Pere Màrtir",
    "location": "Sant Just Desvern"
  },
  {
    "node": "Senlleí, Hortoneda",
    "label": "Senlleí, Hortoneda",
    "location": "Conca de Dalt"
  },
  {
    "node": "Sepultura del soldats morts el 1944 inhumats al cementiri de Vielha",
    "label": "Sepultura del soldats morts el 1944 inhumats al cementiri de Vielha",
    "location": "Vielha e Mijaran"
  },
  {
    "node": "Serra Alta, Foradada",
    "label": "Serra Alta, Foradada",
    "location": "Foradada"
  },
  {
    "node": "Serra del Munt",
    "label": "Serra del Munt",
    "location": null
  },
  {
    "node": "Serra-seca",
    "label": "Serra-seca",
    "location": "Spain"
  },
  {
    "node": "Serra-seca",
    "label": "Serra-seca",
    "location": "Lleida"
  },
  {
    "node": "Serra-seca",
    "label": "Serra-seca",
    "location": "Prats De Lluçanès"
  },
  {
    "node": "Serra-seca",
    "label": "Serra-seca",
    "location": "Odèn"
  },
  {
    "node": "Serrat Gran, Capolat",
    "label": "Serrat Gran, Capolat",
    "location": "Spain"
  },
  {
    "node": "Serrat Gran, Capolat",
    "label": "Serrat Gran, Capolat",
    "location": "Barcelona"
  },
  {
    "node": "Serrat Gran, Capolat",
    "label": "Serrat Gran, Capolat",
    "location": "Capolat"
  },
  {
    "node": "Serrat de Voltora. Soldat republicà",
    "label": "Serrat de Voltora. Soldat republicà",
    "location": "Tarragona"
  },
  {
    "node": "Serrat de Voltora. Soldat republicà",
    "label": "Serrat de Voltora. Soldat republicà",
    "location": "Spain"
  },
  {
    "node": "Serrat de Voltora. Soldat republicà",
    "label": "Serrat de Voltora. Soldat republicà",
    "location": "La Febró"
  },
  {
    "node": "Seròs: Plana De Guinarro",
    "label": "Seròs: Plana De Guinarro",
    "location": "Spain"
  },
  {
    "node": "Seròs: Plana De Guinarro",
    "label": "Seròs: Plana De Guinarro",
    "location": "Lleida"
  },
  {
    "node": "Seròs: Plana De Guinarro",
    "label": "Seròs: Plana De Guinarro",
    "location": "Seròs"
  },
  {
    "node": "Solar Fustes Sebastià. Traslladada Al Valle De Los Caídos.",
    "label": "Solar Fustes Sebastià. Traslladada Al Valle De Los Caídos.",
    "location": "Rialp"
  },
  {
    "node": "Terme Municipal De Flix. Civils",
    "label": "Terme Municipal De Flix. Civils",
    "location": "Flix"
  },
  {
    "node": "Terme Municipal De Flix. Soldats Republicans",
    "label": "Terme Municipal De Flix. Soldats Republicans",
    "location": "Spain"
  },
  {
    "node": "Terme Municipal De Flix. Soldats Republicans",
    "label": "Terme Municipal De Flix. Soldats Republicans",
    "location": "Flix"
  },
  {
    "node": "Terme municipal Santa Creu de Jutglar",
    "label": "Terme municipal Santa Creu de Jutglar",
    "location": "Barcelona"
  },
  {
    "node": "Terme municipal Santa Creu de Jutglar",
    "label": "Terme municipal Santa Creu de Jutglar",
    "location": "Olost"
  },
  {
    "node": "Toll De Carlos",
    "label": "Toll De Carlos",
    "location": "Almatret"
  },
  {
    "node": "Tomba De Gerszon Rotholc",
    "label": "Tomba De Gerszon Rotholc",
    "location": "Tarragona"
  },
  {
    "node": "Tomba De Gerszon Rotholc",
    "label": "Tomba De Gerszon Rotholc",
    "location": "Pradell de la Teixeta"
  },
  {
    "node": "Tomba De Joan Montserrat",
    "label": "Tomba De Joan Montserrat",
    "location": "Spain"
  },
  {
    "node": "Tomba De Joan Montserrat",
    "label": "Tomba De Joan Montserrat",
    "location": "Camarasa"
  },
  {
    "node": "Tormo Matalacabra",
    "label": "Tormo Matalacabra",
    "location": "Spain"
  },
  {
    "node": "Tormo Matalacabra",
    "label": "Tormo Matalacabra",
    "location": "Lleida"
  },
  {
    "node": "Tormo Matalacabra",
    "label": "Tormo Matalacabra",
    "location": "La Granadella"
  },
  {
    "node": "Torrent Dels Albans (I)",
    "label": "Torrent Dels Albans (I)",
    "location": "Spain"
  },
  {
    "node": "Torrent Dels Albans (I)",
    "label": "Torrent Dels Albans (I)",
    "location": "Barcelona"
  },
  {
    "node": "Torrent Dels Albans (I)",
    "label": "Torrent Dels Albans (I)",
    "location": "Olesa de Bonesvalls"
  },
  {
    "node": "Torrent Dels Albans (Ii)",
    "label": "Torrent Dels Albans (Ii)",
    "location": "Catalunya"
  },
  {
    "node": "Torrent Dels Albans (Ii)",
    "label": "Torrent Dels Albans (Ii)",
    "location": "Spain"
  },
  {
    "node": "Torrent Dels Albans (Ii)",
    "label": "Torrent Dels Albans (Ii)",
    "location": "Barcelona"
  },
  {
    "node": "Torrent Dels Albans (Ii)",
    "label": "Torrent Dels Albans (Ii)",
    "location": "Olesa de Bonesvalls"
  },
  {
    "node": "Torrent Dels Albans (Ii)",
    "label": "Torrent Dels Albans (Ii)",
    "location": "Alt Penedès"
  },
  {
    "node": "Tossal Del Morull",
    "label": "Tossal Del Morull",
    "location": "Spain"
  },
  {
    "node": "Tossal Del Morull",
    "label": "Tossal Del Morull",
    "location": "Lleida"
  },
  {
    "node": "Tossal Del Morull",
    "label": "Tossal Del Morull",
    "location": "Bellaguarda"
  },
  {
    "node": "Tossal Gros",
    "label": "Tossal Gros",
    "location": "Spain"
  },
  {
    "node": "Tossal Gros",
    "label": "Tossal Gros",
    "location": "Lleida"
  },
  {
    "node": "Tossal Gros",
    "label": "Tossal Gros",
    "location": "Alfés"
  },
  {
    "node": "Tossal Rodó",
    "label": "Tossal Rodó",
    "location": "Spain"
  },
  {
    "node": "Tossal Rodó",
    "label": "Tossal Rodó",
    "location": "Lleida"
  },
  {
    "node": "Tossal Rodó",
    "label": "Tossal Rodó",
    "location": "Castelldans"
  },
  {
    "node": "Tros De Marieta: Rialp",
    "label": "Tros De Marieta: Rialp",
    "location": "Rialp"
  },
  {
    "node": "Vall De L'aubaga. Poble Vell",
    "label": "Vall De L'aubaga. Poble Vell",
    "location": "Tarragona"
  },
  {
    "node": "Vall De L'aubaga. Poble Vell",
    "label": "Vall De L'aubaga. Poble Vell",
    "location": "Spain"
  },
  {
    "node": "Vall De L'aubaga. Poble Vell",
    "label": "Vall De L'aubaga. Poble Vell",
    "location": "Corbera d'Ebre"
  },
  {
    "node": "Vall De La Torre",
    "label": "Vall De La Torre",
    "location": "Spain"
  },
  {
    "node": "Vall De La Torre",
    "label": "Vall De La Torre",
    "location": "Corbera d'Ebre"
  },
  {
    "node": "Vallada De Sarió",
    "label": "Vallada De Sarió",
    "location": "Tarragona"
  },
  {
    "node": "Vallada De Sarió",
    "label": "Vallada De Sarió",
    "location": "Spain"
  },
  {
    "node": "Vallada De Sarió",
    "label": "Vallada De Sarió",
    "location": "Gandesa"
  },
  {
    "node": "Valldefons",
    "label": "Valldefons",
    "location": "Flix"
  },
  {
    "node": "Venta Fusellé (Fàbrica Cortiella)",
    "label": "Venta Fusellé (Fàbrica Cortiella)",
    "location": "Tarragona"
  },
  {
    "node": "Venta Fusellé (Fàbrica Cortiella)",
    "label": "Venta Fusellé (Fàbrica Cortiella)",
    "location": "Spain"
  },
  {
    "node": "Venta Fusellé (Fàbrica Cortiella)",
    "label": "Venta Fusellé (Fàbrica Cortiella)",
    "location": "Gandesa"
  },
  {
    "node": "Vessant De La Creu De Salitons, Casserres",
    "label": "Vessant De La Creu De Salitons, Casserres",
    "location": "Spain"
  },
  {
    "node": "Vessant De La Creu De Salitons, Casserres",
    "label": "Vessant De La Creu De Salitons, Casserres",
    "location": "Barcelona"
  },
  {
    "node": "Vessant De La Creu De Salitons, Casserres",
    "label": "Vessant De La Creu De Salitons, Casserres",
    "location": "Casserres"
  },
  {
    "node": "Vinyes de la Casa Llarga - Font de la Capella",
    "label": "Vinyes de la Casa Llarga - Font de la Capella",
    "location": "Spain"
  },
  {
    "node": "Vinyes de la Casa Llarga - Font de la Capella",
    "label": "Vinyes de la Casa Llarga - Font de la Capella",
    "location": "Subirats"
  },
  {
    "node": "Vinyetes De Casa Corona",
    "label": "Vinyetes De Casa Corona",
    "location": "Spain"
  },
  {
    "node": "Vinyetes De Casa Corona",
    "label": "Vinyetes De Casa Corona",
    "location": "Lleida"
  },
  {
    "node": "Vinyetes De Casa Corona",
    "label": "Vinyetes De Casa Corona",
    "location": "La Granadella"
  },
  {
    "node": "Cementiri de la Jonquera",
    "label": null,
    "location": "La Jonquera"
  },
  {
    "node": "Camí de la Font d'Ullastrell",
    "label": null,
    "location": "Ullastrell"
  },
  {
    "node": "Pla del Blanco",
    "label": null,
    "location": "Artesa de Lleida"
  },
  {
    "node": "Cementiri vell de Sant Julià de Ramis",
    "label": null,
    "location": "Sant Julià de Ramis"
  },
  {
    "node": "Els Tossals d'Aldover",
    "label": null,
    "location": "Aldover"
  },
  {
    "node": "Exterior del Santuari del Miracle",
    "label": null,
    "location": "Riner"
  },
  {
    "node": "Cementiri de Su",
    "label": null,
    "location": "Riner"
  },
  {
    "node": "Cementiri de Sant Just de Joval",
    "label": null,
    "location": "Clariana de Cardener"
  },
  {
    "node": "Cementiri de Clariana de Cardener",
    "label": null,
    "location": "Clariana de Cardener"
  },
  {
    "node": "Casa Rovira-Sança",
    "label": null,
    "location": "Llobera"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:652",
    "label": null,
    "location": "Tarragona"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:652",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:652",
    "label": null,
    "location": "Amposta"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:653",
    "label": null,
    "location": "Tarragona"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:653",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:653",
    "label": null,
    "location": "El Lloar"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:654",
    "label": null,
    "location": "Tarragona"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:654",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:654",
    "label": null,
    "location": "Margalef"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:655",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:655",
    "label": null,
    "location": "Lleida"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:655",
    "label": null,
    "location": "L'Albagés"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:656",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:656",
    "label": null,
    "location": "Lleida"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:656",
    "label": null,
    "location": "Bell-lloc d'Urgell"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:657",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:657",
    "label": null,
    "location": "Girona"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:657",
    "label": null,
    "location": "Sant Martí d'Empúries"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:658",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:658",
    "label": null,
    "location": "Lleida"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:658",
    "label": null,
    "location": "Guissona"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:659",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:659",
    "label": null,
    "location": "Lleida"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:659",
    "label": null,
    "location": "La Floresta"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:660",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:660",
    "label": null,
    "location": "Lleida"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:660",
    "label": null,
    "location": "Agramunt"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:661",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:661",
    "label": null,
    "location": "Lleida"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:661",
    "label": null,
    "location": "Ivars D'Urgell"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:662",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:2885",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:2885",
    "label": null,
    "location": "Fosa de Prades"
  }
]
```
 > Some Nodes = labels some are null but indicate location (DB problem?) Miquel
### Mass graves (Server)

```sparql
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT ?node ?label ?location WHERE { ?node <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.wikidata.org/entity/Q108163> . ?node <http://www.wikidata.org/entity/P1476> ?label . OPTIONAL { ?node <http://www.wikidata.org/entity/P131> ?location } } ORDER BY ?label LIMIT 30",
    "format": "json"
  }'
```

#### Results:
```json
STATUS: 500
Internal Server Error
```

### Statistics (UI)
```Sparql
SELECT ?type (COUNT(DISTINCT ?entity) AS ?count)
WHERE {
  {
    ?entity a <http://www.wikidata.org/entity/Q5> .
    BIND("Brigadists" AS ?type)
  } UNION {
    ?entity a <http://www.wikidata.org/entity/Q108163> .
    BIND("Mass graves" AS ?type)
  } UNION {
    ?entity a <http://www.wikidata.org/entity/Q49848> .
    BIND("Documents" AS ?type)
  }
}
GROUP BY ?type
ORDER BY ?type
```
#### Results
First time
```json
[
  {
    "node": "A Tocar Del Cementiri De Sant Romà D'abella",
    "label": "A Tocar Del Cementiri De Sant Romà D'abella",
    "location": "Spain"
  },
  {
    "node": "A Tocar Del Cementiri De Sant Romà D'abella",
    "label": "A Tocar Del Cementiri De Sant Romà D'abella",
    "location": "Lleida"
  },
  {
    "node": "A Tocar Del Cementiri De Sant Romà D'abella",
    "label": "A Tocar Del Cementiri De Sant Romà D'abella",
    "location": "Sant Romà d'Abella"
  },
  {
    "node": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "label": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "location": "Catalunya"
  },
  {
    "node": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "label": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "location": "Spain"
  },
  {
    "node": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "label": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "location": "Barcelona"
  },
  {
    "node": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "label": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "location": "Sant Feliu de Llobregat"
  },
  {
    "node": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "label": "Al Costat Del Cementiri De Sant Feliu De Llobregat",
    "location": "Baix Llobregat"
  },
  {
    "node": "Aljub Al Soleràs",
    "label": "Aljub Al Soleràs",
    "location": "Spain"
  },
  {
    "node": "Aljub Al Soleràs",
    "label": "Aljub Al Soleràs",
    "location": "Lleida"
  },
  {
    "node": "Aljub Al Soleràs",
    "label": "Aljub Al Soleràs",
    "location": "El Soleràs"
  },
  {
    "node": "Antic Camí De Llanera",
    "label": "Antic Camí De Llanera",
    "location": "Llobera"
  },
  {
    "node": "Aqüeducte del Collet",
    "label": "Aqüeducte del Collet",
    "location": "Barcelona"
  },
  {
    "node": "Aqüeducte del Collet",
    "label": "Aqüeducte del Collet",
    "location": "Guardiola de Berguedà"
  },
  {
    "node": "Aulivar Del Civit",
    "label": "Aulivar Del Civit",
    "location": "Spain"
  },
  {
    "node": "Aulivar Del Civit",
    "label": "Aulivar Del Civit",
    "location": "Lleida"
  },
  {
    "node": "Aulivar Del Civit",
    "label": "Aulivar Del Civit",
    "location": "El Cogul"
  },
  {
    "node": "Aulivarets De Vespella De Gaià",
    "label": "Aulivarets De Vespella De Gaià",
    "location": "Spain"
  },
  {
    "node": "Aulivarets De Vespella De Gaià",
    "label": "Aulivarets De Vespella De Gaià",
    "location": "Vespella de Gaià"
  },
  {
    "node": "Aumaec",
    "label": "Aumaec",
    "location": null
  },
  {
    "node": "Avenc De La Figuerota. Puig Francàs",
    "label": "Avenc De La Figuerota. Puig Francàs",
    "location": "Tarragona"
  },
  {
    "node": "Avenc De La Figuerota. Puig Francàs",
    "label": "Avenc De La Figuerota. Puig Francàs",
    "location": "Spain"
  },
  {
    "node": "Avenc De La Figuerota. Puig Francàs",
    "label": "Avenc De La Figuerota. Puig Francàs",
    "location": "El Montmell"
  },
  {
    "node": "Bancal Del Panser",
    "label": "Bancal Del Panser",
    "location": "Spain"
  },
  {
    "node": "Bancal Del Panser",
    "label": "Bancal Del Panser",
    "location": "Lleida"
  },
  {
    "node": "Bancal Del Panser",
    "label": "Bancal Del Panser",
    "location": "El Cogul"
  },
  {
    "node": "Bancal de l'Anton",
    "label": "Bancal de l'Anton",
    "location": "Spain"
  },
  {
    "node": "Bancal de l'Anton",
    "label": "Bancal de l'Anton",
    "location": "Lleida"
  },
  {
    "node": "Bancal de l'Anton",
    "label": "Bancal de l'Anton",
    "location": "El Cogul"
  },
  {
    "node": "Banyadé: Solana Del Pas Del Pi",
    "label": "Banyadé: Solana Del Pas Del Pi",
    "location": "Spain"
  },
  {
    "node": "Banyadé: Solana Del Pas Del Pi",
    "label": "Banyadé: Solana Del Pas Del Pi",
    "location": "Conca de Dalt"
  },
  {
    "node": "Barranc De Torrenova",
    "label": "Barranc De Torrenova",
    "location": "Vilalba dels Arcs"
  },
  {
    "node": "Barranc de la Call",
    "label": "Barranc de la Call",
    "location": "Spain"
  },
  {
    "node": "Barranc de la Call",
    "label": "Barranc de la Call",
    "location": "Isona i Conca Dellà"
  },
  {
    "node": "Bordes De Cabrils",
    "label": "Bordes De Cabrils",
    "location": "Spain"
  },
  {
    "node": "Bordes De Cabrils",
    "label": "Bordes De Cabrils",
    "location": "Lleida"
  },
  {
    "node": "Bordes De Cabrils",
    "label": "Bordes De Cabrils",
    "location": "Farrera"
  },
  {
    "node": "Bordes De Tressó",
    "label": "Bordes De Tressó",
    "location": "Spain"
  },
  {
    "node": "Bordes De Tressó",
    "label": "Bordes De Tressó",
    "location": "Lleida"
  },
  {
    "node": "Bordes De Tressó",
    "label": "Bordes De Tressó",
    "location": "Farrera"
  },
  {
    "node": "Bosc I Trinxeres Del Coll De Ban",
    "label": "Bosc I Trinxeres Del Coll De Ban",
    "location": "Bassella"
  },
  {
    "node": "Ca La Maxina (Torregassa)",
    "label": "Ca La Maxina (Torregassa)",
    "location": "Tarragona"
  },
  {
    "node": "Ca La Maxina (Torregassa)",
    "label": "Ca La Maxina (Torregassa)",
    "location": "Spain"
  },
  {
    "node": "Ca La Maxina (Torregassa)",
    "label": "Ca La Maxina (Torregassa)",
    "location": "Sant Jaume dels Domenys"
  },
  {
    "node": "Cabana De L'agnès",
    "label": "Cabana De L'agnès",
    "location": "Spain"
  },
  {
    "node": "Cabana De L'agnès",
    "label": "Cabana De L'agnès",
    "location": "Lleida"
  },
  {
    "node": "Cabana De L'agnès",
    "label": "Cabana De L'agnès",
    "location": "L'Albagés"
  },
  {
    "node": "Cal Corretger",
    "label": "Cal Corretger",
    "location": "Spain"
  },
  {
    "node": "Cal Corretger",
    "label": "Cal Corretger",
    "location": "Santa Susanna"
  },
  {
    "node": "Cal Trepat",
    "label": "Cal Trepat",
    "location": "Spain"
  },
  {
    "node": "Cal Trepat",
    "label": "Cal Trepat",
    "location": "Lleida"
  },
  {
    "node": "Cal Trepat",
    "label": "Cal Trepat",
    "location": "Tàrrega"
  },
  {
    "node": "Camp De La Pona",
    "label": "Camp De La Pona",
    "location": "Spain"
  },
  {
    "node": "Camp De La Pona",
    "label": "Camp De La Pona",
    "location": "Lleida"
  },
  {
    "node": "Camp De La Pona",
    "label": "Camp De La Pona",
    "location": "Montellà i Martinet"
  },
  {
    "node": "Camp De Treball Núm. 2 De L’hospitalet De L’infant.",
    "label": "Camp De Treball Núm. 2 De L’hospitalet De L’infant.",
    "location": "Spain"
  },
  {
    "node": "Camp De Treball Núm. 2 De L’hospitalet De L’infant.",
    "label": "Camp De Treball Núm. 2 De L’hospitalet De L’infant.",
    "location": "Vandellòs I L'hospitalet De L'infant"
  },
  {
    "node": "Camp Dels Morts De La Casagolda",
    "label": "Camp Dels Morts De La Casagolda",
    "location": "Spain"
  },
  {
    "node": "Camp Dels Morts De La Casagolda",
    "label": "Camp Dels Morts De La Casagolda",
    "location": "Lleida"
  },
  {
    "node": "Camp Dels Morts De La Casagolda",
    "label": "Camp Dels Morts De La Casagolda",
    "location": "Castellar de la Ribera"
  },
  {
    "node": "Camp Malacara",
    "label": "Camp Malacara",
    "location": "Spain"
  },
  {
    "node": "Camp Malacara",
    "label": "Camp Malacara",
    "location": "Lleida"
  },
  {
    "node": "Camp Malacara",
    "label": "Camp Malacara",
    "location": "Tarrés"
  },
  {
    "node": "Camí De L'Hort D'En Tona - Bòbila Del Sogas",
    "label": "Camí De L'Hort D'En Tona - Bòbila Del Sogas",
    "location": "Spain"
  },
  {
    "node": "Camí De L'Hort D'En Tona - Bòbila Del Sogas",
    "label": "Camí De L'Hort D'En Tona - Bòbila Del Sogas",
    "location": "Vilafranca del Penedès"
  },
  {
    "node": "Camí De La Font De Conill. Cabra Del Camp",
    "label": "Camí De La Font De Conill. Cabra Del Camp",
    "location": "Tarragona"
  },
  {
    "node": "Camí De La Font De Conill. Cabra Del Camp",
    "label": "Camí De La Font De Conill. Cabra Del Camp",
    "location": "Spain"
  },
  {
    "node": "Camí De La Font De Conill. Cabra Del Camp",
    "label": "Camí De La Font De Conill. Cabra Del Camp",
    "location": "Cabra del Camp"
  },
  {
    "node": "Camí De Les Eres (Cometes).",
    "label": "Camí De Les Eres (Cometes).",
    "location": "Tarragona"
  },
  {
    "node": "Camí De Les Eres (Cometes).",
    "label": "Camí De Les Eres (Cometes).",
    "location": "Spain"
  },
  {
    "node": "Camí De Les Eres (Cometes).",
    "label": "Camí De Les Eres (Cometes).",
    "location": "Corbera d'Ebre"
  },
  {
    "node": "Camí Fondo De Torres De Segre (Pala De La Gemma)",
    "label": "Camí Fondo De Torres De Segre (Pala De La Gemma)",
    "location": "Soses"
  },
  {
    "node": "Camí Nou Del Mas De Galofre",
    "label": "Camí Nou Del Mas De Galofre",
    "location": "Tarragona"
  },
  {
    "node": "Camí Nou Del Mas De Galofre",
    "label": "Camí Nou Del Mas De Galofre",
    "location": "Spain"
  },
  {
    "node": "Camí Nou Del Mas De Galofre",
    "label": "Camí Nou Del Mas De Galofre",
    "location": "L'Albiol"
  },
  {
    "node": "Camí Vell De Falset",
    "label": "Camí Vell De Falset",
    "location": "Spain"
  },
  {
    "node": "Camí Vell De Falset",
    "label": "Camí Vell De Falset",
    "location": "Gratallops"
  },
  {
    "node": "Camí Vell De La Pobla De Massaluca",
    "label": "Camí Vell De La Pobla De Massaluca",
    "location": "Tarragona"
  },
  {
    "node": "Camí Vell De La Pobla De Massaluca",
    "label": "Camí Vell De La Pobla De Massaluca",
    "location": "Spain"
  },
  {
    "node": "Camí Vell De La Pobla De Massaluca",
    "label": "Camí Vell De La Pobla De Massaluca",
    "location": "Vilalba dels Arcs"
  },
  {
    "node": "Camí de les Monges (II)",
    "label": "Camí de les Monges (II)",
    "location": "Spain"
  },
  {
    "node": "Camí de les Monges (II)",
    "label": "Camí de les Monges (II)",
    "location": "Barcelona"
  },
  {
    "node": "Camí de les Monges (II)",
    "label": "Camí de les Monges (II)",
    "location": "Ullastrell"
  },
  {
    "node": "Can Carous",
    "label": "Can Carous",
    "location": "Spain"
  },
  {
    "node": "Can Carous",
    "label": "Can Carous",
    "location": "Barcelona"
  },
  {
    "node": "Can Carous",
    "label": "Can Carous",
    "location": "Gurb"
  },
  {
    "node": "Can Carreres",
    "label": "Can Carreres",
    "location": "Spain"
  },
  {
    "node": "Can Carreres",
    "label": "Can Carreres",
    "location": "Rubí"
  },
  {
    "node": "Can Maçana",
    "label": "Can Maçana",
    "location": "Barcelona"
  },
  {
    "node": "Can Maçana",
    "label": "Can Maçana",
    "location": "El Bruc"
  },
  {
    "node": "Cantallops (vinyes a tocar de la N-340)",
    "label": "Cantallops (vinyes a tocar de la N-340)",
    "location": "Spain"
  },
  {
    "node": "Cantallops (vinyes a tocar de la N-340)",
    "label": "Cantallops (vinyes a tocar de la N-340)",
    "location": "Barcelona"
  },
  {
    "node": "Cantallops (vinyes a tocar de la N-340)",
    "label": "Cantallops (vinyes a tocar de la N-340)",
    "location": "Subirats"
  },
  {
    "node": "Carbonelles",
    "label": "Carbonelles",
    "location": "Spain"
  },
  {
    "node": "Carbonelles",
    "label": "Carbonelles",
    "location": "Lleida"
  },
  {
    "node": "Carbonelles",
    "label": "Carbonelles",
    "location": "Torrebesses"
  },
  {
    "node": "Casa Blanca, creu de ferro de Bellprat",
    "label": "Casa Blanca, creu de ferro de Bellprat",
    "location": "Spain"
  },
  {
    "node": "Casa Blanca, creu de ferro de Bellprat",
    "label": "Casa Blanca, creu de ferro de Bellprat",
    "location": "Barcelona"
  },
  {
    "node": "Casa Blanca, creu de ferro de Bellprat",
    "label": "Casa Blanca, creu de ferro de Bellprat",
    "location": "Bellprat"
  },
  {
    "node": "Casanova De Clarà",
    "label": "Casanova De Clarà",
    "location": "Spain"
  },
  {
    "node": "Casanova De Clarà",
    "label": "Casanova De Clarà",
    "location": "Lleida"
  },
  {
    "node": "Casanova De Clarà",
    "label": "Casanova De Clarà",
    "location": "Castellar de la Ribera"
  },
  {
    "node": "Caseta D'en Codolà",
    "label": "Caseta D'en Codolà",
    "location": "Spain"
  },
  {
    "node": "Caseta D'en Codolà",
    "label": "Caseta D'en Codolà",
    "location": "Girona"
  },
  {
    "node": "Caseta D'en Codolà",
    "label": "Caseta D'en Codolà",
    "location": "Cassà de la Selva"
  },
  {
    "node": "Caseta De Peons Ferroviaris",
    "label": "Caseta De Peons Ferroviaris",
    "location": "Tarragona"
  },
  {
    "node": "Caseta De Peons Ferroviaris",
    "label": "Caseta De Peons Ferroviaris",
    "location": "Spain"
  },
  {
    "node": "Caseta De Peons Ferroviaris",
    "label": "Caseta De Peons Ferroviaris",
    "location": "Móra la Nova"
  },
  {
    "node": "Caseta de peons caminers de Guialmons. Les Piles",
    "label": "Caseta de peons caminers de Guialmons. Les Piles",
    "location": "Spain"
  },
  {
    "node": "Caseta de peons caminers de Guialmons. Les Piles",
    "label": "Caseta de peons caminers de Guialmons. Les Piles",
    "location": "Guialmons"
  },
  {
    "node": "Cementeri de Montardit d'Enviny",
    "label": "Cementeri de Montardit d'Enviny",
    "location": "Spain"
  },
  {
    "node": "Cementeri de Montardit d'Enviny",
    "label": "Cementeri de Montardit d'Enviny",
    "location": "Sort"
  },
  {
    "node": "Cementir",
    "label": "Cementir",
    "location": null
  },
  {
    "node": "Cementiri  Vell de Vimbodí. Soldats de la 13a Brigada Internacional.",
    "label": "Cementiri  Vell de Vimbodí. Soldats de la 13a Brigada Internacional.",
    "location": "Spain"
  },
  {
    "node": "Cementiri  Vell de Vimbodí. Soldats de la 13a Brigada Internacional.",
    "label": "Cementiri  Vell de Vimbodí. Soldats de la 13a Brigada Internacional.",
    "location": "Vimbodí i Poblet"
  },
  {
    "node": "Cementiri Ampolla",
    "label": "Cementiri Ampolla",
    "location": "Spain"
  },
  {
    "node": "Cementiri Ampolla",
    "label": "Cementiri Ampolla",
    "location": "L'Ampolla"
  },
  {
    "node": "Cementiri Antic D'almacelles",
    "label": "Cementiri Antic D'almacelles",
    "location": "Spain"
  },
  {
    "node": "Cementiri Antic D'almacelles",
    "label": "Cementiri Antic D'almacelles",
    "location": "Lleida"
  },
  {
    "node": "Cementiri Antic D'almacelles",
    "label": "Cementiri Antic D'almacelles",
    "location": "Almacelles"
  },
  {
    "node": "Cementiri Balaguer. Fossa Dels 19",
    "label": "Cementiri Balaguer. Fossa Dels 19",
    "location": "Balaguer"
  },
  {
    "node": "Cementiri Bellmunt Del Priorat",
    "label": "Cementiri Bellmunt Del Priorat",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri Bellmunt Del Priorat",
    "label": "Cementiri Bellmunt Del Priorat",
    "location": "Spain"
  },
  {
    "node": "Cementiri Bellmunt Del Priorat",
    "label": "Cementiri Bellmunt Del Priorat",
    "location": "Bellmunt del Priorat"
  },
  {
    "node": "Cementiri D'Arenys De Mar",
    "label": "Cementiri D'Arenys De Mar",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'Arenys De Mar",
    "label": "Cementiri D'Arenys De Mar",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri D'Arenys De Mar",
    "label": "Cementiri D'Arenys De Mar",
    "location": "Arenys de Mar"
  },
  {
    "node": "Cementiri D'Arenys De Munt",
    "label": "Cementiri D'Arenys De Munt",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'Arenys De Munt",
    "label": "Cementiri D'Arenys De Munt",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri D'Arenys De Munt",
    "label": "Cementiri D'Arenys De Munt",
    "location": "Arenys de Munt"
  },
  {
    "node": "Cementiri D'Es Bòrdes",
    "label": "Cementiri D'Es Bòrdes",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'Es Bòrdes",
    "label": "Cementiri D'Es Bòrdes",
    "location": "Es Bòrdes"
  },
  {
    "node": "Cementiri D'Estaràs",
    "label": "Cementiri D'Estaràs",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'Estaràs",
    "label": "Cementiri D'Estaràs",
    "location": "Lleida"
  },
  {
    "node": "Cementiri D'Estaràs",
    "label": "Cementiri D'Estaràs",
    "location": "Estaràs"
  },
  {
    "node": "Cementiri D'alcanó",
    "label": "Cementiri D'alcanó",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'alcanó",
    "label": "Cementiri D'alcanó",
    "location": "Lleida"
  },
  {
    "node": "Cementiri D'alcanó",
    "label": "Cementiri D'alcanó",
    "location": "Alcanó"
  },
  {
    "node": "Cementiri D'alcover. Ossera",
    "label": "Cementiri D'alcover. Ossera",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri D'alcover. Ossera",
    "label": "Cementiri D'alcover. Ossera",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'alcover. Ossera",
    "label": "Cementiri D'alcover. Ossera",
    "location": "Alcover"
  },
  {
    "node": "Cementiri D'alentorn. Enterrament De Vicente Boquera",
    "label": "Cementiri D'alentorn. Enterrament De Vicente Boquera",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'alentorn. Enterrament De Vicente Boquera",
    "label": "Cementiri D'alentorn. Enterrament De Vicente Boquera",
    "location": "Alentorn"
  },
  {
    "node": "Cementiri D'almenar",
    "label": "Cementiri D'almenar",
    "location": "Almenar"
  },
  {
    "node": "Cementiri D'alta-riba",
    "label": "Cementiri D'alta-riba",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'alta-riba",
    "label": "Cementiri D'alta-riba",
    "location": "Estaràs"
  },
  {
    "node": "Cementiri D'altron",
    "label": "Cementiri D'altron",
    "location": "Catalunya"
  },
  {
    "node": "Cementiri D'altron",
    "label": "Cementiri D'altron",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'altron",
    "label": "Cementiri D'altron",
    "location": "Lleida"
  },
  {
    "node": "Cementiri D'altron",
    "label": "Cementiri D'altron",
    "location": "Pallars Sobirà"
  },
  {
    "node": "Cementiri D'altron",
    "label": "Cementiri D'altron",
    "location": "Altron"
  },
  {
    "node": "Cementiri D'alòs De Balaguer. Sepultura De Juan Campoy Sánchez",
    "label": "Cementiri D'alòs De Balaguer. Sepultura De Juan Campoy Sánchez",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'alòs De Balaguer. Sepultura De Juan Campoy Sánchez",
    "label": "Cementiri D'alòs De Balaguer. Sepultura De Juan Campoy Sánchez",
    "location": "Lleida"
  },
  {
    "node": "Cementiri D'alòs De Balaguer. Sepultura De Juan Campoy Sánchez",
    "label": "Cementiri D'alòs De Balaguer. Sepultura De Juan Campoy Sánchez",
    "location": "Alòs de Balaguer"
  },
  {
    "node": "Cementiri D'amer. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri D'amer. Traslladada Al Valle De Los Caídos",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'amer. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri D'amer. Traslladada Al Valle De Los Caídos",
    "location": "Girona"
  },
  {
    "node": "Cementiri D'amer. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri D'amer. Traslladada Al Valle De Los Caídos",
    "location": "Amer"
  },
  {
    "node": "Cementiri D'anglesola",
    "label": "Cementiri D'anglesola",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'anglesola",
    "label": "Cementiri D'anglesola",
    "location": "Lleida"
  },
  {
    "node": "Cementiri D'anglesola",
    "label": "Cementiri D'anglesola",
    "location": "Anglesola"
  },
  {
    "node": "Cementiri D'escós",
    "label": "Cementiri D'escós",
    "location": "Escós"
  },
  {
    "node": "Cementiri D'esparreguera. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri D'esparreguera. Traslladada Al Valle De Los Caídos",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'esparreguera. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri D'esparreguera. Traslladada Al Valle De Los Caídos",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri D'esparreguera. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri D'esparreguera. Traslladada Al Valle De Los Caídos",
    "location": "Esparreguera"
  },
  {
    "node": "Cementiri D'esterri De Cardós",
    "label": "Cementiri D'esterri De Cardós",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'esterri De Cardós",
    "label": "Cementiri D'esterri De Cardós",
    "location": "Lleida"
  },
  {
    "node": "Cementiri D'esterri De Cardós",
    "label": "Cementiri D'esterri De Cardós",
    "location": "Esterri de Cardós"
  },
  {
    "node": "Cementiri D'herba-Savina",
    "label": "Cementiri D'herba-Savina",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'herba-Savina",
    "label": "Cementiri D'herba-Savina",
    "location": "Lleida"
  },
  {
    "node": "Cementiri D'herba-Savina",
    "label": "Cementiri D'herba-Savina",
    "location": "Conca de Dalt"
  },
  {
    "node": "Cementiri D'horta De Sant Joan. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri D'horta De Sant Joan. Traslladada Al Valle De Los Caídos.",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri D'horta De Sant Joan. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri D'horta De Sant Joan. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'horta De Sant Joan. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri D'horta De Sant Joan. Traslladada Al Valle De Los Caídos.",
    "location": "Horta de Sant Joan"
  },
  {
    "node": "Cementiri D'igualada",
    "label": "Cementiri D'igualada",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'igualada",
    "label": "Cementiri D'igualada",
    "location": "Igualada"
  },
  {
    "node": "Cementiri D'ivars D'urgell",
    "label": "Cementiri D'ivars D'urgell",
    "location": "Spain"
  },
  {
    "node": "Cementiri D'ivars D'urgell",
    "label": "Cementiri D'ivars D'urgell",
    "location": "Lleida"
  },
  {
    "node": "Cementiri D'unha",
    "label": "Cementiri D'unha",
    "location": "Lleida"
  },
  {
    "node": "Cementiri D'unha",
    "label": "Cementiri D'unha",
    "location": "Naut Aran"
  },
  {
    "node": "Cementiri De Banyeres Del Penedès",
    "label": "Cementiri De Banyeres Del Penedès",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Banyeres Del Penedès",
    "label": "Cementiri De Banyeres Del Penedès",
    "location": "Banyeres del Penedès"
  },
  {
    "node": "Cementiri De Barcelona (sense Determinar). Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Barcelona (sense Determinar). Traslladada Al Valle De Los Caídos.",
    "location": "Catalunya"
  },
  {
    "node": "Cementiri De Barcelona (sense Determinar). Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Barcelona (sense Determinar). Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Barcelona (sense Determinar). Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Barcelona (sense Determinar). Traslladada Al Valle De Los Caídos.",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Barcelona (sense Determinar). Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Barcelona (sense Determinar). Traslladada Al Valle De Los Caídos.",
    "location": "Barcelonès"
  },
  {
    "node": "Cementiri De Bassella",
    "label": "Cementiri De Bassella",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Bassella",
    "label": "Cementiri De Bassella",
    "location": "Bassella"
  },
  {
    "node": "Cementiri De Bellprat",
    "label": "Cementiri De Bellprat",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Bellprat",
    "label": "Cementiri De Bellprat",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Bellprat",
    "label": "Cementiri De Bellprat",
    "location": "Bellprat"
  },
  {
    "node": "Cementiri De Bellpuig",
    "label": "Cementiri De Bellpuig",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Bellpuig",
    "label": "Cementiri De Bellpuig",
    "location": "Bellpuig"
  },
  {
    "node": "Cementiri De Bonastre",
    "label": "Cementiri De Bonastre",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De Bonastre",
    "label": "Cementiri De Bonastre",
    "location": "Catalunya"
  },
  {
    "node": "Cementiri De Bonastre",
    "label": "Cementiri De Bonastre",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Bonastre",
    "label": "Cementiri De Bonastre",
    "location": "Bonastre"
  },
  {
    "node": "Cementiri De Bonastre",
    "label": "Cementiri De Bonastre",
    "location": "Baix Penedès"
  },
  {
    "node": "Cementiri De Bot. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Bot. Traslladada Al Valle De Cuelgamuros",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De Bot. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Bot. Traslladada Al Valle De Cuelgamuros",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Bot. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Bot. Traslladada Al Valle De Cuelgamuros",
    "location": "Bot"
  },
  {
    "node": "Cementiri De Bovera",
    "label": "Cementiri De Bovera",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Bovera",
    "label": "Cementiri De Bovera",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Bovera",
    "label": "Cementiri De Bovera",
    "location": "Bovera"
  },
  {
    "node": "Cementiri De Cabrera De Mar",
    "label": "Cementiri De Cabrera De Mar",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Cabrera De Mar",
    "label": "Cementiri De Cabrera De Mar",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Cabrera De Mar",
    "label": "Cementiri De Cabrera De Mar",
    "location": "Cabrera de Mar"
  },
  {
    "node": "Cementiri De Cabó (Camp De Treball)",
    "label": "Cementiri De Cabó (Camp De Treball)",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Cabó (Camp De Treball)",
    "label": "Cementiri De Cabó (Camp De Treball)",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Cabó (Camp De Treball)",
    "label": "Cementiri De Cabó (Camp De Treball)",
    "location": "Cabó"
  },
  {
    "node": "Cementiri De Calaf",
    "label": "Cementiri De Calaf",
    "location": "Catalunya"
  },
  {
    "node": "Cementiri De Calaf",
    "label": "Cementiri De Calaf",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Calaf",
    "label": "Cementiri De Calaf",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Calaf",
    "label": "Cementiri De Calaf",
    "location": "Calaf"
  },
  {
    "node": "Cementiri De Calaf",
    "label": "Cementiri De Calaf",
    "location": "Anoia"
  },
  {
    "node": "Cementiri De Caldes D'Estrac",
    "label": "Cementiri De Caldes D'Estrac",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Caldes D'Estrac",
    "label": "Cementiri De Caldes D'Estrac",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Caldes D'Estrac",
    "label": "Cementiri De Caldes D'Estrac",
    "location": "Caldes d'Estrac"
  },
  {
    "node": "Cementiri De Camarasa",
    "label": "Cementiri De Camarasa",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Camarasa",
    "label": "Cementiri De Camarasa",
    "location": "Camarasa"
  },
  {
    "node": "Cementiri De Castellbisbal",
    "label": "Cementiri De Castellbisbal",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Castellbisbal",
    "label": "Cementiri De Castellbisbal",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Castellbisbal",
    "label": "Cementiri De Castellbisbal",
    "location": "Castellbisbal"
  },
  {
    "node": "Cementiri De Castellciutat",
    "label": "Cementiri De Castellciutat",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Castellciutat",
    "label": "Cementiri De Castellciutat",
    "location": "Castellciutat"
  },
  {
    "node": "Cementiri De Castellfollit De La Roca. Traslladada A Cuelgamuros",
    "label": "Cementiri De Castellfollit De La Roca. Traslladada A Cuelgamuros",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Castellfollit De La Roca. Traslladada A Cuelgamuros",
    "label": "Cementiri De Castellfollit De La Roca. Traslladada A Cuelgamuros",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Castellfollit De La Roca. Traslladada A Cuelgamuros",
    "label": "Cementiri De Castellfollit De La Roca. Traslladada A Cuelgamuros",
    "location": "Castellfollit de la Roca"
  },
  {
    "node": "Cementiri De Castellgalí",
    "label": "Cementiri De Castellgalí",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Castellgalí",
    "label": "Cementiri De Castellgalí",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Castellgalí",
    "label": "Cementiri De Castellgalí",
    "location": "Castellgalí"
  },
  {
    "node": "Cementiri De Castellolí",
    "label": "Cementiri De Castellolí",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Castellolí",
    "label": "Cementiri De Castellolí",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Castellolí",
    "label": "Cementiri De Castellolí",
    "location": "Castellolí"
  },
  {
    "node": "Cementiri De Castellserà",
    "label": "Cementiri De Castellserà",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Castellserà",
    "label": "Cementiri De Castellserà",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Castellserà",
    "label": "Cementiri De Castellserà",
    "location": "Castellserà"
  },
  {
    "node": "Cementiri De Celrà. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Celrà. Traslladada Al Valle De Cuelgamuros",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Celrà. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Celrà. Traslladada Al Valle De Cuelgamuros",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Celrà. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Celrà. Traslladada Al Valle De Cuelgamuros",
    "location": "Celrà"
  },
  {
    "node": "Cementiri De Cerdanyola Del Vallès, Fossa Dels Anarquistes",
    "label": "Cementiri De Cerdanyola Del Vallès, Fossa Dels Anarquistes",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Cerdanyola Del Vallès, Fossa Dels Anarquistes",
    "label": "Cementiri De Cerdanyola Del Vallès, Fossa Dels Anarquistes",
    "location": "Cerdanyola del Vallès"
  },
  {
    "node": "Cementiri De Comabella",
    "label": "Cementiri De Comabella",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Comabella",
    "label": "Cementiri De Comabella",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Comabella",
    "label": "Cementiri De Comabella",
    "location": "Sant Guim de la Plana"
  },
  {
    "node": "Cementiri De Concabella",
    "label": "Cementiri De Concabella",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Concabella",
    "label": "Cementiri De Concabella",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Concabella",
    "label": "Cementiri De Concabella",
    "location": "Els Plans de Sió"
  },
  {
    "node": "Cementiri De Dosrius",
    "label": "Cementiri De Dosrius",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Dosrius",
    "label": "Cementiri De Dosrius",
    "location": "Dosrius"
  },
  {
    "node": "Cementiri De Falset",
    "label": "Cementiri De Falset",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De Falset",
    "label": "Cementiri De Falset",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Falset",
    "label": "Cementiri De Falset",
    "location": "Falset"
  },
  {
    "node": "Cementiri De Figueres. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Figueres. Traslladada Al Valle De Los Caídos",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Figueres. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Figueres. Traslladada Al Valle De Los Caídos",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Figueres. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Figueres. Traslladada Al Valle De Los Caídos",
    "location": "Figueres"
  },
  {
    "node": "Cementiri De Flix. Repressió A La Reraguarda",
    "label": "Cementiri De Flix. Repressió A La Reraguarda",
    "location": "Flix"
  },
  {
    "node": "Cementiri De Flix. Soldats Morts A L'hospital Militar.",
    "label": "Cementiri De Flix. Soldats Morts A L'hospital Militar.",
    "location": "Flix"
  },
  {
    "node": "Cementiri De Flix. Víctimes De Bombardeig.",
    "label": "Cementiri De Flix. Víctimes De Bombardeig.",
    "location": "Flix"
  },
  {
    "node": "Cementiri De Florejacs Ii",
    "label": "Cementiri De Florejacs Ii",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Florejacs Ii",
    "label": "Cementiri De Florejacs Ii",
    "location": "Torrefeta"
  },
  {
    "node": "Cementiri De Fontanet",
    "label": "Cementiri De Fontanet",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Fontanet",
    "label": "Cementiri De Fontanet",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Fontanet",
    "label": "Cementiri De Fontanet",
    "location": "Torà"
  },
  {
    "node": "Cementiri De Garrigoles. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Garrigoles. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Garrigoles. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Garrigoles. Traslladada Al Valle De Los Caídos.",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Garrigoles. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Garrigoles. Traslladada Al Valle De Los Caídos.",
    "location": "Garrigoles"
  },
  {
    "node": "Cementiri De Garrigàs",
    "label": "Cementiri De Garrigàs",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Garrigàs",
    "label": "Cementiri De Garrigàs",
    "location": "Garrigàs"
  },
  {
    "node": "Cementiri De L'ametlla De Mar I Voltant De La Masia Ponts",
    "label": "Cementiri De L'ametlla De Mar I Voltant De La Masia Ponts",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De L'ametlla De Mar I Voltant De La Masia Ponts",
    "label": "Cementiri De L'ametlla De Mar I Voltant De La Masia Ponts",
    "location": "Catalunya"
  },
  {
    "node": "Cementiri De L'ametlla De Mar I Voltant De La Masia Ponts",
    "label": "Cementiri De L'ametlla De Mar I Voltant De La Masia Ponts",
    "location": "Spain"
  },
  {
    "node": "Cementiri De L'ametlla De Mar I Voltant De La Masia Ponts",
    "label": "Cementiri De L'ametlla De Mar I Voltant De La Masia Ponts",
    "location": "Baix Ebre"
  },
  {
    "node": "Cementiri De L'ametlla De Mar I Voltant De La Masia Ponts",
    "label": "Cementiri De L'ametlla De Mar I Voltant De La Masia Ponts",
    "location": "L'Ametlla de Mar"
  },
  {
    "node": "Cementiri De La Doma De La Garriga",
    "label": "Cementiri De La Doma De La Garriga",
    "location": "La Garriga"
  },
  {
    "node": "Cementiri De La Granadella. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De La Granadella. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De La Granadella. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De La Granadella. Traslladada Al Valle De Los Caídos.",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De La Granadella. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De La Granadella. Traslladada Al Valle De Los Caídos.",
    "location": "La Granadella"
  },
  {
    "node": "Cementiri De La Guingueta D'àneu",
    "label": "Cementiri De La Guingueta D'àneu",
    "location": "La Guingueta d'Àneu"
  },
  {
    "node": "Cementiri De La Pobla De Mafumet",
    "label": "Cementiri De La Pobla De Mafumet",
    "location": "Spain"
  },
  {
    "node": "Cementiri De La Pobla De Mafumet",
    "label": "Cementiri De La Pobla De Mafumet",
    "location": "La Pobla de Mafumet"
  },
  {
    "node": "Cementiri De La Secuita. Repressió De Reraguarda.",
    "label": "Cementiri De La Secuita. Repressió De Reraguarda.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De La Secuita. Repressió De Reraguarda.",
    "label": "Cementiri De La Secuita. Repressió De Reraguarda.",
    "location": "La Secuita"
  },
  {
    "node": "Cementiri De La Selva Del Camp. Civils Morts A L'Hospital Intercomarcal.",
    "label": "Cementiri De La Selva Del Camp. Civils Morts A L'Hospital Intercomarcal.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De La Selva Del Camp. Civils Morts A L'Hospital Intercomarcal.",
    "label": "Cementiri De La Selva Del Camp. Civils Morts A L'Hospital Intercomarcal.",
    "location": "La Selva del Camp"
  },
  {
    "node": "Cementiri De La Seu D'Urgell. Civils Reinhumats El 1937",
    "label": "Cementiri De La Seu D'Urgell. Civils Reinhumats El 1937",
    "location": "Spain"
  },
  {
    "node": "Cementiri De La Seu D'Urgell. Civils Reinhumats El 1937",
    "label": "Cementiri De La Seu D'Urgell. Civils Reinhumats El 1937",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De La Seu D'Urgell. Civils Reinhumats El 1937",
    "label": "Cementiri De La Seu D'Urgell. Civils Reinhumats El 1937",
    "location": "La Seu d'Urgell"
  },
  {
    "node": "Cementiri De La Seu D'Urgell. Soldats Morts A L'Hospital Del X Cos D'Exèrcit",
    "label": "Cementiri De La Seu D'Urgell. Soldats Morts A L'Hospital Del X Cos D'Exèrcit",
    "location": "Spain"
  },
  {
    "node": "Cementiri De La Seu D'Urgell. Soldats Morts A L'Hospital Del X Cos D'Exèrcit",
    "label": "Cementiri De La Seu D'Urgell. Soldats Morts A L'Hospital Del X Cos D'Exèrcit",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De La Seu D'Urgell. Soldats Morts A L'Hospital Del X Cos D'Exèrcit",
    "label": "Cementiri De La Seu D'Urgell. Soldats Morts A L'Hospital Del X Cos D'Exèrcit",
    "location": "La Seu d'Urgell"
  },
  {
    "node": "Cementiri De La Tallada D'empordà. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De La Tallada D'empordà. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De La Tallada D'empordà. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De La Tallada D'empordà. Traslladada Al Valle De Los Caídos.",
    "location": "Girona"
  },
  {
    "node": "Cementiri De La Tallada D'empordà. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De La Tallada D'empordà. Traslladada Al Valle De Los Caídos.",
    "location": "La Tallada d'Empordà"
  },
  {
    "node": "Cementiri De La Torre De Claramunt",
    "label": "Cementiri De La Torre De Claramunt",
    "location": "Spain"
  },
  {
    "node": "Cementiri De La Torre De Claramunt",
    "label": "Cementiri De La Torre De Claramunt",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De La Torre De Claramunt",
    "label": "Cementiri De La Torre De Claramunt",
    "location": "La Torre De Claramunt"
  },
  {
    "node": "Cementiri De La Torre De L'Espanyol",
    "label": "Cementiri De La Torre De L'Espanyol",
    "location": "Spain"
  },
  {
    "node": "Cementiri De La Torre De L'Espanyol",
    "label": "Cementiri De La Torre De L'Espanyol",
    "location": "La Torre de l'Espanyol"
  },
  {
    "node": "Cementiri De Les Oluges II",
    "label": "Cementiri De Les Oluges II",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Les Oluges II",
    "label": "Cementiri De Les Oluges II",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Les Oluges II",
    "label": "Cementiri De Les Oluges II",
    "location": "Les Oluges"
  },
  {
    "node": "Cementiri De Les Pallargues",
    "label": "Cementiri De Les Pallargues",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Les Pallargues",
    "label": "Cementiri De Les Pallargues",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Les Pallargues",
    "label": "Cementiri De Les Pallargues",
    "location": "Els Plans de Sió"
  },
  {
    "node": "Cementiri De Linyola",
    "label": "Cementiri De Linyola",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Linyola",
    "label": "Cementiri De Linyola",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Linyola",
    "label": "Cementiri De Linyola",
    "location": "Linyola"
  },
  {
    "node": "Cementiri De Llagunes",
    "label": "Cementiri De Llagunes",
    "location": "Llagunes"
  },
  {
    "node": "Cementiri De Llavorsi (III)",
    "label": "Cementiri De Llavorsi (III)",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Llavorsi (III)",
    "label": "Cementiri De Llavorsi (III)",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Llavorsi (III)",
    "label": "Cementiri De Llavorsi (III)",
    "location": "Llavorsí"
  },
  {
    "node": "Cementiri De Lleida. Departament De Sant Josep. Víctimes De La Violència Revolucionària",
    "label": "Cementiri De Lleida. Departament De Sant Josep. Víctimes De La Violència Revolucionària",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Lleida. Departament De Sant Josep. Víctimes De La Violència Revolucionària",
    "label": "Cementiri De Lleida. Departament De Sant Josep. Víctimes De La Violència Revolucionària",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Lleida. Víctimes De La Repressió Franquista",
    "label": "Cementiri De Lleida. Víctimes De La Repressió Franquista",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Lleida. Víctimes De La Repressió Franquista",
    "label": "Cementiri De Lleida. Víctimes De La Repressió Franquista",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Lloret De Mar. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Lloret De Mar. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Lloret De Mar. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Lloret De Mar. Traslladada Al Valle De Los Caídos.",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Lloret De Mar. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Lloret De Mar. Traslladada Al Valle De Los Caídos.",
    "location": "Lloret de Mar"
  },
  {
    "node": "Cementiri De Maials",
    "label": "Cementiri De Maials",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Maials",
    "label": "Cementiri De Maials",
    "location": "Maials"
  },
  {
    "node": "Cementiri De Manresa",
    "label": "Cementiri De Manresa",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Manresa",
    "label": "Cementiri De Manresa",
    "location": "Manresa"
  },
  {
    "node": "Cementiri De Martorell. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Martorell. Traslladada Al Valle De Los Caídos",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Martorell. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Martorell. Traslladada Al Valle De Los Caídos",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Martorell. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Martorell. Traslladada Al Valle De Los Caídos",
    "location": "Martorell"
  },
  {
    "node": "Cementiri De Masdenverge",
    "label": "Cementiri De Masdenverge",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Masdenverge",
    "label": "Cementiri De Masdenverge",
    "location": "Masdenverge"
  },
  {
    "node": "Cementiri De Monistrol De Montserrat. Fossa De Soldats Republicans",
    "label": "Cementiri De Monistrol De Montserrat. Fossa De Soldats Republicans",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Monistrol De Montserrat. Fossa De Soldats Republicans",
    "label": "Cementiri De Monistrol De Montserrat. Fossa De Soldats Republicans",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Monistrol De Montserrat. Fossa De Soldats Republicans",
    "label": "Cementiri De Monistrol De Montserrat. Fossa De Soldats Republicans",
    "location": "Monistrol de Montserrat"
  },
  {
    "node": "Cementiri De Monistrol De Montserrat. Víctimes De La Violència A La Rereguarda",
    "label": "Cementiri De Monistrol De Montserrat. Víctimes De La Violència A La Rereguarda",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Monistrol De Montserrat. Víctimes De La Violència A La Rereguarda",
    "label": "Cementiri De Monistrol De Montserrat. Víctimes De La Violència A La Rereguarda",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Monistrol De Montserrat. Víctimes De La Violència A La Rereguarda",
    "label": "Cementiri De Monistrol De Montserrat. Víctimes De La Violència A La Rereguarda",
    "location": "Monistrol de Montserrat"
  },
  {
    "node": "Cementiri De Mont-roig",
    "label": "Cementiri De Mont-roig",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Mont-roig",
    "label": "Cementiri De Mont-roig",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Mont-roig",
    "label": "Cementiri De Mont-roig",
    "location": "Els Plans de Sió"
  },
  {
    "node": "Cementiri De Montblanc. Fossa De Soldats Republicans",
    "label": "Cementiri De Montblanc. Fossa De Soldats Republicans",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De Montblanc. Fossa De Soldats Republicans",
    "label": "Cementiri De Montblanc. Fossa De Soldats Republicans",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Montblanc. Fossa De Soldats Republicans",
    "label": "Cementiri De Montblanc. Fossa De Soldats Republicans",
    "location": "Montblanc"
  },
  {
    "node": "Cementiri De Montferrer (Camp De Treball)",
    "label": "Cementiri De Montferrer (Camp De Treball)",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Montferrer (Camp De Treball)",
    "label": "Cementiri De Montferrer (Camp De Treball)",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Montferrer (Camp De Treball)",
    "label": "Cementiri De Montferrer (Camp De Treball)",
    "location": "Montferrer i Castellbò"
  },
  {
    "node": "Cementiri De Montgai",
    "label": "Cementiri De Montgai",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Montgai",
    "label": "Cementiri De Montgai",
    "location": "Montgai"
  },
  {
    "node": "Cementiri De Montjuïc. Fossar De La Pedrera",
    "label": "Cementiri De Montjuïc. Fossar De La Pedrera",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Montjuïc. Fossar De La Pedrera",
    "label": "Cementiri De Montjuïc. Fossar De La Pedrera",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Móra D'ebre",
    "label": "Cementiri De Móra D'ebre",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Móra D'ebre",
    "label": "Cementiri De Móra D'ebre",
    "location": "Móra d'Ebre"
  },
  {
    "node": "Cementiri De Pardines. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Pardines. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Pardines. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Pardines. Traslladada Al Valle De Los Caídos.",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Pardines. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Pardines. Traslladada Al Valle De Los Caídos.",
    "location": "Pardines"
  },
  {
    "node": "Cementiri De Poboleda",
    "label": "Cementiri De Poboleda",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Poboleda",
    "label": "Cementiri De Poboleda",
    "location": "Poboleda"
  },
  {
    "node": "Cementiri De Ponts. Repressió A La Rereguarda.",
    "label": "Cementiri De Ponts. Repressió A La Rereguarda.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Ponts. Repressió A La Rereguarda.",
    "label": "Cementiri De Ponts. Repressió A La Rereguarda.",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Ponts. Repressió A La Rereguarda.",
    "label": "Cementiri De Ponts. Repressió A La Rereguarda.",
    "location": "Ponts"
  },
  {
    "node": "Cementiri De Prats De Rei",
    "label": "Cementiri De Prats De Rei",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Prats De Rei",
    "label": "Cementiri De Prats De Rei",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Prats De Rei",
    "label": "Cementiri De Prats De Rei",
    "location": "Els Prats de Rei"
  },
  {
    "node": "Cementiri De Preixens",
    "label": "Cementiri De Preixens",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Preixens",
    "label": "Cementiri De Preixens",
    "location": "Preixens"
  },
  {
    "node": "Cementiri De Puigdelfí. Fossa De Soldats Republicans.",
    "label": "Cementiri De Puigdelfí. Fossa De Soldats Republicans.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Puigdelfí. Fossa De Soldats Republicans.",
    "label": "Cementiri De Puigdelfí. Fossa De Soldats Republicans.",
    "location": "Puigdelfí"
  },
  {
    "node": "Cementiri De Queixans. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Queixans. Traslladada Al Valle De Los Caídos",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Queixans. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Queixans. Traslladada Al Valle De Los Caídos",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Queixans. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Queixans. Traslladada Al Valle De Los Caídos",
    "location": "Fontanals de Cerdanya"
  },
  {
    "node": "Cementiri De Reus. Cipriano Martos",
    "label": "Cementiri De Reus. Cipriano Martos",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Reus. Cipriano Martos",
    "label": "Cementiri De Reus. Cipriano Martos",
    "location": "Reus"
  },
  {
    "node": "Cementiri De Reus. Fossa Històrica 5.",
    "label": "Cementiri De Reus. Fossa Històrica 5.",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De Reus. Fossa Històrica 5.",
    "label": "Cementiri De Reus. Fossa Històrica 5.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Reus. Fossa Històrica 5.",
    "label": "Cementiri De Reus. Fossa Històrica 5.",
    "location": "Reus"
  },
  {
    "node": "Cementiri De Reus. Soldats Republicans I Civils.",
    "label": "Cementiri De Reus. Soldats Republicans I Civils.",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De Reus. Soldats Republicans I Civils.",
    "label": "Cementiri De Reus. Soldats Republicans I Civils.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Reus. Soldats Republicans I Civils.",
    "label": "Cementiri De Reus. Soldats Republicans I Civils.",
    "location": "Reus"
  },
  {
    "node": "Cementiri De Rialp (I)",
    "label": "Cementiri De Rialp (I)",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Rialp (I)",
    "label": "Cementiri De Rialp (I)",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Rialp (I)",
    "label": "Cementiri De Rialp (I)",
    "location": "Rialp"
  },
  {
    "node": "Cementiri De Riner",
    "label": "Cementiri De Riner",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Riner",
    "label": "Cementiri De Riner",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Riner",
    "label": "Cementiri De Riner",
    "location": "Riner"
  },
  {
    "node": "Cementiri De Ripoll. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Ripoll. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Ripoll. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Ripoll. Traslladada Al Valle De Los Caídos.",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Ripoll. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Ripoll. Traslladada Al Valle De Los Caídos.",
    "location": "Ripoll"
  },
  {
    "node": "Cementiri De Rocafort De Queralt. Fossa Dels Soldats Franquistes",
    "label": "Cementiri De Rocafort De Queralt. Fossa Dels Soldats Franquistes",
    "location": "Rocafort de Queralt"
  },
  {
    "node": "Cementiri De Rocafort De Queralt. Fossa Dels Soldats Franquistes",
    "label": "Cementiri De Rocafort De Queralt. Fossa Dels Soldats Franquistes",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Roda De Ter",
    "label": "Cementiri De Roda De Ter",
    "location": "Catalunya"
  },
  {
    "node": "Cementiri De Roda De Ter",
    "label": "Cementiri De Roda De Ter",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Roda De Ter",
    "label": "Cementiri De Roda De Ter",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Roda De Ter",
    "label": "Cementiri De Roda De Ter",
    "location": "Roda de Ter"
  },
  {
    "node": "Cementiri De Roda De Ter",
    "label": "Cementiri De Roda De Ter",
    "location": "Osona"
  },
  {
    "node": "Cementiri De Sant Boi De Llobregat. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Boi De Llobregat. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Boi De Llobregat. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Boi De Llobregat. Traslladada Al Valle De Los Caídos.",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Sant Boi De Llobregat. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Boi De Llobregat. Traslladada Al Valle De Los Caídos.",
    "location": "Sant Boi de Llobregat"
  },
  {
    "node": "Cementiri De Sant Domí",
    "label": "Cementiri De Sant Domí",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Domí",
    "label": "Cementiri De Sant Domí",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Sant Domí",
    "label": "Cementiri De Sant Domí",
    "location": "Sant Guim de Freixenet"
  },
  {
    "node": "Cementiri De Sant Feliu De Codines. Fossa De Guillermo Ganuza",
    "label": "Cementiri De Sant Feliu De Codines. Fossa De Guillermo Ganuza",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Sant Feliu De Codines. Fossa De Guillermo Ganuza",
    "label": "Cementiri De Sant Feliu De Codines. Fossa De Guillermo Ganuza",
    "location": "Sant Feliu de Codines"
  },
  {
    "node": "Cementiri De Sant Feliu De Guíxols. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Feliu De Guíxols. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Feliu De Guíxols. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Feliu De Guíxols. Traslladada Al Valle De Los Caídos.",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Sant Feliu De Guíxols. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Feliu De Guíxols. Traslladada Al Valle De Los Caídos.",
    "location": "Sant Feliu de Guíxols"
  },
  {
    "node": "Cementiri De Sant Feliu De Llobregat. Mausoleu Dels 14 Del Canyet",
    "label": "Cementiri De Sant Feliu De Llobregat. Mausoleu Dels 14 Del Canyet",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Feliu De Llobregat. Mausoleu Dels 14 Del Canyet",
    "label": "Cementiri De Sant Feliu De Llobregat. Mausoleu Dels 14 Del Canyet",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Sant Feliu De Llobregat. Mausoleu Dels 14 Del Canyet",
    "label": "Cementiri De Sant Feliu De Llobregat. Mausoleu Dels 14 Del Canyet",
    "location": "Sant Feliu de Llobregat"
  },
  {
    "node": "Cementiri De Sant Gregori. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Sant Gregori. Traslladada Al Valle De Cuelgamuros",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Gregori. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Sant Gregori. Traslladada Al Valle De Cuelgamuros",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Sant Gregori. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Sant Gregori. Traslladada Al Valle De Cuelgamuros",
    "location": "Sant Gregori"
  },
  {
    "node": "Cementiri De Sant Hilari Sacalm",
    "label": "Cementiri De Sant Hilari Sacalm",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Hilari Sacalm",
    "label": "Cementiri De Sant Hilari Sacalm",
    "location": "Sant Hilari Sacalm"
  },
  {
    "node": "Cementiri De Sant Joan De Vilatorrada",
    "label": "Cementiri De Sant Joan De Vilatorrada",
    "location": "Sant Joan de Vilatorrada"
  },
  {
    "node": "Cementiri De Sant Joan Despí",
    "label": "Cementiri De Sant Joan Despí",
    "location": "Catalunya"
  },
  {
    "node": "Cementiri De Sant Joan Despí",
    "label": "Cementiri De Sant Joan Despí",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Joan Despí",
    "label": "Cementiri De Sant Joan Despí",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Sant Joan Despí",
    "label": "Cementiri De Sant Joan Despí",
    "location": "Sant Joan Despí"
  },
  {
    "node": "Cementiri De Sant Joan Despí",
    "label": "Cementiri De Sant Joan Despí",
    "location": "Baix Llobregat"
  },
  {
    "node": "Cementiri De Sant Llorenç De Morunys",
    "label": "Cementiri De Sant Llorenç De Morunys",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Llorenç De Morunys",
    "label": "Cementiri De Sant Llorenç De Morunys",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Sant Llorenç De Morunys",
    "label": "Cementiri De Sant Llorenç De Morunys",
    "location": "Sant Llorenç de Morunys"
  },
  {
    "node": "Cementiri De Sant Martí De Merlès",
    "label": "Cementiri De Sant Martí De Merlès",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Sant Martí De Merlès",
    "label": "Cementiri De Sant Martí De Merlès",
    "location": "Sant Martí de Merlès"
  },
  {
    "node": "Cementiri De Sant Martí Del Brull",
    "label": "Cementiri De Sant Martí Del Brull",
    "location": "El Brull"
  },
  {
    "node": "Cementiri De Sant Miquel De Campmajor. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Miquel De Campmajor. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Miquel De Campmajor. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Miquel De Campmajor. Traslladada Al Valle De Los Caídos.",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Sant Miquel De Campmajor. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Miquel De Campmajor. Traslladada Al Valle De Los Caídos.",
    "location": "Sant Miquel de Campmajor"
  },
  {
    "node": "Cementiri De Sant Pere De Ribes",
    "label": "Cementiri De Sant Pere De Ribes",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Pere De Ribes",
    "label": "Cementiri De Sant Pere De Ribes",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Sant Pere De Ribes",
    "label": "Cementiri De Sant Pere De Ribes",
    "location": "Sant Pere de Ribes"
  },
  {
    "node": "Cementiri De Sant Quintí De Mediona",
    "label": "Cementiri De Sant Quintí De Mediona",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Quintí De Mediona",
    "label": "Cementiri De Sant Quintí De Mediona",
    "location": "Sant Quintí de Mediona"
  },
  {
    "node": "Cementiri De Sant Quintí De Mediona. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Quintí De Mediona. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Quintí De Mediona. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Quintí De Mediona. Traslladada Al Valle De Los Caídos.",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Sant Quintí De Mediona. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Quintí De Mediona. Traslladada Al Valle De Los Caídos.",
    "location": "Sant Quintí de Mediona"
  },
  {
    "node": "Cementiri De Sant Sebastià. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Sebastià. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sant Sebastià. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Sebastià. Traslladada Al Valle De Los Caídos.",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Sant Sebastià. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Sant Sebastià. Traslladada Al Valle De Los Caídos.",
    "location": "Sitges"
  },
  {
    "node": "Cementiri De Santa Bàrbara",
    "label": "Cementiri De Santa Bàrbara",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Santa Bàrbara",
    "label": "Cementiri De Santa Bàrbara",
    "location": "Santa Bàrbara"
  },
  {
    "node": "Cementiri De Santa Coloma De Farners",
    "label": "Cementiri De Santa Coloma De Farners",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Santa Coloma De Farners",
    "label": "Cementiri De Santa Coloma De Farners",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Santa Coloma De Farners",
    "label": "Cementiri De Santa Coloma De Farners",
    "location": "Santa Coloma de Farners"
  },
  {
    "node": "Cementiri De Santa Susanna",
    "label": "Cementiri De Santa Susanna",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Santa Susanna",
    "label": "Cementiri De Santa Susanna",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Santa Susanna",
    "label": "Cementiri De Santa Susanna",
    "location": "Riner"
  },
  {
    "node": "Cementiri De Sarrià De Ter. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Sarrià De Ter. Traslladada Al Valle De Cuelgamuros",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sarrià De Ter. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Sarrià De Ter. Traslladada Al Valle De Cuelgamuros",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Sarrià De Ter. Traslladada Al Valle De Cuelgamuros",
    "label": "Cementiri De Sarrià De Ter. Traslladada Al Valle De Cuelgamuros",
    "location": "Sarrià de Ter"
  },
  {
    "node": "Cementiri De Sedó",
    "label": "Cementiri De Sedó",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sedó",
    "label": "Cementiri De Sedó",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Sedó",
    "label": "Cementiri De Sedó",
    "location": "Torrefeta i Florejacs"
  },
  {
    "node": "Cementiri De Sedó II",
    "label": "Cementiri De Sedó II",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sedó II",
    "label": "Cementiri De Sedó II",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Sedó II",
    "label": "Cementiri De Sedó II",
    "location": "Torrefeta"
  },
  {
    "node": "Cementiri De Sils",
    "label": "Cementiri De Sils",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sils",
    "label": "Cementiri De Sils",
    "location": "Sils"
  },
  {
    "node": "Cementiri De Sisteró Pelagalls II",
    "label": "Cementiri De Sisteró Pelagalls II",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Sisteró Pelagalls II",
    "label": "Cementiri De Sisteró Pelagalls II",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Sisteró Pelagalls II",
    "label": "Cementiri De Sisteró Pelagalls II",
    "location": "Els Plans de Sió"
  },
  {
    "node": "Cementiri De Tarragona. Fossa 1 Repressió Franquista.",
    "label": "Cementiri De Tarragona. Fossa 1 Repressió Franquista.",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De Tarragona. Fossa 1 Repressió Franquista.",
    "label": "Cementiri De Tarragona. Fossa 1 Repressió Franquista.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Tarragona. Fossa 2 Repressió Franquista",
    "label": "Cementiri De Tarragona. Fossa 2 Repressió Franquista",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De Tarragona. Fossa 2 Repressió Franquista",
    "label": "Cementiri De Tarragona. Fossa 2 Repressió Franquista",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Tarragona. Fossa Del Cementiri Neutre. Víctimes De La Repressió Franquista.",
    "label": "Cementiri De Tarragona. Fossa Del Cementiri Neutre. Víctimes De La Repressió Franquista.",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De Tarragona. Fossa Del Cementiri Neutre. Víctimes De La Repressió Franquista.",
    "label": "Cementiri De Tarragona. Fossa Del Cementiri Neutre. Víctimes De La Repressió Franquista.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Tarroja De Segarra",
    "label": "Cementiri De Tarroja De Segarra",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Tarroja De Segarra",
    "label": "Cementiri De Tarroja De Segarra",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Tarroja De Segarra",
    "label": "Cementiri De Tarroja De Segarra",
    "location": "Tarroja de Segarra"
  },
  {
    "node": "Cementiri De Tarrés",
    "label": "Cementiri De Tarrés",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Tarrés",
    "label": "Cementiri De Tarrés",
    "location": "Tarrés"
  },
  {
    "node": "Cementiri De Terrades. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Terrades. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Terrades. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Terrades. Traslladada Al Valle De Los Caídos.",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Terrades. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Terrades. Traslladada Al Valle De Los Caídos.",
    "location": "Terrades"
  },
  {
    "node": "Cementiri De Torrebesses",
    "label": "Cementiri De Torrebesses",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Torrebesses",
    "label": "Cementiri De Torrebesses",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Torrebesses",
    "label": "Cementiri De Torrebesses",
    "location": "Torrebesses"
  },
  {
    "node": "Cementiri De Torà",
    "label": "Cementiri De Torà",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Torà",
    "label": "Cementiri De Torà",
    "location": "Torà"
  },
  {
    "node": "Cementiri De Toses. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Toses. Traslladada Al Valle De Los Caídos",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Toses. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Toses. Traslladada Al Valle De Los Caídos",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Toses. Traslladada Al Valle De Los Caídos",
    "label": "Cementiri De Toses. Traslladada Al Valle De Los Caídos",
    "location": "Toses"
  },
  {
    "node": "Cementiri De Tírvia",
    "label": "Cementiri De Tírvia",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Tírvia",
    "label": "Cementiri De Tírvia",
    "location": "Tírvia"
  },
  {
    "node": "Cementiri De Vallverd",
    "label": "Cementiri De Vallverd",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Vallverd",
    "label": "Cementiri De Vallverd",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Vallverd",
    "label": "Cementiri De Vallverd",
    "location": "Ivars D'Urgell"
  },
  {
    "node": "Cementiri De Vila-Rodona. Repressió A La Reraguarda",
    "label": "Cementiri De Vila-Rodona. Repressió A La Reraguarda",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri De Vila-Rodona. Repressió A La Reraguarda",
    "label": "Cementiri De Vila-Rodona. Repressió A La Reraguarda",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Vila-Rodona. Repressió A La Reraguarda",
    "label": "Cementiri De Vila-Rodona. Repressió A La Reraguarda",
    "location": "Vila-rodona"
  },
  {
    "node": "Cementiri De Vilac",
    "label": "Cementiri De Vilac",
    "location": "Vielha e Mijaran"
  },
  {
    "node": "Cementiri De Vilademuls. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Vilademuls. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Vilademuls. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Vilademuls. Traslladada Al Valle De Los Caídos.",
    "location": "Girona"
  },
  {
    "node": "Cementiri De Vilademuls. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Vilademuls. Traslladada Al Valle De Los Caídos.",
    "location": "Vilademuls"
  },
  {
    "node": "Cementiri De Viladrau. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Viladrau. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Viladrau. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Viladrau. Traslladada Al Valle De Los Caídos.",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri De Viladrau. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Viladrau. Traslladada Al Valle De Los Caídos.",
    "location": "Viladrau"
  },
  {
    "node": "Cementiri De Vilafranca Del Penedès",
    "label": "Cementiri De Vilafranca Del Penedès",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Vilafranca Del Penedès",
    "label": "Cementiri De Vilafranca Del Penedès",
    "location": "Vilafranca del Penedès"
  },
  {
    "node": "Cementiri De Vilalba Dels Arcs. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Vilalba Dels Arcs. Traslladada Al Valle De Los Caídos.",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Vilalba Dels Arcs. Traslladada Al Valle De Los Caídos.",
    "label": "Cementiri De Vilalba Dels Arcs. Traslladada Al Valle De Los Caídos.",
    "location": "Vilalba dels Arcs"
  },
  {
    "node": "Cementiri De Vilamur",
    "label": "Cementiri De Vilamur",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Vilamur",
    "label": "Cementiri De Vilamur",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Vilamur",
    "label": "Cementiri De Vilamur",
    "location": "Vilamur"
  },
  {
    "node": "Cementiri De Vilanova De Bellpuig",
    "label": "Cementiri De Vilanova De Bellpuig",
    "location": "Spain"
  },
  {
    "node": "Cementiri De Vilanova De Bellpuig",
    "label": "Cementiri De Vilanova De Bellpuig",
    "location": "Lleida"
  },
  {
    "node": "Cementiri De Vilanova De Bellpuig",
    "label": "Cementiri De Vilanova De Bellpuig",
    "location": "Vilanova De Bellpuig"
  },
  {
    "node": "Cementiri Del Catllar. Repressió De Reraguarda.",
    "label": "Cementiri Del Catllar. Repressió De Reraguarda.",
    "location": "Spain"
  },
  {
    "node": "Cementiri Del Catllar. Repressió De Reraguarda.",
    "label": "Cementiri Del Catllar. Repressió De Reraguarda.",
    "location": "El Catllar"
  },
  {
    "node": "Cementiri Del Catllar. Soldat De L'exèrcit Popular De La República",
    "label": "Cementiri Del Catllar. Soldat De L'exèrcit Popular De La República",
    "location": "Spain"
  },
  {
    "node": "Cementiri Del Catllar. Soldat De L'exèrcit Popular De La República",
    "label": "Cementiri Del Catllar. Soldat De L'exèrcit Popular De La República",
    "location": "El Catllar"
  },
  {
    "node": "Cementiri Del Llor",
    "label": "Cementiri Del Llor",
    "location": "Spain"
  },
  {
    "node": "Cementiri Del Llor",
    "label": "Cementiri Del Llor",
    "location": "Lleida"
  },
  {
    "node": "Cementiri Del Llor",
    "label": "Cementiri Del Llor",
    "location": "Torrefeta"
  },
  {
    "node": "Cementiri Del Palau D'Anglesola",
    "label": "Cementiri Del Palau D'Anglesola",
    "location": "Spain"
  },
  {
    "node": "Cementiri Del Palau D'Anglesola",
    "label": "Cementiri Del Palau D'Anglesola",
    "location": "Lleida"
  },
  {
    "node": "Cementiri Del Palau D'Anglesola",
    "label": "Cementiri Del Palau D'Anglesola",
    "location": "El Palau D'Anglesola"
  },
  {
    "node": "Cementiri Del Perelló",
    "label": "Cementiri Del Perelló",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri Del Perelló",
    "label": "Cementiri Del Perelló",
    "location": "Catalunya"
  },
  {
    "node": "Cementiri Del Perelló",
    "label": "Cementiri Del Perelló",
    "location": "Spain"
  },
  {
    "node": "Cementiri Del Perelló",
    "label": "Cementiri Del Perelló",
    "location": "Baix Ebre"
  },
  {
    "node": "Cementiri Del Perelló",
    "label": "Cementiri Del Perelló",
    "location": "El Perelló"
  },
  {
    "node": "Cementiri Del Talladell",
    "label": "Cementiri Del Talladell",
    "location": "Spain"
  },
  {
    "node": "Cementiri Del Talladell",
    "label": "Cementiri Del Talladell",
    "location": "Tàrrega"
  },
  {
    "node": "Cementiri Dels Guiamets",
    "label": "Cementiri Dels Guiamets",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri Dels Guiamets",
    "label": "Cementiri Dels Guiamets",
    "location": "Spain"
  },
  {
    "node": "Cementiri Dels Guiamets",
    "label": "Cementiri Dels Guiamets",
    "location": "Els Guiamets"
  },
  {
    "node": "Cementiri Dels Reguers",
    "label": "Cementiri Dels Reguers",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri Dels Reguers",
    "label": "Cementiri Dels Reguers",
    "location": "Spain"
  },
  {
    "node": "Cementiri Dels Reguers",
    "label": "Cementiri Dels Reguers",
    "location": "Tortosa"
  },
  {
    "node": "Cementiri Dels Reguers II",
    "label": "Cementiri Dels Reguers II",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri Dels Reguers II",
    "label": "Cementiri Dels Reguers II",
    "location": "Spain"
  },
  {
    "node": "Cementiri Dels Reguers II",
    "label": "Cementiri Dels Reguers II",
    "location": "Els Reguers"
  },
  {
    "node": "Cementiri El Molar",
    "label": "Cementiri El Molar",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri El Molar",
    "label": "Cementiri El Molar",
    "location": "Spain"
  },
  {
    "node": "Cementiri El Molar",
    "label": "Cementiri El Molar",
    "location": "El Molar"
  },
  {
    "node": "Cementiri Nou del Soleràs",
    "label": "Cementiri Nou del Soleràs",
    "location": "Spain"
  },
  {
    "node": "Cementiri Nou del Soleràs",
    "label": "Cementiri Nou del Soleràs",
    "location": "El Soleràs"
  },
  {
    "node": "Cementiri Roní (I)",
    "label": "Cementiri Roní (I)",
    "location": "Spain"
  },
  {
    "node": "Cementiri Roní (I)",
    "label": "Cementiri Roní (I)",
    "location": "Lleida"
  },
  {
    "node": "Cementiri Roní (I)",
    "label": "Cementiri Roní (I)",
    "location": "Rialp"
  },
  {
    "node": "Cementiri Sant Sadurní D'Anoia. Soldats Franquistes",
    "label": "Cementiri Sant Sadurní D'Anoia. Soldats Franquistes",
    "location": "Spain"
  },
  {
    "node": "Cementiri Sant Sadurní D'Anoia. Soldats Franquistes",
    "label": "Cementiri Sant Sadurní D'Anoia. Soldats Franquistes",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri Sant Sadurní D'Anoia. Soldats Franquistes",
    "label": "Cementiri Sant Sadurní D'Anoia. Soldats Franquistes",
    "location": "Sant Sadurní d'Anoia"
  },
  {
    "node": "Cementiri Vell D'Abrera",
    "label": "Cementiri Vell D'Abrera",
    "location": "Spain"
  },
  {
    "node": "Cementiri Vell D'Abrera",
    "label": "Cementiri Vell D'Abrera",
    "location": "Abrera"
  },
  {
    "node": "Cementiri Vell D'albinyana",
    "label": "Cementiri Vell D'albinyana",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri Vell D'albinyana",
    "label": "Cementiri Vell D'albinyana",
    "location": "Catalunya"
  },
  {
    "node": "Cementiri Vell D'albinyana",
    "label": "Cementiri Vell D'albinyana",
    "location": "Spain"
  },
  {
    "node": "Cementiri Vell D'albinyana",
    "label": "Cementiri Vell D'albinyana",
    "location": "Albinyana"
  },
  {
    "node": "Cementiri Vell D'albinyana",
    "label": "Cementiri Vell D'albinyana",
    "location": "Baix Penedès"
  },
  {
    "node": "Cementiri Vell Del Soleràs",
    "label": "Cementiri Vell Del Soleràs",
    "location": "Catalunya"
  },
  {
    "node": "Cementiri Vell Del Soleràs",
    "label": "Cementiri Vell Del Soleràs",
    "location": "Spain"
  },
  {
    "node": "Cementiri Vell Del Soleràs",
    "label": "Cementiri Vell Del Soleràs",
    "location": "Lleida"
  },
  {
    "node": "Cementiri Vell Del Soleràs",
    "label": "Cementiri Vell Del Soleràs",
    "location": "El Soleràs"
  },
  {
    "node": "Cementiri Vell Del Soleràs",
    "label": "Cementiri Vell Del Soleràs",
    "location": "Garrigues"
  },
  {
    "node": "Cementiri d'Ainet de Besan",
    "label": "Cementiri d'Ainet de Besan",
    "location": "Spain"
  },
  {
    "node": "Cementiri d'Ainet de Besan",
    "label": "Cementiri d'Ainet de Besan",
    "location": "Alins"
  },
  {
    "node": "Cementiri d'Alins",
    "label": "Cementiri d'Alins",
    "location": "Spain"
  },
  {
    "node": "Cementiri d'Alins",
    "label": "Cementiri d'Alins",
    "location": "Lleida"
  },
  {
    "node": "Cementiri d'Alins",
    "label": "Cementiri d'Alins",
    "location": "Alins"
  },
  {
    "node": "Cementiri d'Alta-Riba II",
    "label": "Cementiri d'Alta-Riba II",
    "location": "Estaràs"
  },
  {
    "node": "Cementiri d'Altafulla. Fossa de soldats republicans",
    "label": "Cementiri d'Altafulla. Fossa de soldats republicans",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri d'Altafulla. Fossa de soldats republicans",
    "label": "Cementiri d'Altafulla. Fossa de soldats republicans",
    "location": "Spain"
  },
  {
    "node": "Cementiri d'Altafulla. Fossa de soldats republicans",
    "label": "Cementiri d'Altafulla. Fossa de soldats republicans",
    "location": "Altafulla"
  },
  {
    "node": "Cementiri d'Alòs de Balaguer. Tomba de Josep Gou Marsà",
    "label": "Cementiri d'Alòs de Balaguer. Tomba de Josep Gou Marsà",
    "location": "Spain"
  },
  {
    "node": "Cementiri d'Alòs de Balaguer. Tomba de Josep Gou Marsà",
    "label": "Cementiri d'Alòs de Balaguer. Tomba de Josep Gou Marsà",
    "location": "Lleida"
  },
  {
    "node": "Cementiri d'Alòs de Balaguer. Tomba de Josep Gou Marsà",
    "label": "Cementiri d'Alòs de Balaguer. Tomba de Josep Gou Marsà",
    "location": "Alòs de Balaguer"
  },
  {
    "node": "Cementiri d'Ogern. Víctimes del Camp de Treball núm. 5 del SIM",
    "label": "Cementiri d'Ogern. Víctimes del Camp de Treball núm. 5 del SIM",
    "location": "Ogern"
  },
  {
    "node": "Cementiri d'Ulldemolins",
    "label": "Cementiri d'Ulldemolins",
    "location": "Ulldemolins"
  },
  {
    "node": "Cementiri d'Àreu",
    "label": "Cementiri d'Àreu",
    "location": null
  },
  {
    "node": "Cementiri de Biure de Gaià. Fossa d'un soldat republicà.",
    "label": "Cementiri de Biure de Gaià. Fossa d'un soldat republicà.",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Biure de Gaià. Fossa d'un soldat republicà.",
    "label": "Cementiri de Biure de Gaià. Fossa d'un soldat republicà.",
    "location": "Biure de Gaià"
  },
  {
    "node": "Cementiri de Bolvir. Traslladada al Valle de los Caídos",
    "label": "Cementiri de Bolvir. Traslladada al Valle de los Caídos",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Bolvir. Traslladada al Valle de los Caídos",
    "label": "Cementiri de Bolvir. Traslladada al Valle de los Caídos",
    "location": "Girona"
  },
  {
    "node": "Cementiri de Bolvir. Traslladada al Valle de los Caídos",
    "label": "Cementiri de Bolvir. Traslladada al Valle de los Caídos",
    "location": "Bolvir"
  },
  {
    "node": "Cementiri de Capçanes",
    "label": "Cementiri de Capçanes",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Capçanes",
    "label": "Cementiri de Capçanes",
    "location": "Capçanes"
  },
  {
    "node": "Cementiri de Castellnou de Bages",
    "label": "Cementiri de Castellnou de Bages",
    "location": "Castellnou de Bages"
  },
  {
    "node": "Cementiri de Collbató",
    "label": "Cementiri de Collbató",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de Collbató",
    "label": "Cementiri de Collbató",
    "location": "Collbató"
  },
  {
    "node": "Cementiri de Cornellà de Llobregat. Traslladada al Valle de los Caídos",
    "label": "Cementiri de Cornellà de Llobregat. Traslladada al Valle de los Caídos",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Cornellà de Llobregat. Traslladada al Valle de los Caídos",
    "label": "Cementiri de Cornellà de Llobregat. Traslladada al Valle de los Caídos",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de Cornellà de Llobregat. Traslladada al Valle de los Caídos",
    "label": "Cementiri de Cornellà de Llobregat. Traslladada al Valle de los Caídos",
    "location": "Cornellà de Llobregat"
  },
  {
    "node": "Cementiri de Cornudella de Montsant",
    "label": "Cementiri de Cornudella de Montsant",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri de Cornudella de Montsant",
    "label": "Cementiri de Cornudella de Montsant",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Cornudella de Montsant",
    "label": "Cementiri de Cornudella de Montsant",
    "location": "Cornudella de Montsant"
  },
  {
    "node": "Cementiri de Darmós",
    "label": "Cementiri de Darmós",
    "location": "Darmós"
  },
  {
    "node": "Cementiri de Girona",
    "label": "Cementiri de Girona",
    "location": "Girona"
  },
  {
    "node": "Cementiri de Gra",
    "label": "Cementiri de Gra",
    "location": "Torrefeta"
  },
  {
    "node": "Cementiri de Guissona II",
    "label": "Cementiri de Guissona II",
    "location": "Guissona"
  },
  {
    "node": "Cementiri de Lleida. Departament de Sant Miquel. Traslladada al Valle de Cuelgamuros",
    "label": "Cementiri de Lleida. Departament de Sant Miquel. Traslladada al Valle de Cuelgamuros",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Lleida. Departament de Sant Miquel. Traslladada al Valle de Cuelgamuros",
    "label": "Cementiri de Lleida. Departament de Sant Miquel. Traslladada al Valle de Cuelgamuros",
    "location": "Lleida"
  },
  {
    "node": "Cementiri de Llessui",
    "label": "Cementiri de Llessui",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Llessui",
    "label": "Cementiri de Llessui",
    "location": "Llessui"
  },
  {
    "node": "Cementiri de Marçà",
    "label": "Cementiri de Marçà",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Marçà",
    "label": "Cementiri de Marçà",
    "location": "Marçà"
  },
  {
    "node": "Cementiri de Moià",
    "label": "Cementiri de Moià",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Moià",
    "label": "Cementiri de Moià",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de Moià",
    "label": "Cementiri de Moià",
    "location": "Moià"
  },
  {
    "node": "Cementiri de Montjuïc. Víctimes de bombardeig de la Barceloneta",
    "label": "Cementiri de Montjuïc. Víctimes de bombardeig de la Barceloneta",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Montjuïc. Víctimes de bombardeig de la Barceloneta",
    "label": "Cementiri de Montjuïc. Víctimes de bombardeig de la Barceloneta",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de Montmaneu",
    "label": "Cementiri de Montmaneu",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Montmaneu",
    "label": "Cementiri de Montmaneu",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de Montmaneu",
    "label": "Cementiri de Montmaneu",
    "location": "Montmaneu"
  },
  {
    "node": "Cementiri de Polinyà",
    "label": "Cementiri de Polinyà",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Polinyà",
    "label": "Cementiri de Polinyà",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de Polinyà",
    "label": "Cementiri de Polinyà",
    "location": "Polinyà"
  },
  {
    "node": "Cementiri de Pontons",
    "label": "Cementiri de Pontons",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Pontons",
    "label": "Cementiri de Pontons",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de Pontons",
    "label": "Cementiri de Pontons",
    "location": "Pontons"
  },
  {
    "node": "Cementiri de Pradell de la Teixeta",
    "label": "Cementiri de Pradell de la Teixeta",
    "location": "Pradell de la Teixeta"
  },
  {
    "node": "Cementiri de Prades. Soldats del Cos d’Exèrcit Marroquí",
    "label": "Cementiri de Prades. Soldats del Cos d’Exèrcit Marroquí",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri de Prades. Soldats del Cos d’Exèrcit Marroquí",
    "label": "Cementiri de Prades. Soldats del Cos d’Exèrcit Marroquí",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Prades. Soldats del Cos d’Exèrcit Marroquí",
    "label": "Cementiri de Prades. Soldats del Cos d’Exèrcit Marroquí",
    "location": "Prades"
  },
  {
    "node": "Cementiri de Rocafort de Queralt. Fossa de soldats republicans.",
    "label": "Cementiri de Rocafort de Queralt. Fossa de soldats republicans.",
    "location": "Rocafort de Queralt"
  },
  {
    "node": "Cementiri de Rocafort de Queralt. Fossa de soldats republicans.",
    "label": "Cementiri de Rocafort de Queralt. Fossa de soldats republicans.",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Sant Guim de Freixenet",
    "label": "Cementiri de Sant Guim de Freixenet",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Sant Guim de Freixenet",
    "label": "Cementiri de Sant Guim de Freixenet",
    "location": "Sant Guim de Freixenet"
  },
  {
    "node": "Cementiri de Sant Guim de Freixenet II",
    "label": "Cementiri de Sant Guim de Freixenet II",
    "location": "Sant Guim de Freixenet"
  },
  {
    "node": "Cementiri de Sant Julià de Ramis. Traslladada al Valle de Cuelgamuros",
    "label": "Cementiri de Sant Julià de Ramis. Traslladada al Valle de Cuelgamuros",
    "location": "Sant Julià de Ramis"
  },
  {
    "node": "Cementiri de Sant Martí de Tous",
    "label": "Cementiri de Sant Martí de Tous",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Sant Martí de Tous",
    "label": "Cementiri de Sant Martí de Tous",
    "location": "Sant Martí de Tous"
  },
  {
    "node": "Cementiri de Sant Mateu de Bages",
    "label": "Cementiri de Sant Mateu de Bages",
    "location": "Sant Mateu de Bages"
  },
  {
    "node": "Cementiri de Sant Pere de Riudebitlles. Traslladada al Valle de los Caídos",
    "label": "Cementiri de Sant Pere de Riudebitlles. Traslladada al Valle de los Caídos",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Sant Pere de Riudebitlles. Traslladada al Valle de los Caídos",
    "label": "Cementiri de Sant Pere de Riudebitlles. Traslladada al Valle de los Caídos",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de Sant Pere de Riudebitlles. Traslladada al Valle de los Caídos",
    "label": "Cementiri de Sant Pere de Riudebitlles. Traslladada al Valle de los Caídos",
    "location": "Sant Pere de Riudebitlles"
  },
  {
    "node": "Cementiri de Tarragona. Repressió de rereguarda",
    "label": "Cementiri de Tarragona. Repressió de rereguarda",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri de Tarragona. Repressió de rereguarda",
    "label": "Cementiri de Tarragona. Repressió de rereguarda",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Torregrossa",
    "label": "Cementiri de Torregrossa",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Torregrossa",
    "label": "Cementiri de Torregrossa",
    "location": "Torregrossa"
  },
  {
    "node": "Cementiri de Torrelles de Foix",
    "label": "Cementiri de Torrelles de Foix",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Torrelles de Foix",
    "label": "Cementiri de Torrelles de Foix",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de Torrelles de Foix",
    "label": "Cementiri de Torrelles de Foix",
    "location": "Torrelles de Foix"
  },
  {
    "node": "Cementiri de Torroja del Priorat",
    "label": "Cementiri de Torroja del Priorat",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Torroja del Priorat",
    "label": "Cementiri de Torroja del Priorat",
    "location": "Torroja del Priorat"
  },
  {
    "node": "Cementiri de Tàrrega",
    "label": "Cementiri de Tàrrega",
    "location": "Spain"
  },
  {
    "node": "Cementiri de Tàrrega",
    "label": "Cementiri de Tàrrega",
    "location": "Lleida"
  },
  {
    "node": "Cementiri de Tàrrega",
    "label": "Cementiri de Tàrrega",
    "location": "Tàrrega"
  },
  {
    "node": "Cementiri de l'Albi",
    "label": "Cementiri de l'Albi",
    "location": "Spain"
  },
  {
    "node": "Cementiri de l'Albi",
    "label": "Cementiri de l'Albi",
    "location": "L'Albi"
  },
  {
    "node": "Cementiri de l'Espluga de Francolí. Soldats procedents de l’Hospital Militar de les Masies",
    "label": "Cementiri de l'Espluga de Francolí. Soldats procedents de l’Hospital Militar de les Masies",
    "location": "Tarragona"
  },
  {
    "node": "Cementiri de l'Espluga de Francolí. Soldats procedents de l’Hospital Militar de les Masies",
    "label": "Cementiri de l'Espluga de Francolí. Soldats procedents de l’Hospital Militar de les Masies",
    "location": "Spain"
  },
  {
    "node": "Cementiri de l'Espluga de Francolí. Soldats procedents de l’Hospital Militar de les Masies",
    "label": "Cementiri de l'Espluga de Francolí. Soldats procedents de l’Hospital Militar de les Masies",
    "location": "L'Espluga de Francolí"
  },
  {
    "node": "Cementiri de la Gornal. Soldats republicans",
    "label": "Cementiri de la Gornal. Soldats republicans",
    "location": "Spain"
  },
  {
    "node": "Cementiri de la Gornal. Soldats republicans",
    "label": "Cementiri de la Gornal. Soldats republicans",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de la Gornal. Soldats republicans",
    "label": "Cementiri de la Gornal. Soldats republicans",
    "location": "Castellet i la Gornal"
  },
  {
    "node": "Cementiri de la Guixera de Sort",
    "label": "Cementiri de la Guixera de Sort",
    "location": "Spain"
  },
  {
    "node": "Cementiri de la Guixera de Sort",
    "label": "Cementiri de la Guixera de Sort",
    "location": "Lleida"
  },
  {
    "node": "Cementiri de la Guixera de Sort",
    "label": "Cementiri de la Guixera de Sort",
    "location": "Sort"
  },
  {
    "node": "Cementiri de la Palma d'Ebre. Soldats republicans i civils",
    "label": "Cementiri de la Palma d'Ebre. Soldats republicans i civils",
    "location": "La Palma d'Ebre"
  },
  {
    "node": "Cementiri de la Pobla de Claramunt",
    "label": "Cementiri de la Pobla de Claramunt",
    "location": "Spain"
  },
  {
    "node": "Cementiri de la Pobla de Claramunt",
    "label": "Cementiri de la Pobla de Claramunt",
    "location": "Barcelona"
  },
  {
    "node": "Cementiri de la Pobla de Claramunt",
    "label": "Cementiri de la Pobla de Claramunt",
    "location": "La Pobla de Claramunt"
  },
  {
    "node": "Cementiri de la Pobla de Cérvoles",
    "label": "Cementiri de la Pobla de Cérvoles",
    "location": "Spain"
  },
  {
    "node": "Cementiri de la Pobla de Cérvoles",
    "label": "Cementiri de la Pobla de Cérvoles",
    "location": "La Pobla de Cérvoles"
  },
  {
    "node": "Cementiri de la Pobla de Segur. Panteó de víctimes de la rereguarda",
    "label": "Cementiri de la Pobla de Segur. Panteó de víctimes de la rereguarda",
    "location": "La Pobla de Segur"
  },
  {
    "node": "Cementiri de la Seu d'Urgell. Inhumats en fossa de beneficiència",
    "label": "Cementiri de la Seu d'Urgell. Inhumats en fossa de beneficiència",
    "location": "Spain"
  },
  {
    "node": "Cementiri de la Seu d'Urgell. Inhumats en fossa de beneficiència",
    "label": "Cementiri de la Seu d'Urgell. Inhumats en fossa de beneficiència",
    "location": "Lleida"
  },
  {
    "node": "Cementiri de la Seu d'Urgell. Inhumats en fossa de beneficiència",
    "label": "Cementiri de la Seu d'Urgell. Inhumats en fossa de beneficiència",
    "location": "La Seu d'Urgell"
  },
  {
    "node": "Cementiri del Cogul",
    "label": "Cementiri del Cogul",
    "location": "Spain"
  },
  {
    "node": "Cementiri del Cogul",
    "label": "Cementiri del Cogul",
    "location": "El Cogul"
  },
  {
    "node": "Cementiri del Masroig",
    "label": "Cementiri del Masroig",
    "location": "El Masroig"
  },
  {
    "node": "Cementiri del Pinell de Brai",
    "label": "Cementiri del Pinell de Brai",
    "location": "El Pinell de Brai"
  },
  {
    "node": "Cementiri del Vilosell",
    "label": "Cementiri del Vilosell",
    "location": "Spain"
  },
  {
    "node": "Cementiri del Vilosell",
    "label": "Cementiri del Vilosell",
    "location": "El Vilosell"
  },
  {
    "node": "Cinglo Alt - rodalies de la masia de Bonrepòs",
    "label": "Cinglo Alt - rodalies de la masia de Bonrepòs",
    "location": "Spain"
  },
  {
    "node": "Cinglo Alt - rodalies de la masia de Bonrepòs",
    "label": "Cinglo Alt - rodalies de la masia de Bonrepòs",
    "location": "Gavet de la Conca"
  },
  {
    "node": "Closa De Fonolleres",
    "label": "Closa De Fonolleres",
    "location": "Spain"
  },
  {
    "node": "Closa De Fonolleres",
    "label": "Closa De Fonolleres",
    "location": "Tàrrega"
  },
  {
    "node": "Codinera De La Casa Tapioles",
    "label": "Codinera De La Casa Tapioles",
    "location": "Spain"
  },
  {
    "node": "Codinera De La Casa Tapioles",
    "label": "Codinera De La Casa Tapioles",
    "location": "Lleida"
  },
  {
    "node": "Codinera De La Casa Tapioles",
    "label": "Codinera De La Casa Tapioles",
    "location": "Altès"
  },
  {
    "node": "Coll De Leix - Gargallera 2",
    "label": "Coll De Leix - Gargallera 2",
    "location": "Spain"
  },
  {
    "node": "Coll De Leix - Gargallera 2",
    "label": "Coll De Leix - Gargallera 2",
    "location": "Montferrer i Castellbò"
  },
  {
    "node": "Coma De La Carretera D'Alcanó",
    "label": "Coma De La Carretera D'Alcanó",
    "location": "Spain"
  },
  {
    "node": "Coma De La Carretera D'Alcanó",
    "label": "Coma De La Carretera D'Alcanó",
    "location": "Granyena de les Garrigues"
  },
  {
    "node": "Cometes I. Poble Vell",
    "label": "Cometes I. Poble Vell",
    "location": "Tarragona"
  },
  {
    "node": "Cometes I. Poble Vell",
    "label": "Cometes I. Poble Vell",
    "location": "Spain"
  },
  {
    "node": "Cometes I. Poble Vell",
    "label": "Cometes I. Poble Vell",
    "location": "Corbera d'Ebre"
  },
  {
    "node": "Cometes II. Poble Vell",
    "label": "Cometes II. Poble Vell",
    "location": "Tarragona"
  },
  {
    "node": "Cometes II. Poble Vell",
    "label": "Cometes II. Poble Vell",
    "location": "Spain"
  },
  {
    "node": "Cometes II. Poble Vell",
    "label": "Cometes II. Poble Vell",
    "location": "Corbera d'Ebre"
  },
  {
    "node": "Corba del Salt",
    "label": "Corba del Salt",
    "location": "Spain"
  },
  {
    "node": "Corba del Salt",
    "label": "Corba del Salt",
    "location": "Lleida"
  },
  {
    "node": "Corba del Salt",
    "label": "Corba del Salt",
    "location": "Alt Àneu"
  },
  {
    "node": "Costa Del Mas Dels Quadros",
    "label": "Costa Del Mas Dels Quadros",
    "location": "Spain"
  },
  {
    "node": "Costa Del Mas Dels Quadros",
    "label": "Costa Del Mas Dels Quadros",
    "location": "Lleida"
  },
  {
    "node": "Costa Del Mas Dels Quadros",
    "label": "Costa Del Mas Dels Quadros",
    "location": "Llobera"
  },
  {
    "node": "Costa Negra: La Socarrada",
    "label": "Costa Negra: La Socarrada",
    "location": "Rialp"
  },
  {
    "node": "Cota 705 - Punta Alta",
    "label": "Cota 705 - Punta Alta",
    "location": "Tarragona"
  },
  {
    "node": "Cota 705 - Punta Alta",
    "label": "Cota 705 - Punta Alta",
    "location": "Spain"
  },
  {
    "node": "Cota 705 - Punta Alta",
    "label": "Cota 705 - Punta Alta",
    "location": "El Pinell de Brai"
  },
  {
    "node": "Devesa Del Baiget",
    "label": "Devesa Del Baiget",
    "location": "Spain"
  },
  {
    "node": "Devesa Del Baiget",
    "label": "Devesa Del Baiget",
    "location": "Lleida"
  },
  {
    "node": "Devesa Del Baiget",
    "label": "Devesa Del Baiget",
    "location": "Cervià de les Garrigues"
  },
  {
    "node": "Domenges",
    "label": "Domenges",
    "location": "Tarragona"
  },
  {
    "node": "Domenges",
    "label": "Domenges",
    "location": "Spain"
  },
  {
    "node": "Domenges",
    "label": "Domenges",
    "location": "Gandesa"
  },
  {
    "node": "El Rovellar",
    "label": "El Rovellar",
    "location": "Tarragona"
  },
  {
    "node": "El Rovellar",
    "label": "El Rovellar",
    "location": "Spain"
  },
  {
    "node": "El Rovellar",
    "label": "El Rovellar",
    "location": "La Palma d'Ebre"
  },
  {
    "node": "Els Guascos",
    "label": "Els Guascos",
    "location": "Spain"
  },
  {
    "node": "Els Guascos",
    "label": "Els Guascos",
    "location": "Lleida"
  },
  {
    "node": "Els Guascos",
    "label": "Els Guascos",
    "location": "Tarrés"
  },
  {
    "node": "Els Omells De Na Gaia",
    "label": "Els Omells De Na Gaia",
    "location": "Spain"
  },
  {
    "node": "Els Omells De Na Gaia",
    "label": "Els Omells De Na Gaia",
    "location": "Els Omells de na Gaia"
  },
  {
    "node": "Els Prats. Fossa Del Punt De Socors De Cabra Del Camp",
    "label": "Els Prats. Fossa Del Punt De Socors De Cabra Del Camp",
    "location": "Cabra del Camp"
  },
  {
    "node": "Els Verats",
    "label": "Els Verats",
    "location": "Tarragona"
  },
  {
    "node": "Els Verats",
    "label": "Els Verats",
    "location": "Spain"
  },
  {
    "node": "Els Verats",
    "label": "Els Verats",
    "location": "La Palma d'Ebre"
  },
  {
    "node": "Era Del Castell",
    "label": "Era Del Castell",
    "location": "Spain"
  },
  {
    "node": "Era Del Castell",
    "label": "Era Del Castell",
    "location": "Lleida"
  },
  {
    "node": "Era Del Castell",
    "label": "Era Del Castell",
    "location": "El Cogul"
  },
  {
    "node": "Eretes Noves - Boscos",
    "label": "Eretes Noves - Boscos",
    "location": "Spain"
  },
  {
    "node": "Eretes Noves - Boscos",
    "label": "Eretes Noves - Boscos",
    "location": "La Torre de l'Espanyol"
  },
  {
    "node": "Ermita De La Consolació",
    "label": "Ermita De La Consolació",
    "location": "Spain"
  },
  {
    "node": "Ermita De La Consolació",
    "label": "Ermita De La Consolació",
    "location": "Torroja del Priorat"
  },
  {
    "node": "Es Colomines: Tredos",
    "label": "Es Colomines: Tredos",
    "location": "Spain"
  },
  {
    "node": "Es Colomines: Tredos",
    "label": "Es Colomines: Tredos",
    "location": "Naut Aran"
  },
  {
    "node": "Església De La Granja Sant Vicenç Ferrer",
    "label": "Església De La Granja Sant Vicenç Ferrer",
    "location": "Spain"
  },
  {
    "node": "Església De La Granja Sant Vicenç Ferrer",
    "label": "Església De La Granja Sant Vicenç Ferrer",
    "location": "Penelles"
  },
  {
    "node": "Espai De La Tabacalera",
    "label": "Espai De La Tabacalera",
    "location": "Tarragona"
  },
  {
    "node": "Espai De La Tabacalera",
    "label": "Espai De La Tabacalera",
    "location": "Catalunya"
  },
  {
    "node": "Espai De La Tabacalera",
    "label": "Espai De La Tabacalera",
    "location": "Spain"
  },
  {
    "node": "Espai De La Tabacalera",
    "label": "Espai De La Tabacalera",
    "location": "Tarragonès"
  },
  {
    "node": "Estació De Flix",
    "label": "Estació De Flix",
    "location": "Tarragona"
  },
  {
    "node": "Estació De Flix",
    "label": "Estació De Flix",
    "location": "Catalunya"
  },
  {
    "node": "Estació De Flix",
    "label": "Estació De Flix",
    "location": "Spain"
  },
  {
    "node": "Estació De Flix",
    "label": "Estació De Flix",
    "location": "Ribera d'Ebre"
  },
  {
    "node": "Estació De Flix",
    "label": "Estació De Flix",
    "location": "Flix"
  },
  {
    "node": "Exterior Cementiri Gandesa",
    "label": "Exterior Cementiri Gandesa",
    "location": "Tarragona"
  },
  {
    "node": "Exterior Cementiri Gandesa",
    "label": "Exterior Cementiri Gandesa",
    "location": "Spain"
  },
  {
    "node": "Exterior Cementiri Gandesa",
    "label": "Exterior Cementiri Gandesa",
    "location": "Gandesa"
  },
  {
    "node": "Exterior Del Cementiri De Balaguer. Fossa De Soldats Marroquins",
    "label": "Exterior Del Cementiri De Balaguer. Fossa De Soldats Marroquins",
    "location": "Spain"
  },
  {
    "node": "Exterior Del Cementiri De Balaguer. Fossa De Soldats Marroquins",
    "label": "Exterior Del Cementiri De Balaguer. Fossa De Soldats Marroquins",
    "location": "Lleida"
  },
  {
    "node": "Exterior Del Cementiri De Balaguer. Fossa De Soldats Marroquins",
    "label": "Exterior Del Cementiri De Balaguer. Fossa De Soldats Marroquins",
    "location": "Balaguer"
  },
  {
    "node": "Extramurs Del Cementiri De Gratallops",
    "label": "Extramurs Del Cementiri De Gratallops",
    "location": "Spain"
  },
  {
    "node": "Extramurs Del Cementiri De Gratallops",
    "label": "Extramurs Del Cementiri De Gratallops",
    "location": "Gratallops"
  },
  {
    "node": "Fondo del Bosc Glaçat",
    "label": "Fondo del Bosc Glaçat",
    "location": "Spain"
  },
  {
    "node": "Fondo del Bosc Glaçat",
    "label": "Fondo del Bosc Glaçat",
    "location": "Barcelona"
  },
  {
    "node": "Fondo del Bosc Glaçat",
    "label": "Fondo del Bosc Glaçat",
    "location": "Olesa de Bonesvalls"
  },
  {
    "node": "Font Del Fortet",
    "label": "Font Del Fortet",
    "location": "Spain"
  },
  {
    "node": "Font Del Fortet",
    "label": "Font Del Fortet",
    "location": "Capafonts"
  },
  {
    "node": "Fora Del Cementiri D'Ars",
    "label": "Fora Del Cementiri D'Ars",
    "location": "Spain"
  },
  {
    "node": "Fora Del Cementiri D'Ars",
    "label": "Fora Del Cementiri D'Ars",
    "location": "Lleida"
  },
  {
    "node": "Fora Del Cementiri D'Ars",
    "label": "Fora Del Cementiri D'Ars",
    "location": "Les Valls de Valira"
  },
  {
    "node": "Forn De Calç Del Camp Del Muntaner",
    "label": "Forn De Calç Del Camp Del Muntaner",
    "location": "Spain"
  },
  {
    "node": "Forn De Calç Del Camp Del Muntaner",
    "label": "Forn De Calç Del Camp Del Muntaner",
    "location": "Barcelona"
  },
  {
    "node": "Forn De Calç Del Camp Del Muntaner",
    "label": "Forn De Calç Del Camp Del Muntaner",
    "location": "Olesa de Bonesvalls"
  },
  {
    "node": "Fosa de Prades",
    "label": "Fosa de Prades",
    "location": "Spain"
  },
  {
    "node": "Fossa Comuna Amb Cossos De Soldats Recollits Al Terme. Cementiri De La Granadella",
    "label": "Fossa Comuna Amb Cossos De Soldats Recollits Al Terme. Cementiri De La Granadella",
    "location": "Spain"
  },
  {
    "node": "Fossa Comuna Amb Cossos De Soldats Recollits Al Terme. Cementiri De La Granadella",
    "label": "Fossa Comuna Amb Cossos De Soldats Recollits Al Terme. Cementiri De La Granadella",
    "location": "Lleida"
  },
  {
    "node": "Fossa Comuna Amb Cossos De Soldats Recollits Al Terme. Cementiri De La Granadella",
    "label": "Fossa Comuna Amb Cossos De Soldats Recollits Al Terme. Cementiri De La Granadella",
    "location": "La Granadella"
  },
  {
    "node": "Fossa D'altadill I",
    "label": "Fossa D'altadill I",
    "location": "Spain"
  },
  {
    "node": "Fossa D'altadill I",
    "label": "Fossa D'altadill I",
    "location": "Lleida"
  },
  {
    "node": "Fossa D'altadill I",
    "label": "Fossa D'altadill I",
    "location": "Sant Guim de Freixenet"
  },
  {
    "node": "Fossa D'altadill Ii",
    "label": "Fossa D'altadill Ii",
    "location": "Spain"
  },
  {
    "node": "Fossa D'altadill Ii",
    "label": "Fossa D'altadill Ii",
    "location": "Lleida"
  },
  {
    "node": "Fossa D'altadill Ii",
    "label": "Fossa D'altadill Ii",
    "location": "Sant Guim de Freixenet"
  },
  {
    "node": "Fossa D'altadill Iii",
    "label": "Fossa D'altadill Iii",
    "location": "Spain"
  },
  {
    "node": "Fossa D'altadill Iii",
    "label": "Fossa D'altadill Iii",
    "location": "Lleida"
  },
  {
    "node": "Fossa D'altadill Iii",
    "label": "Fossa D'altadill Iii",
    "location": "Sant Guim de Freixenet"
  },
  {
    "node": "Fossa De Civils Del Cementiri De Llorenç Del Penedès",
    "label": "Fossa De Civils Del Cementiri De Llorenç Del Penedès",
    "location": "Tarragona"
  },
  {
    "node": "Fossa De Civils Del Cementiri De Llorenç Del Penedès",
    "label": "Fossa De Civils Del Cementiri De Llorenç Del Penedès",
    "location": "Spain"
  },
  {
    "node": "Fossa De Civils Del Cementiri De Llorenç Del Penedès",
    "label": "Fossa De Civils Del Cementiri De Llorenç Del Penedès",
    "location": "Llorenç del Penedès"
  },
  {
    "node": "Fossa Del Cementiri Vell De Mont-roig",
    "label": "Fossa Del Cementiri Vell De Mont-roig",
    "location": "Spain"
  },
  {
    "node": "Fossa Del Cementiri Vell De Mont-roig",
    "label": "Fossa Del Cementiri Vell De Mont-roig",
    "location": "Lleida"
  },
  {
    "node": "Fossa Del Cementiri Vell De Mont-roig",
    "label": "Fossa Del Cementiri Vell De Mont-roig",
    "location": "Els Plans de Sió"
  },
  {
    "node": "Fossa Dels Brigadistes",
    "label": "Fossa Dels Brigadistes",
    "location": "Spain"
  },
  {
    "node": "Fossa Dels Brigadistes",
    "label": "Fossa Dels Brigadistes",
    "location": "Lleida"
  },
  {
    "node": "Fossa Dels Brigadistes",
    "label": "Fossa Dels Brigadistes",
    "location": "Bellaguarda"
  },
  {
    "node": "Fossa Dels Italians Del Cementiri De L'albi",
    "label": "Fossa Dels Italians Del Cementiri De L'albi",
    "location": "Spain"
  },
  {
    "node": "Fossa Dels Italians Del Cementiri De L'albi",
    "label": "Fossa Dels Italians Del Cementiri De L'albi",
    "location": "Lleida"
  },
  {
    "node": "Fossa Dels Italians Del Cementiri De L'albi",
    "label": "Fossa Dels Italians Del Cementiri De L'albi",
    "location": "L'Albi"
  },
  {
    "node": "Fossa Dels Rebels Italians. Cementiri Dels Caputxins De Mataró",
    "label": "Fossa Dels Rebels Italians. Cementiri Dels Caputxins De Mataró",
    "location": "Spain"
  },
  {
    "node": "Fossa Dels Rebels Italians. Cementiri Dels Caputxins De Mataró",
    "label": "Fossa Dels Rebels Italians. Cementiri Dels Caputxins De Mataró",
    "location": "Barcelona"
  },
  {
    "node": "Fossa Dels Rebels Italians. Cementiri Dels Caputxins De Mataró",
    "label": "Fossa Dels Rebels Italians. Cementiri Dels Caputxins De Mataró",
    "location": "Mataró"
  },
  {
    "node": "Fossa Militar Del Cementiri De Balaguer",
    "label": "Fossa Militar Del Cementiri De Balaguer",
    "location": "Spain"
  },
  {
    "node": "Fossa Militar Del Cementiri De Balaguer",
    "label": "Fossa Militar Del Cementiri De Balaguer",
    "location": "Balaguer"
  },
  {
    "node": "Fossa de Mas Suau",
    "label": "Fossa de Mas Suau",
    "location": "Les Oluges"
  },
  {
    "node": "Fossa de l'era de Cal Casat (Ferran)",
    "label": "Fossa de l'era de Cal Casat (Ferran)",
    "location": "Estaràs"
  },
  {
    "node": "Fossa de l'era de la Maria Antònia (Ferran)",
    "label": "Fossa de l'era de la Maria Antònia (Ferran)",
    "location": "Estaràs"
  },
  {
    "node": "Fossa de l'ermita de la Mare de Déu de Santes Masses",
    "label": "Fossa de l'ermita de la Mare de Déu de Santes Masses",
    "location": "Torrefeta"
  },
  {
    "node": "Fossa de la Costa de l'Aguda",
    "label": "Fossa de la Costa de l'Aguda",
    "location": "Torà"
  },
  {
    "node": "Fossa del Mas de Can Ranxet (Portell)",
    "label": "Fossa del Mas de Can Ranxet (Portell)",
    "location": "Sant Ramon"
  },
  {
    "node": "Fossa del cementiri de Vilabella",
    "label": "Fossa del cementiri de Vilabella",
    "location": "Tarragona"
  },
  {
    "node": "Fossa del cementiri de Vilabella",
    "label": "Fossa del cementiri de Vilabella",
    "location": "Vilabella"
  },
  {
    "node": "Fossa dels germans Inglés Andreu. Cementiri de Tarrés",
    "label": "Fossa dels germans Inglés Andreu. Cementiri de Tarrés",
    "location": "Spain"
  },
  {
    "node": "Fossa dels germans Inglés Andreu. Cementiri de Tarrés",
    "label": "Fossa dels germans Inglés Andreu. Cementiri de Tarrés",
    "location": "Lleida"
  },
  {
    "node": "Fossa dels germans Inglés Andreu. Cementiri de Tarrés",
    "label": "Fossa dels germans Inglés Andreu. Cementiri de Tarrés",
    "location": "Tarrés"
  },
  {
    "node": "Fosses 4 I 5 Del Cementiri De Terrassa",
    "label": "Fosses 4 I 5 Del Cementiri De Terrassa",
    "location": "Spain"
  },
  {
    "node": "Fosses 4 I 5 Del Cementiri De Terrassa",
    "label": "Fosses 4 I 5 Del Cementiri De Terrassa",
    "location": "Barcelona"
  },
  {
    "node": "Fosses 4 I 5 Del Cementiri De Terrassa",
    "label": "Fosses 4 I 5 Del Cementiri De Terrassa",
    "location": "Terrassa"
  },
  {
    "node": "Fosses De Maquis Al Cementiri De Camprodon",
    "label": "Fosses De Maquis Al Cementiri De Camprodon",
    "location": "Spain"
  },
  {
    "node": "Fosses De Maquis Al Cementiri De Camprodon",
    "label": "Fosses De Maquis Al Cementiri De Camprodon",
    "location": "Girona"
  },
  {
    "node": "Fosses De Maquis Al Cementiri De Camprodon",
    "label": "Fosses De Maquis Al Cementiri De Camprodon",
    "location": "Camprodon"
  },
  {
    "node": "Fosses del Riu de l'Oró",
    "label": "Fosses del Riu de l'Oró",
    "location": "Spain"
  },
  {
    "node": "Fosses del Riu de l'Oró",
    "label": "Fosses del Riu de l'Oró",
    "location": "Lleida"
  },
  {
    "node": "Fosses del Riu de l'Oró",
    "label": "Fosses del Riu de l'Oró",
    "location": "Cervià de les Garrigues"
  },
  {
    "node": "Fuses: Sant Marti De Canals",
    "label": "Fuses: Sant Marti De Canals",
    "location": "Spain"
  },
  {
    "node": "Fuses: Sant Marti De Canals",
    "label": "Fuses: Sant Marti De Canals",
    "location": "Lleida"
  },
  {
    "node": "Fuses: Sant Marti De Canals",
    "label": "Fuses: Sant Marti De Canals",
    "location": "Conca de Dalt"
  },
  {
    "node": "Galobardes",
    "label": "Galobardes",
    "location": "Spain"
  },
  {
    "node": "Galobardes",
    "label": "Galobardes",
    "location": "Barcelona"
  },
  {
    "node": "Galobardes",
    "label": "Galobardes",
    "location": "Prats De Lluçanès"
  },
  {
    "node": "Garriga Del Maleneta - Racó Del Boteret",
    "label": "Garriga Del Maleneta - Racó Del Boteret",
    "location": "Tarragona"
  },
  {
    "node": "Garriga Del Maleneta - Racó Del Boteret",
    "label": "Garriga Del Maleneta - Racó Del Boteret",
    "location": "Ulldemolins"
  },
  {
    "node": "Ginestrets - Cota 356",
    "label": "Ginestrets - Cota 356",
    "location": "Tarragona"
  },
  {
    "node": "Ginestrets - Cota 356",
    "label": "Ginestrets - Cota 356",
    "location": "Spain"
  },
  {
    "node": "Ginestrets - Cota 356",
    "label": "Ginestrets - Cota 356",
    "location": "Corbera d'Ebre"
  },
  {
    "node": "Guixera La Reductora",
    "label": "Guixera La Reductora",
    "location": "Spain"
  },
  {
    "node": "Guixera La Reductora",
    "label": "Guixera La Reductora",
    "location": "Òdena"
  },
  {
    "node": "Hospital De Sang De Casa Torriella",
    "label": "Hospital De Sang De Casa Torriella",
    "location": "Spain"
  },
  {
    "node": "Hospital De Sang De Casa Torriella",
    "label": "Hospital De Sang De Casa Torriella",
    "location": "Lleida"
  },
  {
    "node": "Hospital De Sang De Casa Torriella",
    "label": "Hospital De Sang De Casa Torriella",
    "location": "Montanissell"
  },
  {
    "node": "Inhumacions a l'interior i a l'exterior del cementiri de Rodonyà",
    "label": "Inhumacions a l'interior i a l'exterior del cementiri de Rodonyà",
    "location": "Tarragona"
  },
  {
    "node": "Inhumacions a l'interior i a l'exterior del cementiri de Rodonyà",
    "label": "Inhumacions a l'interior i a l'exterior del cementiri de Rodonyà",
    "location": "Rodonyà"
  },
  {
    "node": "Inhumació Al Camí Ral A Llavaneres",
    "label": "Inhumació Al Camí Ral A Llavaneres",
    "location": "Spain"
  },
  {
    "node": "Inhumació Al Camí Ral A Llavaneres",
    "label": "Inhumació Al Camí Ral A Llavaneres",
    "location": "Sant Andreu de Llavaneres"
  },
  {
    "node": "L'escrita",
    "label": "L'escrita",
    "location": "Spain"
  },
  {
    "node": "L'escrita",
    "label": "L'escrita",
    "location": "Lleida"
  },
  {
    "node": "L'escrita",
    "label": "L'escrita",
    "location": "La Guingueta d'Àneu"
  },
  {
    "node": "La Boverola Pei",
    "label": "La Boverola Pei",
    "location": "Spain"
  },
  {
    "node": "La Boverola Pei",
    "label": "La Boverola Pei",
    "location": "Lleida"
  },
  {
    "node": "La Boverola Pei",
    "label": "La Boverola Pei",
    "location": "La Granadella"
  },
  {
    "node": "La Cadolla",
    "label": "La Cadolla",
    "location": "Spain"
  },
  {
    "node": "La Cadolla",
    "label": "La Cadolla",
    "location": "Almatret"
  },
  {
    "node": "La Carrerada",
    "label": "La Carrerada",
    "location": "Sant Romà d'Abella"
  },
  {
    "node": "La Casella De Can Soteras",
    "label": "La Casella De Can Soteras",
    "location": "Spain"
  },
  {
    "node": "La Casella De Can Soteras",
    "label": "La Casella De Can Soteras",
    "location": "Castellolí"
  },
  {
    "node": "La Cogulla. Cota 1062",
    "label": "La Cogulla. Cota 1062",
    "location": "Tarragona"
  },
  {
    "node": "La Cogulla. Cota 1062",
    "label": "La Cogulla. Cota 1062",
    "location": "Spain"
  },
  {
    "node": "La Cogulla. Cota 1062",
    "label": "La Cogulla. Cota 1062",
    "location": "La Morera de Montsant"
  },
  {
    "node": "La Figuera",
    "label": "La Figuera",
    "location": "Tarragona"
  },
  {
    "node": "La Figuera",
    "label": "La Figuera",
    "location": "Catalunya"
  },
  {
    "node": "La Figuera",
    "label": "La Figuera",
    "location": "Spain"
  },
  {
    "node": "La Figuera",
    "label": "La Figuera",
    "location": "Priorat"
  },
  {
    "node": "La Figuera",
    "label": "La Figuera",
    "location": "La Figuera"
  },
  {
    "node": "La Griera",
    "label": "La Griera",
    "location": "Spain"
  },
  {
    "node": "La Griera",
    "label": "La Griera",
    "location": "Gurb"
  },
  {
    "node": "La Plana del Mas Soler",
    "label": "La Plana del Mas Soler",
    "location": "Tarragona"
  },
  {
    "node": "La Plana del Mas Soler",
    "label": "La Plana del Mas Soler",
    "location": "Spain"
  },
  {
    "node": "La Plana del Mas Soler",
    "label": "La Plana del Mas Soler",
    "location": "Tivissa"
  },
  {
    "node": "La Saira",
    "label": "La Saira",
    "location": "Spain"
  },
  {
    "node": "La Saira",
    "label": "La Saira",
    "location": "Lleida"
  },
  {
    "node": "La Saira",
    "label": "La Saira",
    "location": "Almacelles"
  },
  {
    "node": "La Serra | Camí de la Masia",
    "label": "La Serra | Camí de la Masia",
    "location": "Spain"
  },
  {
    "node": "La Serra | Camí de la Masia",
    "label": "La Serra | Camí de la Masia",
    "location": "Lleida"
  },
  {
    "node": "La Serra | Camí de la Masia",
    "label": "La Serra | Camí de la Masia",
    "location": "Baldomar"
  },
  {
    "node": "La Serreta",
    "label": "La Serreta",
    "location": "Lleida"
  },
  {
    "node": "La Serreta",
    "label": "La Serreta",
    "location": "La Baronia de Rialb"
  },
  {
    "node": "La Sort Del Quimet De Prats",
    "label": "La Sort Del Quimet De Prats",
    "location": "Spain"
  },
  {
    "node": "La Sort Del Quimet De Prats",
    "label": "La Sort Del Quimet De Prats",
    "location": "Lleida"
  },
  {
    "node": "La Sort Del Quimet De Prats",
    "label": "La Sort Del Quimet De Prats",
    "location": "La Granadella"
  },
  {
    "node": "La Teulera",
    "label": "La Teulera",
    "location": "Spain"
  },
  {
    "node": "La Teulera",
    "label": "La Teulera",
    "location": "Lleida"
  },
  {
    "node": "La Teulera",
    "label": "La Teulera",
    "location": "Vilanova De Meià"
  },
  {
    "node": "La Venta (l'Hostal de la Serra)",
    "label": "La Venta (l'Hostal de la Serra)",
    "location": "Margalef"
  },
  {
    "node": "La Voltera. La Febró",
    "label": "La Voltera. La Febró",
    "location": "Spain"
  },
  {
    "node": "La Voltera. La Febró",
    "label": "La Voltera. La Febró",
    "location": "La Febró - Prades"
  },
  {
    "node": "La serra Fosca",
    "label": "La serra Fosca",
    "location": "Spain"
  },
  {
    "node": "La serra Fosca",
    "label": "La serra Fosca",
    "location": "Lleida"
  },
  {
    "node": "La serra Fosca",
    "label": "La serra Fosca",
    "location": "L'Albagés"
  },
  {
    "node": "Les Basses",
    "label": "Les Basses",
    "location": "Spain"
  },
  {
    "node": "Les Basses",
    "label": "Les Basses",
    "location": "Vinaixa"
  },
  {
    "node": "Les Cadolles - Les Comitjanes",
    "label": "Les Cadolles - Les Comitjanes",
    "location": "Spain"
  },
  {
    "node": "Les Cadolles - Les Comitjanes",
    "label": "Les Cadolles - Les Comitjanes",
    "location": "La Palma d'Ebre"
  },
  {
    "node": "Les Collades: Bosc De Tres Comuns",
    "label": "Les Collades: Bosc De Tres Comuns",
    "location": "Spain"
  },
  {
    "node": "Les Collades: Bosc De Tres Comuns",
    "label": "Les Collades: Bosc De Tres Comuns",
    "location": "Lleida"
  },
  {
    "node": "Les Collades: Bosc De Tres Comuns",
    "label": "Les Collades: Bosc De Tres Comuns",
    "location": "Rialp"
  },
  {
    "node": "Les Deveses De Prades. Soldats Republicans",
    "label": "Les Deveses De Prades. Soldats Republicans",
    "location": "Spain"
  },
  {
    "node": "Les Deveses De Prades. Soldats Republicans",
    "label": "Les Deveses De Prades. Soldats Republicans",
    "location": "Prades"
  },
  {
    "node": "Les Guixeres De Sort",
    "label": "Les Guixeres De Sort",
    "location": "Spain"
  },
  {
    "node": "Les Guixeres De Sort",
    "label": "Les Guixeres De Sort",
    "location": "Sort"
  },
  {
    "node": "Les Planes - Vall De Jacob",
    "label": "Les Planes - Vall De Jacob",
    "location": "Tarragona"
  },
  {
    "node": "Les Planes - Vall De Jacob",
    "label": "Les Planes - Vall De Jacob",
    "location": "Catalunya"
  },
  {
    "node": "Les Planes - Vall De Jacob",
    "label": "Les Planes - Vall De Jacob",
    "location": "Spain"
  },
  {
    "node": "Les Planes - Vall De Jacob",
    "label": "Les Planes - Vall De Jacob",
    "location": "Ribera d'Ebre"
  },
  {
    "node": "Les Planes - Vall De Jacob",
    "label": "Les Planes - Vall De Jacob",
    "location": "Ascó"
  },
  {
    "node": "Les Pobles, Mont-Roig Del Camp",
    "label": "Les Pobles, Mont-Roig Del Camp",
    "location": "Tarragona"
  },
  {
    "node": "Les Pobles, Mont-Roig Del Camp",
    "label": "Les Pobles, Mont-Roig Del Camp",
    "location": "Spain"
  },
  {
    "node": "Les Pobles, Mont-Roig Del Camp",
    "label": "Les Pobles, Mont-Roig Del Camp",
    "location": "Mont-roig del Camp"
  },
  {
    "node": "Les Solanes",
    "label": "Les Solanes",
    "location": "Spain"
  },
  {
    "node": "Les Solanes",
    "label": "Les Solanes",
    "location": "Móra d'Ebre"
  },
  {
    "node": "Les Trufes",
    "label": "Les Trufes",
    "location": "Spain"
  },
  {
    "node": "Les Trufes",
    "label": "Les Trufes",
    "location": "Batea"
  },
  {
    "node": "Lo Coll",
    "label": "Lo Coll",
    "location": "Spain"
  },
  {
    "node": "Lo Coll",
    "label": "Lo Coll",
    "location": "Lleida"
  },
  {
    "node": "Lo Coll",
    "label": "Lo Coll",
    "location": "La Granadella"
  },
  {
    "node": "Lo Forat De La Gandaia",
    "label": "Lo Forat De La Gandaia",
    "location": "Tarragona"
  },
  {
    "node": "Lo Forat De La Gandaia",
    "label": "Lo Forat De La Gandaia",
    "location": "Catalunya"
  },
  {
    "node": "Lo Forat De La Gandaia",
    "label": "Lo Forat De La Gandaia",
    "location": "Spain"
  },
  {
    "node": "Lo Forat De La Gandaia",
    "label": "Lo Forat De La Gandaia",
    "location": "Priorat"
  },
  {
    "node": "Lo Forat De La Gandaia",
    "label": "Lo Forat De La Gandaia",
    "location": "La Morera de Montsant"
  },
  {
    "node": "Lo Molló",
    "label": "Lo Molló",
    "location": "Tarragona"
  },
  {
    "node": "Lo Molló",
    "label": "Lo Molló",
    "location": "Catalunya"
  },
  {
    "node": "Lo Molló",
    "label": "Lo Molló",
    "location": "Spain"
  },
  {
    "node": "Lo Molló",
    "label": "Lo Molló",
    "location": "Terra Alta"
  },
  {
    "node": "Lo Molló",
    "label": "Lo Molló",
    "location": "La Pobla de Massaluca"
  },
  {
    "node": "Lo Solanell: Hortoneda",
    "label": "Lo Solanell: Hortoneda",
    "location": "Spain"
  },
  {
    "node": "Lo Solanell: Hortoneda",
    "label": "Lo Solanell: Hortoneda",
    "location": "Lleida"
  },
  {
    "node": "Lo Solanell: Hortoneda",
    "label": "Lo Solanell: Hortoneda",
    "location": "Conca de Dalt"
  },
  {
    "node": "Los Caus",
    "label": "Los Caus",
    "location": "Spain"
  },
  {
    "node": "Los Caus",
    "label": "Los Caus",
    "location": "Lleida"
  },
  {
    "node": "Los Caus",
    "label": "Los Caus",
    "location": "El Cogul"
  },
  {
    "node": "Los Esplans del Corona",
    "label": "Los Esplans del Corona",
    "location": "Spain"
  },
  {
    "node": "Los Esplans del Corona",
    "label": "Los Esplans del Corona",
    "location": "Lleida"
  },
  {
    "node": "Los Esplans del Corona",
    "label": "Los Esplans del Corona",
    "location": "El Soleràs"
  },
  {
    "node": "Los Raïmats",
    "label": "Los Raïmats",
    "location": "Tarragona"
  },
  {
    "node": "Los Raïmats",
    "label": "Los Raïmats",
    "location": "Spain"
  },
  {
    "node": "Los Raïmats",
    "label": "Los Raïmats",
    "location": "La Fatarella"
  },
  {
    "node": "Mallolis",
    "label": "Mallolis",
    "location": "Spain"
  },
  {
    "node": "Mallolis",
    "label": "Mallolis",
    "location": "Lleida"
  },
  {
    "node": "Mallolis",
    "label": "Mallolis",
    "location": "Farrera"
  },
  {
    "node": "Maqui Al Cementiri De L'església Dels Constantins",
    "label": "Maqui Al Cementiri De L'església Dels Constantins",
    "location": "Spain"
  },
  {
    "node": "Maqui Al Cementiri De L'església Dels Constantins",
    "label": "Maqui Al Cementiri De L'església Dels Constantins",
    "location": "Girona"
  },
  {
    "node": "Maqui Al Cementiri De L'església Dels Constantins",
    "label": "Maqui Al Cementiri De L'església Dels Constantins",
    "location": "Constantins"
  },
  {
    "node": "Maquis Al Cementiri De L'església De Castanyet",
    "label": "Maquis Al Cementiri De L'església De Castanyet",
    "location": "Girona"
  },
  {
    "node": "Maquis Al Cementiri De L'església De Castanyet",
    "label": "Maquis Al Cementiri De L'església De Castanyet",
    "location": "Castanyet"
  },
  {
    "node": "Mare de Déu de les Ares",
    "label": "Mare de Déu de les Ares",
    "location": "Spain"
  },
  {
    "node": "Mare de Déu de les Ares",
    "label": "Mare de Déu de les Ares",
    "location": "Alt Àneu"
  },
  {
    "node": "Mas D'en Rafel",
    "label": "Mas D'en Rafel",
    "location": null
  },
  {
    "node": "Mas De Barbaretes",
    "label": "Mas De Barbaretes",
    "location": "Tarragona"
  },
  {
    "node": "Mas De Barbaretes",
    "label": "Mas De Barbaretes",
    "location": "Spain"
  },
  {
    "node": "Mas De Barbaretes",
    "label": "Mas De Barbaretes",
    "location": "La Fatarella"
  },
  {
    "node": "Mas De L'alfredo",
    "label": "Mas De L'alfredo",
    "location": "Spain"
  },
  {
    "node": "Mas De L'alfredo",
    "label": "Mas De L'alfredo",
    "location": "Lleida"
  },
  {
    "node": "Mas De L'alfredo",
    "label": "Mas De L'alfredo",
    "location": "L'Albagés"
  },
  {
    "node": "Mas De La Bernarda",
    "label": "Mas De La Bernarda",
    "location": "Spain"
  },
  {
    "node": "Mas De La Bernarda",
    "label": "Mas De La Bernarda",
    "location": "Llardecans"
  },
  {
    "node": "Mas De La Pila",
    "label": "Mas De La Pila",
    "location": "Tarragona"
  },
  {
    "node": "Mas De La Pila",
    "label": "Mas De La Pila",
    "location": "Spain"
  },
  {
    "node": "Mas De La Pila",
    "label": "Mas De La Pila",
    "location": "Corbera d'Ebre"
  },
  {
    "node": "Mas De Les Aluges. Partida De Sant Miquel",
    "label": "Mas De Les Aluges. Partida De Sant Miquel",
    "location": "Spain"
  },
  {
    "node": "Mas De Les Aluges. Partida De Sant Miquel",
    "label": "Mas De Les Aluges. Partida De Sant Miquel",
    "location": "Vespella de Gaià"
  },
  {
    "node": "Mas De Prades",
    "label": "Mas De Prades",
    "location": "Ascó"
  },
  {
    "node": "Mas Del Geser",
    "label": "Mas Del Geser",
    "location": "Tarragona"
  },
  {
    "node": "Mas Del Geser",
    "label": "Mas Del Geser",
    "location": "Spain"
  },
  {
    "node": "Mas Del Geser",
    "label": "Mas Del Geser",
    "location": "Corbera d'Ebre"
  },
  {
    "node": "Mas Del Puig",
    "label": "Mas Del Puig",
    "location": "Torelló"
  },
  {
    "node": "Mas Dels Mitgers",
    "label": "Mas Dels Mitgers",
    "location": "Spain"
  },
  {
    "node": "Mas Dels Mitgers",
    "label": "Mas Dels Mitgers",
    "location": "Lleida"
  },
  {
    "node": "Mas Dels Mitgers",
    "label": "Mas Dels Mitgers",
    "location": "La Granadella"
  },
  {
    "node": "Mas D’en Blai",
    "label": "Mas D’en Blai",
    "location": "Vilalba dels Arcs"
  },
  {
    "node": "Mas Torrenova - Parc Eòlic Bon Vent",
    "label": "Mas Torrenova - Parc Eòlic Bon Vent",
    "location": "Tarragona"
  },
  {
    "node": "Mas Torrenova - Parc Eòlic Bon Vent",
    "label": "Mas Torrenova - Parc Eòlic Bon Vent",
    "location": "Spain"
  },
  {
    "node": "Mas Torrenova - Parc Eòlic Bon Vent",
    "label": "Mas Torrenova - Parc Eòlic Bon Vent",
    "location": "Corbera d'Ebre"
  },
  {
    "node": "Mas de Puigvistós de Prats de Lluçanès",
    "label": "Mas de Puigvistós de Prats de Lluçanès",
    "location": "Barcelona"
  },
  {
    "node": "Mas de Puigvistós de Prats de Lluçanès",
    "label": "Mas de Puigvistós de Prats de Lluçanès",
    "location": "Prats De Lluçanès"
  },
  {
    "node": "Mas del Primo",
    "label": "Mas del Primo",
    "location": "Tarragona"
  },
  {
    "node": "Mas del Primo",
    "label": "Mas del Primo",
    "location": "Spain"
  },
  {
    "node": "Mas del Primo",
    "label": "Mas del Primo",
    "location": "Caseres"
  },
  {
    "node": "Mas del Sant",
    "label": "Mas del Sant",
    "location": "Spain"
  },
  {
    "node": "Mas del Sant",
    "label": "Mas del Sant",
    "location": "Benissanet"
  },
  {
    "node": "Mas d’en Blanc",
    "label": "Mas d’en Blanc",
    "location": "Tarragona"
  },
  {
    "node": "Mas d’en Blanc",
    "label": "Mas d’en Blanc",
    "location": "Spain"
  },
  {
    "node": "Mas d’en Blanc",
    "label": "Mas d’en Blanc",
    "location": "Vespella de Gaià"
  },
  {
    "node": "Mas d’en Grau - Comes d'en Bonet",
    "label": "Mas d’en Grau - Comes d'en Bonet",
    "location": "Tarragona"
  },
  {
    "node": "Mas d’en Grau - Comes d'en Bonet",
    "label": "Mas d’en Grau - Comes d'en Bonet",
    "location": "Corbera d'Ebre"
  },
  {
    "node": "Masia Can Rovira",
    "label": "Masia Can Rovira",
    "location": "Spain"
  },
  {
    "node": "Masia Can Rovira",
    "label": "Masia Can Rovira",
    "location": "Barcelona"
  },
  {
    "node": "Masia Can Rovira",
    "label": "Masia Can Rovira",
    "location": "Gurb"
  },
  {
    "node": "Masia De Sanromà",
    "label": "Masia De Sanromà",
    "location": "Tarragona"
  },
  {
    "node": "Masia De Sanromà",
    "label": "Masia De Sanromà",
    "location": "Spain"
  },
  {
    "node": "Masia De Sanromà",
    "label": "Masia De Sanromà",
    "location": "Bellvei"
  },
  {
    "node": "Masia Subirana",
    "label": "Masia Subirana",
    "location": "Spain"
  },
  {
    "node": "Masia Subirana",
    "label": "Masia Subirana",
    "location": "Barcelona"
  },
  {
    "node": "Masia Subirana",
    "label": "Masia Subirana",
    "location": "Sant Julià de Cerdanyola"
  },
  {
    "node": "Mausoleu De Les Víctimes De La Repressió A La Rereguarda. Cementiri De Solivella",
    "label": "Mausoleu De Les Víctimes De La Repressió A La Rereguarda. Cementiri De Solivella",
    "location": "Tarragona"
  },
  {
    "node": "Mausoleu De Les Víctimes De La Repressió A La Rereguarda. Cementiri De Solivella",
    "label": "Mausoleu De Les Víctimes De La Repressió A La Rereguarda. Cementiri De Solivella",
    "location": "Solivella"
  },
  {
    "node": "Mausoleu dels montcadencs víctimes de la violència a la rereguarda. Cementiri de Montcada i Reixac",
    "label": "Mausoleu dels montcadencs víctimes de la violència a la rereguarda. Cementiri de Montcada i Reixac",
    "location": "Spain"
  },
  {
    "node": "Mausoleu dels montcadencs víctimes de la violència a la rereguarda. Cementiri de Montcada i Reixac",
    "label": "Mausoleu dels montcadencs víctimes de la violència a la rereguarda. Cementiri de Montcada i Reixac",
    "location": "Barcelona"
  },
  {
    "node": "Mausoleu dels montcadencs víctimes de la violència a la rereguarda. Cementiri de Montcada i Reixac",
    "label": "Mausoleu dels montcadencs víctimes de la violència a la rereguarda. Cementiri de Montcada i Reixac",
    "location": "Montcada i Reixac"
  },
  {
    "node": "Molina De Josepet",
    "label": "Molina De Josepet",
    "location": "Spain"
  },
  {
    "node": "Molina De Josepet",
    "label": "Molina De Josepet",
    "location": "Rialp"
  },
  {
    "node": "Muntanya De La Fembra Morta",
    "label": "Muntanya De La Fembra Morta",
    "location": "Spain"
  },
  {
    "node": "Muntanya De La Fembra Morta",
    "label": "Muntanya De La Fembra Morta",
    "location": "Castellolí"
  },
  {
    "node": "Nínxol Isidre Formentí Turet. Cementiri de Juncosa",
    "label": "Nínxol Isidre Formentí Turet. Cementiri de Juncosa",
    "location": "Juncosa"
  },
  {
    "node": "Nínxol de Magdalena Girth al cementiri de Sant Feliu de Guíxols",
    "label": "Nínxol de Magdalena Girth al cementiri de Sant Feliu de Guíxols",
    "location": "Spain"
  },
  {
    "node": "Nínxol de Magdalena Girth al cementiri de Sant Feliu de Guíxols",
    "label": "Nínxol de Magdalena Girth al cementiri de Sant Feliu de Guíxols",
    "location": "Girona"
  },
  {
    "node": "Nínxol de Magdalena Girth al cementiri de Sant Feliu de Guíxols",
    "label": "Nínxol de Magdalena Girth al cementiri de Sant Feliu de Guíxols",
    "location": "Sant Feliu de Guíxols"
  },
  {
    "node": "Nínxol de Marcos Goñi Almándoz",
    "label": "Nínxol de Marcos Goñi Almándoz",
    "location": "Spain"
  },
  {
    "node": "Nínxol de Marcos Goñi Almándoz",
    "label": "Nínxol de Marcos Goñi Almándoz",
    "location": "Barcelona"
  },
  {
    "node": "Nínxol de Marcos Goñi Almándoz",
    "label": "Nínxol de Marcos Goñi Almándoz",
    "location": "Montcada i Reixac"
  },
  {
    "node": "Nínxol del cementiri dels Arcs",
    "label": "Nínxol del cementiri dels Arcs",
    "location": "Spain"
  },
  {
    "node": "Nínxol del cementiri dels Arcs",
    "label": "Nínxol del cementiri dels Arcs",
    "location": "Lleida"
  },
  {
    "node": "Nínxol del cementiri dels Arcs",
    "label": "Nínxol del cementiri dels Arcs",
    "location": "Bellvís"
  },
  {
    "node": "Nínxols de Brigadistes Internacionals al cementiri de Sant Feliu de Guíxols",
    "label": "Nínxols de Brigadistes Internacionals al cementiri de Sant Feliu de Guíxols",
    "location": "Spain"
  },
  {
    "node": "Nínxols de Brigadistes Internacionals al cementiri de Sant Feliu de Guíxols",
    "label": "Nínxols de Brigadistes Internacionals al cementiri de Sant Feliu de Guíxols",
    "location": "Girona"
  },
  {
    "node": "Nínxols de Brigadistes Internacionals al cementiri de Sant Feliu de Guíxols",
    "label": "Nínxols de Brigadistes Internacionals al cementiri de Sant Feliu de Guíxols",
    "location": "Sant Feliu de Guíxols"
  },
  {
    "node": "Nínxols de Brigadistes del cementiri de Tàrrega",
    "label": "Nínxols de Brigadistes del cementiri de Tàrrega",
    "location": "Spain"
  },
  {
    "node": "Nínxols de Brigadistes del cementiri de Tàrrega",
    "label": "Nínxols de Brigadistes del cementiri de Tàrrega",
    "location": "Lleida"
  },
  {
    "node": "Nínxols de Brigadistes del cementiri de Tàrrega",
    "label": "Nínxols de Brigadistes del cementiri de Tàrrega",
    "location": "Tàrrega"
  },
  {
    "node": "Oliola: Al voltant de la població",
    "label": "Oliola: Al voltant de la població",
    "location": "Spain"
  },
  {
    "node": "Oliola: Al voltant de la població",
    "label": "Oliola: Al voltant de la població",
    "location": "Oliola"
  },
  {
    "node": "Panteó dels militars de la Mestrança d'Artilleria",
    "label": "Panteó dels militars de la Mestrança d'Artilleria",
    "location": "Montcada i Reixac"
  },
  {
    "node": "Partida De La Cova (Malladeta)",
    "label": "Partida De La Cova (Malladeta)",
    "location": "Tarragona"
  },
  {
    "node": "Partida De La Cova (Malladeta)",
    "label": "Partida De La Cova (Malladeta)",
    "location": "Spain"
  },
  {
    "node": "Partida De La Cova (Malladeta)",
    "label": "Partida De La Cova (Malladeta)",
    "location": "El Perelló"
  },
  {
    "node": "Partida De Les Espadelles - Balma",
    "label": "Partida De Les Espadelles - Balma",
    "location": "Spain"
  },
  {
    "node": "Partida De Les Espadelles - Balma",
    "label": "Partida De Les Espadelles - Balma",
    "location": "Margalef"
  },
  {
    "node": "Partida Del Mataret",
    "label": "Partida Del Mataret",
    "location": "Spain"
  },
  {
    "node": "Partida Del Mataret",
    "label": "Partida Del Mataret",
    "location": "L'Ampolla"
  },
  {
    "node": "Partida Del Negral De Bellvís",
    "label": "Partida Del Negral De Bellvís",
    "location": "Spain"
  },
  {
    "node": "Partida Del Negral De Bellvís",
    "label": "Partida Del Negral De Bellvís",
    "location": "Lleida"
  },
  {
    "node": "Partida Del Negral De Bellvís",
    "label": "Partida Del Negral De Bellvís",
    "location": "Bellvís"
  },
  {
    "node": "Partida La Costa",
    "label": "Partida La Costa",
    "location": "Spain"
  },
  {
    "node": "Partida La Costa",
    "label": "Partida La Costa",
    "location": "la Bisbal de Montsant"
  },
  {
    "node": "Partida Les Àligues - Joveres",
    "label": "Partida Les Àligues - Joveres",
    "location": "Spain"
  },
  {
    "node": "Partida Les Àligues - Joveres",
    "label": "Partida Les Àligues - Joveres",
    "location": "la Bisbal de Montsant"
  },
  {
    "node": "Partida Pla de Junquet - Coma",
    "label": "Partida Pla de Junquet - Coma",
    "location": "la Bisbal de Montsant"
  },
  {
    "node": "Partida de Salanques",
    "label": "Partida de Salanques",
    "location": "Tarragona"
  },
  {
    "node": "Partida de Salanques",
    "label": "Partida de Salanques",
    "location": "Spain"
  },
  {
    "node": "Partida de Salanques",
    "label": "Partida de Salanques",
    "location": "Poboleda"
  },
  {
    "node": "Partida dels Prats a Mont-roig del Camp",
    "label": "Partida dels Prats a Mont-roig del Camp",
    "location": "Tarragona"
  },
  {
    "node": "Partida dels Prats a Mont-roig del Camp",
    "label": "Partida dels Prats a Mont-roig del Camp",
    "location": "Spain"
  },
  {
    "node": "Partida dels Prats a Mont-roig del Camp",
    "label": "Partida dels Prats a Mont-roig del Camp",
    "location": "Mont-roig del Camp"
  },
  {
    "node": "Peixera d'Aspa",
    "label": "Peixera d'Aspa",
    "location": "Spain"
  },
  {
    "node": "Peixera d'Aspa",
    "label": "Peixera d'Aspa",
    "location": "Lleida"
  },
  {
    "node": "Peixera d'Aspa",
    "label": "Peixera d'Aspa",
    "location": "El Cogul"
  },
  {
    "node": "Pineda A Prop Del Camp Dels Morts",
    "label": "Pineda A Prop Del Camp Dels Morts",
    "location": "Spain"
  },
  {
    "node": "Pineda A Prop Del Camp Dels Morts",
    "label": "Pineda A Prop Del Camp Dels Morts",
    "location": "Lleida"
  },
  {
    "node": "Pineda A Prop Del Camp Dels Morts",
    "label": "Pineda A Prop Del Camp Dels Morts",
    "location": "Castellar de la Ribera"
  },
  {
    "node": "Pla Moran",
    "label": "Pla Moran",
    "location": "Pradell de la Teixeta"
  },
  {
    "node": "Pla de Bassar. Partida del mas Blanc",
    "label": "Pla de Bassar. Partida del mas Blanc",
    "location": "Tarragona"
  },
  {
    "node": "Pla de Bassar. Partida del mas Blanc",
    "label": "Pla de Bassar. Partida del mas Blanc",
    "location": "Spain"
  },
  {
    "node": "Pla de Bassar. Partida del mas Blanc",
    "label": "Pla de Bassar. Partida del mas Blanc",
    "location": "L'Albiol"
  },
  {
    "node": "Pla dels Panteons. Cementiri de Mataró",
    "label": "Pla dels Panteons. Cementiri de Mataró",
    "location": "Spain"
  },
  {
    "node": "Pla dels Panteons. Cementiri de Mataró",
    "label": "Pla dels Panteons. Cementiri de Mataró",
    "location": "Barcelona"
  },
  {
    "node": "Pla dels Panteons. Cementiri de Mataró",
    "label": "Pla dels Panteons. Cementiri de Mataró",
    "location": "Mataró"
  },
  {
    "node": "Plandiranes: Figuerola D'orcau",
    "label": "Plandiranes: Figuerola D'orcau",
    "location": "Spain"
  },
  {
    "node": "Plandiranes: Figuerola D'orcau",
    "label": "Plandiranes: Figuerola D'orcau",
    "location": "Lleida"
  },
  {
    "node": "Plandiranes: Figuerola D'orcau",
    "label": "Plandiranes: Figuerola D'orcau",
    "location": "Isona i Conca Dellà"
  },
  {
    "node": "Planell De Campirme",
    "label": "Planell De Campirme",
    "location": "Spain"
  },
  {
    "node": "Planell De Campirme",
    "label": "Planell De Campirme",
    "location": "Llavorsí"
  },
  {
    "node": "Plans De Rafel",
    "label": "Plans De Rafel",
    "location": "Spain"
  },
  {
    "node": "Plans De Rafel",
    "label": "Plans De Rafel",
    "location": "Batea"
  },
  {
    "node": "Pleta Barrada",
    "label": "Pleta Barrada",
    "location": "Spain"
  },
  {
    "node": "Pleta Barrada",
    "label": "Pleta Barrada",
    "location": "Gimenells i el Pla de la Font"
  },
  {
    "node": "Poliespotiu del Soleràs",
    "label": "Poliespotiu del Soleràs",
    "location": "Spain"
  },
  {
    "node": "Poliespotiu del Soleràs",
    "label": "Poliespotiu del Soleràs",
    "location": "Lleida"
  },
  {
    "node": "Poliespotiu del Soleràs",
    "label": "Poliespotiu del Soleràs",
    "location": "El Soleràs"
  },
  {
    "node": "Pont D'adrall",
    "label": "Pont D'adrall",
    "location": "Spain"
  },
  {
    "node": "Pont D'adrall",
    "label": "Pont D'adrall",
    "location": "Adrall"
  },
  {
    "node": "Pont De La Borda Dels Rengars",
    "label": "Pont De La Borda Dels Rengars",
    "location": "Spain"
  },
  {
    "node": "Pont De La Borda Dels Rengars",
    "label": "Pont De La Borda Dels Rengars",
    "location": "Lleida"
  },
  {
    "node": "Pont De La Borda Dels Rengars",
    "label": "Pont De La Borda Dels Rengars",
    "location": "La Guingueta d'Àneu"
  },
  {
    "node": "Pont de Guils",
    "label": "Pont de Guils",
    "location": "Lleida"
  },
  {
    "node": "Pont de Guils",
    "label": "Pont de Guils",
    "location": "Castellàs"
  },
  {
    "node": "Pont de Montellà",
    "label": "Pont de Montellà",
    "location": "Spain"
  },
  {
    "node": "Pont de Montellà",
    "label": "Pont de Montellà",
    "location": "Martinet"
  },
  {
    "node": "Pou De Pich I Aguilera",
    "label": "Pou De Pich I Aguilera",
    "location": "Tarragona"
  },
  {
    "node": "Pou De Pich I Aguilera",
    "label": "Pou De Pich I Aguilera",
    "location": "Spain"
  },
  {
    "node": "Pou De Pich I Aguilera",
    "label": "Pou De Pich I Aguilera",
    "location": "Reus"
  },
  {
    "node": "Pou Del Baró",
    "label": "Pou Del Baró",
    "location": "Tarragona"
  },
  {
    "node": "Pou Del Baró",
    "label": "Pou Del Baró",
    "location": "Catalunya"
  },
  {
    "node": "Pou Del Baró",
    "label": "Pou Del Baró",
    "location": "Spain"
  },
  {
    "node": "Pou Del Baró",
    "label": "Pou Del Baró",
    "location": "Terra Alta"
  },
  {
    "node": "Pou Del Baró",
    "label": "Pou Del Baró",
    "location": "Gandesa"
  },
  {
    "node": "Prat De Sant Clem",
    "label": "Prat De Sant Clem",
    "location": "La Torre de Capdella"
  },
  {
    "node": "Prat De Ton D'iguan / Prat De Giranto",
    "label": "Prat De Ton D'iguan / Prat De Giranto",
    "location": "Spain"
  },
  {
    "node": "Prat De Ton D'iguan / Prat De Giranto",
    "label": "Prat De Ton D'iguan / Prat De Giranto",
    "location": "Alt Àneu"
  },
  {
    "node": "Prat del Cerni",
    "label": "Prat del Cerni",
    "location": "Spain"
  },
  {
    "node": "Prat del Cerni",
    "label": "Prat del Cerni",
    "location": "Sant Romà d'Abella"
  },
  {
    "node": "Propietat D'en Josep Roy. Traslladada Al Valle De Los Caídos.",
    "label": "Propietat D'en Josep Roy. Traslladada Al Valle De Los Caídos.",
    "location": "Rialp"
  },
  {
    "node": "Punta de la Sinyora",
    "label": "Punta de la Sinyora",
    "location": "Juncosa"
  },
  {
    "node": "Punta del Sacarrenyo",
    "label": "Punta del Sacarrenyo",
    "location": "Spain"
  },
  {
    "node": "Punta del Sacarrenyo",
    "label": "Punta del Sacarrenyo",
    "location": "Lleida"
  },
  {
    "node": "Punta del Sacarrenyo",
    "label": "Punta del Sacarrenyo",
    "location": "El Cogul"
  },
  {
    "node": "Punta dels Sabaters",
    "label": "Punta dels Sabaters",
    "location": "Spain"
  },
  {
    "node": "Punta dels Sabaters",
    "label": "Punta dels Sabaters",
    "location": "Lleida"
  },
  {
    "node": "Punta dels Sabaters",
    "label": "Punta dels Sabaters",
    "location": "La Granadella"
  },
  {
    "node": "Pàndols - Ermita De Santa Magdalena",
    "label": "Pàndols - Ermita De Santa Magdalena",
    "location": "Tarragona"
  },
  {
    "node": "Pàndols - Ermita De Santa Magdalena",
    "label": "Pàndols - Ermita De Santa Magdalena",
    "location": "Spain"
  },
  {
    "node": "Pàndols - Ermita De Santa Magdalena",
    "label": "Pàndols - Ermita De Santa Magdalena",
    "location": "El Pinell de Brai"
  },
  {
    "node": "Pàndols/Cota 698",
    "label": "Pàndols/Cota 698",
    "location": "Spain"
  },
  {
    "node": "Pàndols/Cota 698",
    "label": "Pàndols/Cota 698",
    "location": "El Pinell de Brai"
  },
  {
    "node": "Quatre Camins",
    "label": "Quatre Camins",
    "location": "Spain"
  },
  {
    "node": "Quatre Camins",
    "label": "Quatre Camins",
    "location": "Ascó"
  },
  {
    "node": "Rabós, Prop Del Coll De Banyuls",
    "label": "Rabós, Prop Del Coll De Banyuls",
    "location": "Spain"
  },
  {
    "node": "Rabós, Prop Del Coll De Banyuls",
    "label": "Rabós, Prop Del Coll De Banyuls",
    "location": "Rabós"
  },
  {
    "node": "Racó Dels Italians Del Cementiri Del Cogul",
    "label": "Racó Dels Italians Del Cementiri Del Cogul",
    "location": "Spain"
  },
  {
    "node": "Racó Dels Italians Del Cementiri Del Cogul",
    "label": "Racó Dels Italians Del Cementiri Del Cogul",
    "location": "Lleida"
  },
  {
    "node": "Racó Dels Italians Del Cementiri Del Cogul",
    "label": "Racó Dels Italians Del Cementiri Del Cogul",
    "location": "El Cogul"
  },
  {
    "node": "Racó del Quico",
    "label": "Racó del Quico",
    "location": "Spain"
  },
  {
    "node": "Racó del Quico",
    "label": "Racó del Quico",
    "location": "Lleida"
  },
  {
    "node": "Racó del Quico",
    "label": "Racó del Quico",
    "location": "Granyena de les Garrigues"
  },
  {
    "node": "Rams",
    "label": "Rams",
    "location": "Spain"
  },
  {
    "node": "Rams",
    "label": "Rams",
    "location": "Lleida"
  },
  {
    "node": "Rams",
    "label": "Rams",
    "location": "Vilanova De Meià"
  },
  {
    "node": "Ribamala",
    "label": "Ribamala",
    "location": "Spain"
  },
  {
    "node": "Ribamala",
    "label": "Ribamala",
    "location": "Girona"
  },
  {
    "node": "Ribamala",
    "label": "Ribamala",
    "location": "Sant Joan de les Abadesses"
  },
  {
    "node": "Riu De Turons: Masos De Sant Marti",
    "label": "Riu De Turons: Masos De Sant Marti",
    "location": "Isona i Conca Dellà"
  },
  {
    "node": "Rocalladre: Era De La Garriga D'en Marian",
    "label": "Rocalladre: Era De La Garriga D'en Marian",
    "location": "Spain"
  },
  {
    "node": "Rocalladre: Era De La Garriga D'en Marian",
    "label": "Rocalladre: Era De La Garriga D'en Marian",
    "location": "Ulldemolins"
  },
  {
    "node": "Sant Pau: Camí D'accés A L'ermita",
    "label": "Sant Pau: Camí D'accés A L'ermita",
    "location": "Tarragona"
  },
  {
    "node": "Sant Pau: Camí D'accés A L'ermita",
    "label": "Sant Pau: Camí D'accés A L'ermita",
    "location": "Catalunya"
  },
  {
    "node": "Sant Pau: Camí D'accés A L'ermita",
    "label": "Sant Pau: Camí D'accés A L'ermita",
    "location": "Spain"
  },
  {
    "node": "Sant Pau: Camí D'accés A L'ermita",
    "label": "Sant Pau: Camí D'accés A L'ermita",
    "location": "Cabacés"
  },
  {
    "node": "Sant Pau: Camí D'accés A L'ermita",
    "label": "Sant Pau: Camí D'accés A L'ermita",
    "location": "Priorat"
  },
  {
    "node": "Sant Pere Màrtir",
    "label": "Sant Pere Màrtir",
    "location": "Spain"
  },
  {
    "node": "Sant Pere Màrtir",
    "label": "Sant Pere Màrtir",
    "location": "Barcelona"
  },
  {
    "node": "Sant Pere Màrtir",
    "label": "Sant Pere Màrtir",
    "location": "Sant Just Desvern"
  },
  {
    "node": "Senlleí, Hortoneda",
    "label": "Senlleí, Hortoneda",
    "location": "Conca de Dalt"
  },
  {
    "node": "Sepultura del soldats morts el 1944 inhumats al cementiri de Vielha",
    "label": "Sepultura del soldats morts el 1944 inhumats al cementiri de Vielha",
    "location": "Vielha e Mijaran"
  },
  {
    "node": "Serra Alta, Foradada",
    "label": "Serra Alta, Foradada",
    "location": "Foradada"
  },
  {
    "node": "Serra del Munt",
    "label": "Serra del Munt",
    "location": null
  },
  {
    "node": "Serra-seca",
    "label": "Serra-seca",
    "location": "Spain"
  },
  {
    "node": "Serra-seca",
    "label": "Serra-seca",
    "location": "Lleida"
  },
  {
    "node": "Serra-seca",
    "label": "Serra-seca",
    "location": "Prats De Lluçanès"
  },
  {
    "node": "Serra-seca",
    "label": "Serra-seca",
    "location": "Odèn"
  },
  {
    "node": "Serrat Gran, Capolat",
    "label": "Serrat Gran, Capolat",
    "location": "Spain"
  },
  {
    "node": "Serrat Gran, Capolat",
    "label": "Serrat Gran, Capolat",
    "location": "Barcelona"
  },
  {
    "node": "Serrat Gran, Capolat",
    "label": "Serrat Gran, Capolat",
    "location": "Capolat"
  },
  {
    "node": "Serrat de Voltora. Soldat republicà",
    "label": "Serrat de Voltora. Soldat republicà",
    "location": "Tarragona"
  },
  {
    "node": "Serrat de Voltora. Soldat republicà",
    "label": "Serrat de Voltora. Soldat republicà",
    "location": "Spain"
  },
  {
    "node": "Serrat de Voltora. Soldat republicà",
    "label": "Serrat de Voltora. Soldat republicà",
    "location": "La Febró"
  },
  {
    "node": "Seròs: Plana De Guinarro",
    "label": "Seròs: Plana De Guinarro",
    "location": "Spain"
  },
  {
    "node": "Seròs: Plana De Guinarro",
    "label": "Seròs: Plana De Guinarro",
    "location": "Lleida"
  },
  {
    "node": "Seròs: Plana De Guinarro",
    "label": "Seròs: Plana De Guinarro",
    "location": "Seròs"
  },
  {
    "node": "Solar Fustes Sebastià. Traslladada Al Valle De Los Caídos.",
    "label": "Solar Fustes Sebastià. Traslladada Al Valle De Los Caídos.",
    "location": "Rialp"
  },
  {
    "node": "Terme Municipal De Flix. Civils",
    "label": "Terme Municipal De Flix. Civils",
    "location": "Flix"
  },
  {
    "node": "Terme Municipal De Flix. Soldats Republicans",
    "label": "Terme Municipal De Flix. Soldats Republicans",
    "location": "Spain"
  },
  {
    "node": "Terme Municipal De Flix. Soldats Republicans",
    "label": "Terme Municipal De Flix. Soldats Republicans",
    "location": "Flix"
  },
  {
    "node": "Terme municipal Santa Creu de Jutglar",
    "label": "Terme municipal Santa Creu de Jutglar",
    "location": "Barcelona"
  },
  {
    "node": "Terme municipal Santa Creu de Jutglar",
    "label": "Terme municipal Santa Creu de Jutglar",
    "location": "Olost"
  },
  {
    "node": "Toll De Carlos",
    "label": "Toll De Carlos",
    "location": "Almatret"
  },
  {
    "node": "Tomba De Gerszon Rotholc",
    "label": "Tomba De Gerszon Rotholc",
    "location": "Tarragona"
  },
  {
    "node": "Tomba De Gerszon Rotholc",
    "label": "Tomba De Gerszon Rotholc",
    "location": "Pradell de la Teixeta"
  },
  {
    "node": "Tomba De Joan Montserrat",
    "label": "Tomba De Joan Montserrat",
    "location": "Spain"
  },
  {
    "node": "Tomba De Joan Montserrat",
    "label": "Tomba De Joan Montserrat",
    "location": "Camarasa"
  },
  {
    "node": "Tormo Matalacabra",
    "label": "Tormo Matalacabra",
    "location": "Spain"
  },
  {
    "node": "Tormo Matalacabra",
    "label": "Tormo Matalacabra",
    "location": "Lleida"
  },
  {
    "node": "Tormo Matalacabra",
    "label": "Tormo Matalacabra",
    "location": "La Granadella"
  },
  {
    "node": "Torrent Dels Albans (I)",
    "label": "Torrent Dels Albans (I)",
    "location": "Spain"
  },
  {
    "node": "Torrent Dels Albans (I)",
    "label": "Torrent Dels Albans (I)",
    "location": "Barcelona"
  },
  {
    "node": "Torrent Dels Albans (I)",
    "label": "Torrent Dels Albans (I)",
    "location": "Olesa de Bonesvalls"
  },
  {
    "node": "Torrent Dels Albans (Ii)",
    "label": "Torrent Dels Albans (Ii)",
    "location": "Catalunya"
  },
  {
    "node": "Torrent Dels Albans (Ii)",
    "label": "Torrent Dels Albans (Ii)",
    "location": "Spain"
  },
  {
    "node": "Torrent Dels Albans (Ii)",
    "label": "Torrent Dels Albans (Ii)",
    "location": "Barcelona"
  },
  {
    "node": "Torrent Dels Albans (Ii)",
    "label": "Torrent Dels Albans (Ii)",
    "location": "Olesa de Bonesvalls"
  },
  {
    "node": "Torrent Dels Albans (Ii)",
    "label": "Torrent Dels Albans (Ii)",
    "location": "Alt Penedès"
  },
  {
    "node": "Tossal Del Morull",
    "label": "Tossal Del Morull",
    "location": "Spain"
  },
  {
    "node": "Tossal Del Morull",
    "label": "Tossal Del Morull",
    "location": "Lleida"
  },
  {
    "node": "Tossal Del Morull",
    "label": "Tossal Del Morull",
    "location": "Bellaguarda"
  },
  {
    "node": "Tossal Gros",
    "label": "Tossal Gros",
    "location": "Spain"
  },
  {
    "node": "Tossal Gros",
    "label": "Tossal Gros",
    "location": "Lleida"
  },
  {
    "node": "Tossal Gros",
    "label": "Tossal Gros",
    "location": "Alfés"
  },
  {
    "node": "Tossal Rodó",
    "label": "Tossal Rodó",
    "location": "Spain"
  },
  {
    "node": "Tossal Rodó",
    "label": "Tossal Rodó",
    "location": "Lleida"
  },
  {
    "node": "Tossal Rodó",
    "label": "Tossal Rodó",
    "location": "Castelldans"
  },
  {
    "node": "Tros De Marieta: Rialp",
    "label": "Tros De Marieta: Rialp",
    "location": "Rialp"
  },
  {
    "node": "Vall De L'aubaga. Poble Vell",
    "label": "Vall De L'aubaga. Poble Vell",
    "location": "Tarragona"
  },
  {
    "node": "Vall De L'aubaga. Poble Vell",
    "label": "Vall De L'aubaga. Poble Vell",
    "location": "Spain"
  },
  {
    "node": "Vall De L'aubaga. Poble Vell",
    "label": "Vall De L'aubaga. Poble Vell",
    "location": "Corbera d'Ebre"
  },
  {
    "node": "Vall De La Torre",
    "label": "Vall De La Torre",
    "location": "Spain"
  },
  {
    "node": "Vall De La Torre",
    "label": "Vall De La Torre",
    "location": "Corbera d'Ebre"
  },
  {
    "node": "Vallada De Sarió",
    "label": "Vallada De Sarió",
    "location": "Tarragona"
  },
  {
    "node": "Vallada De Sarió",
    "label": "Vallada De Sarió",
    "location": "Spain"
  },
  {
    "node": "Vallada De Sarió",
    "label": "Vallada De Sarió",
    "location": "Gandesa"
  },
  {
    "node": "Valldefons",
    "label": "Valldefons",
    "location": "Flix"
  },
  {
    "node": "Venta Fusellé (Fàbrica Cortiella)",
    "label": "Venta Fusellé (Fàbrica Cortiella)",
    "location": "Tarragona"
  },
  {
    "node": "Venta Fusellé (Fàbrica Cortiella)",
    "label": "Venta Fusellé (Fàbrica Cortiella)",
    "location": "Spain"
  },
  {
    "node": "Venta Fusellé (Fàbrica Cortiella)",
    "label": "Venta Fusellé (Fàbrica Cortiella)",
    "location": "Gandesa"
  },
  {
    "node": "Vessant De La Creu De Salitons, Casserres",
    "label": "Vessant De La Creu De Salitons, Casserres",
    "location": "Spain"
  },
  {
    "node": "Vessant De La Creu De Salitons, Casserres",
    "label": "Vessant De La Creu De Salitons, Casserres",
    "location": "Barcelona"
  },
  {
    "node": "Vessant De La Creu De Salitons, Casserres",
    "label": "Vessant De La Creu De Salitons, Casserres",
    "location": "Casserres"
  },
  {
    "node": "Vinyes de la Casa Llarga - Font de la Capella",
    "label": "Vinyes de la Casa Llarga - Font de la Capella",
    "location": "Spain"
  },
  {
    "node": "Vinyes de la Casa Llarga - Font de la Capella",
    "label": "Vinyes de la Casa Llarga - Font de la Capella",
    "location": "Subirats"
  },
  {
    "node": "Vinyetes De Casa Corona",
    "label": "Vinyetes De Casa Corona",
    "location": "Spain"
  },
  {
    "node": "Vinyetes De Casa Corona",
    "label": "Vinyetes De Casa Corona",
    "location": "Lleida"
  },
  {
    "node": "Vinyetes De Casa Corona",
    "label": "Vinyetes De Casa Corona",
    "location": "La Granadella"
  },
  {
    "node": "Cementiri de la Jonquera",
    "label": null,
    "location": "La Jonquera"
  },
  {
    "node": "Camí de la Font d'Ullastrell",
    "label": null,
    "location": "Ullastrell"
  },
  {
    "node": "Pla del Blanco",
    "label": null,
    "location": "Artesa de Lleida"
  },
  {
    "node": "Cementiri vell de Sant Julià de Ramis",
    "label": null,
    "location": "Sant Julià de Ramis"
  },
  {
    "node": "Els Tossals d'Aldover",
    "label": null,
    "location": "Aldover"
  },
  {
    "node": "Exterior del Santuari del Miracle",
    "label": null,
    "location": "Riner"
  },
  {
    "node": "Cementiri de Su",
    "label": null,
    "location": "Riner"
  },
  {
    "node": "Cementiri de Sant Just de Joval",
    "label": null,
    "location": "Clariana de Cardener"
  },
  {
    "node": "Cementiri de Clariana de Cardener",
    "label": null,
    "location": "Clariana de Cardener"
  },
  {
    "node": "Casa Rovira-Sança",
    "label": null,
    "location": "Llobera"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:652",
    "label": null,
    "location": "Tarragona"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:652",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:652",
    "label": null,
    "location": "Amposta"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:653",
    "label": null,
    "location": "Tarragona"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:653",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:653",
    "label": null,
    "location": "El Lloar"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:654",
    "label": null,
    "location": "Tarragona"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:654",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:654",
    "label": null,
    "location": "Margalef"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:655",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:655",
    "label": null,
    "location": "Lleida"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:655",
    "label": null,
    "location": "L'Albagés"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:656",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:656",
    "label": null,
    "location": "Lleida"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:656",
    "label": null,
    "location": "Bell-lloc d'Urgell"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:657",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:657",
    "label": null,
    "location": "Girona"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:657",
    "label": null,
    "location": "Sant Martí d'Empúries"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:658",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:658",
    "label": null,
    "location": "Lleida"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:658",
    "label": null,
    "location": "Guissona"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:659",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:659",
    "label": null,
    "location": "Lleida"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:659",
    "label": null,
    "location": "La Floresta"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:660",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:660",
    "label": null,
    "location": "Lleida"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:660",
    "label": null,
    "location": "Agramunt"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:661",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:661",
    "label": null,
    "location": "Lleida"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:661",
    "label": null,
    "location": "Ivars D'Urgell"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:662",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:2885",
    "label": null,
    "location": "Spain"
  },
  {
    "node": "4:8fe754b2-5d6b-4db6-9374-cf11f861e0f7:2885",
    "label": null,
    "location": "Fosa de Prades"
  }
]
```

> does this data answers the query correctly?

Second time:
```json
[
  {
    "type": "Person",
    "count": 1029
  },
  {
    "type": "Document",
    "count": 724
  },
  {
    "type": "MassGrave",
    "count": 492
  },
  {
    "type": "Location",
    "count": 411
  },
  {
    "type": "Organization",
    "count": 156
  },
  {
    "type": "Country",
    "count": 42
  },
  {
    "type": "Event",
    "count": 36
  }
]
```

Screen:
![[Screenshot 2026-04-16 at 8.07.13 PM.png]]
> why the Json copied from UI contains more entity types and the UI the ones present on screen?

### Statistics (Server)
```sql
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT ?type (COUNT(DISTINCT ?entity) AS ?count) WHERE { { ?entity a <http://www.wikidata.org/entity/Q5> . BIND(\"Brigadists\" AS ?type) } UNION { ?entity a <http://www.wikidata.org/entity/Q108163> . BIND(\"Mass graves\" AS ?type) } UNION { ?entity a <http://www.wikidata.org/entity/Q49848> . BIND(\"Documents\" AS ?type) } } GROUP BY ?type ORDER BY ?type",
    "format": "json"
  }'
```

#### Results:
```json
{
  "results": [
    {
      "category": "Brigadists",
      "count": 1030
    },
    {
      "category": "Mass graves",
      "count": 492
    },
    {
      "category": "Documents",
      "count": 724
    }
  ],
  "columns": [
    "category",
    "count"
  ]
}
```


### Entity Types (UI)

```Sparql
SELECT DISTINCT ?type (COUNT(?node) AS ?count)
WHERE {
  ?node <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> ?type .
}
GROUP BY ?type
ORDER BY DESC(?count)
LIMIT 20
```

#### Results
```json
[
  {
    "type": "Person",
    "count": 1029
  },
  {
    "type": "Document",
    "count": 724
  },
  {
    "type": "MassGrave",
    "count": 492
  },
  {
    "type": "Location",
    "count": 411
  },
  {
    "type": "Organization",
    "count": 156
  },
  {
    "type": "Country",
    "count": 42
  },
  {
    "type": "Event",
    "count": 36
  }
]
```

### Entity Types (Server)
```Sparql
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT DISTINCT ?type (COUNT(?node) AS ?count) WHERE { ?node <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> ?type . } GROUP BY ?type ORDER BY DESC(?count) LIMIT 20",
    "format": "json"
  }'
```

#### Results:
```json
{
  "results": [
    {
      "category": "Person",
      "count": 1030
    },
    {
      "category": "Document",
      "count": 724
    },
    {
      "category": "MassGrave",
      "count": 492
    },
    {
      "category": "Location",
      "count": 417
    },
    {
      "category": "Organization",
      "count": 171
    },
    {
      "category": "Country",
      "count": 42
    },
    {
      "category": "Event",
      "count": 39
    }
  ],
  "columns": [
    "category",
    "count"
  ]
}
```



## Test 1 – Total number of nodes 

Objective: verify the global size of the graph at node level as a baseline control metric before any other evaluation.

### Cypher:

```cypher
MATCH (n)
RETURN count(n) AS totalNodes;
```
#### Cypher results (JSON)
```
[
  {
    "totalNodes": 2890
  }
]
```
### SPARQL:
```sparql
SELECT (COUNT(DISTINCT ?n) AS ?totalNodes)
WHERE {
  {
    ?n ?p ?o .
  }
  UNION
  {
    ?s ?p ?n .
  }
}
```
#### SPARQL results (JSON)
```Sparql
Error: Request failed with status code 500
```

### Server:
```
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT (COUNT(DISTINCT ?n) AS ?totalNodes) WHERE { { ?n ?p ?o . } UNION { ?s ?p ?n . } }",
    "format": "json"
  }'
```

#### Results 1:
```json
STATUS: 500
Internal Server Error
```
#### Results 2
```json

curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT (COUNT(DISTINCT ?n) AS ?totalNodes) WHERE { { ?n ?p ?o . } UNION { ?s ?p ?n . } }",
    "format": "json"
  }'
{"results":[{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890},{"totalNodes":2890}],"columns":["totalNodes"]}%                
```

> observación: aggregation/cardinality bug? I evaluated the query and the eval plat says that might be a server problem. 

#### Results 3
```
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT (COUNT(DISTINCT ?n) AS ?totalNodes) WHERE { { ?n ?p ?o . } UNION { ?s ?p ?n . } }",
    "format": "json"
  }'curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT (COUNT(DISTINCT ?n) AS ?totalNodes) WHERE { { ?n ?p ?o . } UNION { ?s ?p ?n . } }",
    "format": "json"
  }'
curl: (22) The requested URL returned error: 422
{"detail":[{"type":"json_invalid","loc":["body",131],"msg":"JSON decode error","input":{},"ctx":{"error":"Extra data"}}]}curl: (22) The requested URL returned error: 422
{"detail":[{"type":"json_invalid","loc":["body",131],"msg":"JSON decode error","input":{},"ctx":{"error":"Extra data"}}]}%
```
## Test 2 – Total number of relationships

Objective: verify the global size of the graph at relationship/triple level and track growth or loss across runs.

### Cypher
```cypher
MATCH ()-[r]->()
RETURN count(r) AS totalRelationships;
```
#### Cypher results (JSON)
```
[
  {
    "totalRelationships": 4482
  }
]
```
### SPARQL:
```
SELECT (COUNT(*) AS ?totalRelationships)
WHERE {
  ?subject ?predicate ?object .
}
```
#### SPARQL results (JSON)
```
Error: timeout of 30000ms exceeded
```

### Server:
```
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT (COUNT(*) AS ?totalRelationships) WHERE { ?subject ?predicate ?object . }",
    "format": "json"
  }'
```

#### Results:
```json
STATUS: 500
Internal Server Error
```


## Test 3 – Nodes per label (overview)
Objective: identify the semantic classes present in the graph and confirm that expected node types are available.

### Cypher
```cypher
CALL db.labels()
YIELD label
RETURN label
ORDER BY label;
```
#### Cypher results (JSON)
```json
[
  {
    "label": "Chunk"
  },
  {
    "label": "Country"
  },
  {
    "label": "Document"
  },
  {
    "label": "Event"
  },
  {
    "label": "Location"
  },
  {
    "label": "MassGrave"
  },
  {
    "label": "Organization"
  },
  {
    "label": "Person"
  }
]
```
### SPARQL:
```
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT DISTINCT ?label
WHERE {
  ?n rdf:type ?label .
}
ORDER BY ?label
```
#### SPARQL results (JSON)
```
Error: timeout of 30000ms exceeded
```

### Server:
```
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> SELECT DISTINCT ?label WHERE { ?n rdf:type ?label . } ORDER BY ?label",
    "format": "json"
  }'
```

#### Results:
```json
STATUS: 500
Internal Server Error
```

#### Server results (JSON)
```
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> SELECT DISTINCT ?label WHERE { ?n rdf:type ?label . } ORDER BY ?label",
    "format": "json"
  }'
curl: (22) The requested URL returned error: 500
Internal Server Error%
```
## Test 4 – Relationships per type
Objective: validate that key predicates exist and estimate their volume to detect missing or under-populated relations.

### Cypher
```cypher
MATCH ()-[r:LOCATED_IN]->()
RETURN count(r) AS locatedInRels;
```
#### Cypher results (JSON)
```
[
  {
    "locatedInRels": 1684
  }
]
```
### SPARQL:
```
SELECT ?relType (COUNT(*) AS ?count)
WHERE {
  ?subject ?predicate ?object .
  BIND(STR(?predicate) AS ?relType)
}
GROUP BY ?relType
ORDER BY DESC(?count)
```
#### SPARQL results (JSON)
```
[
  {
    "locatedInRels": 1684
  }
]
```
### Server:
```
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT ?relType (COUNT(*) AS ?count) WHERE { ?subject ?predicate ?object . BIND(STR(?predicate) AS ?relType) } GROUP BY ?relType ORDER BY DESC(?count)",
    "format": "json"
  }'
```

#### Results 1:
```json
STATUS: 500
Internal Server Error
```

#### Results 2
```
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> SELECT DISTINCT ?label WHERE { ?n rdf:type ?label . } ORDER BY ?label",
    "format": "json"
  }'
curl: (22) The requested URL returned error: 500
Internal Server Error%                                                   
elenagomez@Elenas-MacBook-Pro Documents % curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "PREFIX ex: <https://example.org/ns#> SELECT (COUNT(*) AS ?locatedInRels) WHERE { ?subject ex:LOCATED_IN ?object . }",
    "format": "json"
  }'
```
## Test 5 – Approximate number of properties on nodes
### Query 1 - Node properties: list all keys and how many nodes have each

Objective: measure metadata coverage across node attributes and identify sparse or overused properties.

#### Cypher
```Cypher
MATCH (n)
UNWIND keys(n) AS key
RETURN key AS propertyName, count(*) AS nodesWithProperty
ORDER BY nodesWithProperty DESC, propertyName;
```

##### Cypher results (JSON)
```json
[
  {
    "propertyName": "P1476",
    "nodesWithProperty": 1474
  },
  {
    "propertyName": "_normalized_name",
    "nodesWithProperty": 1392
  },
  {
    "propertyName": "name",
    "nodesWithProperty": 1392
  },
  {
    "propertyName": "id",
    "nodesWithProperty": 1116
  },
  {
    "propertyName": "P27",
    "nodesWithProperty": 674
  },
  {
    "propertyName": "titol",
    "nodesWithProperty": 410
  },
  {
    "propertyName": "id_fosa",
    "nodesWithProperty": 312
  },
  {
    "propertyName": "P625_lat",
    "nodesWithProperty": 259
  },
  {
    "propertyName": "P625_lng",
    "nodesWithProperty": 256
  },
  {
    "propertyName": "P17",
    "nodesWithProperty": 248
  },
  {
    "propertyName": "P131",
    "nodesWithProperty": 218
  },
  {
    "propertyName": "P742",
    "nodesWithProperty": 199
  },
  {
    "propertyName": "P569",
    "nodesWithProperty": 193
  },
  {
    "propertyName": "P625",
    "nodesWithProperty": 183
  },
  {
    "propertyName": "P106",
    "nodesWithProperty": 130
  },
  {
    "propertyName": "conservacio",
    "nodesWithProperty": 123
  },
  {
    "propertyName": "mida",
    "nodesWithProperty": 123
  },
  {
    "propertyName": "fitxa",
    "nodesWithProperty": 119
  },
  {
    "propertyName": "gender",
    "nodesWithProperty": 106
  },
  {
    "propertyName": "P1142",
    "nodesWithProperty": 103
  },
  {
    "propertyName": "categoria_de_fosses",
    "nodesWithProperty": 90
  },
  {
    "propertyName": "tipologia_inhumats",
    "nodesWithProperty": 90
  },
  {
    "propertyName": "comments",
    "nodesWithProperty": 73
  },
  {
    "propertyName": "context_defuncio",
    "nodesWithProperty": 60
  },
  {
    "propertyName": "category",
    "nodesWithProperty": 46
  },
  {
    "propertyName": "conservation",
    "nodesWithProperty": 40
  },
  {
    "propertyName": "size",
    "nodesWithProperty": 39
  },
  {
    "propertyName": "P570",
    "nodesWithProperty": 31
  },
  {
    "propertyName": "provincia",
    "nodesWithProperty": 30
  },
  {
    "propertyName": "url",
    "nodesWithProperty": 29
  },
  {
    "propertyName": "T_tol",
    "nodesWithProperty": 28
  },
  {
    "propertyName": "categoria",
    "nodesWithProperty": 20
  },
  {
    "propertyName": "categoria_fosses",
    "nodesWithProperty": 20
  },
  {
    "propertyName": "comarca",
    "nodesWithProperty": 20
  },
  {
    "propertyName": "comunitat_autonoma",
    "nodesWithProperty": 20
  },
  {
    "propertyName": "latitude",
    "nodesWithProperty": 19
  },
  {
    "propertyName": "longitude",
    "nodesWithProperty": 19
  },
  {
    "propertyName": "node_id",
    "nodesWithProperty": 18
  },
  {
    "propertyName": "nombre",
    "nodesWithProperty": 13
  },
  {
    "propertyName": "pais",
    "nodesWithProperty": 12
  },
  {
    "propertyName": "P131_municipality",
    "nodesWithProperty": 10
  },
  {
    "propertyName": "P131_municipio",
    "nodesWithProperty": 10
  },
  {
    "propertyName": "P131_province",
    "nodesWithProperty": 10
  },
  {
    "propertyName": "P131_provincia",
    "nodesWithProperty": 10
  },
  {
    "propertyName": "coordenadas_lat",
    "nodesWithProperty": 10
  },
  {
    "propertyName": "coordenadas_lng",
    "nodesWithProperty": 10
  },
  {
    "propertyName": "death_context",
    "nodesWithProperty": 10
  },
  {
    "propertyName": "municipio",
    "nodesWithProperty": 10
  },
  {
    "propertyName": "tipologia",
    "nodesWithProperty": 10
  },
  {
    "propertyName": "title",
    "nodesWithProperty": 10
  },
  {
    "propertyName": "typology",
    "nodesWithProperty": 10
  },
  {
    "propertyName": "victim_typology",
    "nodesWithProperty": 10
  },
  {
    "propertyName": "Categoria_de_fosses",
    "nodesWithProperty": 9
  },
  {
    "propertyName": "Comarca",
    "nodesWithProperty": 9
  },
  {
    "propertyName": "Comunitat_aut_noma",
    "nodesWithProperty": 9
  },
  {
    "propertyName": "Conservaci_",
    "nodesWithProperty": 9
  },
  {
    "propertyName": "Context_defunci_",
    "nodesWithProperty": 9
  },
  {
    "propertyName": "Fitxa",
    "nodesWithProperty": 9
  },
  {
    "propertyName": "Mida",
    "nodesWithProperty": 9
  },
  {
    "propertyName": "Tipologia_inhumats",
    "nodesWithProperty": 9
  },
  {
    "propertyName": "status",
    "nodesWithProperty": 6
  },
  {
    "propertyName": "uuid",
    "nodesWithProperty": 6
  },
  {
    "propertyName": "description",
    "nodesWithProperty": 5
  },
  {
    "propertyName": "notes",
    "nodesWithProperty": 3
  },
  {
    "propertyName": "origin",
    "nodesWithProperty": 3
  },
  {
    "propertyName": "fecha_nacimiento",
    "nodesWithProperty": 1
  },
  {
    "propertyName": "fosa_comun",
    "nodesWithProperty": 1
  },
  {
    "propertyName": "instance_of",
    "nodesWithProperty": 1
  },
  {
    "propertyName": "is_primary",
    "nodesWithProperty": 1
  }
]
```

#### SPARQL
```sparql
SELECT ?propertyName (COUNT(*) AS ?nodesWithProperty)
WHERE {
  ?n ?property ?value .
  BIND(STR(?property) AS ?propertyName)
}
GROUP BY ?propertyName
ORDER BY DESC(?nodesWithProperty) ?propertyName
```

##### SPARQL results (JSON)
```json
[
  {
    "propertyName": "LOCATED_IN",
    "nodesWithProperty": 1684
  },
  {
    "propertyName": "COUNTRY_OF_CITIZENSHIP",
    "nodesWithProperty": 883
  },
  {
    "propertyName": "DOCUMENTED_IN",
    "nodesWithProperty": 701
  },
  {
    "propertyName": "MEMBER_OF",
    "nodesWithProperty": 491
  },
  {
    "propertyName": "PARTICIPATED_IN",
    "nodesWithProperty": 291
  },
  {
    "propertyName": "TREATED_AT",
    "nodesWithProperty": 128
  },
  {
    "propertyName": "RELATED_TO",
    "nodesWithProperty": 89
  },
  {
    "propertyName": "CONTAINS",
    "nodesWithProperty": 40
  },
  {
    "propertyName": "HAS_TYPOLOGY",
    "nodesWithProperty": 39
  },
  {
    "propertyName": "AUTHORED_BY",
    "nodesWithProperty": 37
  },
  {
    "propertyName": "CAUSED_BY",
    "nodesWithProperty": 23
  },
  {
    "propertyName": "PLACE_OF_BIRTH",
    "nodesWithProperty": 23
  },
  {
    "propertyName": "BURIED_IN",
    "nodesWithProperty": 14
  },
  {
    "propertyName": "SERVED_IN",
    "nodesWithProperty": 12
  },
  {
    "propertyName": "HAS_IDEOLOGY",
    "nodesWithProperty": 10
  },
  {
    "propertyName": "TRAVELLED_TO",
    "nodesWithProperty": 5
  },
  {
    "propertyName": "HAS_OCCUPATION",
    "nodesWithProperty": 4
  },
  {
    "propertyName": "KNOWS",
    "nodesWithProperty": 3
  },
  {
    "propertyName": "DETAINED_AT",
    "nodesWithProperty": 2
  },
  {
    "propertyName": "SIBLING_OF",
    "nodesWithProperty": 2
  },
  {
    "propertyName": "partner",
    "nodesWithProperty": 1
  }
]
```

#### Server
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT ?propertyName (COUNT(*) AS ?nodesWithProperty) WHERE { ?n ?property ?value . BIND(STR(?property) AS ?propertyName) } GROUP BY ?propertyName ORDER BY DESC(?nodesWithProperty) ?propertyName",
    "format": "json"
  }'
```

##### Results:
```json
curl: (22) The requested URL returned error: 500
Internal Server Error%               
```

### Query 2 - Per relationship type: with vs. without properties

Objective: check which relationship types preserve metadata and which are being stored as bare links.

#### Cypher
```Cypher
MATCH ()-[r]->()
WITH type(r) AS relType, size(keys(r)) AS propCount
RETURN
  relType,
  count(*) AS totalRelationships,
  count(CASE WHEN propCount = 0 THEN 1 END) AS withoutProperties,
  count(CASE WHEN propCount > 0 THEN 1 END) AS withProperties
ORDER BY totalRelationships DESC, relType;

```

#### Cypher results (JSON) #op
```json
```

#### SPARQL
```sparql
SELECT ?relType
       (COUNT(*) AS ?totalRelationships)
WHERE {
  ?s ?p ?o .
  BIND(STR(?p) AS ?relType)
}
GROUP BY ?relType
ORDER BY DESC(?totalRelationships) ?relType
```

#### SPARQL results (JSON) #op
```json
```

#### Server
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT ?relType (COUNT(*) AS ?totalRelationships) WHERE { ?s ?p ?o . BIND(STR(?p) AS ?relType) } GROUP BY ?relType ORDER BY DESC(?totalRelationships) ?relType",
    "format": "json"
  }'
```

#### Results:
```json
STATUS: 500
Internal Server Error
```

### Query 3 - Relationships per label
Objective: cross-check node-label and property co-occurrence to detect uneven modelling between entity classes.

#### Cypher
```Cypher
MATCH (n)
UNWIND labels(n) AS label
UNWIND keys(n)   AS key
RETURN label, key AS propertyName, count(*) AS nodesWithProperty
ORDER BY label, nodesWithProperty DESC, propertyName;
```

#### Cypher results (JSON)
```json
[
  {
    "relType": "LOCATED_IN",
    "totalRelationships": 1684,
    "withoutProperties": 1682,
    "withProperties": 2
  },
  {
    "relType": "COUNTRY_OF_CITIZENSHIP",
    "totalRelationships": 883,
    "withoutProperties": 883,
    "withProperties": 0
  },
  {
    "relType": "DOCUMENTED_IN",
    "totalRelationships": 701,
    "withoutProperties": 701,
    "withProperties": 0
  },
  {
    "relType": "MEMBER_OF",
    "totalRelationships": 491,
    "withoutProperties": 491,
    "withProperties": 0
  },
  {
    "relType": "PARTICIPATED_IN",
    "totalRelationships": 291,
    "withoutProperties": 291,
    "withProperties": 0
  },
  {
    "relType": "TREATED_AT",
    "totalRelationships": 128,
    "withoutProperties": 126,
    "withProperties": 2
  },
  {
    "relType": "RELATED_TO",
    "totalRelationships": 89,
    "withoutProperties": 89,
    "withProperties": 0
  },
  {
    "relType": "CONTAINS",
    "totalRelationships": 40,
    "withoutProperties": 40,
    "withProperties": 0
  },
  {
    "relType": "HAS_TYPOLOGY",
    "totalRelationships": 39,
    "withoutProperties": 39,
    "withProperties": 0
  },
  {
    "relType": "AUTHORED_BY",
    "totalRelationships": 37,
    "withoutProperties": 37,
    "withProperties": 0
  },
  {
    "relType": "CAUSED_BY",
    "totalRelationships": 23,
    "withoutProperties": 23,
    "withProperties": 0
  },
  {
    "relType": "PLACE_OF_BIRTH",
    "totalRelationships": 23,
    "withoutProperties": 23,
    "withProperties": 0
  },
  {
    "relType": "BURIED_IN",
    "totalRelationships": 14,
    "withoutProperties": 14,
    "withProperties": 0
  },
  {
    "relType": "SERVED_IN",
    "totalRelationships": 12,
    "withoutProperties": 12,
    "withProperties": 0
  },
  {
    "relType": "HAS_IDEOLOGY",
    "totalRelationships": 10,
    "withoutProperties": 10,
    "withProperties": 0
  },
  {
    "relType": "TRAVELLED_TO",
    "totalRelationships": 5,
    "withoutProperties": 4,
    "withProperties": 1
  },
  {
    "relType": "HAS_OCCUPATION",
    "totalRelationships": 4,
    "withoutProperties": 4,
    "withProperties": 0
  },
  {
    "relType": "KNOWS",
    "totalRelationships": 3,
    "withoutProperties": 3,
    "withProperties": 0
  },
  {
    "relType": "DETAINED_AT",
    "totalRelationships": 2,
    "withoutProperties": 0,
    "withProperties": 2
  },
  {
    "relType": "SIBLING_OF",
    "totalRelationships": 2,
    "withoutProperties": 2,
    "withProperties": 0
  },
  {
    "relType": "partner",
    "totalRelationships": 1,
    "withoutProperties": 1,
    "withProperties": 0
  }
]
```

#### SPARQL
```sparql
SELECT ?label ?propertyName (COUNT(*) AS ?nodesWithProperty)
WHERE {
  ?n a ?labelIRI ;
     ?property ?value .
  BIND(STR(?labelIRI) AS ?label)
  BIND(STR(?property) AS ?propertyName)
}
GROUP BY ?label ?propertyName
ORDER BY ?label DESC(?nodesWithProperty) ?propertyName
```

#### SPARQL results (JSON) #op
```json
```

#### Server
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT ?label ?propertyName (COUNT(*) AS ?nodesWithProperty) WHERE { ?n a ?labelIRI ; ?property ?value . BIND(STR(?labelIRI) AS ?label) BIND(STR(?property) AS ?propertyName) } GROUP BY ?label ?propertyName ORDER BY ?label DESC(?nodesWithProperty) ?propertyName",
    "format": "json"
  }'
```

#### Results:
```json
STATUS: 500
Internal Server Error
```

## Test 6 – Approximate number of properties on relationships

### Query 1 - Count relationships with vs. without any properties (global)

Objective: quantify how much relational context is encoded as properties versus only as edge existence.

#### Cypher
```Cypher
MATCH ()-[r]->()
WITH r, size(keys(r)) AS propCount
RETURN
  count(*) AS totalRelationships,
  count(CASE WHEN propCount = 0 THEN 1 END) AS relationshipsWithoutProperties,
  count(CASE WHEN propCount > 0 THEN 1 END) AS relationshipsWithProperties;
```

##### Cypher results (JSON)
```json
[
  {
    "totalRelationships": 4482,
    "relationshipsWithoutProperties": 4475,
    "relationshipsWithProperties": 7
  }
]
```

#### SPARQL
```sparql
SELECT ?predicate (COUNT(*) AS ?edges)
WHERE {
  ?subject ?predicate ?object .
}
GROUP BY ?predicate
ORDER BY DESC(?edges)
```

##### SPARQL results (JSON) #op 
```json
```

#### Server
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT ?predicate (COUNT(*) AS ?edges) WHERE { ?subject ?predicate ?object . } GROUP BY ?predicate ORDER BY DESC(?edges)",
    "format": "json"
  }'
```

##### Results:
```json
STATUS: 500
Internal Server Error
```

## Test 7 - Database-level metadata - Interpreting "all metadata present in the knowledge base"

Structure note: this test is mostly Neo4j-admin oriented. For checks that have no strict SPARQL equivalent, SPARQL/Server blocks use the closest graph-level approximation.

### Query 1 - Show databases

Objective: confirm target database context and avoid running diagnostics against the wrong environment.

#### Cypher
```cypher
SHOW DATABASES;
```

#### Cypher results (JSON)
```json
```

#### SPARQL
```sparql
# No direct SPARQL equivalent for database catalog commands (SHOW DATABASES).
```

#### SPARQL results (JSON)
```json
```

#### Server
```bash
# N/A for SHOW DATABASES in SPARQL API.
```

#### Results:
```json
```

### Query 2 - Labels, relationship types, property keys (structural overview)

Objective: obtain a high-level schema inventory to support quality and interoperability checks.

#### Cypher
```cypher
CALL db.labels() YIELD label
RETURN label
ORDER BY label;
```

#### Cypher results (JSON)
```json
```

#### SPARQL
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT DISTINCT ?label
WHERE {
  ?n rdf:type ?label .
}
ORDER BY ?label
```

#### SPARQL results (JSON)
```json
```

#### Server
```bash
curl --fail-with-body --silent --show-error   -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}"   -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}"   -H 'Content-Type: application/json'   -H 'Accept: application/json'   -d '{
    "query": "PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> SELECT DISTINCT ?label WHERE { ?n rdf:type ?label . } ORDER BY ?label",
    "format": "json"
  }'
```

#### Results:
```json
```

### Query 3 - Node schema: which labels have which properties (with counts)

Objective: inspect label-level property structure, expected datatypes, and mandatory flags for schema consistency.

#### Cypher
```cypher
CALL db.schema.nodeTypeProperties()
YIELD nodeLabels, propertyName, propertyTypes, mandatory
RETURN nodeLabels,
       propertyName,
       propertyTypes,
       mandatory
ORDER BY nodeLabels, propertyName;
```

#### Cypher results (JSON)
```json
```

#### SPARQL
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT ?label ?propertyName (COUNT(*) AS ?nodesWithProperty)
WHERE {
  ?n rdf:type ?label ;
     ?property ?value .
  BIND(STR(?property) AS ?propertyName)
}
GROUP BY ?label ?propertyName
ORDER BY ?label DESC(?nodesWithProperty) ?propertyName
```

#### SPARQL results (JSON)
```json
```

#### Server
```bash
curl --fail-with-body --silent --show-error   -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}"   -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}"   -H 'Content-Type: application/json'   -H 'Accept: application/json'   -d '{
    "query": "PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> SELECT ?label ?propertyName (COUNT(*) AS ?nodesWithProperty) WHERE { ?n rdf:type ?label ; ?property ?value . BIND(STR(?property) AS ?propertyName) } GROUP BY ?label ?propertyName ORDER BY ?label DESC(?nodesWithProperty) ?propertyName",
    "format": "json"
  }'
```

#### Results:
```json
```

### Query 4 - All property keys registered in the database

Objective: list the full attribute vocabulary and detect uncontrolled key proliferation.

#### Cypher
```cypher
CALL db.propertyKeys() YIELD propertyKey
RETURN propertyKey
ORDER BY propertyKey;
```

#### Cypher results (JSON)
```json
```

#### SPARQL
```sparql
SELECT DISTINCT ?propertyName
WHERE {
  ?n ?property ?value .
  BIND(STR(?property) AS ?propertyName)
}
ORDER BY ?propertyName
```

#### SPARQL results (JSON)
```json
```

#### Server
```bash
curl --fail-with-body --silent --show-error   -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}"   -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}"   -H 'Content-Type: application/json'   -H 'Accept: application/json'   -d '{
    "query": "SELECT DISTINCT ?propertyName WHERE { ?n ?property ?value . BIND(STR(?property) AS ?propertyName) } ORDER BY ?propertyName",
    "format": "json"
  }'
```

#### Results:
```json
```

### Query 5 - Relationship schema: which relationship types have which properties

Objective: verify relational schema consistency and check whether edge-level attributes follow a stable model.

#### Cypher
```cypher
CALL db.schema.relTypeProperties()
YIELD relType, propertyName, propertyTypes, mandatory
RETURN relType,
       propertyName,
       propertyTypes,
       mandatory
ORDER BY relType, propertyName;
```

#### Cypher results (JSON)
```json
```

#### SPARQL
```sparql
SELECT ?relType ?propertyName (COUNT(*) AS ?relationshipsWithProperty)
WHERE {
  ?s ?predicate ?o .
  ?s ?property ?v .
  BIND(STR(?predicate) AS ?relType)
  BIND(STR(?property) AS ?propertyName)
}
GROUP BY ?relType ?propertyName
ORDER BY ?relType DESC(?relationshipsWithProperty) ?propertyName
```

#### SPARQL results (JSON)
```json
```

#### Server
```bash
curl --fail-with-body --silent --show-error   -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}"   -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}"   -H 'Content-Type: application/json'   -H 'Accept: application/json'   -d '{
    "query": "SELECT ?relType ?propertyName (COUNT(*) AS ?relationshipsWithProperty) WHERE { ?s ?predicate ?o . ?s ?property ?v . BIND(STR(?predicate) AS ?relType) BIND(STR(?property) AS ?propertyName) } GROUP BY ?relType ?propertyName ORDER BY ?relType DESC(?relationshipsWithProperty) ?propertyName",
    "format": "json"
  }'
```

#### Results:
```json
```

### Query 6 - Node property coverage by label

Shows, for each label, which property keys appear and in how many nodes.
Objective: evaluate completeness per entity type and find labels with weak metadata population.

#### Cypher
```cypher
MATCH (n)
UNWIND labels(n) AS label
UNWIND keys(n) AS propertyName
RETURN label,
       propertyName,
       count(*) AS nodesWithProperty
ORDER BY label, nodesWithProperty DESC, propertyName;
```

#### Cypher results (JSON)
```json
```

#### SPARQL
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT ?label ?propertyName (COUNT(*) AS ?nodesWithProperty)
WHERE {
  ?n rdf:type ?label ;
     ?property ?value .
  BIND(STR(?property) AS ?propertyName)
}
GROUP BY ?label ?propertyName
ORDER BY ?label DESC(?nodesWithProperty) ?propertyName
```

#### SPARQL results (JSON)
```json
```

#### Server
```bash
curl --fail-with-body --silent --show-error   -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}"   -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}"   -H 'Content-Type: application/json'   -H 'Accept: application/json'   -d '{
    "query": "PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> SELECT ?label ?propertyName (COUNT(*) AS ?nodesWithProperty) WHERE { ?n rdf:type ?label ; ?property ?value . BIND(STR(?property) AS ?propertyName) } GROUP BY ?label ?propertyName ORDER BY ?label DESC(?nodesWithProperty) ?propertyName",
    "format": "json"
  }'
```

#### Results:
```json
```

### Query 7 - Relationship property coverage by relationship type

Shows, for each relationship type, which property keys appear and in how many relationships.
Objective: evaluate completeness per predicate type and identify relations missing descriptive metadata.

#### Cypher
```cypher
MATCH ()-[r]->()
UNWIND keys(r) AS propertyName
RETURN type(r) AS relType,
       propertyName,
       count(*) AS relationshipsWithProperty
ORDER BY relType, relationshipsWithProperty DESC, propertyName;
```

#### Cypher results (JSON) #op 
```json
```

#### SPARQL
```sparql
SELECT ?relType ?propertyName (COUNT(*) AS ?relationshipsWithProperty)
WHERE {
  ?s ?predicate ?o .
  ?s ?property ?v .
  BIND(STR(?predicate) AS ?relType)
  BIND(STR(?property) AS ?propertyName)
}
GROUP BY ?relType ?propertyName
ORDER BY ?relType DESC(?relationshipsWithProperty) ?propertyName
```

#### SPARQL results (JSON) #op 
```json
```

#### Server
```bash
curl --fail-with-body --silent --show-error   -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}"   -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}"   -H 'Content-Type: application/json'   -H 'Accept: application/json'   -d '{
    "query": "SELECT ?relType ?propertyName (COUNT(*) AS ?relationshipsWithProperty) WHERE { ?s ?predicate ?o . ?s ?property ?v . BIND(STR(?predicate) AS ?relType) BIND(STR(?property) AS ?propertyName) } GROUP BY ?relType ?propertyName ORDER BY ?relType DESC(?relationshipsWithProperty) ?propertyName",
    "format": "json"
  }'
```

#### Results: #op
```json
```

### Query 8 - Node labels without any properties

Useful to detect labels that only exist structurally and store no metadata fields.
Objective: detect entity classes that may be semantically empty and require enrichment.

#### Cypher
```cypher
MATCH (n)
UNWIND labels(n) AS label
WITH label, n, size(keys(n)) AS propCount
RETURN label,
       count(*) AS totalNodes,
       count(CASE WHEN propCount = 0 THEN 1 END) AS nodesWithoutProperties,
       count(CASE WHEN propCount > 0 THEN 1 END) AS nodesWithProperties
ORDER BY nodesWithoutProperties DESC, label;
```

#### Cypher results (JSON) #op
```json
```

#### SPARQL
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT ?label (COUNT(DISTINCT ?n) AS ?totalNodes)
WHERE {
  ?n rdf:type ?label .
  FILTER NOT EXISTS { ?n ?p ?o . FILTER(?p != rdf:type) }
}
GROUP BY ?label
ORDER BY DESC(?totalNodes) ?label
```

#### SPARQL results (JSON) #op
```json
```

#### Server
```bash
curl --fail-with-body --silent --show-error   -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}"   -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}"   -H 'Content-Type: application/json'   -H 'Accept: application/json'   -d '{
    "query": "PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> SELECT ?label (COUNT(DISTINCT ?n) AS ?totalNodes) WHERE { ?n rdf:type ?label . FILTER NOT EXISTS { ?n ?p ?o . FILTER(?p != rdf:type) } } GROUP BY ?label ORDER BY DESC(?totalNodes) ?label",
    "format": "json"
  }'
```

#### Results: #op
```json
```

### Query 9 - Relationship types without any properties

Objective: detect predicate classes that may be too generic or insufficiently documented for analysis.

#### Cypher
```cypher
MATCH ()-[r]->()
WITH type(r) AS relType, r, size(keys(r)) AS propCount
RETURN relType,
       count(*) AS totalRelationships,
       count(CASE WHEN propCount = 0 THEN 1 END) AS relationshipsWithoutProperties,
       count(CASE WHEN propCount > 0 THEN 1 END) AS relationshipsWithProperties
ORDER BY relationshipsWithoutProperties DESC, relType;
```

#### Cypher results (JSON) #op
```json
```

#### SPARQL
```sparql
SELECT ?relType (COUNT(*) AS ?edges)
WHERE {
  ?s ?predicate ?o .
  BIND(STR(?predicate) AS ?relType)
}
GROUP BY ?relType
ORDER BY DESC(?edges)
```

#### SPARQL results (JSON) #op
```json
```

#### Server
```bash
curl --fail-with-body --silent --show-error   -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}"   -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}"   -H 'Content-Type: application/json'   -H 'Accept: application/json'   -d '{
    "query": "SELECT ?relType (COUNT(*) AS ?edges) WHERE { ?s ?predicate ?o . BIND(STR(?predicate) AS ?relType) } GROUP BY ?relType ORDER BY DESC(?edges)",
    "format": "json"
  }'
```

#### Results: #op
```json
```

### Query 10 - Observed value types for node properties

This gives an empirical summary of the values currently stored, beyond the schema procedures.
Objective: validate real-world datatype usage and identify type drift for the same property key.

#### Cypher
```cypher
MATCH (n)
UNWIND labels(n) AS label
UNWIND keys(n) AS propertyName
WITH label, propertyName, valueType(n[propertyName]) AS observedType
RETURN label,
       propertyName,
       observedType,
       count(*) AS occurrences
ORDER BY label, propertyName, occurrences DESC, observedType;
```

#### Cypher results (JSON) #op
```json
```

#### SPARQL
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT ?label ?propertyName (DATATYPE(?value) AS ?observedType) (COUNT(*) AS ?occurrences)
WHERE {
  ?n rdf:type ?label ;
     ?property ?value .
  BIND(STR(?property) AS ?propertyName)
}
GROUP BY ?label ?propertyName (DATATYPE(?value))
ORDER BY ?label ?propertyName DESC(?occurrences) ?observedType
```

#### SPARQL results (JSON) #op
```json
```

#### Server
```bash
curl --fail-with-body --silent --show-error   -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}"   -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}"   -H 'Content-Type: application/json'   -H 'Accept: application/json'   -d '{
    "query": "PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> SELECT ?label ?propertyName (DATATYPE(?value) AS ?observedType) (COUNT(*) AS ?occurrences) WHERE { ?n rdf:type ?label ; ?property ?value . BIND(STR(?property) AS ?propertyName) } GROUP BY ?label ?propertyName (DATATYPE(?value)) ORDER BY ?label ?propertyName DESC(?occurrences) ?observedType",
    "format": "json"
  }'
```

#### Results: #op 
```json
```

### Query 11 - Observed value types for relationship properties

Objective: validate edge-property datatype consistency and detect modelling anomalies across relation types.

#### Cypher
```cypher
MATCH ()-[r]->()
UNWIND keys(r) AS propertyName
WITH type(r) AS relType, propertyName, valueType(r[propertyName]) AS observedType
RETURN relType,
       propertyName,
       observedType,
       count(*) AS occurrences
ORDER BY relType, propertyName, occurrences DESC, observedType;
```

#### Cypher results (JSON) #op
```json
```

#### SPARQL
```sparql
SELECT ?relType ?propertyName (DATATYPE(?value) AS ?observedType) (COUNT(*) AS ?occurrences)
WHERE {
  ?s ?predicate ?o .
  ?s ?property ?value .
  BIND(STR(?predicate) AS ?relType)
  BIND(STR(?property) AS ?propertyName)
}
GROUP BY ?relType ?propertyName (DATATYPE(?value))
ORDER BY ?relType ?propertyName DESC(?occurrences) ?observedType
```

#### SPARQL results (JSON) #op
```json
```

#### Server
```bash
curl --fail-with-body --silent --show-error   -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}"   -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}"   -H 'Content-Type: application/json'   -H 'Accept: application/json'   -d '{
    "query": "SELECT ?relType ?propertyName (DATATYPE(?value) AS ?observedType) (COUNT(*) AS ?occurrences) WHERE { ?s ?predicate ?o . ?s ?property ?value . BIND(STR(?predicate) AS ?relType) BIND(STR(?property) AS ?propertyName) } GROUP BY ?relType ?propertyName (DATATYPE(?value)) ORDER BY ?relType ?propertyName DESC(?occurrences) ?observedType",
    "format": "json"
  }'
```

#### Results: #op
```json
```

# 2. Final ingestion validation block (3 databases + mapping)

Purpose: validate that the three source databases (`Cultura y censura`, `fosas comunes`, `SIDBRINT`) were ingested correctly, and that cross-source consistency rules hold.

> Note: these tests assume source/provenance values are stored in literals (for example, in a source field, source URI, or cited dataset title). If your ingestion uses different provenance fields, replace the provenance filters accordingly.

### Test A1 - Source footprint by provenance string

Objective: verify that all three expected sources are present in the graph after full ingestion.

#### Cypher
```cypher
MATCH (n)
UNWIND keys(n) AS k
WITH n, k, toLower(toString(n[k])) AS s
WITH n,
     CASE
       WHEN s CONTAINS "cultura" OR s CONTAINS "censura" THEN "cultura_y_censura"
       WHEN s CONTAINS "fosa" THEN "fosas_comunes"
       WHEN s CONTAINS "sidbrint" THEN "sidbrint"
       ELSE "other"
     END AS sourceTag
RETURN sourceTag, count(DISTINCT n) AS count
ORDER BY count DESC;
```

##### Cypher results (JSON)
```json
Error: Request failed with status code 500
```

#### SPARQL
```sparql
SELECT ?sourceTag (COUNT(DISTINCT ?node) AS ?count)
WHERE {
  ?node ?p ?src .
  FILTER(isLiteral(?src))
  BIND(LCASE(STR(?src)) AS ?s)
  BIND(
    IF(CONTAINS(?s, "cultura") || CONTAINS(?s, "censura"), "cultura_y_censura",
      IF(CONTAINS(?s, "fosa"), "fosas_comunes",
        IF(CONTAINS(?s, "sidbrint"), "sidbrint", "other")))
    AS ?sourceTag
  )
}
GROUP BY ?sourceTag
ORDER BY DESC(?count)
```

##### Results #op
```json

```

#### Server (API)
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT ?sourceTag (COUNT(DISTINCT ?node) AS ?count) WHERE { ?node ?p ?src . FILTER(isLiteral(?src)) BIND(LCASE(STR(?src)) AS ?s) BIND(IF(CONTAINS(?s, \"cultura\") || CONTAINS(?s, \"censura\"), \"cultura_y_censura\", IF(CONTAINS(?s, \"fosa\"), \"fosas_comunes\", IF(CONTAINS(?s, \"sidbrint\"), \"sidbrint\", \"other\"))) AS ?sourceTag) } GROUP BY ?sourceTag ORDER BY DESC(?count)",
    "format": "json"
  }'
```

##### Results:
```json
STATUS: 404
404 page not found
```


### Test A2 - Fosas comunes required fields completeness

Objective: validate required mapped fields (`name/title`, `country`, and at least one location field) for mass-grave entities.

#### Cypher
```cypher
MATCH (g)
WHERE any(lbl IN labels(g) WHERE lbl IN ["MassGrave","Q108163"])
RETURN
  count(DISTINCT g) AS totalMassGraves,
  count(DISTINCT CASE WHEN g.P1476 IS NOT NULL THEN g END) AS withName,
  count(DISTINCT CASE WHEN g.P17 IS NOT NULL THEN g END) AS withCountry,
  count(DISTINCT CASE WHEN g.P131 IS NOT NULL OR g.P276 IS NOT NULL THEN g END) AS withAdminLocation;
```

##### Cypher results (JSON) #op
```json
```

#### Platform (SPARQL)
```sparql
SELECT
  (COUNT(DISTINCT ?g) AS ?totalMassGraves)
  (COUNT(DISTINCT ?gWithName) AS ?withName)
  (COUNT(DISTINCT ?gWithCountry) AS ?withCountry)
  (COUNT(DISTINCT ?gWithAdmin) AS ?withAdminLocation)
WHERE {
  ?g a <http://www.wikidata.org/entity/Q108163> .
  OPTIONAL { ?g <http://www.wikidata.org/entity/P1476> ?name . BIND(?g AS ?gWithName) }
  OPTIONAL { ?g <http://www.wikidata.org/entity/P17> ?country . BIND(?g AS ?gWithCountry) }
  OPTIONAL {
    { ?g <http://www.wikidata.org/entity/P131> ?admin . }
    UNION
    { ?g <http://www.wikidata.org/entity/P276> ?admin . }
    BIND(?g AS ?gWithAdmin)
  }
}
```
##### Results #op 
```json

STATUS: 500
Internal Server Error

```
#### Server (API)
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT (COUNT(DISTINCT ?g) AS ?totalMassGraves) (COUNT(DISTINCT ?gWithName) AS ?withName) (COUNT(DISTINCT ?gWithCountry) AS ?withCountry) (COUNT(DISTINCT ?gWithAdmin) AS ?withAdminLocation) WHERE { ?g a <http://www.wikidata.org/entity/Q108163> . OPTIONAL { ?g <http://www.wikidata.org/entity/P1476> ?name . BIND(?g AS ?gWithName) } OPTIONAL { ?g <http://www.wikidata.org/entity/P17> ?country . BIND(?g AS ?gWithCountry) } OPTIONAL { { ?g <http://www.wikidata.org/entity/P131> ?admin . } UNION { ?g <http://www.wikidata.org/entity/P276> ?admin . } BIND(?g AS ?gWithAdmin) } }",
    "format": "json"
  }'
```

##### Results:
```json
STATUS: 404
404 page not found
```


### Test A3 - Fosas comunes coordinate integrity (P625)

Objective: detect mass-grave records with malformed coordinate literals.

#### Cypher
```cypher
MATCH (g)
WHERE any(lbl IN labels(g) WHERE lbl IN ["MassGrave","Q108163"])
  AND g.P625 IS NOT NULL
WITH g, toString(g.P625) AS coord
WHERE NOT coord =~ "^-?([0-8]?\\d(\\.\\d+)?|90(\\.0+)?),\\s*-?((1[0-7]\\d)|(\\d?\\d))(\\.\\d+)?|180(\\.0+)?$"
RETURN g, coord
LIMIT 100;
```

##### Cypher results (JSON) #op
```json
```

#### Platform (SPARQL)
```sparql
SELECT ?g ?coord
WHERE {
  ?g a <http://www.wikidata.org/entity/Q108163> ;
     <http://www.wikidata.org/entity/P625> ?coord .
  FILTER(
    !REGEX(STR(?coord), "^-?([0-8]?\\d(\\.\\d+)?|90(\\.0+)?),\\s*-?((1[0-7]\\d)|(\\d?\\d))(\\.\\d+)?|180(\\.0+)?$")
  )
}
LIMIT 100
```
##### Results #op
```json

STATUS: 500
Internal Server Error

```
#### Server (API)
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT ?g ?coord WHERE { ?g a <http://www.wikidata.org/entity/Q108163> ; <http://www.wikidata.org/entity/P625> ?coord . FILTER(!REGEX(STR(?coord), \"^-?([0-8]?\\\\d(\\\\.\\\\d+)?|90(\\\\.0+)?),\\\\s*-?((1[0-7]\\\\d)|(\\\\d?\\\\d))(\\\\.\\\\d+)?|180(\\\\.0+)?$\")) } LIMIT 100",
    "format": "json"
  }'
```

##### Results:
```json
STATUS: 404
404 page not found
```


### Test B1 - SIDBRINT person integrity

Objective: validate that person entities include core identity fields (label and at least one temporal marker).

#### Cypher
```cypher
MATCH (p)
WHERE any(lbl IN labels(p) WHERE lbl IN ["Person","Q5"])
RETURN
  count(DISTINCT p) AS totalPersons,
  count(DISTINCT CASE WHEN p.P1476 IS NOT NULL THEN p END) AS withLabel,
  count(DISTINCT CASE WHEN p.P569 IS NOT NULL OR p.P570 IS NOT NULL THEN p END) AS withBirthOrDeath;
```

##### Cypher results (JSON) #op 
```json
```

#### Platform (SPARQL)
```sparql
SELECT
  (COUNT(DISTINCT ?p) AS ?totalPersons)
  (COUNT(DISTINCT ?withLabel) AS ?withLabel)
  (COUNT(DISTINCT ?withBirthOrDeath) AS ?withBirthOrDeath)
WHERE {
  ?p a <http://www.wikidata.org/entity/Q5> .
  OPTIONAL { ?p <http://www.wikidata.org/entity/P1476> ?label . BIND(?p AS ?withLabel) }
  OPTIONAL {
    { ?p <http://www.wikidata.org/entity/P569> ?birth . }
    UNION
    { ?p <http://www.wikidata.org/entity/P570> ?death . }
    BIND(?p AS ?withBirthOrDeath)
  }
}
```
##### Results #op
```json

STATUS: 500
Internal Server Error

```
#### Server (API)
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT (COUNT(DISTINCT ?p) AS ?totalPersons) (COUNT(DISTINCT ?withLabel) AS ?withLabel) (COUNT(DISTINCT ?withBirthOrDeath) AS ?withBirthOrDeath) WHERE { ?p a <http://www.wikidata.org/entity/Q5> . OPTIONAL { ?p <http://www.wikidata.org/entity/P1476> ?label . BIND(?p AS ?withLabel) } OPTIONAL { { ?p <http://www.wikidata.org/entity/P569> ?birth . } UNION { ?p <http://www.wikidata.org/entity/P570> ?death . } BIND(?p AS ?withBirthOrDeath) } }",
    "format": "json"
  }'
```

##### Results:
```json
STATUS: 404
404 page not found
```


### Test C1 - Cultura y censura document integrity

Objective: verify document-class entities and minimal descriptive metadata.

#### Cypher
```cypher
MATCH (d)
WHERE any(lbl IN labels(d) WHERE lbl IN ["Document","Q49848"])
RETURN
  count(DISTINCT d) AS totalDocuments,
  count(DISTINCT CASE WHEN d.P1476 IS NOT NULL THEN d END) AS withTitle;
```

##### Cypher results (JSON) #op 
```json
```

#### Platform (SPARQL)
```sparql
SELECT
  (COUNT(DISTINCT ?d) AS ?totalDocuments)
  (COUNT(DISTINCT ?withTitle) AS ?withTitle)
WHERE {
  ?d a <http://www.wikidata.org/entity/Q49848> .
  OPTIONAL { ?d <http://www.wikidata.org/entity/P1476> ?title . BIND(?d AS ?withTitle) }
}
```
##### Results #op 
```json

STATUS: 500
Internal Server Error

```

#### Server (API)
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT (COUNT(DISTINCT ?d) AS ?totalDocuments) (COUNT(DISTINCT ?withTitle) AS ?withTitle) WHERE { ?d a <http://www.wikidata.org/entity/Q49848> . OPTIONAL { ?d <http://www.wikidata.org/entity/P1476> ?title . BIND(?d AS ?withTitle) } }",
    "format": "json"
  }'
```

##### Results:
```json
STATUS: 404
404 page not found
```


### Test X1 - Cross-source duplicate candidates by normalized title

Objective: detect potential duplicate entities generated by multi-source ingest.

#### Cypher
```cypher
MATCH (n)
WHERE n.P1476 IS NOT NULL
WITH toLower(replace(replace(replace(toString(n.P1476), " ", ""), "-", ""), ".", "")) AS normalizedLabel, n
WITH normalizedLabel, count(DISTINCT n) AS nodes
WHERE nodes > 1
RETURN normalizedLabel, nodes
ORDER BY nodes DESC
LIMIT 100;
```

##### Cypher results (JSON) #op 
```json
```

#### Platform (SPARQL)
```sparql
SELECT ?normalizedLabel (COUNT(DISTINCT ?n) AS ?nodes)
WHERE {
  ?n <http://www.wikidata.org/entity/P1476> ?label .
  BIND(LCASE(REPLACE(STR(?label), "[^\\p{L}\\p{N}]+", "")) AS ?normalizedLabel)
}
GROUP BY ?normalizedLabel
HAVING (COUNT(DISTINCT ?n) > 1)
ORDER BY DESC(?nodes)
LIMIT 100
```
##### Results #op 
```json

STATUS: 500
Internal Server Error

```
#### Server (API)
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT ?normalizedLabel (COUNT(DISTINCT ?n) AS ?nodes) WHERE { ?n <http://www.wikidata.org/entity/P1476> ?label . BIND(LCASE(REPLACE(STR(?label), \"[^\\\\p{L}\\\\p{N}]+\", \"\")) AS ?normalizedLabel) } GROUP BY ?normalizedLabel HAVING (COUNT(DISTINCT ?n) > 1) ORDER BY DESC(?nodes) LIMIT 100",
    "format": "json"
  }'
```

##### Results:
```json
STATUS: 404
404 page not found
```


### Test X2 - Type conflict check per entity

Objective: detect nodes with unusually high class multiplicity (possible merge errors).

#### Cypher
```cypher
MATCH (n)
WITH n, size(labels(n)) AS typeCount
WHERE typeCount > 3
RETURN n, typeCount
ORDER BY typeCount DESC
LIMIT 100;
```

##### Cypher results (JSON) #op
```json
```

#### Platform (SPARQL)
```sparql
SELECT ?n (COUNT(DISTINCT ?type) AS ?typeCount)
WHERE {
  ?n a ?type .
}
GROUP BY ?n
HAVING (COUNT(DISTINCT ?type) > 3)
ORDER BY DESC(?typeCount)
LIMIT 100
```
##### Results #op 
```json

STATUS: 500
Internal Server Error

```
#### Server (API)
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT ?n (COUNT(DISTINCT ?type) AS ?typeCount) WHERE { ?n a ?type . } GROUP BY ?n HAVING (COUNT(DISTINCT ?type) > 3) ORDER BY DESC(?typeCount) LIMIT 100",
    "format": "json"
  }'
```

##### Results: #op
```json
STATUS: 404
404 page not found
```


# 3. Types of SPARQL search:

> Note: the SPARQL examples below assume an RDF view of the graph. `rdf:type` is standard; `ex:` is a placeholder namespace and should be replaced with the real ontology/predicate IRIs before running.

## 1. SELECT queries

#### 1. Basic triple patterns: ?subject ?predicate ?object

Cypher equivalent: match (subject)-[r]->(object) and return subject id, relationship type, object id.
Objective: retrieve the minimal graph statement unit for structural inspection and downstream sampling.

##### Cypher
```cypher
MATCH (subject)-[r]->(object)
RETURN id(subject) AS subject, type(r) AS predicate, id(object) AS object;
```

###### Results #op 
```json

```
##### SPARQL
```sparql
SELECT ?subject ?predicate ?object
WHERE {
  ?subject ?predicate ?object .
}
```

###### Results #op 
```json

```

##### Server (SPARQL via API)
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT ?subject ?predicate ?object WHERE { ?subject ?predicate ?object . }",
    "format": "json"
  }'
```

###### Results:
```json
STATUS: 500
Internal Server Error
```


## 2. FILTER clauses: basic string and numeric comparisons

**String:** nodes whose label (name/title/text) contains a substring (case-insensitive).
Objective: test semantic filtering capacity and verify retrieval precision for targeted terms.

##### Cypher
```cypher
MATCH (n)
WHERE toLower(coalesce(n.name, n.title, n.text, "")) CONTAINS "brigadista"
RETURN id(n) AS subject, labels(n) AS labels, coalesce(n.name, n.title, n.text) AS label
LIMIT 50;
```

###### Results #op
```json

```

##### SPARQL
```sparql
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX dc: <http://purl.org/dc/terms/>
PREFIX schema: <https://schema.org/>

SELECT ?subject ?label
WHERE {
  ?subject ?predicate ?label .
  FILTER(?predicate IN (rdfs:label, dc:title, schema:name))
  FILTER(CONTAINS(LCASE(STR(?label)), "brigadista"))
}
LIMIT 50
```
###### Results #op 
```json
STATUS: 500
Internal Server Error
```

##### Server (SPARQL via API)
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> PREFIX dc: <http://purl.org/dc/terms/> PREFIX schema: <https://schema.org/> SELECT ?subject ?label WHERE { ?subject ?predicate ?label . FILTER(?predicate IN (rdfs:label, dc:title, schema:name)) FILTER(CONTAINS(LCASE(STR(?label)), \"brigadista\")) } LIMIT 50",
    "format": "json"
  }'
```

###### Results: #op
```json
STATUS: 500
Internal Server Error
```


## 3. LIMIT / OFFSET: result pagination

Objective: test stable pagination and deterministic ordering for reproducible batches and UI navigation.

##### Cypher
```cypher
MATCH (subject)-[r]->(object)
RETURN id(subject) AS subject, type(r) AS predicate, id(object) AS object
ORDER BY subject, predicate, object
SKIP 0
LIMIT 25;
```

###### Results #op 
```json

```

##### SPARQL
```sparql
SELECT ?subject ?predicate ?object
WHERE {
  ?subject ?predicate ?object .
}
ORDER BY ?subject ?predicate ?object
LIMIT 25
OFFSET 0
```

###### Results #op 
```json

```

##### Server (SPARQL via API)
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT ?subject ?predicate ?object WHERE { ?subject ?predicate ?object . } ORDER BY ?subject ?predicate ?object LIMIT 25 OFFSET 0",
    "format": "json"
  }'
```

###### Results: #op 
```json
STATUS: 404
404 page not found
```


## 4. ASK queries

#### 1. Boolean: check for pattern existence

Returns one row with a boolean: does the pattern exist?
Objective: validate fast existence checks for conditional workflows and rule triggers.

##### Cypher
```cypher
MATCH (subject)-[r]->(object)
WITH subject, r, object
LIMIT 1
RETURN count(*) > 0 AS result;
```
###### Results
```json
STATUS: 500
Internal Server Error
```

##### SPARQL
```sparql
ASK
WHERE {
  ?subject ?predicate ?object .
}
```
###### Results
```json
STATUS: 500
Internal Server Error
```

##### Server (SPARQL via API)
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "ASK WHERE { ?subject ?predicate ?object . }",
    "format": "json"
  }'
```

###### Results:
```json
STATUS: 404
404 page not found
```


#### 2. Basic ASK: e.g. “exists any MassGrave?”

Objective: verify class-level existence checks for domain entities used in monitoring and alerts.

##### Cypher
```cypher
MATCH (n:MassGrave)
WITH n
LIMIT 1
RETURN count(*) > 0 AS result;
```
###### Results
```json
{"results":[{"result":true}],"columns":["result"]}
```

##### SPARQL
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX ex: <https://example.org/ns#>

ASK
WHERE {
  ?n rdf:type ex:MassGrave .
}
```
###### Results
```json
STATUS: 500
Internal Server Error
```

##### Server (SPARQL via API)
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> PREFIX ex: <https://example.org/ns#> ASK WHERE { ?n rdf:type ex:MassGrave . }",
    "format": "json"
  }'
```

###### Results:
```json
STATUS: 404
404 page not found
```


## 5. COUNT queries (extended)

Objective: validate aggregate consistency for core graph magnitudes and support monitoring dashboards with reproducible totals.

#### 1. Custom COUNT syntax: COUNT(?variable)

Cypher equivalent: `count(n)` or `count(*)` for the bound variable / pattern.

**Count all nodes:**

Objective: compute entity cardinality for baseline comparisons between dataset versions.

##### Cypher
```cypher
MATCH (n)
RETURN count(n) AS count;
```

###### Results #op
```json
```
##### SPARQL
```sparql
SELECT (COUNT(DISTINCT ?n) AS ?count)
WHERE {
  {
    ?n ?p ?o .
  }
  UNION
  {
    ?s ?p ?n .
  }
}
```
###### Results
```json
STATUS: 500
Internal Server Error
```

##### Server (SPARQL via API)
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT (COUNT(DISTINCT ?n) AS ?count) WHERE { { ?n ?p ?o . } UNION { ?s ?p ?n . } }",
    "format": "json"
  }'
```

###### Results:
```json
STATUS: 404
404 page not found
```

**Count relationships (triples):**

Objective: compute assertion cardinality and detect unexpected relation inflation or loss.

##### Cypher
```cypher
MATCH ()-[r]->()
RETURN count(r) AS count;
```
###### Results
```json
{"results":[{"count":4482}],"columns":["count"]}
```

##### SPARQL
```sparql
SELECT (COUNT(*) AS ?count)
WHERE {
  ?subject ?predicate ?object .
}
```
###### Results
```json
STATUS: 500
Internal Server Error
```

##### Server (SPARQL via API)
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT (COUNT(*) AS ?count) WHERE { ?subject ?predicate ?object . }",
    "format": "json"
  }'
```

###### Results:
```json
STATUS: 404
404 page not found
```

## 6. CONSTRUCT

Return a graph-shaped payload (equivalent to SPARQL CONSTRUCT): nodes + relationships as collections.
Objective: verify graph reconstruction/export behavior for downstream visualization, interchange, or pipeline reuse.

##### Cypher
```cypher
CALL {
  MATCH (n)
  RETURN collect({ id: id(n), labels: labels(n), props: properties(n) }) AS nodes
}
CALL {
  MATCH (source)-[r]->(target)
  RETURN collect({ sourceId: id(source), targetId: id(target), type: type(r), props: properties(r) }) AS relationships
}
RETURN nodes, relationships;
```

###### Results #op 
```json
```

##### SPARQL
```sparql
CONSTRUCT {
  ?subject ?predicate ?object .
}
WHERE {
  ?subject ?predicate ?object .
}
```
###### Results
```json
STATUS: 500
Internal Server Error
```

##### Server (SPARQL via API)
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "CONSTRUCT { ?subject ?predicate ?object . } WHERE { ?subject ?predicate ?object . }",
    "format": "json"
  }'
```

###### Results:
```json
STATUS: 404
404 page not found
```


## 7. DESCRIBE

Describe one node by id: its properties and outgoing/incoming relationships (and neighbour ids).
Objective: validate entity-centric inspection and provenance-style drill-down for debugging and curation workflows.

##### Cypher
```cypher
MATCH (n)
WHERE id(n) = 0
OPTIONAL MATCH (n)-[r]->(m)
RETURN id(n) AS id, labels(n) AS labels, properties(n) AS props, collect({ type: type(r), targetId: id(m) }) AS outRels;
```
###### Results
```json
{"results":[{"id":0,"labels":["Document"],"props":{"name":"72148","_normalized_name":"72148"},"outRels":[{"targetId":null,"type":null}]}],"columns":["id","labels","props","outRels"]}
```

##### SPARQL
```sparql
DESCRIBE ?n
WHERE {
  VALUES ?n { <https://example.org/resource/0> }
}
```
###### Results #op
```json
```

##### Server (SPARQL via API)
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "DESCRIBE ?n WHERE { VALUES ?n { <https://example.org/resource/0> } }",
    "format": "json"
  }'
```

###### Results:
```json
STATUS: 404
404 page not found
```

## 8. FILTER

Restrict by string (e.g. label contains "brigadista") or by numeric range (e.g. id in range).

##### Cypher
```cypher
MATCH (n)
WHERE toLower(coalesce(n.name, n.title, n.text, "")) CONTAINS "brigadista"
RETURN id(n) AS subject, labels(n) AS labels, coalesce(n.name, n.title, n.text) AS label
LIMIT 50;
```

###### Results #op
```json
```

##### SPARQL
```sparql
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX dc: <http://purl.org/dc/terms/>
PREFIX schema: <https://schema.org/>

SELECT ?subject ?label
WHERE {
  ?subject ?predicate ?label .
  FILTER(?predicate IN (rdfs:label, dc:title, schema:name))
  FILTER(CONTAINS(LCASE(STR(?label)), "brigadista"))
}
LIMIT 50
```
###### Results
```json
STATUS: 500
Internal Server Error
```

##### Server (SPARQL via API)
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> PREFIX dc: <http://purl.org/dc/terms/> PREFIX schema: <https://schema.org/> SELECT ?subject ?label WHERE { ?subject ?predicate ?label . FILTER(?predicate IN (rdfs:label, dc:title, schema:name)) FILTER(CONTAINS(LCASE(STR(?label)), \"brigadista\")) } LIMIT 50",
    "format": "json"
  }'
```

###### Results:
```json
STATUS: 404
404 page not found
```


## 9. ORDER BY

Sort results (e.g. by subject, then predicate, then object) and paginate with SKIP/LIMIT.
Objective: ensure deterministic ordering so repeated runs return stable sequences for review and auditing.

##### Cypher
```cypher
MATCH (subject)-[r]->(object)
RETURN id(subject) AS subject, type(r) AS predicate, id(object) AS object
ORDER BY subject, predicate, object
SKIP 0
LIMIT 25;
```

###### Results #op
```json
```

##### SPARQL
```sparql
SELECT ?subject ?predicate ?object
WHERE {
  ?subject ?predicate ?object .
}
ORDER BY ?subject ?predicate ?object
LIMIT 25
OFFSET 0
```

###### Results #op
```json
```

##### Server (SPARQL via API)
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT ?subject ?predicate ?object WHERE { ?subject ?predicate ?object . } ORDER BY ?subject ?predicate ?object LIMIT 25 OFFSET 0",
    "format": "json"
  }'
```

###### Results:
```json
STATUS: 404
404 page not found
```

## GROUP BY

Group by node label and count nodes per type (no explicit GROUP BY; use WITH + aggregation).
Objective: profile class distribution and detect imbalance across entity types.

##### Cypher
```cypher
MATCH (n)
UNWIND labels(n) AS type
RETURN type, count(n) AS count
ORDER BY count DESC
LIMIT 20;
```

###### Results #op
```json
```

##### SPARQL
```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT ?type (COUNT(DISTINCT ?n) AS ?count)
WHERE {
  ?n rdf:type ?type .
}
GROUP BY ?type
ORDER BY DESC(?count)
LIMIT 20
```

###### Results #op
```json
```

##### Server (SPARQL via API)
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> SELECT ?type (COUNT(DISTINCT ?n) AS ?count) WHERE { ?n rdf:type ?type . } GROUP BY ?type ORDER BY DESC(?count) LIMIT 20",
    "format": "json"
  }'
```

###### Results:
```json
STATUS: 404
404 page not found
```

## 10. AGGREGATIONS

Count nodes, count relationships, or both in one response.
Objective: validate multi-metric aggregation in a single query to reduce API calls and keep metrics synchronized.

##### Cypher
```cypher
MATCH (n)
WITH count(n) AS nodeCount
MATCH ()-[r]->()
WITH nodeCount, count(r) AS relCount
RETURN nodeCount, relCount;
```
###### Results
```json
STATUS: 500
Internal Server Error
```

##### SPARQL
```sparql
SELECT ?nodeCount ?relCount
WHERE {
  {
    SELECT (COUNT(DISTINCT ?n) AS ?nodeCount)
    WHERE {
      { ?n ?p1 ?o1 . }
      UNION
      { ?s1 ?p1 ?n . }
    }
  }
  {
    SELECT (COUNT(*) AS ?relCount)
    WHERE {
      ?s2 ?p2 ?o2 .
    }
  }
}
```
###### Results #op
```json
```

##### Server (SPARQL via API)
```bash
curl --fail-with-body --silent --show-error \
  -u "${UBXAT_USER:?Set UBXAT_USER}:${UBXAT_PASSWORD:?Set UBXAT_PASSWORD}" \
  -X POST "${UBXAT_SPARQL_ENDPOINT:-https://ubxat.peninsula.co/cognitive/api/v1/sparql}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
    "query": "SELECT ?nodeCount ?relCount WHERE { { SELECT (COUNT(DISTINCT ?n) AS ?nodeCount) WHERE { { ?n ?p1 ?o1 . } UNION { ?s1 ?p1 ?n . } } } { SELECT (COUNT(*) AS ?relCount) WHERE { ?s2 ?p2 ?o2 . } } }",
    "format": "json"
  }'
```

###### Results:
```json
STATUS: 404
404 page not found
```

# Summary
## Searches compared

| Objective          | task                                  | Cypher                     | SPARQL                                | Server |
| ------------------ | ------------------------------------- | -------------------------- | ------------------------------------- | ------ |
| 1. SELECT          | Triple-pattern retrieval (`?s ?p ?o`) | Success                    | Mixed (`timeout` first, then success) | `500`  |
| 2. FILTER          | String filter (`brigadista`)          | Success (`[]`, no matches) | `500`                                 | `500`  |
| 3. LIMIT/OFFSET    | Ordered pagination                    | Success                    | `timeout`                             | `404`  |
| 4. ASK             | Existence checks                      | Success                    | Mixed (one `timeout`, one success)    | `404`  |
| 5. COUNT (ext)     | Node/relationship counting            | Success                    | Failed (`timeout` / `500`)            | `404`  |
| 6. CONSTRUCT       | Graph-shaped export                   | Success                    | `timeout`                             | `404`  |
| 7. DESCRIBE        | Entity-centric inspection             | Success                    | Success (minimal payload)             | `404`  |
| 8. FILTER (retest) | String filter (repeat block)          | Success (`[]`, no matches) | `500`                                 | `404`  |
| 9. ORDER BY        | Stable sorting                        | `500`                      | `timeout`                             | `404`  |
| 9b. GROUP BY       | Type distribution                     | Success                    | Empty result block                    | `404`  |
| 10. AGGREGATIONS   | Multi-metric aggregation              | Empty result block         | Empty result block                    | `404`  |


## Server access assessment (live re-check)

A live replay of all `Server (SPARQL via API)` blocks showed mixed but degraded operability: previous manual re-checks recovered valid responses in selected queries (e.g., ASK/COUNT/GROUP BY/AGGREGATIONS), but the full sequential replay updated in this document ended with `0/13` successful responses (`500` in the first blocks and then mostly `404`). This indicates the endpoint is reachable but currently unstable or inconsistently routed/authenticated across requests, so server-side results should be treated as non-reproducible until backend configuration is stabilized.

## Server queries that returned data (live checks)

| Query block | Query intent | Status | Data recovered (preview) |
|---|---|---|---|
| 4. ASK queries (variant 1) | Generic existence check (`ASK WHERE { ?s ?p ?o }`) | `200` | `true` |
| 5. COUNT queries (extended) - count nodes | Distinct node count | `200` | `count = 2867` |
| 5. COUNT queries (extended) - count relationships | Relationship count | `200` | `count = 4482` |
| 6. CONSTRUCT | Triple payload export | `200` | Rows returned (`subject`, `predicate`, `object`) |
| GROUP BY | Count by type/label | `200` | `Person 1029`, `Document 724`, `MassGrave 492`, ... |
| 10. AGGREGATIONS | Multi-metric totals | `200` | `nodeCount = 2890`, `relCount = 4482` |

### Probable causes for missing results in other server queries

- **Backend route/proxy instability**: repeated `404 page not found` in protocol/advanced suites suggests endpoint routing mismatch or intermittent gateway mapping.
- **Server-side execution failures**: repeated `500 Internal Server Error` in SELECT/FILTER and early test blocks indicates query-handler crashes before returning payloads.
- **Query translation limits**: failing blocks concentrate in operations that often require extra translation logic (`ORDER BY`, `DESCRIBE`, complex FILTER variants).
- **Session/auth inconsistency across runs**: some manual checks returned `200`, but full sequential replay returned `0/13`, suggesting non-deterministic auth/routing context.
- **Operational instability (non-reproducibility)**: contradictory outcomes over short intervals indicate unstable backend state rather than only query syntax errors.

### Server query errors map

| Block | Server query scope | Error |
|---|---|---|
| Test 0 | Main nodes / People / Mass graves | `STATUS: 500` (`Internal Server Error`) |
| Test 1 | Total nodes | `STATUS: 500` (`Internal Server Error`) |
| Test 2 | Total relationships | `STATUS: 500` (`Internal Server Error`) |
| Test 3 | Nodes per label | `STATUS: 500` (`Internal Server Error`) |
| Test 4 | Relationships per type | `STATUS: 500` (`Internal Server Error`) |
| Test 5 | Node/relationship property diagnostics | `STATUS: 500` (`Internal Server Error`) |
| Test 6 | Relationship property totals | `STATUS: 500` (`Internal Server Error`) |
| 2. Final ingestion validation | A1, A2, A3, B1, C1, X1, X2 | `STATUS: 404` (`404 page not found`) |
| SELECT/FILTER suite | SELECT, FILTER | `STATUS: 500` (`Internal Server Error`) |
| Protocol/advanced suite | LIMIT/OFFSET, ASK, COUNT(ext), CONSTRUCT, DESCRIBE, FILTER, ORDER BY, GROUP BY, AGGREGATIONS | `STATUS: 404` (`404 page not found`) |





## Cypher vs SPARQL data evaluation

### Evidence-based comparison

| Dimension | Cypher | SPARQL | Assessment |
|---|---|---|---|
| Query success rate (recorded blocks) | High in core blocks (SELECT, LIMIT/OFFSET, ASK, COUNT, CONSTRUCT, GROUP BY, DESCRIBE) with some failures (`ORDER BY`, empty AGGREGATIONS block) | Lower and unstable (timeouts/`500` in multiple blocks; one minimal DESCRIBE success; some empty result blocks) | **Cypher stronger** for reproducible execution in current environment |
| Data completeness in returned payloads | Rich graph payloads and structured tabular outputs (e.g., CONSTRUCT, GROUP BY counts) | Often incomplete due to timeout/failure; when successful, payloads may be minimal | **Cypher stronger** for actionable data extraction |
| Consistency across repeated intents | Generally consistent in successful blocks (counts and structure aligned internally) | Mixed behavior across equivalent intents (success in isolated checks, failures in many logged tests) | **Cypher stronger** for consistency |
| Operational robustness | Some degradation but still usable for most analytical checks | Frequent timeout/failure under comparable operations | **Cypher stronger** for robustness |

### Interpreted result

For this test corpus and run context, **Cypher is currently the primary reliable method** for data retrieval and validation. **SPARQL remains partially usable** but non-reproducible under several core/advanced operations, so SPARQL-derived conclusions should be treated as provisional unless revalidated after backend stabilization.

### Minimal decision rule for next runs

- Use **Cypher-first** for baseline metrics, ingestion validation, and curation diagnostics.
- Use **SPARQL as confirmatory/parallel check** only where responses are stable.
- Mark any SPARQL timeout/`500`/empty block as **inconclusive** (not negative evidence about data content).

# Evaluation framework (complement to query tests)

This framework complements technical query checks with data-quality, fairness, usability, and decision-support evaluation.

## 2.1 Scope and unit of analysis

- **System under test**: Neo4j + SPARQL/Cypher API (`/cognitive/api/v1/sparql`) and derived UI workflows.
- **Evidence unit**: one test run = one query + one dataset snapshot + one evaluator note.
- **Evaluation levels**:
  1) data/model level (graph structure, properties, consistency),
  2) interaction level (human interpretation and task success),
  3) governance level (bias, transparency, privacy, traceability).

## 2.2 Dimensions and indicators

### A) Data and schema quality

Use Test 1–11 and metadata tests already defined in this document, following the multi-dimensional semantic-quality logic proposed for ORKG comparisons (D'Souza et al., 2024, DOI: `10.36253/jlis.it-547`).

**Core indicators**
- Coverage of node properties by label.
- Coverage of relationship properties by type.
- Missing metadata rate (empty or null critical fields).
- Type consistency (same property key, stable value type).
- Structural completeness (orphan nodes, disconnected expected entities).

### B) Query effectiveness and robustness

Use SELECT/ASK/COUNT/FILTER/ORDER/GROUP/AGGREGATIONS blocks, aligning effectiveness checks with benchmark-style KGQA evaluation (Gounakis et al., 2023, DOI: `10.1145/3603163.3609067`), robustness under realistic degradation (Jiang et al., 2022, DOI: `10.1007/s00799-021-00313-y`), and repository-performance comparison logic (Li et al., 2022, DOI: `10.1016/j.compenvurbsys.2022.101884`).

**Core indicators**
- Query success rate (valid response / total attempts).
- Result consistency across equivalent Cypher/SPARQL intents.
- Response stability under pagination (`LIMIT/OFFSET`) and sorting.
- Degradation under noisy/partial filters (robustness stress tests).

### C) Fairness and bias risk (data + outputs)

Inspired by lifecycle bias checks, fairness auditing, and philosophical fairness framing (Chen et al., 2023, DOI: `10.2196/43251`; Binns, 2018, URL: `https://proceedings.mlr.press/v81/binns18a.html`; Gallegos et al., 2024).

**Core indicators**
- Representation balance across relevant groups/categories.
- Differential error or omission rates by group/category.
- Sensitivity to protected or proxy attributes (counterfactual checks when possible).
- Documentation of potential harms and mitigation actions.

### D) Human-centered usability and cognitive load

Inspired by structured user-testing guidance, cognitive-load reduction studies, and expert-based evaluation of AI-assisted design spaces (EuropeanaConnect Deliverable 3.2.3, 2011; Calvo Flores, 2023, URL: `http://hdl.handle.net/10803/688422`; Çiçek & Özkar, 2025, DOI: `10.1007/s10798-025-10033-y`).

**Core indicators**
- Task completion rate for predefined user tasks.
- Time to insight (seconds/minutes to complete each task).
- Error rate (wrong interpretation, wrong filter, wrong conclusion).
- Perceived workload (e.g., NASA-TLX short form or 1–5 cognitive load item).
- Explanation clarity/trust rating (1–5).

### E) Transparency, ethics, and governance

This dimension follows human-centered trustworthy-AI framing around safety, trust, governance, and lifecycle risk mitigation (Calvano, 2024, DOI: `10.1145/3661167.3661223`; Chen et al., 2023, DOI: `10.2196/43251`).

**Core indicators**
- Explainability availability (can user trace why a result appears?).
- Provenance traceability (source document/entity path present).
- Privacy safeguards documented (sensitive attributes handling).
- Compliance checklist status (GDPR/AI Act-relevant controls, if applicable).

## 2.3 Scoring rubric (0–4)

- **0 = absent**: no evidence.
- **1 = poor**: ad hoc, unstable, not reproducible.
- **2 = partial**: some evidence, major gaps.
- **3 = good**: consistent evidence, minor gaps.
- **4 = strong**: robust, reproducible, documented mitigation.

For each dimension, compute:

`dimension_score = average(indicator_scores)`

Global score:

`overall_score = average(A, B, C, D, E)`

Optional weighting (if needed for HerStory priorities):
- A: 25%
- B: 20%
- C: 20%
- D: 20%
- E: 15%

## 2.4 Evaluation protocol (no execution yet)

1. **Freeze context**: define dataset snapshot/date and test objective.
2. **Run technical battery**: execute Test 1–11 + SPARQL/Cypher equivalence checks.
3. **Run bias checks**: compare coverage/errors across relevant groups.
4. **Run user mini-study**: 3–5 representative tasks, 5–8 participants (or experts).
5. **Score rubric**: assign 0–4 by indicator with short evidence note.
6. **Prioritize fixes**: high-impact gaps first (data, fairness, usability blockers).
7. **Re-test**: rerun same battery after changes to measure improvement.

## 2.5 Minimal reporting template

```markdown
### Evaluation run
- Date:
- Dataset snapshot:
- Evaluators:
- Goal:

### Scores (0–4)
- A) Data/schema quality:
- B) Query effectiveness/robustness:
- C) Fairness/bias risk:
- D) Usability/cognitive load:
- E) Transparency/ethics/governance:
- Overall:

### Key findings
1.
2.
3.

### Risks
1.
2.

### Actions
1.
2.
```

## 2.6 Source basis used to derive this framework

- Gounakis, N., Mountantonakis, M., & Tzitzikas, Y. (2023). CIDOC-CRM KGQA benchmark/evaluation. DOI: `10.1145/3603163.3609067`.
- D'Souza, J., et al. (2024). ORKG multi-dimensional semantic quality assessment. DOI: `10.36253/jlis.it-547`.
- Jiang, M., et al. (2022). Robustness under OCR-noisy deployment conditions. DOI: `10.1007/s00799-021-00313-y`.
- Li, W. W., et al. (2022). Repository infrastructure benchmark. DOI: `10.1016/j.compenvurbsys.2022.101884`.
- Calvano, M. (2024). Human-centered SAI quality/trust/safety framing. DOI: `10.1145/3661167.3661223`.
- Chen, Y., et al. (2023). Biases across AI lifecycle + HCAI mitigation. DOI: `10.2196/43251`.
- Binns, R. (2018). Fairness definitions and political-philosophy framing. URL: `https://proceedings.mlr.press/v81/binns18a.html`.
- Calvo Flores, L. (2023). Cognitive load reduction for decision-support visualizations. URL: `http://hdl.handle.net/10803/688422`.
- Çiçek, S., & Özkar, M. (2025). Expert-evaluated AI-assisted design-space method. DOI: `10.1007/s10798-025-10033-y`.
