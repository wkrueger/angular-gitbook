# Considerações sobre Estilos

* Estilos de componentes possuem escopo restrito e **isolado** a esses componentes. Isto significa que componentes filho, por padrão, não recebem o estilo do componente pai;
* Este comportamento pode ser burlado com o seletor `::ng-deep` \*;

> \(\*\) O seletor ng-deep é deprecado mas não tende a ser substituído até que um equivalente seja oficialmente publicado nas especificações do CSS.

```css
.componente-filho ::ng-deep svg {
  stroke: black;
}

:host {
  /* estilos *deste* componente */
  display: block;
}
```

* O seletor `:host` é usado pra aplicar estilos à raiz do componente;
* Além dos estilos isolados de componente, o projeto também conta com **estilos globais**, que são os presentes na raiz `src/styles.scss`.

