![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - BTG+ - BoostLab
Última atualização: 04/06/2021 <br />
Em caso de dúvidas, entrar em contato com: [nathalia.paschotto@reamp.com.br](nathalia.paschotto@reamp.com.br)

<br />

## Sumário

- [Geral](#geral)
- [Perguntas Frequentes](#perguntas-frequentes-geral)
- [Entre em contato com a gente](#entre-em-contato-com-a-gente-geral) 
- [Sobre nos](#sobre-nos) 
- [Business Hub](#business-Hub)
- [Linha de credito](#linha-de-credito)
- [Mentoria](#mentoria)


## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referente ao ambiente:

[https://www.boostlab.com.br/](https://www.boostlab.com.br/)

<br />


Link de referência: [Documentação Oficial Google Tag Manager](https://developers.google.com/tag-manager/quickstart)


## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />



## Overview e Descrições Técnicas

### Camada de dados (DataLayer)

> É um array de objetos javascript utilizado pelo Google Tag Manager para receber em seus atributos, dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação.

## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />

> Tudo que estiver como geral, deverá ter a mesma nomencratura no elemento do site. (em todas as páginas onde estiver o mesmo elemento)

## Implementação

### Camada de dados (DataLayer)

> É um array de objetos javascript utilizado pelo Google Tag Manager para receber em seus atributos, dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação.

**Instalação**<br />
Inserir a camada de dados antes do snippet de instalação do Google Tag Manager. Exemplo:


```html
<script>
	window.dataLayer = window.dataLayer || [];
	window.dataLayer.push({
		'atributo1': '[[valor1]]',
		'atributo2': '[[valor2]]'
	});
</script>
```

### Geral

**Quando: No clique dos itens do header**<br />

- **Onde:** Em  todas as páginas que estiver disponível
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'boostlab:[[nome-pagina]]',
    'eventAction': 'clique:header',
    'eventLabel': '[[nome-item]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]] | 'home', 'sobre-nos', 'linha-de-credito', 'fale-com-a-gente' e etc. |  Deve retornar o nome da página. |
| [[nome-item]] | 'nossos-produtos', 'logo', 'seus-beneficios', 'entre-na-fila-de-espera' e etc. | Retornar o nome do item clicado.   |


<br />

**Quando: No clique do menu superior**<br />

- **Onde:** Em  todas as páginas que estiver disponível
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'boostlab:[[nome-pagina]]',
    'eventAction': 'clique:header',
    'eventLabel': '[[nome-menu]]:[[submenu]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]] | 'home', 'sobre-nos', 'linha-de-credito', 'fale-com-a-gente' e etc. |  Deve retornar o nome da página. |
| [[nome-menu]] | 'sobre-nos', 'business-hub', 'mentoria', 'perguntas-frequentes' e etc. | Retornar o nome do menu clicado.   |
| [[submenu]] | 'linha de crédito'.| Retornar o nome do submenu clicado.   |


<br />

**Quando: No clique do itens do footer**<br />

- **Onde:** Em  todas as páginas que estiver disponível
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'boostlab:[[nome-pagina]]',
    'eventAction': 'clique:footer',
    'eventLabel': '[[secao]]:[[nome-item]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]] | 'home', 'sobre-nos', 'linha-de-credito', 'fale-com-a-gente' e etc. |  Deve retornar o nome da página. |
| [[secao]] | 'mapa-do-site', 'siga-o-boostlab-nas-redes' e 'entre-em-contato'. | Retornar o nome da seção que está sendo interagida.  |
| [[nome-item]]| 'home', 'business-hub', 'linha-de-credito' , 'linkedin', 'instagram' , 'fale-com-a-gente' , 'logo'e etc.   |Retornar o nome do item clicado dentro da seção. |


<br />

---

### Perguntas Frequentes

<b>(GERAL) </b>

**Quando: Na interação com as dúvidas**<br />

- **Onde:** Em  todas as páginas que estiver disponível
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'boostlab:[[nome-pagina]]',
    'eventAction': 'interacao:duvidas',
    'eventLabel': '[[nome-pergunta]]:[[acao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]] | 'home', 'sobre-nos', 'linha-de-credito', 'fale-com-a-gente' e etc. |  Deve retornar o nome da página. |
| [[nome-pergunta]] |  'que-nivel-de-startups-podem-aplicar', 'tenho-so-uma-ideia-posso-me-inscrever', 'minha-empresa-nao-e-uma-startup-posso-me-inscrever' e etc. | Deve retornar o nome da pergunta.  |
| [[acao]]| 'abriu' ou 'fechou' . |Deve retornar a ação do usuário. |


<br />

---

### Entre em contato com a gente

<b>(GERAL) </b>

**Quando: Na interação com os campo do formúlario de contato.**<br />

- **Onde:** Em  todas as páginas que estiver disponível
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'boostlab:[[nome-pagina]]',
    'eventAction': 'interacao:formulario:[[nome-formulario]]',
    'eventLabel': 'preencheu:campo:[[nome-campo]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]] | 'home', 'sobre-nos', 'linha-de-credito', 'fale-com-a-gente' e etc. |  Deve retornar o nome da página. |
| [[nome-formulario]] |   'venha-dar-um-boost-no-seu-negocio' e etc.| Deve retornar o nome do formulário.   |
| [[nome-campo]]| 'seu-nome', 'nome-empresa', 'e-mail' e etc. |Retornar o nome do campo preenchido.  |


<br />

**Quando: Na interação com os campo de filtro do formúlario de contato.**<br />

- **Onde:** Em  todas as páginas que estiver disponível
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'boostlab:[[nome-pagina]]',
    'eventAction': 'interacao:formulario:[[nome-formulario]]',
    'eventLabel': 'preencheu:campo:[[nome-filtro]]',
    
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]] | 'home', 'sobre-nos', 'linha-de-credito', 'fale-com-a-gente' e etc. |  Deve retornar o nome da página. |
| [[nome-formulario]] | 'venha-dar-um-boost-no-seu-negocio' e etc.| Deve retornar o nome do formulário.   |
| [[nome-filtro]] | 'ramo-atuacao' e 'qual-produto-deseja-atuacao' | Retornar o nome filtrado.   |


<br />

**Quando: Na tentativa de callback de envio do formulário de contato.**<br />

- **Onde:** Em  todas as páginas que estiver disponível
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'boostlab:[[nome-pagina]]',
    'eventAction': 'callback:formulario:[[nome-formulario]]',
    'eventLabel': '[[status]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-pagina]] | 'home', 'sobre-nos', 'linha-de-credito', 'fale-com-a-gente' e etc. |  Deve retornar o nome da página. |
| [[nome-formulario]] | 'boostlab-insights' .| Deve retornar o nome do formulário.   |
| [[status]] | 'sucesso', 'erro:email-invalido', 'pagina-indisponivel-no-momento' e etc.| Retornar a mensagem de sucesso ou tipo de erro.   |


<br />

---

### Home

**Quando: Ao clicar nos elementos do banner .**<br />

- **Onde:**  Na página home.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'boostlab:home',
    'eventAction': 'clique:banner:[[nome-banner]]',
    'eventLabel': '[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-banner]] | 'credito-para-statups-com-receita-recorrente' e 'inscricoes-abertas-batch'| Deve retornar o nome do banner. |
| [[nome-botao]] | 'simular-agora' e 'inscreva-se-agora'.| Deve retornar o nome do botão clicado no banner.  |


<br />

**Quando: Na interação com os campo do formúlario de solicitação de conteúdo.**<br />

- **Onde:**  Na página home.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'boostlab:home',
    'eventAction': 'interacao:formulario:[[nome-formulario]]',
    'eventLabel': 'preencheu:campo:[[nome-campo]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-formulario]] | 'credito-para-statups-com-receita-recorrente' e 'inscricoes-abertas-batch'.| Deve retornar o nome do banner. |
| [[nome-campo]] | 'simular-agora' e 'inscreva-se-agora'.| Deve retornar o nome do botão clicado no banner.  |


<br />

**Quando: Na tentativa de callback de envio do formulário de solicitação de conteúdo.**<br />

- **Onde:**  Na página home.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'boostlab:home',
    'eventAction': 'callback:formulario:[[nome-formulario]]',
    'eventLabel': '[[status]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-formulario]] |  'boostlab-insights' e etc| Deve retornar o nome do formulário. |
| [[status]]| 'sucesso', 'erro:email-invalido', 'pagina-indisponivel-no-momento' e etc.|  Retornar a mensagem de sucesso ou tipo de erro.  |



<br />

**Quando: Ao clicar nos botões  de cada seção.**<br />

- **Onde:**  Na página home.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'boostlab:home',
    'eventAction': 'clique:[[link-ou-botao]]',
    'eventLabel': '[[secao]:[[nome-item]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[link-ou-botao]] | 'link' ou 'botao'| Deve retornar o tipo de elemento interagido. |
| [[secao]|  'noticias-e-artigos' ou 'boostlab-na-midia'.|   Deve retornar o nome da seção que foi interagida. |
| [[nome-item]]| 'valor-invest', 'exame', 'neo-feed', 'estadao', 'leia-mais' e etc.| Deve retornar o nome do botão ou link clicado. |


<br />

---

### Sobre nos

**Quando: Ao clicar nos botões 'saiba-mais'.**<br />

- **Onde:** Na página sobre nós.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'boostlab:sobre-nos',
    'eventAction': 'clique:botao',
    'eventLabel': '[[titulo-card]]:[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[titulo-card]] |  'business-hub' e 'o-programa' e etc.| Deve retornar o titulo do card. |
| [[nome-botao]] | 'saiba-mais'.|   Deve retornar o nome do botão clicado na seção. |



<br />

---

### Business Hub

**Quando: Ao clicar nos elementos de cada seção.**<br />

- **Onde:**  Na página business.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'boostlab:business-hub',
    'eventAction': 'clique:[[link-ou-botao]]',
    'eventLabel': '[[secao]:[[nome-item]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[link-ou-botao]] | 'link' ou 'botao'| Deve retornar o tipo de elemento interagido. |
| [[secao]|  'diferenciais'.|   Deve retornar o nome da seção que foi interagida. |
| [[nome-item]]| 'btg-pactual', 'exame', 'programa-de-mentoria' ou 'global-finance'.| Deve retornar o nome do botão ou link clicado. |


<br />

---

### Linha de credito

**Quando: Ao clicar nos elementos de cada seção.**<br />

- **Onde:**  Na página linha de crédito.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'boostlab:linha-de-credito',
    'eventAction': 'clique:[[link-ou-botao]]',
    'eventLabel': '[[secao]:[[nome-item]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[link-ou-botao]] | 'link' ou 'botao'| Deve retornar o tipo de elemento interagido. |
| [[secao]|   'caracteristicas', 'solicitacao-de-financiamento' e etc. |Deve retornar o nome da seção que foi interagida.|
| [[nome-item]]| 'solicite-seu-financiamento'.| Deve retornar o nome do botão ou link clicado. |


<br />

**Quando: Ao clicar nos elementos de cada seção.**<br />

- **Onde:**  Na página linha de crédito.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'boostlab:linha-de-credito',
    'eventAction': 'interacao:duvidas',
    'eventLabel': '[[nome-pergunta]]:[[acao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[link-ou-botao]] | 'link' ou 'botao'| Deve retornar o tipo de elemento interagido. |
| [[secao]|   'o-que-e-a-linha-de-credito-mrr', 'minha-empresa-nao-e-uma-startup-posso-me-inscrever' e etc. |Deve retornar o nome da pergunta.|
| [[nome-item]]| 'abriu' ou 'fechou'.| Deve retornar a ação do usuário.  |


<br />


---

### Mentoria

**Quando: Ao clicar nos elementos do banner.**<br />

- **Onde:**  Na página de Mentoria.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'boostlab:mentoria',
    'eventAction': 'clique:botao:banner',
    'eventLabel': '[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] |'inscreva-se'.|  Deve retornar o nome do botão . |


<br />

**Quando:Ao clicar em algum card de mentores do programa.**<br />

- **Onde:**  Na página de Mentoria.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'boostlab:mentoria',
    'eventAction': 'clique:card',
    'eventLabel': '[[titulo-card]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[titulo-card]] |'amos-genish', 'andre-alves', 'andre-iasi' e etc.|  Deve retornar o titulo do card . |


<br />

**Quando:Ao clicar no botão 'ver-mais' mentores.**<br />

- **Onde:**  Na página de Mentoria.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'boostlab:mentoria',
    'eventAction': 'clique:botao',
    'eventLabel': 'ver-mais'
  });
</script>

```

<br />

**Quando:Ao clicar em algum card da seção Alumni.**<br />

- **Onde:**  Na página de Mentoria.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'boostlab:mentoria',
    'eventAction': 'clique:link',
    'eventLabel': 'imagem:potencializada-alumni'
  });
</script>

```

<br />

**Quando:Ao clicar em algum card de mentores do programa.**<br />

- **Onde:**  Na página de Mentoria.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'boostlab:mentoria',
    'eventAction': 'interacao:aba',
    'eventLabel': '[[nome-item]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-item]] | 'btg-pactual' ou 'ace'.| Deve retornar o nome da aba clicada . |


<br />

---

<br />

> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
