# MongoDB - Aula 05 - Exercício
autor: Vinícius Galvão

## 1. Importar as collections restaurantes e pokemons
```js
➜  ~  mongoimport --host 127.0.0.1 --db be-mean --collection restaurantes --drop --file ~/Downloads/restaurantes.json   
2015-11-24T01:19:57.659-0300    connected to: 127.0.0.1
2015-11-24T01:19:57.659-0300    dropping: be-mean.restaurantes
2015-11-24T01:19:57.659-0300    imported 25359 documents

➜  ~  mongoimport --host 127.0.0.1 --db be-mean --collection pokemons --drop --file ~/Downloads/pokemons.json   
2015-11-24T01:17:14.403-0300    connected to: 127.0.0.1
2015-11-24T01:17:14.403-0300    dropping: be-mean.pokemons
2015-11-24T01:17:14.403-0300    imported 610 documents
```

## 2. Distinct por `cuisine` na restaurantes
```js
MBP-de-Vinicius(mongod-3.0.6) be-mean> db.restaurantes.distinct('cuisine')
[
  "Bakery",
  "Irish",
  "Hamburgers",
  "American ",
  "Jewish/Kosher",
  "Delicatessen",
  "Ice Cream, Gelato, Yogurt, Ices",
  "Chinese",
  "Other",
  "Chicken",
  "Turkish",
  "Caribbean",
  "Donuts",
  "Sandwiches/Salads/Mixed Buffet",
  "Bagels/Pretzels",
  "Continental",
  "Pizza",
  "Italian",
  "Steak",
  "Polish",
  "Latin (Cuban, Dominican, Puerto Rican, South & Central American)",
  "German",
  "French",
  "Pizza/Italian",
  "Mexican",
  "Spanish",
  "Café/Coffee/Tea",
  "Tex-Mex",
  "Pancakes/Waffles",
  "Soul Food",
  "Seafood",
  "Hotdogs",
  "Greek",
  "Not Listed/Not Applicable",
  "African",
  "Japanese",
  "Indian",
  "Armenian",
  "Thai",
  "Chinese/Cuban",
  "Mediterranean",
  "Korean",
  "Bottled beverages, including water, sodas, juices, etc.",
  "Russian",
  "Eastern European",
  "Middle Eastern",
  "Asian",
  "Ethiopian",
  "Vegetarian",
  "Barbecue",
  "Egyptian",
  "English",
  "Sandwiches",
  "Portuguese",
  "Indonesian",
  "Chinese/Japanese",
  "Filipino",
  "Juice, Smoothies, Fruit Salads",
  "Brazilian",
  "Afghan",
  "Vietnamese/Cambodian/Malaysia",
  "CafÃ©/Coffee/Tea",
  "Soups & Sandwiches",
  "Tapas",
  "Moroccan",
  "Pakistani",
  "Peruvian",
  "Bangladeshi",
  "Czech",
  "Salads",
  "Creole",
  "Fruits/Vegetables",
  "Iranian",
  "Cajun",
  "Scandinavian",
  "Polynesian",
  "Soups",
  "Australian",
  "Hotdogs/Pretzels",
  "Southwestern",
  "Nuts/Confectionary",
  "Hawaiian",
  "Creole/Cajun",
  "Californian",
  "Chilean"
]
```

## 3. Distinct por `types` na pokemons
```js
MBP-de-Vinicius(mongod-3.0.6) be-mean> db.pokemons.distinct('types')
[
  "fire",
  "water",
  "bug",
  "flying",
  "normal",
  "poison",
  "electric",
  "steel",
  "ice",
  "ghost",
  "psychic",
  "fighting",
  "grass",
  "ground",
  "fairy",
  "rock",
  "dark",
  "dragon"
]

```

## 4. As primeiras 3 pág. com .limit() e .skip() de pokemons (5 em 5)
```js
MBP-de-Vinicius(mongod-3.0.6) be-mean> db.pokemons.find({}, {name: 1, _id: 0}).limit(5).skip(0)
{
  "name": "Charmeleon"
}
{
  "name": "Charmander"
}
{
  "name": "Blastoise"
}
{
  "name": "Caterpie"
}
{
  "name": "Metapod"
}
Fetched 5 record(s) in 1ms
MBP-de-Vinicius(mongod-3.0.6) be-mean> db.pokemons.find({}, {name: 1, _id: 0}).limit(5).skip(5)
{
  "name": "Spearow"
}
{
  "name": "Butterfree"
}
{
  "name": "Wartortle"
}
{
  "name": "Kakuna"
}
{
  "name": "Farfetchd"
}
Fetched 5 record(s) in 1ms
MBP-de-Vinicius(mongod-3.0.6) be-mean> db.pokemons.find({}, {name: 1, _id: 0}).limit(5).skip(10)
{
  "name": "Magnemite"
}
{
  "name": "Magneton"
}
{
  "name": "Doduo"
}
{
  "name": "Seel"
}
{
  "name": "Dodrio"
}
Fetched 5 record(s) in 1ms
```

## 5. Group ou Aggregate contando a quantidade de pokemons de cada tipo
```js
MBP-de-Vinicius(mongod-3.0.6) be-mean> db.pokemons.aggregate([
  { $unwind : "$types"},
  { $group: {
    _id: "$types",
    total: {$sum: 1}
    }
  }
])
{
  "result": [
    {
      "_id": "fairy",
      "total": 28
    },
    {
      "_id": "fighting",
      "total": 38
    },
    {
      "_id": "psychic",
      "total": 62
    },
    {
      "_id": "dark",
      "total": 38
    },
    {
      "_id": "ground",
      "total": 51
    },
    {
      "_id": "grass",
      "total": 75
    },
    {
      "_id": "electric",
      "total": 40
    },
    {
      "_id": "steel",
      "total": 37
    },
    {
      "_id": "rock",
      "total": 46
    },
    {
      "_id": "flying",
      "total": 77
    },
    {
      "_id": "fire",
      "total": 47
    },
    {
      "_id": "ice",
      "total": 24
    },
    {
      "_id": "bug",
      "total": 61
    },
    {
      "_id": "poison",
      "total": 54
    },
    {
      "_id": "normal",
      "total": 78
    },
    {
      "_id": "ghost",
      "total": 34
    },
    {
      "_id": "dragon",
      "total": 20
    },
    {
      "_id": "water",
      "total": 105
    }
  ],
  "ok": 1
}
```

## 6. Realizar 3 counts na pokemons.

* Todos:
```js
db.pokemons.count();
610
```

* Só do `types` `fire`:
```js
db.pokemons.count({ types: "fire"});
47
```

* Só com defesa menor que 50:
```js
db.pokemons.count({ defense: { $lt: 50 }});
138
```
