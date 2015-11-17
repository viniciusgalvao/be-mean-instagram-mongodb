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
Nessa primeira aula vamos conhecer os comandos `export & import` que são bem intuítivos e de fácil utilização.

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
