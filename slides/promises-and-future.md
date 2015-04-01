
# Promises
### Conceito, Motivo e Implementações

---

## O que é?

- Algo que será ou não cumprido
- Tarefas assíncronas <!-- .element: class="fragment" -->
- Proposto em 1976 em artigos sobre processamento paralelo <!-- .element: class="fragment" -->

Note: Uma promessa é algo que pode não estar pronto, mas será ou não cumprida em algum momento.
Em Ciência da Computação o conceito de Promessas, Futuros e Atrasos são maneiras de lidar com tarefas assíncronas, e não é um conceito novo.
Na verdade, estes conceitos datam de 76, quando Daniel Friedman e David Wise cunharam o termo na Conferência Internacional em Processamento Paralelo.
Eles são baseados na idéia de atrasar o uso do resultado de uma tarefa assíncrona até que a tarefa seja completada.

---

## Simplificando a sincronização em sistemas concorrentes


- Menos callbacks <!-- .element: class="fragment" -->
- Menos níveis de identação <!-- .element: class="fragment" -->
- Mais controle sobre o tratamento de exceções <!-- .element: class="fragment" -->
- Mais semântica <!-- .element: class="fragment" -->

Note: Promessas podem ajudar a manter uma sintaxe mais limpa no tratamento de tarefas assíncronas, facilitar a sincronização destas tarefas e simplificar o tratamento de exceções, proporcionando uma melhor semântica (um melhor significado no código) no controle deste tipo de fluxo

---

## Estados de Promessas

- Pendente
- Cumprida
- Rejeitada

Note: Cada promessa representa o possível resultado de uma tarefa, e inicia no estado Pendente. Ela pode ser cumprida e retornar o valor de sucesso ou, sendo rejeitada, retornar detalhes do erro.

---

## Sem promessas

```
function readJSON(filename, callback){
  fs.readFile(filename, 'utf8', function (err, res){
    if (err) return callback(err);
    try {
      res = JSON.parse(res);
    } catch (ex) {
      return callback(ex);
    }
    callback(null, res);
  });
}
```

Note: Aqui temos um trecho de código assíncrono sem promessas.
A função de callback parece um pouco fora de lugar aqui, sendo chamada em ocasiões diferentes com parâmetros diferentes.
na primeira chamada, ela retorna um erro na função readFile.
na segunda, um erro na função parse, e 
na terceira, uma execução com erro null e um resultado válido.

---

## Sem Promessas

- Sem retorno
- Sem throw
- Sem Stacktrace

Note: 
Percebemos que o retorno pe usado apenas para evitar que a função continue executando, já que os valores retornados não são recebidos em um callback.

Do mesmo modo, não há motivo para lançar erros/exceções pois elas não serão tratadas.

Assim, não teremos um stacktrace disponível, pois o callback atua em uma thread separada.

---

## Com promessas
```
function readJSON(filename){
  return readFile(filename, 'utf8').then(JSON.parse);
}
```

Note: E aqui, a mesma funcionalidade se a função readFile pudesse retornar uma promessa.
Assim que a readFile produzir um valor, este alimentaria a função parse e o programa continuaria.

---

## Implementações em JS

- [then/promise](https://github.com/then/promise) Implementação simples do padrão aberto [Promises/A+](https://promisesaplus.com/)
- [kriskowal/q](https://github.com/kriskowal/q/blob/v1/design/README.js) Implementação que inspira o serviço $q do angularjs
- [petkaantonov/bluebird](https://github.com/petkaantonov/bluebird) Implementação focada em performance
