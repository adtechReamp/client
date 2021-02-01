![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - Compras Parque D Pedro
Última atualização: 21/01/2020 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Implementação](#implementa%c3%a7%c3%a3o)
- [Especificações Globais](#especifica%c3%a7%c3%b5es-globais)
- [Dimensões Globais](#dimens&otilde;es-globais)
- [Geral](#geral)




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
	        'dimension4': '[[Nome página]],
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
| [[Nome página]] | 'sobre-o-shopping', 'marcas' e etc | Deve retornar o nome da página  |
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
    'eventCategory': 'shopping-leblon:geral',
    'eventAction': 'clique:header',
    'eventLabel': '[[nome-item]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-item]] | 'instagram', 'logo' e etc. | Retornar o nome do item clicado.   |


<br />

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
    'eventLabel': '[[nome-cor]]:[[nome-produto]]',
    'dimension4': '[[Nome Loja]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-cor]] | 'branco', 'preto', 'azul' e etc | Deve retornar a cor selecionada. |
| [[nome-produto]] | 'tenis-era-save-our-planet-branco-e-preto' e etc | Deve retornar o nome do produto. |
| [[Nome Loja]] | 'concept', 'marisa' e etc | Deve retornar o nome da loja |


<br />


> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
