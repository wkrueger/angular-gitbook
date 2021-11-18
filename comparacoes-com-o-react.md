# Comparações com o React

**Onde o Angular pode parecer mais fácil, se comparado ao React**

* O uso de _templates_ HTML e folhas de estilo (ao invés de JSX e CSS-in-JS) é algo mais familiar a pessoas com experiência prévia de web;
* O uso da injeção de dependências do Angular é muito mais simples do que as alternativas do React (contexto e Redux); Há uma sobrecarga cognitiva menor e é mais difícil de dar tiro no pé;
* Não é necessário se preocupar em fazer alterações imutáveis de estado (na maioria das situações); O re-render é mais "automágico";
* É mais difícil dar tiro no pé. Uma aplicação Angular sem preocupação com otimização ainda tem uma performance razoável, enquanto no caso do React é muito fácil criarmos renders extremamente lentos;
* A framework abstrai para si a complexa configuração de build e "code splitting", você geralmente não toca em configuração de webpack;
* Módulos sugeridos de formulários e roteador podem não ter a melhor experiência, mas são estáveis; As libs da moda não mudam todo ano, o que é excelente pra projetos duráveis. O ecossistema em geral é mais estável.
