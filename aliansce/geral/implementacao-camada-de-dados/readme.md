![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - Geral
Última atualização: 21/01/2020 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Implementação](#implementa%c3%a7%c3%a3o)
- [Especificações Globais](#especifica%c3%a7%c3%b5es-globais)
- [Dimensões Globais](#dimens&otilde;es-globais)
- [Geral](#geral)
- [Bem vindo](#bem-vindo)
- [Cadastro](#cadastro)
- [Login](#login)
- [Esqueci minha senha](#esqueci-minha-senha)
- [Home](#home)
- [Cinema](#cinema)
- [O Shopping](#o-shopping)
- [Lojas](#lojas)
- [Alimentação](#alimenta&ccedil;&atilde;o)
- [Contato](#contato)
- [Área Logada](#&aacute;rea-logada)
- [Vitrine de produtos](#vitrine-de-produtos)

## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referentes aos ambientes:

[www.bangushopping.com](www.bangushopping.com),
[www.boulevardshoppingbauru.com.br](www.boulevardshoppingbauru.com.br),
[www.boulevardbelem.com.br](www.boulevardbelem.com.br),
[www.boulevardshopping.com.br](www.boulevardshopping.com.br),
[www.boulevardcampos.com.br](www.boulevardcampos.com.br),
[www.boulevardvilavelha.com.br](www.boulevardvilavelha.com.br),
[www.boulevardshoppingbrasilia.com.br](www.boulevardshoppingbrasilia.com.br),
[www.cariocashopping.com.br](www.cariocashopping.com.br),
[www.caxiasshopping.com.br](www.caxiasshopping.com.br),
[www.parqueshoppingba.com.br/](www.parqueshoppingba.com.br/),
[www.parqueshoppingbelem.com.br](www.parqueshoppingbelem.com.br),
[www.maceioparqueshopping.com.br](www.maceioparqueshopping.com.br),
[www.passeioshopping.com.br](www.passeioshopping.com.br),
[recreioshopping.com.br](recreioshopping.com.br),
[www.santanaparqueshopping.com.br](www.santanaparqueshopping.com.br),
[www.saogoncaloshopping.com.br/](www.saogoncaloshopping.com.br/),
[www.shoppingdabahia.com.br](www.shoppingdabahia.com.br),
[www.shoppinggranderio.com.br](www.shoppinggranderio.com.br),
[www.shoppingparangaba.com.br](www.shoppingparangaba.com.br),
[www.shoppingtaboao.com.br](www.shoppingtaboao.com.br),
[www.viaparqueshopping.com.br](www.viaparqueshopping.com.br),
[www.westplaza.com.br](www.westplaza.com.br),
[www.shoppingpracanovaaracatuba.com.br](www.shoppingpracanovaaracatuba.com.br),
[www.boulevardlondrinashopping.com.br/](www.boulevardlondrinashopping.com.br/),
[www.francashopping.com.br/](www.francashopping.com.br/),
[www.manauarashopping.com.br/](www.manauarashopping.com.br/),
[www.parquedpedro.com.br/](www.parquedpedro.com.br/),
[www.passeiodasaguasshopping.com.br/](www.passeiodasaguasshopping.com.br/),
[www.shoppingcampolimpo.com.br/](www.shoppingcampolimpo.com.br/),
[www.shoppingmetropole.com.br/](www.shoppingmetropole.com.br/),
[www.plazasulshopping.com.br/](www.plazasulshopping.com.br/),
[www.uberlandiashopping.com.br/](www.uberlandiashopping.com.br/),<br />
[www.pracanovashopping.com.br](www.pracanovashopping.com.br),<br />
[boulevardfeira.com.br/](boulevardfeira.com.br/)<br />

<br />

## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />

---

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

### Especificações Globais:

**Itens Gerais:**<br />
Todas as informações entre colchetes `[[  ]]` são variáveis dinâmicas que devem ser preenchidas com seus respectivos valores; <br />
Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais; <br />
Caso a informação solicitada não estiver disponível retornar tipagem ´undefined´.



### Dimensões Globais:

**Dimensões Customizadas para todas as páginas:**<br />
Deve ser disparado um push de dataLayer no momento de carregamento de todas as páginas do site (Considerar também todas as trocas de Path, quando o conteúdo da página é alterado mas a página não recarrega).<br />


```html
<script>
	window.dataLayer = window.dataLayer || [];
	dataLayer.push({
		'dimension1': '[[User ID]]',
		'dimension2': '[[GA ClientID]]',
		'dimension3': '[[GTM-ID]]',
	  'dimension4': '[[Nome Ambiente]],
    'dimension5': '[[Nome Loja]],
    'dimension6': '[[Localização]],
    'dimension7': '[[Device ID]]

	
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[User ID]]			| '1234656'			    | ID definido após o cadastro e login										|
| [[GA ClientID]]	| 'XXXXXXXXXX:XXXX:XX'	| ID aleatório do Google Analytics										|
| [[GTM-ID]]			| 'GTM-TK8RPDC'		| ID do container do GTM instalado no ambiente										|
| [[Nome Ambiente]] | parque-d-pedro', 'shopping-taboao' e etc | Deve retornar o nome do shopping visitado.  |
| [[Nome Loja]] | 'concept', 'marisa' e etc | Deve retornar o nome da loja  |
| [[Localização]] | 'capao-redondo', 'morumbi', 'santa-cruz' e etc. | Deve retornar a localização  |
| [[Device ID]]   | 'XXXXXXX' | Deve retornar o ID do dispositivo utilizado   |

---

### Geral

**Quando: No clique dos links do header**<br />

- **Onde:** Em todas as páginas do site em que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:geral',
    'eventAction': 'clique:header',
    'eventLabel': '[[nome-item]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[nome-item]] |  'logo', 'horario-funcionamento', 'login' ou 'buscar'. | Retornar o nome do item clicado.   |


<br />

**Quando: No clique dos links do footer**<br />

- **Onde:** Em todas as páginas do site em que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:geral',
    'eventAction': 'clique:footer',
    'eventLabel': '[[secao]]:[[nome-item]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[secao]] | 'o-shopping', 'compre-online', 'lojas', 'social', 'endereco' e etc. | Deve retornar o nome da seção   |
| [[nome-item]] | 'sobre-o-shopping', 'marcas', 'lista-de-lojas' e etc. | Deve retornar o nome do item clicado. |


<br />

**Quando: No clique dos itens do menu.**<br />

- **Onde:** Em todas as páginas do site em que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:geral',
    'eventAction': 'clique:menu',
    'eventLabel': '[[item-menu]]:[[item-submenu]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[item-menu]] | 'o-shopping', 'shopping-online', 'lojas' e etc. | Deve retornar o nome do item do menu clicado.  |
| [[item-submenu]] |  'sobre-o-shopping', 'marcas', 'lista-de-lojas' e etc. |Deve retornar o nome do item do submenu clicado.   |

<br />

### Bem vindo

**Quando: No clique dos botões ou links**<br />

- **Onde:** Na página "Bem vindo"

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:bem-vindo',
    'eventAction': 'clique:[[botao ou link]]',
    'eventLabel': '[[nome-item]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[botao ou link]] | 'botao' ou 'link' |  Deve retornar o tipo de elemento clicado.  |
| [[nome-item]] |  'entrar', 'novo-usuario', esqueci-minha-senha' e etc | Deve retornar o nome do botão ou link clicado.  |

<br />

### Cadastro


**Quando: Na interação com os campos.**<br />

- **Onde:** Na página de cadastro.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:cadastro',
    'eventAction': 'interacao:campo',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[nome-campo]] |  'nome', 'email', 'bairro' e etc | Deve retornar o nome do campo preenchido.  |


<br />

**Quando: Na interação com o checkbox.**<br />

- **Onde:** Na página de cadastro.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:cadastro',
    'eventAction': 'interacao:checkbox',
    'eventLabel': '[[acao]]:autorizo-o-uso-dos-meus-dados'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[acao]] |  'check', 'uncheck' | Deve retornar a ação do usuário.  |



<br />

**Quando: No clique dos botões**<br />

- **Onde:** Na página de cadastro.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:cadastro',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[nome-botao]] |  'enviar-codigo-de-verificacao', 'criar', 'cancelar' | Deve retornar o nome do botão clicado.   |


<br />

**Quando: Na tentativa de callback para efetuar o cadastro**<br />

- **Onde:** Na página de cadastro.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': '[[nome-ambiente]]:cadastro',
    'eventAction': 'callback',
    'eventLabel': '[[status]]',
    'dimension1': '[[User ID]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[status]] | 'sucesso', 'erro:usuario-ou-senha-invalidos', 'erro:pagina-fora-do-ar' e etc | Deve retornar a mensagem de sucesso ou o tipo de erro. |
| [[[User ID]] | '1234656' e etc | ID definido após o cadastro e login |


<br />


### Login

**Quando: Na interação com os campos**<br />

- **Onde:** Na página de login.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:login',
    'eventAction': 'interacao:campo',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[nome-campo]] |   'email', 'senha' | Deve retornar o nome do campo preenchido.   |


<br />

**Quando: No clique dos botões**<br />

- **Onde:** Na página de login.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:login',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[nome-botao]] |  'entrar', 'cancelar' | Deve retornar o nome do botão clicado.   |


<br />

**Quando: Na tentativa de callback para efetuar o login**<br />

- **Onde:** Na página de login.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'login',
    'eventCategory': '[[nome-ambiente]]:login',
    'eventAction': 'callback',
    'eventLabel': '[[status]]',
    'dimension1': '[[User ID]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[status]] | 'sucesso', 'erro:usuario-ou-senha-invalidos', 'erro:pagina-fora-do-ar' e etc | Deve retornar a mensagem de sucesso ou o tipo de erro. |
| [[[User ID]] | '1234656' e etc | ID definido após o cadastro e login |

<br />

### Esqueci minha senha

**Quando: Na interação com os campos**<br />

- **Onde:** Na página "Esqueci minha senha"
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': [[nome-ambiente]]:esqueci-minha-senha',
    'eventAction': 'interacao:campo',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[nome-campo]] |   'email', 'codigo-de-verificacao' | Deve retornar o nome do campo preenchido.   |


<br />

**Quando: No clique dos botões**<br />

- **Onde:** Na página "Esqueci minha senha"

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:esqueci-minha-senha',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[nome-botao]] |  'enviar-codigo-de-verificacao', 'continuar', 'cancelar' e etc | Deve retornar o nome do botão clicado.   |


<br />

**Quando: Na tentativa de callback para cadastrar a nova senha**<br />

- **Onde:** Na página "Esqueci minha senha".

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:esqueci-minha-senha',
    'eventAction': 'callback',
    'eventLabel': '[[status]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[status]] | 'sucesso', 'erro:nao-encontramos-sua-conta' e etc | Deve retornar a mensagem de sucesso ou o tipo de erro. |


<br />

### Home

**Quando: No clique do botão flutuante**<br />

- **Onde:** Na página home.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:home',
    'eventAction': 'clique:botao-flutuante',
    'eventLabel': 'compre-online'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |


<br />

**Quando: No clique dos botões ou links de cada seção**<br />

- **Onde:** Na página home.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:home',
    'eventAction': 'clique:[[botao-ou-link]]',
    'eventLabel': '[[secao]]:[[nome-item]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[botao-ou-link]] | 'botao' ou 'link' | Deve retornar o tipo de elemento clicado.  |
| [[secao]] |  'acontece', 'lojas', 'cinema' e etc' | Deve retornar o nome da seção. |
| [[nome-item]] | 'leia-mais', 'agenda', 'buscar', 'todos-os-filmes' e etc | Deve retornar o nome do item clicado.  |


<br />

**Quando: No clique dos cards na seção de cinema**<br />

- **Onde:** Na página home.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:home',
    'eventAction': 'clique:card',
    'eventLabel': 'cinema:[[nome-filme]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[nome-filme]] | 'sapatinho-vermelho-e-os-setes-anoes', 'um-tio-quase-perfeito-2' e etc | Deve retornar o nome do filme.  |


<br />

**Quando: No clique dos links "comprar" na seção de cinema**<br />

- **Onde:** Na página home.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:home',
    'eventAction': 'clique:link',
    'eventLabel': 'comprar:[[nome-filme]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[nome-filme]] | 'sapatinho-vermelho-e-os-setes-anoes', 'um-tio-quase-perfeito-2' e etc | Deve retornar o nome do filme.  |


<br />

**Quando: Na interação com o campo de busca na seção de lojas**<br />

- **Onde:** Na página home.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:home',
    'eventAction': 'interacao:campo:lojas',
    'eventLabel': 'busca:[[termo-buscado]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[termo-buscado]] |  'vivara', 'marisa' e etc |  Deve retornar o termo buscado. |


<br />

**Quando: Na interação com o campo de filtro na seção de lojas**<br />

- **Onde:** Na página home.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:home',
    'eventAction': 'interacao:filtro:lojas',
    'eventLabel': 'filtre-por-categoria:[[nome-item]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[nome-item]] | 'artigos-diversos', 'conveniencia-servicos', 'alimentacao' e etc | Deve retornar o nome do item escolhido no filtro.  |


<br />

**Quando: Na tentativa de callback para efetuar a busca na seção de lojas**<br />

- **Onde:** Na página home.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:home',
    'eventAction': 'callback:busca:lojas',
    'eventLabel': '[[termo-buscado]]:[[status]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[termo-buscado]] |  'artwalk', 'vivara' e etc|  Deve retornar o termo buscado. |
| [[status]] |  'sucesso', 'erro:loja-nao-encontrada e etc |  Deve retornar a mensagem de sucesso ou o tipo de erro |


<br />

### Cinema

**Quando: No clique do link "comprar" de cada filme**<br />

- **Onde:** Na página de cinema.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:cinema',
    'eventAction': 'clique:link',
    'eventLabel': 'comprar:[[nome-filme]]:[[data-selecionada]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[nome-filme]] |  'mulher-maravilha-1984' e etc |  Deve  retornar o nome do filme. |
| [[data-selecionada]] | 'sexta-08/01' e etc | Deve retornar a data selecionada. |


<br />

**Quando: No clique do botão "confira os preços de bilheteria"**<br />

- **Onde:** Na página de cinema.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:cinema',
    'eventAction': 'clique:botao',
    'eventLabel': 'confira-os-precos-de-bilheteria'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |



<br />


### O Shopping

**Quando: No clique dos botões ou links de cada seção.**<br />

- **Onde:** Na página Sobre o Shopping.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:o-shopping',
    'eventAction': 'clique:[[card-ou-botao]]',
    'eventLabel': 'acontece:[[nome-item]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[card-ou-botao]] | 'botao' ou 'card'. | Deve retornar o tipo de elemento clicado. |
| [[nome-item]] | 'agenda', 'o maravilhoso natal premiado', 'compre-online' e etc. | Deve retornar o nome do item clicado. |



<br />

**Quando: Ao clicar em um dos botões das opções de piso.**<br />

- **Onde:**  Na página Mapa Interno.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:mapa-interno',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-piso]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[nome-piso]] | 'l1', 'mezanino', 'terreo' e etc. | Deve retornar o nome do piso selecionado. |



<br />

**Quando: Ao interagir com os itens de Facilidades.**<br />

- **Onde:**  Na página Facilidades.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:facilidades',
    'eventAction': 'interacao:itens',
    'eventLabel': '[[nome-item]]:[[acao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |
| [[nome-item]] |  'achados-e-perdidos', 'wifi', 'caixas-eletronicos' e etc. | Deve retornar o nome do item de Facilidades clicado.  |
| [[acao]] | 'abriu' ou 'fechou'. | Deve retornar a ação do usuário.  |



<br />

**Quando: No clique do item "ver no mapa"**<br />

- **Onde:**  Na página Facilidades.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:facilidades',
    'eventAction': 'clique:link',
    'eventLabel': 'ver-no-mapa'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]] | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao' | Deve retornar o nome do ambiente. |


<br />

> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>