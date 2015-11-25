# be-mean-instagram-mongodb #
Guia de referência do conteúdo ministrado no módulo **mongoDB** do curso gratuíto [*Construa seu Instagram com MEAN*](http://dagora.net/be-mean/) da [Webschool.io](https://github.com/Webschool-io/)

## Apresentação (Slides) ##
[Link para slides](
https://docs.google.com/presentation/d/1KXxmcwd47x4v2SymyiBPK7ucn80PruSvcw4mZ5S3nWc/edit?usp=sharing
)

### Sobre o MongoDB ###
O **MongoDB** é uma aplicação de código aberto, de alta performance, sem esquemas, orientado a **documentos**. Foi escrito na linguagem de programação **C++**. Além de orientado a documentos, é formado por um conjunto de documentos **JSON**.

Agora que sabemos que o **MongoDB** é orientado a documentos, precisamos saber que existem outros tipos de bancos **NO-SQL**:
```
- Chave/Valor
- Documentos
- Grafos
- Colunas
- Mistos
```

### Aula 01 ###
Nessa primeira aula vamos conhecer os comandos `export & import` que são bem intuitivos e de fácil utilização.

##### Export #####
```
mongoexport --host 127.0.0.1 --db database --collection collection --out data.json
```
##### Import #####

```
mongoimport --host 127.0.0.1 --db database --collection collection --drop --file data.json
```

**DICA:** Instale uma ferramenta chamada **[mongohacker](https://tylerbrock.github.io/mongo-hacker/)**, ela melhora a visualização de buscas e resultados no `console`.

#### Links da Aula ####
- [Vídeo da Aula](https://www.youtube.com/watch?v=leYxsEAL_yY)
- [Exercício Solicitado](https://github.com/Webschool-io/be-mean-instagram/blob/master/apostila/mongodb/export_import.md)
- [Exercício Resolvido](https://github.com/Webschool-io/be-mean-instagram-mongodb-excercises/blob/master/class-01/class-01-resolved-viniciusgalvao-vinicius-galvao.md)

### Aula 02 ###
Nessa aula iremos conhecer alguns comandos para **manusear** bancos e coleções, como também iremos aprender como **inserir e buscar** informações no **MongoDB**.

**COMANDOS BÁSICOS**

- `use db_name` especifica o database que será usado, quando não existe ele cria.
- `mongo database` conecta ao mongo db já especificando o banco a ser utilizado.
- `show dbs` mostra todas as databases criadas.
- `show collections` mostra todas as coleções referente a base de dados setada.

**DICA:** Caso você queirar criar uma **coleção** vazia basta utilizar função `db.createCollection(name, json_config)`

**- insert()**

É responsável por inserir um documento em uma respectiva coleção.

SINTAXE:
```
db.collection.insert({field: value, field: value})
```

**- save()**

É responsável por inserir e salvar um documento, para isso deve ser definido um objeto.

SINTAXE:
```
db.collection.save(bject)
```

**- find()**

É responsável por acessar os dados de uma coleção, basicamente ele vai percorrer todos os registros da coleção.

SINTAXE:
```
db.collection.find({query}, {fields})
```

**- findOne()**

É responsável por acessar os dados de um documento, ele vai retornar um objeto direto.

SINTAXE:
```
db.collection.findOne({query})
```

### Aula 03 ###

>Conteúdo na aula 03

### Aula 04 ###
No MongoDB temos duas formas para alterar um documento, Utilizando o comando `save()` ou `update()`.

Lembrando que no caso do `save()` é preciso antes buscar o documento necessário para posteriormente poder modificá-lo.

Já no caso do `update()` isso não é necessário pois ele faz isso todo de uma vez só em um comando sendo mais fácil para buscar e alterar documentos de uma vez só.

A função `update()` recebe três parâmetros:

```
- query
- modifications
- options (não é obrigatório)
```

SINTAXE: `db.collection.update(query, mod, options)`

**DICA:**  Não utilize o `update()` sem os **operadores de modificação** se não souber o que está fazendo, pois corre um sério risco de você __perder dados__ do seu __documento__.

**OPERADORES DE MODIFICAÇÃO**

- `$set` *modifica o valor de um campo ou cria ele, caso não exista.*
>`{$set: {field: value}}`

- `$setOnInsert` *irá inserir um documento adcional a nossa modificação caso haja um __upsert__*.
>`{$setOnInsert: {field: value, field: value, field: value ...}}`

- `$unset` *deleta campos do documento.*
>`{$unset: {field: true or false}}`

- `$inc` *incrementa um valor no campo com a quantidade desejada, caso não exista ele irá criar e setar o valor. Para decrementar basta passar um valor negativo.*
>`{$inc: {field: value}}`

**OPERADORES DE ARRAY**
- `$push` *adiciona um valor ao campo do array. Ele irá atualizar ou criar o campo com o valor caso ele não exista.* `{$push: {field: value}}`

- `$pushAll` *adiciona cada valor do [Array_de_valores] caso o campo seja um __Array__ existente. Caso não exista irá criar o campo novo do tipo __Array__ com o valor passado no `$pushAll`.*
>`{$pushAll: {field: ['value', 'othervalue', '']}}`

- `$pull` *retira valor do campo, caso o campo seja um __Array__ existente. Caso não exista ele não fará nada.*
>`{$pull: {field: value}}`

- `$pullAll` *é a função inversa do `$pushAll`. sendo assim remove cada valor do __[Array_de_valores]__ caso o campo seja um __Array__ existente.*
>`{$pullAll: {field: ['value', 'othervalue', '']}}`

**OBS**: Em todos os casos dos **operadores de array** se o campo existir e não for um array irá retornar um erro.

##### OPTIONS #####

> O options é o terceiro e último parâmetro passado na função `db.collection.update(query, mod, OPTIONS)`.

Abaixo vamos ver que existem 3 parâmetros possíveis que podem ser passados dentro do **options**, sendo eles:
```
{
  upsert: boolean,
  multi: boolean,
  writeConcern: document
}
```


`upsert`

Insere o **documento** que está sendo passado como modificação, caso o documento não seja encontrado pela query.

`multi`

Permite alterar vários documentos de uma vez, já que por padrão o **mongodb** não permite esse tipo de alteração.

>O valor padrão dos parâmetros `upsert` e `multi` são **false**.

`writeConcern`

É um documento que descreve a garantia que o **mongodb** fornece ao relatar o sucesso de uma operação de escrita.

>Ele determina o nível de garantia. Quando inserções, atualizações e exclusões tem um **write concern** fraco, operações de escrita retornam rápidamente

### Aula 05 ###
Nessa aula iremos aprender como utilizar  as seguintes funcionalidades:
```
distinct()
limit().skip()
group()
aggregate()
```

Iniciando a aula fomos apresentado à duas funcionalidades para obtermos a quantidade de documentos que possuimos na **colecão**, sendo eles:

**- length()**
  ```
  db.collection.find({}).length()
  ```
**- count()**
   ```
   db.collection.count({})
   ```

  Porém o mais performático é o `.count()`, pois `.length()` coloca todos os documentos na memória e itera para nos retornar o total, sendo assim mais lento que o `.count()`.

**- distinct()**

Retorna um **array de valores únicos** de uma **propriedade(campo)**. Seu retorno **não é uma coleção de documentos**.

```
db.collection.distinct(columname) - > "retorna um array de valores"
db.collection.distintc(columname).length -> "para saber o total de registros no array"
db.collection.distinct(columname).sort() -> "retorna o array em ordem alfabética"
db.collection.distinct(columname).sort().reverse() -> "retorna o array de valores em ordem alfabética inversa"
```


**- limit()**

O `limit()` tem como responsabilidade limitar o número de documentos que serão retornados na query por ordem CRESCENTE.
```
db.collection.find({}).limit(number_of_documents)
```

**- skip()**

O `skip()` é responsável por dizer a partir de qual posição os documentos devem ser retornados.
```
db.collection.find({}).skip(number_of_documents_to_skip)
```

Um exemplo simples de utilizar o `limit()` e `skip()` seria paginar o resultado de uma query.

```
var page = 0;
var perPage = 2;
db.collection.find({}).limit(perPage).skip(perPage * page);
```

**- group()**

Pega os valores iguais de um campo pré-definido e agrupa.

```
db.collection.group({
  initial: { total: 0 }, // agrega proprieadades para o objeto de resultado
  cond: {field: {}},
  reduce: function(current, result) {
    current.fieldname.forEach(function(value) {
      if(result[type]) {
        result[type]++;
      } else {
        result[type] = 1;
      }
      result.total++;
    });
  },
  finalize: function(result){
    // chamada quando a iteração é finalizada e tem um objeto resultado como retorno.
  }
});
```

Existem outras propriedades que podem ser utilizadas no `group()` para saber mais [clique aqui](https://docs.mongodb.org/manual/reference/method/db.collection.group/).

**- aggregate()**

Todas as funções do `aggregate` começam com `$`.

```
db.collection.aggregate([
    { match: {conditional}},
    {$group: {
      _id: {}, // id agrupador.
      field_avg: {$avg: '$field'},
      another_field_avg: {$avg: '$another_field'},
      total: {$sum: 1}
    }
  }
]);
```

Existem outras propriedades que podem ser utilizadas no `aggregate()` para saber mais [clique aqui](https://docs.mongodb.org/manual/reference/method/db.collection.aggregate/).

O `aggregate()` e o `group()` são muito parecidos em suas funcionalidades, fique livre para escolher qual se encaixa melhor para você.

### Aula 06 ###

Nessa aula vamos falar sobre relacionamentos, uma coisa que já precisa ficar clara é que no MongoDB **não existem JOINS**.

O relacionamento no MongoDB é todo **MANUAL**, sabendo disso para fazermos um relacionamento basta salvarmos o **_id** de uma coleção em outra.

###### DBRef #####

O DBRef é um convenção para representar um documento relacionado, isso inclui:

- `$ref` nome da coleção a ser referenciada.
- `$id` o ObjectId do documento referenciado.
- `$db` a database onde a coleção referenciada se encontra.
