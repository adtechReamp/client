![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Analytics & Optimization<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - Puran - Simples de tratar
Última atualização: 08/04/2021 <br />
Em caso de dúvidas, entrar em contato com: [nathalia.paschotto@jellyfish.com](nathalia.paschotto@jellyfish.com)

<br />

## Sumário

- [Objetivo](#objetivo)
- [camada de dados](camada-de-dados)
- [Geral](#geral)
- [Eventos cientificos](#eventos-cientificos)



## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referente ao ambiente:

[http://bp.homolog.enken.cloud/](http://bp.homolog.enken.cloud/)

<br />

---

## Overview e Descrições Técnicas

### Camada de dados 

> É um array de objetos javascript utilizado pelo Google Tag Manager para receber em seus atributos, dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação.

## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />

---

### Geral

**Quando: No clique dos itens do header.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'portal-dos-medicos:geral',
    'eventAction': 'clique:header'',
    'eventLabel': '[[nome-item]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-item]]  |  'logo' e 'abriu-menu'. | Retornar o nome do item clicado.  |


<br />

**Quando: No clique do menu superior lateral.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'portal-dos-medicos:geral',
    'eventAction': 'clique:menu',
    'eventLabel': '[[nome-menu]]:[[submenu]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-menu]] | 'plataformar-para-medico, 'referenciadores', 'eventos-cientificos' e etc. |  Retornar o nome do menu clicado.  |
| [[submenu]] |  'institucional', 'oncologia', 'pediatria' e etc. |Retornar o nome do submenu clicado. |


<br />

**Quando: No clique do itens do footer**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'portal-dos-medicos:geral',
    'eventAction': 'clique:footer',
    'eventLabel': '[[nome-item]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-item]] | Retornar o nome do item clicado dentro da seção. |  'plataformas-para-medico', 'educacao-e-pesquisa', 'eventos', 'instagram' , 'facebook' e etc. |


<br />

**Quando: No clique dos botões dos banners**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'portal-dos-medicos:[[nome-pagina]]',
    'eventAction': 'clique:botao:banner',
    'eventLabel': '[[nome-botao]]:[[nome-banner]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]]  |  'eventos-cientificos', 'referenciadores', 'conheca-bp' e etc.|Deve retornar o nome da página. |
| [[nome-botao]] | 'comece-agora' e etc.| Retornar o nome do botão clicado. |
| [[nome-banner]] |  'bem-vindo(a)-ao-portal-do-medico' e etc.| Retornar o nome do banner clicado. |
<br />

**Quando: No clique dos links de plataformas para os médicos.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'portal-dos-medicos:[[nome-pagina]]',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]:[[nome-banner]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]]  |  'eventos-cientificos', 'referenciadores', 'conheca-bp' e etc.|Deve retornar o nome da página. |
| [[nome-botao]] | 'comece-agora', 'abrir-tasy', 'abrir-2im' e etc.|  Retornar o nome do botão clicado.|
|[[nome-banner]]  | 'agendamento-cirurgico-online', 'indicador-de-performance' e 'tasy' .|  Retornar o nome do botão clicado.|



<br />


**Quando: No clique dos botões ou links de cada seção.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'portal-dos-medicos:[[nome-pagina]]',
    'eventAction': 'clique:[[botao ou link]]',
    'eventLabel': '[[nome-item]]:[[nome-secao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]]  |  'eventos-cientificos', 'referenciadores', 'conheca-bp' e etc.|Deve retornar o nome da página. |
| [[botao ou link]]| 'botao' ou 'link'|Retornar o nome do botão ou link clicado. |
| [[nome-secao]]|'um-hub-de-saude-para-voce-e-seus-pacientes', ' teleducacao' 'plataforma-de-agendamento-cirurgico-on-line', 'contato'  e etc.|Retornar o nome seção. |




<br />

**Quando:   No clique dos botões ou links de cada card.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'portal-dos-medicos:[[nome-pagina]]',
    'eventAction': 'clique:[[botao ou link]]',
    'eventLabel': '[[nome-item]]:[[nome-card]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]]  |  'eventos-cientificos', 'referenciadores', 'conheca-bp' e etc.|Deve retornar o nome da página. |
| [[botao ou link]]|'botao' ou 'link'|Retornar o nome do botão ou link clicado. |
| [[nome-item]]| 'saiba-mais', 'abrir-lista', 'abrir-formulario', 'abrir-tasy' e etc.|Retornar o nome do item clicado.|
| [[nome-card]] |'hospital-bp–unidade-paulista', ' bp-mirante', 'documentos-necessarios','formulario' , 'principais-ferramentas'e etc.|Retornar o nome do card. |






<br />

**Quando:Na interação com o botão de espandir texto dentro de uma div.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'portal-dos-medicos:[[nome-pagina]]',
    'eventAction': 'interacao:leitura',
    'eventLabel': '[titulo-texto]]:[[acao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]]  |  'eventos-cientificos', 'referenciadores', 'conheca-bp' e etc.|Deve retornar o nome da página. |
| [titulo-texto]]|'cuidados', 'emergencia' ,'uti-neurologica' 'programa-segunda-opniao'e etc.| Deve retornar o titulo do texto.|
| [[acao]]| 'abriu' ou 'fechou' |  Deve retornar a ação do usuário. |

---

### Eventos cientificos

**Quando:No clique dos botões ou links de cada card.**<br />

- **Onde:** Na página de eventos cientificos.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'portal-dos-medicos:eventos-cientificos',
    'eventAction': 'clique:[[botao ou link]]',
    'eventLabel': '[[nome-item]]:[[nome-card]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[botao ou link]]|'botao' ou 'link'|Retornar o nome do botão ou link clicado. |
| [[nome-item]]| 'saiba-mais' e 'acessar-plataforma'.|  Retornar o nome do item clicado.|
| [[nome-card]]|'proximos-eventos' e 'teleducacao'. |  Deve retornar o nome do card interagido. |


<br />

**Quando:Na interação com o filtro na aba de eventos.**<br />

- **Onde:** Na página de eventos cientificos.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'portal-dos-medicos:eventos-cientificos',
    'eventAction': 'interação:filtro',
    'eventLabel': 'ano:[[nome-filtro]]:[[nome-aba]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-filtro]]| '2020', '2021 ' e etc.|Deve retornar o texto do filtro.|
| [[nome-aba]]|  'proximos-eventos' e 'eventos-realizados'.|  Retornar o nome da aba.|


<br />

**Quando:Na interação com os campo do formulario.**<br />

- **Onde:** Na página de eventos cientificos.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'portal-dos-medicos:eventos-cientificos',
    'eventAction': '"interação:campo:formulario-cadastro"',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]]| 'nome', 'telefone', 'e-mail' e etc.|Retornar o nome do campo interagido.|



<br />

**Quando:Na interação com o checkbox do formulario.**<br />

- **Onde:** Na página de eventos cientificos.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'portal-dos-medicos:eventos-cientificos',
    'eventAction': 'interação:checkbox:formulario-cadastro',
    'eventLabel': 'aceitou:termo-de-uso-e-politica-de-privacidade'
  });
</script>

```
<br />


**Quando:Na tentativa de callback do envio de formulario.**<br />

- **Onde:** Na página de eventos cientificos.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'portal-dos-medicos:eventos-cientificos',
    'eventAction': 'formulario-cadastro:callback',
    'eventLabel': '[[status]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]]| 'sucesso', 'erro-pagina-indisponivel' e etc.|Deve retornar com o valor de sucesso ou tipo de erro.|



<br />



---

<br />

> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
