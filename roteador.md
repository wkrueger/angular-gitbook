# Roteador

O Angular gera uma aplicação "single page", e o roteador é um componente importantíssimo neste contexto. O roteador permite com que a aplicação não seja totalmente recarregada quando se troca de página.

O que o roteador faz? Em resumo:

* Providencia um componente `<router-outlet>`;

Exemplo: No boilerplate padrão do Angular, o `<router-outlet>` é elemento único do componente raiz.

```typescript
@Component({
  selector: "app-root",
  template: ` <router-outlet></router-outlet> `,
  styles: [],
})
export class AppComponent {}
```

* Solicita a configuração de um mapeamento entre URLs e:
  * Componentes ou;
  * Grupos de subrotas ou;
  * Módulos com subroteadores ou;
  * Redirecionamentos;

Exemplo

```typescript
const routing = RouterModule.forRoot([
  { path: "", component: IntroComponent }, //componente
  { path: "gato/:id", component: GatoComponent },
  {
    path: "cachorro",
    loadChildren: () => import("./Cachorro/Cachorro.module")
      .then((m) => m.CachorroModule), // submódulo
  },
  { path: "capivara", children: [...] },  // agrupamento
  { path: "**", redirectTo: '' }
])

@Module({
  ...
  imports: [routing, ...]
  ...
})
export class AppModule {}
```

* Sempre que um URL é alterado \(ou no carregamento inicial de uma página\), o componente correspondente é carregado no "outlet";
* Fornece os serviços a seguir que podem ser injetados:
  * `ActivatedRoute` pra determinarmos informações sobre o estado do roteador. Como: qual rota está ativada? Quais os parâmetros de URL?
  * `Router`, que é usado pra controlar o roteador \(ir para...\);

```typescript
@Component({ ... })
class AlgumComponente {

  constructor(private route: ActivatedRoute, private router: Router) {}

  async ngOnInit() {
    const queryParams = await this.route.queryParams.pipe(take(1)).toPromise()
    console.log(queryParams)
  }

  goto() {
    this.router.navigate('/someroute', { queryParams: { hello: 'world' } })
  }

}
```

* O uso de links padrão do HTML \(`<a href="/page"/>`\) não é amigável pra SPA's pois fazem recarregar a página toda; Deve ser usada ao invés disso a diretiva `routerLink` fornecida pelo roteador.

```markup
<a [routerLink]="['/hero', hero.id]">Goto hero</a>
```

* **Subroteadores e múltiplos outlets**: Conforme apontado anteriormente, é possível haver "roteadores filho". Neste caso haverá no HTML um `<router-outlet>` dentro de outro. Há também funcionalidade avançada onde um roteador pode controlar múltiplos _outlets_.

Mais informações no \(extenso\) [guia do roteador](https://angular.io/guide/router-tutorial-toh).

