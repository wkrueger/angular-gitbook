# Fluxo de Dados

Uma aplicação é composta por uma árvore de componentes. O estado da aplicação \(ou seja, os dados de origem\) é atrelado a componentes, através de propriedades da classe.

Eventualmente o estado estará armazenado no componente X mas o componente Y também vai querer ter acesso a ele. Para tal comunicação, um dos dois métodos abaixo geralmente é utilizado:

* Propriedades de entrada e saída de componentes;

```markup
<meu-componente [pessoa]="pessoa"></meu-componente>
```

* Injeção de dependência \(serviços\);

```typescript
@Component({
  template: `<h1>Olá {{ pessoa.nome }}`
})
class Filho {
  constructor(public pessoa: PessoaService) {}
}
```

**Quando usar cada tipo de fluxo de dados**

Este pode ser um tópico complexo. Passo aqui uma recomendação simplista, que está longe de ser uma regra!

* Quando um componente é **reutilizável** ou ele vai se **repetir** \(ex: em um loop\), tende-se a usar propriedades de entrada e de saída; Exemplos:
  * Uma linha de uma tabela;
  * Um Cartão;
  * Um _Dropdown_ ;
* Quando uma determinada página possui dados, os quais serão consumidos \(e alterados\) por múltiplos componentes filhos, é interessante que esses dados morem em um _Serviço_ , e seja comunicado aos componentes via injeção de dependência; Exemplo:
  * Uma tela de CRUD;
  * Dados globais da aplicação;

