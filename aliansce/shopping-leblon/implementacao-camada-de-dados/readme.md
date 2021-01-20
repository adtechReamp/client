![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - Shopping Leblon
Última atualização: 20/01/2020 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Implementação](#implementa%c3%a7%c3%a3o)
- [Especificações Globais](#especifica%c3%a7%c3%b5es-globais)
- [Dimensões Globais](#dimens&otilde;es-globais)
- [Geral](#geral)
- [Home](#home)
- [Shopping](#shopping)
- [Vitrine de produtos](#vitrine-de-produtos)
- [Compras online](#compras-online)
- [Cinema](#cinema)
- [Lojas](#lojas)
- [Gastronomia](#gastronomia)
- [Eventos](#eventos)
- [Teatro](#teatro)
- [Planeje sua visita](#planeje-sua-visita)
- [Serviços](#servi&ccedil;os)
- [Fale Conosco](#fale-conosco)
- [Solar](#solar)
- [Cadastro](#cadastro)
- [Login](#login)
- [Esqueci minha senha](#esqueci-minha-senha)
- [Área Logada](#&aacute;rea-logada)



## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados e de data attributes para utilização de recursos de monitoramento do Google Analytics referentes ao ambiente de [https://shoppingleblon.com.br/](https://shoppingleblon.com.br/).

<br />

### **Descrição Geral**

O `snippet` do Google Tag Manager é um pequeno trecho de código javascript ou non-javascript, através do uso de um iframe quando o javascript não está disponível, que é inserido nas páginas do site, tornando possível que a configuração das tags sejam realizadas via interface.


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

**Quando: Ao clicar em um dos elementos do Footer.**<br />

- **Onde:** Em todas as páginas do site em que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:geral',
    'eventAction': 'clique:footer',
    'eventLabel': '[[secao]]:[[nome-item]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[secao]] | 'montes-claros-shopping', 'contato' e etc | Deve retornar o nome da seção do footer.   |
| [[nome-item]] | 'lojas', 'facebook' e etc | Deve retornar o nome do item clicado no Footer.   |


<br />

**Quando: Ao clicar em um dos Links do menu lateral.**<br />

- **Onde:** Em todas as páginas do site em que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:geral',
    'eventAction': 'clique:menu',
    'eventLabel': '[[item-menu]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[item-menu]] | 'shopping', 'compre-online', 'lojas' e etc. | Deve retornar o nome do link clicado no menu lateral.  |


<br />

**Quando: Na interação com a busca.**<br />

- **Onde:** Em todas as páginas do site em que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:geral',
    'eventAction': 'interacao:campo:busca',
    'eventLabel': '[[termo-buscado]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[termo-buscado]] | 'ad-studio', 'sorveteria' e etc | Deve retornar o termo buscado.  |


<br />

**Quando: Na tentativa de callback para busca**<br />

- **Onde:** Em todas as páginas do site em que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'shopping-leblon:geral',
    'eventAction': 'callback:busca',
    'eventLabel': '[[status]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]] | 'sucesso', 'erro:nao-foi-possivel-encontrar' e etc | Deve retornar a mensagem de sucesso ou tipo de erro.   |


<br />

### Home

**Quando: No clique do botões dos banners**<br />

- **Onde:** Na página home.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:home',
    'eventAction': 'clique:botao:banner',
    'eventLabel': '[[nome-botao]]:[[nome-banner]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] | 'clique-e-confira', 'clique-para-ver-todas-as-medidas-de-seguranca' | Deve retornar o nome do botão clicado.  |
| [[nome-banner]] | 'compre-online', 'aberto-para-novos-olhares' e etc | Deve retornar o nome do banner.   |


<br />

### Shopping

**Quando: Na interação dos card**<br />

- **Onde:** Na página shopping.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:shopping',
    'eventAction': 'clique:card',
    'eventLabel': '[[nome-card]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-card]] | 'torres-de-escritorio-chopping-leblon', 'responsabilidade-social' e etc | Deve retornar o nome do card clicado. |


<br />

### Vitrine de produtos

**Quando: Na interação com os filtros.**<br />

- **Onde:** Na página de vitrine de produtos.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:vitrine-de-produtos',
    'eventAction': 'interacao:filtro',
    'eventLabel': '[[nome-filtro]]:[[item-filtrado]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-filtro]] |  'categoria', 'lojas', 'todos-os-canais' e etc | Deve retornar o nome do filtro. |
| [[item-filtrado]] | 'infantil', 'adcos' e etc | Deve retornar o nome filtrado.  |


<br />

**Quando: No clique nos cards dos produtos.**<br />

- **Onde:** Na página de vitrine de produtos.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:vitrine-de-produtos',
    'eventAction': 'clique:card',
    'eventLabel': '[[nome-card]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-card]] |  'biquini-infantil-babados', 'coelho-orelhao' e etc | Deve retornar o nome do card clicado.  |


<br />

**Quando: Ao clicar nos botões dentro dos cards**<br />

- **Onde:** Na página de vitrine de produtos.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:vitrine-de-produtos',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]:[[nome-card]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] |  'whatsapp', 'site-da-loja' e etc. | Deve retornar o  nome do botão clicado.  |
| [[nome-card]] |  'biquini-infantil-babados', 'coelho-orelhao' e etc | Deve retornar o nome do card clicado.  |


<br />

**Quando: Ao clicar no Link "ver mais produtos"**<br />

- **Onde:** Na página de vitrine de produtos.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:vitrine-de-produtos',
    'eventAction': 'clique:link',
    'eventLabel': 'ver-mais-produtos'
  });
</script>
```
<br />


### Compras online


**Quando: Na interação com os filtros**<br />

- **Onde:** Nas páginas de Compra Online.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:compre-online',
    'eventAction': 'interacao:filtro',
    'eventLabel': '[[nome-filtro]]:[[item-filtrado]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-filtro]] |  'segmento', 'a-z' e etc | Deve retornar o nome do filtro.  |
| [[item-filtrado]] |  'alimentacao', 'artigos-diversos' e etc | Deve retornar o nome filtrado.  |


<br />

**Quando: Ao clicar nos botões dentro do Card .**<br />

- **Onde:** Nas páginas de Compra Online.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:compre-online',
    'eventAction': 'clique:card',
    'eventLabel': '[[nome-card]]:[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-card]] |  'abreu-turismo', 'ad-studio' e etc | Deve retornar o nome do card clicado.  |
| [[nome-botao]] |  'delivery', 'whatsapp' e etc| Deve retornar o nome do botão clicado. |


<br />

### Cinema

**Quando: Ao clicar nos filmes em cartaz.**<br />

- **Onde:** Na página cinema.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:cinema',
    'eventAction': 'clique:card',
    'eventLabel': '[[nome-filme]]:[[data]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-filme]] |  'destruicao-final', 'legado-do-filme' e etc  | Deve retornar com o nome do filme. |
| [[data]] |  'ter-12/01', 'quar-13/01' e etc | Deve retornar a data selecionada. |


<br />

**Quando: No clique dos botões ou ícones de cada filme**<br />

- **Onde:** Na página cinema.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:cinema',
    'eventAction': 'clique:[[botao ou icone]]',
    'eventLabel': '[[nome-item]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[botao ou icone]] |  'botao' ou 'icone'   | Deve retornar o tipo de elemento clicado. |
| [[nome-item]] |  'trailer', 'horario-e-detalhes', 'comprar' e etc | Deve retornar o nome do botão ou icone clicado. |


<br />

**Quando: No clique dos botões do modal "horarios e detalhes"**<br />

- **Onde:** Na página cinema.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:cinema',
    'eventAction': 'clique:botao:modal-horario-e-detalhes',
    'eventLabel': '[[nome-botao]]:[[nome-filme]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] |   'comprar' ou 'fechar' | Deve retornar o nome do botão clicado. |
| [[nome-filme]] |  'destruicao-final', 'legado-do-filme' e etc  | Deve retornar com o nome do filme. |


<br />

### Lojas

**Quando: Na interação com os filtros**<br />

- **Onde:** Nas página Lojas.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:lojas',
    'eventAction': 'interacao:filtro',
    'eventLabel': '[[nome-filtro]]:[[item-filtrado]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-filtro]] |  'segmento', 'a-z' e etc | Deve retornar o nome do filtro. |
| [[item-filtrado]] |  'alimentacao', 'artigos-diversos' e etc  | Deve retornar o nome filtrado. |


<br />

**Quando: Na interação com os filtros**<br />

- **Onde:** Nas página Lojas.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:lojas',
    'eventAction': 'interacao:filtro',
    'eventLabel': '[[nome-filtro]]:[[item-filtrado]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-filtro]] |  'segmento', 'a-z' e etc | Deve retornar o nome do filtro. |
| [[item-filtrado]] |  'alimentacao', 'artigos-diversos' e etc  | Deve retornar o nome filtrado. |


<br />

**Quando: No clique dos cards**<br />

- **Onde:** Nas página Lojas.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:lojas',
    'eventAction': 'clique:card',
    'eventLabel': '[[nome-card]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-card]] |  'abreu', 'abraccio' e etc | Deve retornar o nome do card clicado. |


<br />

### Gastronomia




> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>