![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - Compras Parque D Pedro - Linx
Última atualização: 30/04/2020 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Implementação](#implementa%c3%a7%c3%a3o)
- [Especificações Globais](#especifica%c3%a7%c3%b5es-globais)
- [Geral](#geral)
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

---


### Geral

**Quando: Ao clicar em uma das lojas.**<br />

- **Onde:** Na página 'lojas'.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:lojas',
    'eventAction': 'clique:loja',
    'eventLabel': '[[nome-loja]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-loja]] | 'grand-cru', 'alphabeto' e etc | Retornar o nome da loja clicada.   |


<br />

**Quando: Ao clicar em 'ganhar desconto'**<br />

- **Onde:** No modal de cadastro na página home.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:home',
    'eventAction': 'clique:botao',
    'eventLabel': 'ganhar-desconto'
  });
</script>
```


<br />

**Quando: Ao clicar em 'enviar'.**<br />

- **Onde:** No modal de cadastro nas páginas de categoria.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'compras-parque-d-pedro:categorias',
    'eventAction': 'clique:botao',
    'eventLabel': 'enviar'
  });
</script>
```


<br />

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
| [[secao]] | 'categoria', 'marca', 'cor' e etc. | Deve retornar o nome da seção do filtro.    |
| [[nome-filtro]] | 'branco', 'lacoste', 'infantil' e etc. | Deve retornar o nome do checkbox de filtro clicado.    |
| [[acao]] | 'check' ou 'uncheck' | Deve retornar se o usuário marcou ou desmarcou o checkbox.    |


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
| [[consulta-sugerida]] |  'camisa-feminina', 'toalha-de-banho' | Deve retornar o nome do termo de consulta clicado.   |

<br />


### Enhanced E-commerce
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


---


> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
