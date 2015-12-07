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

###### DBRef ######

O DBRef é um convenção para representar um documento relacionado, isso inclui:

- `$ref` nome da coleção a ser referenciada.
- `$id` o ObjectId do documento referenciado.
- `$db` a database onde a coleção referenciada se encontra.

```
{
  "pokemon" : {
    "$ref" : "pokemons",
    "$id" : ObjectId("564220f0613f89ac53a7b5d0"),
    "$db" : "be-mean-instagram"
   }
}
```

###### EXPLAIN ######

O explain mostra o que o banco está fazendo, como ele executa as **queries** internamente.

**Quando usar?**

Sempre que quisermos analisar a query e a forma que ela foi executada.

**Como usar?**

```
  db.collection.find({}).explain()
  db.collection.find({}).explain('executionStats') -> retorna mais informações sobre a execução da query, como o tempo que ele levou para encontrar o registro, documentos examinados entre outros.
```

###### INDEX ######

Uma forma de falarmos ao nosso banco quem são especiais e vamos rodar algo a partir dele.

Por exemplo se eu fizer frequentemente uma certa operação em cima de uma **propriedade** de um documento e precisar que ela seja muito rápida, bastar dizer ao mongo para **indexar** essa propriedade para mim.

Resumindo ele otimiza sua base para fazer pesquisas mais rápidas.

**- getIndexes()**

Lista todos os indíces criados referente a coleção especificada.

```
db.collection.getIndexes()

[
  {
    "v": 1,
    "key": {
      "_id": 1
    },
    "name": "_id_",
    "ns": "database.collection"
  }
]
```

**- createIndex()**

Cria um índice referente a coleção especificada.

```
db.collection.createIndex({ field: 1 or -1 })
db.collection.createIndex({ field: 1, otherfield: 1, ...}) -> nesse caso quando for criada a query ela deve passar as mesmas propriedades que foram criadas para o índice composto funcionar.
1 -> ordem natural
-1 -> ordem inversa
```

**- dropIndex()**

Remove um índice referente a coleção especificada. Ele deve ser removido da mesma forma que foi criada utilizando o  `createIndex()`

```
db.collection.dropIndex({ field: 1 or -1 })
1 -> ordem natural
-1 -> ordem inversa
```

Só crie índices se realmente for nescessário e utilizado.

**- _rand()**

Retorna um número randômico entre 0 e 1. Por exemplo: *0.24257829878479242*

###### GRIDFS ######

É o sistema de arquivos do MongoDB o qual irá armazenar os arquivos binários diretamente no banco.

Utilizar apenas quando o arquivo for maior que 16mb, em caso de tamanho menor ou igual armazenar dentro do documento com uma propriedade do tipo **BinData** para armazenar dados binários.

```
mongofiles -d database -h 127.0.0.1 put filename
```

Na coleção **fs.chunks** fica nosso arquivo binário dividido em pequenas partes, chamadas de chunks, cada chunk é um documento contendo 255kb de dados.

Na coleção **fs.files** temos os metadados do arquivo armazenado. A propriedade ***md5**** você pode utilizar para fazer uma busca e caso você encontre mais de 1 registro e porque existem arquivos duplicados. ai você decide o que fazer com ele, como por exemplo removê-los.

**DICA:** Se for utilizar o GridFS, utilize-o em um servidor próprio para configura-lo da melhor maneira possível. Sendo assim criar o servidor do GridFS separado do Mongod.

###### REPLICA ######

É um espelhamento dos seus dados de um servidor para outro, no MongoDb uma **ReplicaSet** pode conter 50 membros, ou seja, 50 Replicas contando com os árbitros.

Todas as operações de escrita são feitas no primário e replicada para os secundários.

No MongoDB devemos também replicar os Shards.

A replicação ocorre em 2 etapas:
 - Initial Sync
 - Replication (Etapa que deixa os dados sempre atualizados, fica sempre rodando)

O **oplog** é o log de operações do MongoDB onde ficam armazenadas todas as operações que foram realizadas no primário.

Sempre utilizar pelomenos em uma **Replica**.

**USO**

Para criarmos as replicas, primeiramente precisamos criar o(s) diretório(s) onde vão ficar armazenados os dados daquela replica.

Primeiramente vamos criar o diretório

```
mdkir /data/rs1
```
Agora vamos criar a replica

```
mongod --replSet replica_set --port 27017 --dbpath /data/rs1 --logpath /data/rs1/log.txt --fork
```

Iremos configurar e inciar a replica

```
rsconf = {
   _id: "replica_set",
   members: [
    {
     _id: 0,
     host: "127.0.0.1:27017"
    }
  ]
}

rs.initiate(rsconf)
```

Agora adicionaremos os secundários

```
rs.add(127.0.0.1:replport)
```

Nenhum comando pode ser rodado no secundário, apenas no primário.

Para saber o status da replica basta executar o seguinte comando no terminal `rs.status()` e para saber o status do **oplog** `rs.printReplicationInfo()`

Para você rebaixar o **PRIMARY** basta executar o comando `rs.stepDown()` e o MongoDB irá eleger uma secundária como primária.

###### ÁRBITRO ######

É um serviço que ele não replica os dados e ele nunca vira primário, mas tem poder do voto de Minerva na votação de qual Replica secundária deve virar primária.

Só adicionar um árbitro em uma **ReplicaSet** com um número **PAR** de membros, para que o árbitro seja o desempate.

Primeiramente crie um diretório que conterá os dados de configuração.

```
mkdir /data/arb
```

Depois precisa levantar o mongod utilizando --replSet nomeDaReplicaSet com seu diretório anteriormente criado.

```
mongod --port 30000 --dbpath /data/arb --replSet replica_set
```

Após levantar seu árbitro, conecte na Replica primária e adicione o árbitro criado com rs.addArb():

```
rs.addArb("127.0.0.1:30000")
```

### Aula 07 ###

###### SHARDING ######

É o processo de armazenamento de registros de dados em várias máquinas, é a abordagem que o MongoDB faz para atender o crescimento dos dados.

Com Sharding você deve adicionar mais máquinas para suportar o crescimento de dados e as demandas de leitura e escrita.

**Por que usar?**

Porque o seu servidor não aguentará quando alguma coleção sua for maior que sua memória RAM, fazendo com que o MongoDb tenha que paginar os dados quando for ler, impactando na performance.

**Quando usar?**

Quando você analisar seu banco de dados e verificar que uma coleção está chegando perto do tamanho que o servidor tem de memória disponível para o MongoDb.

**Como usar?**

Para usar precisamos entender como é a arquitetura de um cluster com MongoDB, nele possuímos 3 serviços diferentes que são:

 ```
 - shards
 - config servers
 - router (instâncias mongos)
 ```

 **CONFIG SERVERS**

 Para levantar um servidor de configuração vamos criar um diretório

 ```
 mkdir /data/configdb/
 ```

 Agora iremos levantar o mongod com o configserver

 ```
 mongod --configsvr --port 27010
 ```

 **ROUTES**

 Agora iremos usar o **mongos** para levantar nosso servidor de rota.

 ```
 mongos --configdb 127.0.0.1:27010 --port 27011
 mongos --configdb 127.0.0.1:27010,anotherserver:portconfigserver --port 27011 (mais de um config servers)
 ```

 Utilizar mais de 1 config server em produção para o router não ficar perdido em caso de queda de um ***configserver***.

 **SHARDS**

Vamos criar os diretórios onde irão ficar os dados dos shards.

```
mdkir /data/shard1 && mkdir /data/shard2 && mkdir /data/shard3
```

Agora iremos levanta os servidor com shard.

```
mongod --port 27012 --dbpath /data/shard1
```

Shards levantados, precisamos avisar aos routes sobre os shards criados

Vamos conectar ao servidor do ***ROUTES***
```
mongo --port 27011 --host 127.0.0.1
```

E agora iremos adicionar o shard ao routes
```
sh.addShard('127.0.0.1:27012')
```

Para ativarmos nosso sharding, iremos dizer qual a nossa a database

```
sh.enableSharding("dbname")
```

Agora vamos especificar qual a coleção dessa database será ***shardeada***

```
sh.shardCollection("dbname.collection", {"_id": 1}) -> o segundo parâmetro diz que campo que será quebrado.
```

###### GERENCIAMENTO DE USUÁRIOS NO MONGODB ######

**- createUser()**

```
db.createUser({
    user: "ViniciusAdmin",
    pwd: "admin123",
    roles: [{ role: "userAdminAnyDatabase", db: "admin"}]
  }
)
```

**- updateUser()**

```
db.updateUser({
    user: "ViniciusAdmin",
    pwd: "admin123",
    roles: [{ role: "userAdminAnyDatabase", db: "admin"}]
  }
)
```
**- runCommand()**

```
db.runCommand({updateUser: username, customData: {teacher: false}})
db.runCommand({dropUser: username})
db.runCommand({ dropAllUsersFromDatabase: 1})
```

Agora vamos levantar um servidor com autenticação

```
mongod --auth --port portnumber
```

Feito isso, iremos conectar ao mongo utilizando um usuário criado previamente

```
mongo --port portnumber -u "username" -p "password" --authenticationDatabase "dbname"
```

Caso você tenha se conectado sem usuário e queira se autenticar, basta executar
```
use dbname
db.auth(username, password)
```
