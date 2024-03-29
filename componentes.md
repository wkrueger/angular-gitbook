# Componentes

No Angular, um componente é um bloco que une:

* Um template "Angular HTML";
* Uma folha de estilos com escopo isolado (CSS ou SCSS);
* Um arquivo TS para os metadados, estado e a lógica do componente.

O template "Angular HTML" aceita sintaxes específicas do Angular, dentre elas:

* Outros **componentes** podem ser incluídos a partir de suas tags ex: `<meu-componente></meu-componente>`;
* **Diretivas** do Angular podem definir propriedades personalizadas de elementos. Ex: `<div tooltipText="Hello world"></div>`

Um componente é iniciado a partir de uma classe anotada com `@Component`. As propriedades **selector** e **template(Url)** são obrigatórias.

```typescript
import { Component } from "@angular/core"

@Component({
  selector: "app-root",
  template /* ou templateUrl */: `<p>Olá mundo, {{ nomeDaPessoa }}</p>`,
  styleUrls /* ou styles */: ["./app.component.scss"],
})
export class AppComponent {
  nomeDaPessoa = "Ana"
  umaLista = ["um", "dois", "três"]
}
```

* O atributo `selector` indica como este componente será chamado dentro do template.
* No arquivo de módulo, este componente deve ser registrado na chave `declarations`;
* O template e os estilos podem ser declarados ou "em linha" (`template`) ou em outro arquivo (`templateUrl`).

No **corpo da classe** declaramos propriedades e funções para compor o estado e a lógica do componente.

* As propriedades definidas no corpo da classe são acessíveis no HTML a partir da sintaxe de template que veremos adiante;
* Quando o valor de uma propriedade é alterado (ex: `nomeDaPessoa`), a visualização HTML é atualizada de acordo.

**Ciclo de vida:**

* A classe de componente pode também receber alguns métodos predefinidos relacionados ao _ciclo de vida de componente_ . Usos populares são o `ngAfterViewInit()` (ao iniciar componente), `ngOnDestroy()` (ao desmontar componente)  e `ngOnChanges()` (quando uma prop é alterada). Mais em [lifecycle hooks](https://angular.io/guide/lifecycle-hooks).

Docs: [introduction to components](https://angular.io/guide/architecture-components);
