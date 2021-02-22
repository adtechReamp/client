![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - Compras Parque D Pedro
Última atualização: 02/02/2020 <br />
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
- [Lista de Produtos](#lista-de-produtos)
- [PDP](#pdp)
- [Sacola Modal](#sacola-modal)
- [Checkout](#checkout)
- [Enhanced E-commerce](#enhanced-e-commerce)




## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referentes ao ambiente de [https://compras.parquedpedro.com.br/](https://compras.parquedpedro.com.br/).

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
	        'dimension4': '[[Nome Loja]]',
                'dimension5': '[[Localização]]',
                'dimension6': '[[[Device ID]]'
	
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[User ID]]			| '1234656'			    | ID definido após o cadastro e login										|
| [[GA ClientID]]	| 'XXXXXXXXXX:XXXX:XX'	| ID aleatório do Google Analytics										|
| [[GTM-ID]]			| 'GTM-TK8RPDC'		| ID do container do GTM instalado no ambiente										|
| [[Nome Loja]] | 'concept', 'marisa' e etc | Deve retornar o nome da loja  |
| [[Localização]] | 'capao-redondo', 'morumbi', 'santa-cruz' e etc. | Deve retornar a localização  |
| [[Device ID]]   | 'XXXXXXX' | Deve retornar o ID do dispositivo utilizado   |

---

### Geral

**Quando: Ao clicar em um dos elementos do header.**<br />

- **Onde:** Em todas as páginas do site em que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:geral',
    'eventAction': 'clique:header',
    'eventLabel': '[[nome-item]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-item]] | 'logo', 'favoritos', 'login' ou 'sacola' | Retornar o nome do item clicado.   |


<br />

**Quando: No clique dos links do footer**<br />

- **Onde:** Em todas as páginas do site em que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:geral',
    'eventAction': 'clique:footer',
    'eventLabel': '[[secao]]:[[nome-item]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[secao]] | 'o-shopping', 'politicas' e etc | Deve retornar o nome da seção.   |
| [[nome-item]] | 'sobre-o-shopping', 'filmes' e etc | Retornar o nome do item clicado.   |


<br />

**Quando: No clique dos itens do menu superior.**<br />

- **Onde:** Em todas as páginas do site em que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:geral',
    'eventAction': 'clique:menu',
    'eventLabel': '[[item-menu]]:[[secao]]:[[item-submenu]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[item-menu]] | 'moda-feminina', 'moda-masculina', 'joias-e-relogios' e etc. | Deve retornar o nome do item clicado no menu.   |
| [[secao]] | 'calcados', 'joias' , 'roupas' e etc. | Deve retornar, se existente, a seção do menu clicada.    |
| [[item-submenu]] | 'tenis', 'lingeries', 'aneis' e etc. | Deve retornar, se existente, o nome do item clicado no submenu.  |


<br />

**Quando: Ao realizar uma busca na barra de pesquisa.**<br />

- **Onde:** Em todas as páginas do site em que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:geral',
    'eventAction': 'interacao:campo:busca',
    'eventLabel': '[[termo-buscado]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[termo-buscado]] | 'toalha-de-banho', 'camiseta-polo', 'cama-mesa-e-banho' e etc. | Deve retornar o termo buscado na barra de pesquisa.    |


<br />

**Quando: Ao clicar em um dos termos sugeridos na busca.**<br />

- **Onde:** Em todas as páginas do site em que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:geral',
    'eventAction': 'clique:termos:busca',
    'eventLabel': '[[termo-sugerido]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[termo-sugerido]] |  'toalha-de-banho', 'camiseta-polo', 'cama-mesa-e-banho' e etc. | Deve retornar o termo sugerido clicado.   |


<br />

**Quando: No clique para adicionar aos favoritos**<br />

- **Onde:** Em todas as páginas do site em que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:geral',
    'eventAction': 'clique:icone',
    'eventLabel': 'favoritar:[[nome-produto]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'tenis-era-save-our-planet-branco-e-preto' e etc | Deve retornar o nome do produto.  |


<br />

### Bem vindo

**Quando: No clique dos botões ou links**<br />

- **Onde:** Na página "Bem vindo"

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:bem-vindo',
    'eventAction': 'clique:[[botao ou link]]',
    'eventLabel': '[[nome-item]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
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
    'eventCategory': 'compras-parque-d-pedro:cadastro',
    'eventAction': 'interacao:campo',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] |  'nome', 'email', 'bairro' e etc | Deve retornar o nome do campo preenchido.  |


<br />

**Quando: Na interação com o checkbox.**<br />

- **Onde:** Na página de cadastro.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:cadastro',
    'eventAction': 'interacao:checkbox',
    'eventLabel': '[[acao]]:autorizo-o-uso-dos-meus-dados'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[acao]] |  'check', 'uncheck' | Deve retornar a ação do usuário.  |



<br />

**Quando: No clique dos botões**<br />

- **Onde:** Na página de cadastro.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:cadastro',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] |  'enviar-codigo-de-verificacao', 'criar', 'cancelar' | Deve retornar o nome do botão clicado.   |


<br />

**Quando: Na tentativa de callback para efetuar o cadastro**<br />

- **Onde:** Na página de cadastro.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'compras-parque-d-pedro:cadastro',
    'eventAction': 'callback',
    'eventLabel': '[[status]]',
    'dimension1': '[[User ID]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
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
    'eventCategory': 'compras-parque-d-pedro:login',
    'eventAction': 'interacao:campo',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] |   'email', 'senha' | Deve retornar o nome do campo preenchido.   |


<br />

**Quando: No clique dos botões**<br />

- **Onde:** Na página de login.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:login',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] |  'entrar', 'cancelar' | Deve retornar o nome do botão clicado.   |


<br />

**Quando: Na tentativa de callback para efetuar o login**<br />

- **Onde:** Na página de login.

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'login',
    'eventCategory': 'compras-parque-d-pedro:login',
    'eventAction': 'callback',
    'eventLabel': '[[status]]',
    'dimension1': '[[User ID]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
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
    'eventCategory': 'compras-parque-d-pedro:esqueci-minha-senha',
    'eventAction': 'interacao:campo',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] |   'email', 'codigo-de-verificacao' | Deve retornar o nome do campo preenchido.   |


<br />

**Quando: No clique dos botões**<br />

- **Onde:** Na página "Esqueci minha senha"

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:esqueci-minha-senha',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] |  'enviar-codigo-de-verificacao', 'continuar', 'cancelar' e etc | Deve retornar o nome do botão clicado.   |


<br />

**Quando: Na tentativa de callback para cadastrar a nova senha**<br />

- **Onde:** Na página "Esqueci minha senha".

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:esqueci-minha-senha',
    'eventAction': 'callback',
    'eventLabel': '[[status]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]] | 'sucesso', 'erro:nao-encontramos-sua-conta' e etc | Deve retornar a mensagem de sucesso ou o tipo de erro. |


<br />

### Lista de Produtos

**Quando: Ao selecionar um dos checkboxes de filtro.**<br />

- **Onde:** Na página de lista de produtos.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:lista-de-produtos',
    'eventAction': 'interacao:checkbox:filtro',
    'eventLabel': '[[secao]]:[[nome-filtro]]:[[acao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'categoria', 'marca', 'cor' e etc. | Deve retornar o nome da seção do filtro.  |
| [[nome-filtro]] | 'branco', 'lacoste', 'infantil' e etc. | Deve retornar o nome do checkbox de filtro clicado.  |
| [[acao]] | 'check' ou 'uncheck' | Deve retornar se o usuário marcou ou desmarcou o checkbox.  |


<br />

**Quando: Ao clicar em uma das sugestões de consulta.**<br />

- **Onde:** Na página de lista de produtos.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:lista-de-produtos',
    'eventAction': 'clique:sugestao',
    'eventLabel': '[[consulta-sugerida]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[consulta-sugerida]] | 'camisa-feminina', 'toalha-de-banho' e etc. | Deve retornar o nome do termo de consulta clicado.  |


<br />

### PDP

**Quando: No clique para selecionar a cor do produto.**<br />

- **Onde:** Na página do produto
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:pdp',
    'eventAction': 'clique:cor',
    'eventLabel': '[[nome-cor]]:[[nome-produto]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-cor]] | 'branco', 'preto', 'azul' e etc | Deve retornar a cor selecionada. |
| [[nome-produto]] | 'tenis-era-save-our-planet-branco-e-preto' e etc | Deve retornar o nome do produto. |



<br />

**Quando: No clique para selecionar o tamanho do produto**<br />

- **Onde:** Na página do produto
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:pdp',
    'eventAction': 'clique:tamanho',
    'eventLabel': '[[tamanho-selecionado]]:[[nome-produto]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[tamanho-selecionado]] | '35', '40', '41'  e etc | Deve retornar o tamanho selecionado. |
| [[nome-produto]] | 'tenis-era-save-our-planet-branco-e-preto' e etc | Deve retornar o nome do produto. |



<br />

**Quando: No clique para selecionar a quantidade do produto**<br />

- **Onde:** Na página do produto
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:pdp',
    'eventAction': 'interacao:quantidade',
    'eventLabel': '[[quantidade-escolhida]]:[[nome-produto]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[quantidade-escolhida]] | '1', '3', '4' e etc | Deve retornar a quantidade escolhida. |
| [[nome-produto]] | 'tenis-era-save-our-planet-branco-e-preto' e etc | Deve retornar o nome do produto. |



<br />

**Quando: No clique dos botões ou links**<br />

- **Onde:** Na página do produto
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:pdp',
    'eventAction': 'clique:[[botao ou link]]',
    'eventLabel': '[[nome-item]]:[[nome-produto]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[botao ou link]] | 'botao' ou 'link' | Deve retornar o tipo de elemento clicado. |
| [[nome-item]] | 'adicionar-a-sacola', 'favorita' e etc | Deve retornar o nome do botao ou link clicado. |
| [[nome-produto]] | 'tenis-era-save-our-planet-branco-e-preto' e etc | Deve retornar o nome do produto. |



<br />

### Sacola Modal

**Quando: No clique dos botões ou links**<br />

- **Onde:** Na página do modal da sacola
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:sacola-modal',
    'eventAction': 'clique:[[botao ou link]]',
    'eventLabel': '[[nome-item]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[botao ou link]] | 'botao' ou 'link' | Deve retornar o tipo de elemento clicado. |
| [[nome-item]] |  'continuar-comprando', 'finalizar-compra', 'fechar' e etc | Deve retornar o nome do botao ou link clicado. |



<br />

**Quando: No clique para selecionar a quantidade do produto**<br />

- **Onde:** Na página do modal da sacola
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:sacola-modal',
    'eventAction': 'interacao:quantidade',
    'eventLabel': '[[quantidade-escolhida]]:[[nome-produto]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[quantidade-escolhida]] |  '1', '3', '4' e etc | Deve retornar a quantidade escolhida. |
| [[nome-produto]] | 'tenis-era-save-our-planet-branco-e-preto' e etc | Deve retornar o nome do produto. |



<br />

### Checkout

**Quando: No clique dos botões das etapas do checkout**<br />

- **Onde:** Em todas as etapas do checkout que estiver disponível
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:checkout',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]:[[step]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] |  'fechar-pedido', 'escolher-mais-produtos' e etc | Deve retornar o nome do botão clicado. |
| [[step]] |  'carrinho', 'entrega', 'pagamento' | Deve retornar o nome da etapa do checkout. |


<br />

**Quando: No clique para selecionar a quantidade do produto**<br />

- **Onde:** Na etapa do carrinho
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:checkout',
    'eventAction': 'interacao:quantidade',
    'eventLabel': '[[quantidade-escolhida]]:[[nome-produto]]:carrinho'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[quantidade-escolhida]] |   '1', '3', '4' e etc | Deve retornar a quantidade escolhida. |
| [[nome-produto]] | 'tenis-era-save-our-planet-branco-e-preto' e etc | Deve retornar o nome do produto. |


<br />

**Quando: Na interação com o campos de cada etapa do checkout**<br />

- **Onde:** Em todas as etapas do checkout que estiver disponível
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'interacao:campo',
    'eventAction': 'interacao:quantidade',
    'eventLabel': 'preencheu:[[nome-campo]]:[[step]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] |  'cupom-de-desconto', 'cep, 'cartao-de-credito' | Deve retornar o nome do campo preenchido. |
| [[step]] | 'carrinho', 'entrega', 'pagamento' | Deve retornar o nome da etapa do checkout. |


<br />


### Enhanced E-commerce

**Na visualização de algum banner**<br />

- **Onde:** Em todas as páginas que estiver disponivel. 
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'promotionImpression',
    'eventCategory': 'compras-parque-d-pedro:enhanced-ecommerce',
    'eventAction': 'promotionImpression',
'noInteraction': '1',
'ecommerce': {
    'promoView': {
      'promotions': [{
        'id': '[[promotion-id]]',
        'name': '[[nome-promocao]]',
        'position': '[[posicao-promocao]]'
      }]
    }
  }
  });
</script>
```



| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[promotion-id]] |'banner123' e etc | ID único do Banner |
| [[nome-promocao]] | 'polos-diferenciadas' | Deve retornar o nome amigável do banner |
| [[posicao-promocao]] | '1' e etc | Deve retornar a posição que o banner é exibido  |

<br />


**No clique dos banners**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'promotionClick',
  'eventCategory': 'compras-parque-d-pedro:enhanced-ecommerce',
  'eventAction': 'promotionClick',
    'ecommerce': {
    'promoClick': {
      'promotions': [{
        'id': '[[promotion-id]]',
        'name': '[[nome-promocao]]',
        'position': '[[posicao-promocao]]',
        'creative': '[[arte-banner]]'
      }]
    }
  }
});
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[promotion-id]] |'banner123' e etc | ID único do Banner |
| [[nome-promocao]] | 'polos-diferenciadas' | Deve retornar o nome amigável do banner |
| [[posicao-promocao]] | '1' e etc | Deve retornar a posição que o banner é exibido  |

<br />


**Na visualização de uma vitrine de produtos**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'productImpression',
  'eventCategory':'compras-parque-d-pedro:enhanced-ecommerce',
  'eventAction': 'productImpression',
  'noInteraction': '1',
  'ecommerce': {
    'impressions': [{
        'name': '[[nome-produto]]',
        'id': '[[id-produto]]',
        'price':' [[preco-produto]]',
        'category': '[[categoria-produto]]',
        'brand': '[[marca-produto]]',
        'list': '[[lista-produto]]',
        'position': '[[posicao-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[categoria-produto]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[marca-produto]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[lista-produto]] | 'moda-masculina' e etc' | Nome da lista que o produto aparece |
| [[posicao-produto]] | '2' | Posição que o produto aparece em uma lista de produtos |

<br />


**No clique de algum produto**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
    'event': 'productClick',
    'eventCategory': 'compras-parque-d-pedro:enhanced-ecommerce',
    'eventAction': 'productClick',
        'ecommerce': {
        'click': {
            'actionField': {'list': '[[lista-produto]]'},
             'products': [{
               'name': '[[nome-produto]]',
               'id': '[[id-produto]]',
               'price':' [[preco-produto]]',
               'category': '[[categoria-produto]]',
               'brand': '[[marca-produto]]',
               'list': '[[lista-produto]]',
               'position': '[[posicao-produto]]',
               'coupon': '[[cupom-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[categoria-produto]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[marca-produto]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[lista-produto]] | 'moda-masculina' e etc' | Nome da lista que o produto aparece |
| [[posicao-produto]] | '2' | Posição que o produto aparece em uma lista de produtos |
| [[cupom-produto]] | '25%' e etc' | Desconto do produto |

<br />

**Na visualização da página de detalhes do produto**<br />

- **Onde:** Na página de detalhe do produto
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'productDetail',
  'eventCategory': 'compras-parque-d-pedro:enhanced-ecommerce',
  'eventAction': 'productDetail',
  'noInteraction': '1',
  'ecommerce': {
    'detail': {
      'products': [{
        'name': '[[nome-produto]]',
        'id': '[[id-produto]]',
        'price':' [[preco-produto]]',
        'category': '[[categoria-produto]]',
        'brand': '[[marca-produto]]',
        'variant': '[[tamanho-produto]]',
        'coupon': '[[cupom-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[categoria-produto]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[marca-produto]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[tamanho-produto]] | 'm' | Tamanho do produto |
| [[cupom-produto]] | '25%' e etc' | Desconto do produto |

<br />


**Ao adicionar um produto ao carrinho**<br />

- **Onde:** Em todas as páginas que estiver disponivel
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'addToCart',
  'eventCategory':'compras-parque-d-pedro:enhanced-ecommerce',
  'eventAction': 'addToCart',
    'ecommerce': {
    'add': {
      'products': [{
        'name': '[[nome-produto]]',
        'id': '[[id-produto]]',
        'price':' [[preco-produto]]',
        'category': '[[categoria-produto]]',
        'variant': '[[tamanho-produto]]',
        'brand': '[[marca-produto]]',
        'quantity': '[[quantidade-produto]]',
        'coupon': '[[cupom-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[categoria-produto]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[tamanho-produto]] | 'm' | Tamanho do produto |
| [[marca-produto]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |
| [[cupom-produto]] | '25%' e etc' | Desconto do produto |


<br />


**Ao remover um produto do carrinho**<br />

- **Onde:** Na página da Sacola;
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'removeFromCart',
  'eventCategory': 'compras-parque-d-pedro:enhanced-ecommerce',
  'eventAction': 'removeFromCart',
    'ecommerce': {
    'remove': {
      'products': [{
        'name': '[[nome-produto]]',
        'id': '[[id-produto]]',
        'price':' [[preco-produto]]',
        'category': '[[categoria-produto]]',
        'variant': '[[tamanho-produto]]',
        'brand': '[[marca-produto]]',
        'quantity': '[[quantidade-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[categoria-produto]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[tamanho-produto]] | 'm' | Tamanho do produto |
| [[marca-produto]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |


<br />

**No carregamento das etapas do checkout**<br />

- **Onde:** Na página do checkout
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'checkout',
  'eventCategory': 'compras-parque-d-pedro:enhanced-ecommerce',
  'eventAction': 'checkout',
  'noInteraction': '1',
  'ecommerce': {
    'checkout': {
      'actionField': {'step': '[[checkout-index]]'},
      'products': [{
        'name': '[[nome-produto]]',
        'id': '[[id-produto]]',
        'price':' [[preco-produto]]',
        'category': '[[categoria-produto]]',
        'variant': '[[tamanho-produto]]',
        'brand': '[[marca-produto]]',
        'quantity': '[[quantidade-produto]]',
        'coupon': '[[cupom-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[checkout-index]] | '1-carrinho', '2-entrega', '3-pagamento'| Retornar de acordo com a página que o usuário está. |
| [[nome-produto]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[categoria-produto]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[tamanho-produto]] | 'm' | Tamanho do produto |
| [[marca-produto]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |
| [[cupom-produto]] | '25%' e etc' | Desconto do produto |


<br />


**Ao selecionar uma opção de entrega**<br />

- **Onde:** Na página de checkout
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'checkoutOption'',
  'eventCategory': 'compras-parque-d-pedro:enhanced-ecommerce',
  'eventAction': 'checkoutOption',
  'ecommerce': {
    'checkout_option': {
      'actionField': {'option': shipping:[[opcao escolhida]]:[[previsao-entrega]]}
{step:2},
    }
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[opcao escolhida]] | 'receber', 'retirar' | Deve retornar os nomes dos tipos de entrega. |
| [[previsao-entrega]] |  'em-ate-4-dias-uteis', 'pompeia-em-ate-2-dias' | Usar essa variável apenas para etapa de entrega. Retorna as informações de forma de entrega. |


<br />


**Ao selecionar uma opção de pagamento**<br />

- **Onde:** Na página de carrinho e de checkout
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'checkoutOption'',
  'eventCategory': 'compras-parque-d-pedro:enhanced-ecommerce',
  'eventAction': 'checkoutOption',
  'ecommerce': {
    'checkout_option': {
      'actionField': {'option': payment:[[opcao escolhida]]}
{step:3},
    }
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[opcao escolhida]] | 'cartao-de-credito', 'boleto' etc | Deve retornar os nomes dos tipos de entrega. |


<br />

**Na finalização da compra**<br />

- **Onde:** Na página de confirmação de compra
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'purchase',
  'eventCategory': 'compras-parque-d-pedro:enhanced-ecommerce',
  'eventAction': 'purchase',
  'noInteraction': '1',
  'ecommerce': {
    'purchase': {
      'actionField': {
        'id': '[[id-transacao]]',
        'revenue': '[[valor-total-transacao]]',
        'shipping': '[[frete-transacao]]',
        'coupon': '[[coupon-transacao]]', 
        'tax': '[[taxa-transacao]]'
      },
      'products': [{
        'name': '[[nome-produto]]',
        'id': '[[id-produto]]',
        'price':' [[preco-produto]]',
        'category': '[[categoria-produto]]',
        'variant': '[[tamanho-produto]]',
        'brand': '[[marca-produto]]',
        'quantity': '[[quantidade-produto]]',
        'coupon': '[[cupom-produto]]'
      }]
    }
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[id-transacao]] |  '000011652' | ID único da transação |
| [[valor-total-transacao]] |  '250.50' | Valor total da transação incluindo frete e taxas |
| [[frete-transacao]] |  '15.98' | Valor do frete da transação |
| [[taxa-transacao]] |  '2.39' | Valor de taxas da transação |
| [[coupon-transacao]] | 'cupom-2020' | Cupom de desconto utilizado na transação - promoção nivel pedido |
| [[nome-produto]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[categoria-produto]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[tamanho-produto]] | 'm' | Tamanho do produto |
| [[marca-produto]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |
| [[cupom-produto]] | '25%' e etc' | Desconto do produto |


<br />

---


> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
