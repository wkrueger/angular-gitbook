# Serviços e Injeção de Dependências

Uma classe anotada com `@Injectable()` pode ser **atrelada** a um módulo ou componente;

  \- Ex: Se `MeuServico` for atrelado a `MeuComponente`,  a cada instância de `MeuComponente` será criada uma instância de `MeuServico`; Ainda, todos os filhos de `MeuComponente` terão acesso à essa instância\*.

O serviço:

```typescript
@Injectable()
class MeuServico {
  dizerAlgo() {
    console.log('algo')
  }
}
```

Plugando o serviço a um módulo ou a um componente:

```typescript
// atrelamento a módulo
@Module({ 
  ...,
  providers: [MeuServico]
})
class MeuModulo {}


// atrelamento a componente
@Component({ 
  ...,
  providers /* ou viewProviders */: [MeuServico]
})
class MeuComponente {}
```

* Se você passar o serviço `MeuServico` ao `providers` do componente `MeuComponente`, uma instância desse serviço (`new MeuServico()`) será criada para cada `MeuComponente`. Quando `MeuComponente` for destruído, a instância do serviço também é destruída e é invocado o método `ngOnDestroy()`;
* Se você passar um serviço ao módulo raiz, este serviço efetivamente será um _Singleton_ (instância global).

**Consumindo o serviço**

Acesse o serviço o passando como parâmetro no construtor da classe.

```typescript
@Component(...)
class MeuComponente {

  constructor(private meuServico: MeuServico) {}

  aoClicar() {
    this.meuServico.dizerAlgo()
  }
}
```

* Diz-se aqui que uma instância de `MeuServico` foi **"injetada"** em `MeuComponente`;
* Caso o serviço não tenha sido plugado a nenhum componente ou módulo pai, o Angular vai dar erro;
* Caso o serviço tenha sido providenciado em vários lugares (no módulo e no componente), a instância mais local (a do componente) é fornecida;

PS:

> Na sintaxe `constructor(private arg) {}` , o `private` é um atalho para que o argumento seja copiado para uma propriedade de mesmo nome na classe. Esta é uma sintaxe extra do TypeScript.

> Recomendação: NUNCA use `providedIn: "root"`

**.Exemplo de uso do providers como estado compartilhado**

* Uma instância de `PessoaService` é criada junto com `PaiComponent`;
* Esta **mesma** instância é fornecida a `PaiComponent` e `PessoaComponent`;

Diagrama resumido:

```
[PaiComponent]
            |____ providers: [PessoaService]
            |____ injetado:  [PessoaService]

[PessoaComponent]
            |____ injetado:  [PessoaService]
```

Código:

```typescript
/**
/* componente pai
**/
@Injectable()
class PessoasService {
  pessoas = [] as Pessoa[]
  
  removerPessoa(pessoa: Pessoa) {
    const idx = this.pessoas.indexOf(pessoa)
    this.pessoas.splice(idx, 1)
  }
}


/**
/* componente pai
**/
@Component({
  selector: 'app-pai',
  viewProviders: [PessoasService],
  template: `
    <h1>Lista de pessoas</h1>
    <ul *ngFor="let pessoa of pessoasService.pessoas">
      <li>
        <app-pessoa [pessoa]="pessoa"></app-pessoa>
      </li>
    </ul>
  `
})
class PaiComponent {

  constructor(public pessoasService: PessoasService) {}

}


/**
/* componente filho
**/
@Component({
  selector: 'app-pessoa',
  template: `
    <span>{{ pessoa }}</span>
    <button type="button" (click)="remover()">Remover</button>
  `
})
class PessoaComponent {

  constructor(public pessoasService: PessoasService) {}

  @Input() pessoa!: Pessoa
  
  remover() {
    this.pessoasService.remover(this.pessoa)
  }
}
```

**Inversão de Controle**

Além da funcionalidade de delimitação de contexto, a injeção de dependências é de grande utilidade em mocks para testes.

Quando uma classe especifica que quer consumir `ServicoA`, ela não necessariamente recebe a classe exata `ServicoA`. Você pode passar qualquer outra classe ao `providers` que atenda ao mesmo contrato. Ex: As ferramentas de teste permitem que se instanciem módulos injetando serviços "dublês".

Documentação: [introduction to services and dependency injection](https://angular.io/guide/architecture-services);
