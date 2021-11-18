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

* Componentes do Angular devem ser registrados na propriedade `declarations` para estarem disponíveis em templates. Se você tentar incluir `<meu-componente>` dentro de um template HTML, e esse componente não estiver registrado, o compilador registrará um erro.
* A aplicação pode ser dividida em submódulos. Os submódulos pode ser usados pra controlar a divisão do JavaScript gerado (code splitting) - sem o uso de módulos todo o JS é concentrado em um grande arquivo que é carregado na inicialização. Com módulos, partes do código podem ser carregadas apenas quando necessário.

Outros itens:

* A chave `imports` é usada pra importar submódulos. Exemplos de uso;
  * Consumir bibliotecas de terceiros;
  * O projeto foi dividido em submódulos;
  * Uso de recursos opcionais do Angular;
* A chave `providers` é destinada à injeção de dependências. Mais sobre isso adiante!
* Quando um módulo é criado para ser consumido por outros via `imports`, usa-se a chave `exports` para determinar quais componentes são expostos;

Docs: [introduction to modules](https://angular.io/guide/architecture-modules).
