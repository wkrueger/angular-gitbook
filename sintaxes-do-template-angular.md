# Sintaxes do Template Angular

* Alguns dos recursos suportados pelo template Angular:

**Interpolação de variáveis**

* Qualquer **propriedade da classe** de componente é disponível no template.
* Para interpolação usam-se chaves duplas.

```markup
<p>Olá, {{ nomeDaPessoa }}</p>
```

**Passando atributos**

```markup
<!-- 1 -->
<componente entrada="texto texto"></componente>
<!-- 2 -->
<componente [entrada]="umaLista"></componente>
<!-- 3 -->
<componente (saida)="algumaFuncao($event)"></componente>
<!-- 4 -->
<componente [(twoWay)]="variavel"></componente>
```

1. Passa a **string literal** `"texto texto"` para o parâmetro;
2. Passa a **propriedade** declarada na classe para o parâmetro \(no caso, umaLista= \["um", "dois", "três"\]\)
3. Quando componentes emitem eventos, usam-se parênteses. Ex: `(click)`, `(hover)`, `(submit)`;
   * `$event` é o valor emitido pelo evento.
4. A sintaxe `[(twoWay)]` une uma propriedade de saída e uma de entrada em uma mesma notação. É um atalho para `[twoWay]="variavel" (twoWayChange)="variavel = $event"`;

Ver [property binding](https://angular.io/guide/property-binding);

**Loops**

```markup
<!--
@Component(...)
class OComponente {
  lista = ["Maria", "Ana", "José"]
}
-->

<div *ngFor="let item of lista">{{ item }}</div>
```

Aqui, esta div será repetida para cada item da lista.

**Condicionais**

```markup
<!--
@Component(...)
class OComponente {
  exibirItem = false
}
-->

<div *ngIf="exibirItem">Estou ativo.</div>
```

Ver [structural directives](https://angular.io/guide/structural-directives);

**CSS condicional**

```markup
<!--
@Component(...)
class OComponente {
  itemEstaAtivo = true
}
-->

<div [class.active]="itemEstaAtivo"></div>
```

Adiciona a classe `active` se a variável for verdadeira.

Mais informações em [attribute, class and style bindings](https://angular.io/guide/attribute-binding);

**Referenciando elementos**

* Elementos em um template podem ser referenciados na respectiva classe com a anotação `@ViewChild()`;
* Anotações com `#` são usadas pra auxiliar referências.

No exemplo abaixo, acessamos a instância de um componente filho \(DatePicker\) a partir de um componente pai \(AppComponent\), e chamamos um método do filho.

```typescript
// date-picker.component.ts
@Component({ selector: 'date-picker', ... })
export class DatePickerComponent {

  pickDate() {
    console.log('date picked')
  }

}
```

```typescript
// app.component.ts
@Component({
  template: `
    <date-picker #datePicker></date-picker>
    <div #theDiv>Hello</div>
  `,
})
export class AppComponent {
  @ViewChild("datePicker") datePickerElement1!: DatePickerComponent
  // ou
  @ViewChild(DatePickerComponent) datePickerElement2!: DatePickerComponent

  @ViewChild("theDiv") divElement!: ElementRef

  ngAfterViewInit() {
    this.datePickerElement1.pickDate()
  }
}
```

Sobre as anotações de tipo do exemplo acima - lembrando que anotações de tipo são sempre opcionais, você sempre pode só colocar um `any`:

* Usa-se a própria classe do componente \(`DatePickerComponent`\), quando o elemento referenciado é um componente Angular;
* `ElementRef` quando é um elemento HTML qualquer;
* `TemplateRef` quando é uma tag `<ng-template>`

**ng-container**

Se deseja aplicar _ngIf ou_ ngFor sem criar uma div para isso, use ng-container.

```markup
<ng-container *ngFor="let num of umaLista">{{ num }}</ng-container>
```

**ng-template**

Os elementos dentro de um `ng-template` não são diretamente renderizados. Ele é usado para passar um bloco de HTML como variável a um componente ou função \(exemplo: um modal\). Você verá ele sendo usado em bibliotecas de interface de usuário \(ex: Material, Bootstrap, etc\).

Exemplo \(abaixo\): Uma biblioteca especifica a diretiva `hoverPopup` que recebe como entrada uma seção de template. Ao passar o mouse por cima deste componente, um popup com este HTML é exibido.

```markup
<ng-template #popup>
  <p>Bem vindo</p>
</ng-template>

<label [hoverPopup]="popup">Exibir</label>
```

Mais informações na [documentação do template Angular](https://angular.io/guide/template-syntax).

