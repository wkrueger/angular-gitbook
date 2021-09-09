# Propriedades de Entada e Saída

**Entrada**

Anote uma propriedade com `@Input()` para amarrá-la a uma entrada do componente.

Filho:

```typescript
@Component({
  selector: "app-some-component",
  template: `<button type="button">{{ texto }}</button>`,
})
export class SomeComponent {
  @Input() texto = ""

  ngOnChanges(changes) {
    console.log(changes)
  }
}
```

Pai \(consumudor\):

```typescript
@Component({
  selector: "app-consumer",
  template: `<app-some-component texto="Clique aqui"></some-component>`,
})
export class ConsumerComponent {}
```

* No exemplo acima, um botão é desenhado com o conteúdo "Clique aqui".
* A linha `@Input() texto` indica que o componente aceita uma propriedade de entrada;
* A propriedade de entrada é passada no template: 

  ```typescript
  <app-some-component texto="Clique aqui"></app-some-component>
  ```

* O método opcional `ngOnChanges` é chamado sempre que uma `@Input()` sofre alteração.

**Saída**

Um componente envia sinais de saída a partir de `EventEmitter`s anotados com `@Output()`;

* Ao escrever `EventEmitter`, o editor dará várias sugestões. Selecione a pertencente ao `@angular/core`.

Emissor:

```typescript
@Component({
  selector: "app-output",
  template: `<button type="button" (click)="processarClique($event)">Click me</button>`,
})
class OutputComponent {
  @Output() fuiClicado = new EventEmitter<Date>()

  processarClique(ev) {
    this.fuiClicado.emit(new Date())
  }
}
```

Consumidor

```typescript
@Component({
  selector: "app-consumer",
  template: `<app-output (fuiClicado)="tratar($event)"></app-output>`,
})
class ConsumerComponent {
  tratar(ev) {
    console.log(ev) // irá logar a Data atual
  }
}
```

Ver [inputs and outputs](https://angular.io/guide/inputs-outputs).

