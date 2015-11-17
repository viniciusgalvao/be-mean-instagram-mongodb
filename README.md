# be-mean-instagram-mongodb
Guia de referência do conteúdo ministrado no módulo **mongoDB** do curso gratuíto [*Construa seu Instagram com MEAN*](http://dagora.net/be-mean/) da [Webschool.io](https://github.com/Webschool-io/)

## Apresentação (Slides)
[Link para slides](
https://docs.google.com/presentation/d/1KXxmcwd47x4v2SymyiBPK7ucn80PruSvcw4mZ5S3nWc/edit?usp=sharing
)

### Sobre ( `mongodb` )
O **MongoDB** é uma aplicação de código aberto, de alta performance, sem esquemas, orientado a **documentos**. Foi escrito na linguagem de programação **C++**. Além de orientado a documentos, é formado por um conjunto de documentos **JSON**.

Agora que sabemos que o **MongoDB** é orientado a documentos, precisamos saber que existem outros tipos de bancos **NO-SQL**:
```
- Chave/Valor
- Documentos
- Grafos
- Colunas
- Mistos
```

### Aula 01 ( `export & import` )
Nessa primeira aula vamos conhecer os comandos `export & import` que são bem intuitivos e de fácil utilização.

##### Export
```
mongoexport --db database --collection collection --out data.json
```
##### Import

```
mongoimport --db database --collection collection --drop --file data.json
```

**Dica:** Instale uma ferramenta chamada **[mongohacker](https://tylerbrock.github.io/mongo-hacker/)**, ela melhora a visualização de buscas e resultados no `console`.

#### Links da Aula
- [Vídeo da Aula](https://www.youtube.com/watch?v=leYxsEAL_yY)
- [Exercício Solicitado](https://github.com/Webschool-io/be-mean-instagram/blob/master/apostila/mongodb/export_import.md)
- [Exercício Resolvido](https://github.com/Webschool-io/be-mean-instagram/blob/master/apostila/classes/mongodb/exercises/class-01-resolved-viniciusgalvao-vinicius-galvao.md)

### Aula 02 ( CRUD - Insert)
### Aula 03 ( CRUD - Retrieve )
### Aula 04 ( CRUD - Update )
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

- `$set` *modifica o valor de um campo ou cria ele, caso não exista.* `{$set: {field: value}}`

- `$unset` *deleta campos do documento.* `{$unset: {field: true or false}}`

- `$inc` *incrementa um valor no campo com a quantidade desejada, caso não exista ele irá criar e setar o valor. Para decrementar basta passar um valor negativo.* `{$inc: {field: value}}`

**OPERADORES DE ARRAY**
- `$push` *adiciona um valor ao campo do array. Ele irá atualizar ou criar o campo com o valor caso ele não exista.* `{$push: {field: value}}`

- `$pushAll` *adiciona cada valor do [Array_de_valores] caso o campo seja um __Array__ existente. Caso não exista irá criar o campo novo do tipo __Array__ com o valor passado no `$pushAll`.* `{$pushAll: {campo: [Array_de_valores]}}`

- `$pull` *retira valor do campo, caso o campo seja um __Array__ existente. Caso não exista ele não fará nada.* `{$pull: {campo: valor}}`

- `$pullAll` *é a função inversa do `$pushAll`. sendo assim remove cada valor do __[Array_de_valores]__ caso o campo seja um __Array__ existente.* `{$pullAll: {campo: [Array_de_valores]}}`

**OBS**: Em todos os casos dos **operadores de array** se o campo existir e não for um array irá retornar um erro.
