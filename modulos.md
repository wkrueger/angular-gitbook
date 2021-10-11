# Módulos

O ponto de entrada de uma aplicação Angular é o arquivo main.ts (gerado pelo CLI). Esta aponta para o módulo raiz (no caso abaixo, `AppModule`).

```typescript
// main.ts
// ...
platformBrowserDynamic()
  .bootstrapModule(AppModule) // <-- AppModule é o módulo de entrada
  .catch((err) => console.error(err))
```

Um módulo une componentes, submódulos, serviços, diretivas, dentre outros

O módulo raiz `AppModule` aponta que o componente raiz será o `AppComponent`, via propriedade `bootstrap`:

```typescript
// app/app.module.ts
// ...
import { AppComponent } from "./app.component"

@NgModule({
  declarations: [AppComponent], //Componentes e diretivas aqui
  imports: [BrowserModule, AppRoutingModule], // Outros módulos aqui
  providers: [], // Serviços aqui
  bootstrap: [AppComponent], // AppComponent é o módulo de entrada
})
export class AppModule {}
```

* Componentes do Angular devem ser registrados na propriedade `declarations` para estarem disponíveis em templates.
* A aplicação pode ser dividida em submódulos para podermos configurar o _code splitting_ (não é o intuito desse texto). O _code splitting_ é usado pra dividir sua aplicação em partes menores e evitar que o browser fique 1 minuto parado em uma tela branca pra carregar um JS de 15MB.

Outros itens:

* A chave `imports` é usada pra importar submódulos;
  * Caso você use uma biblioteca de terceiros, caso tenha separado seu código em submódulos, ou mesmo precise usar algum recurso adicional do Angular, você incluirá itens no `imports`;
* A chave `providers` é destinada à injeção de dependências. Mais sobre isso adiante!
* Quando um módulo é para ser consumido por outros via `imports`, usa-se a chave `exports` para determinar quais componentes são expostos;

Docs: [introduction to modules](https://angular.io/guide/architecture-modules).
