![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Área - Digital Analytics<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - XXXXXX XXXXXXX
Última atualização: XX/XX/XXXX <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados e de data attributes para utilização de recursos de monitoramento do Google Analytics referentes ao ambiente de [XXXXX](XXXXX).

<br />

### **Descrição Geral**

O `snippet` do Google Tag Manager é um pequeno trecho de código javascript ou non-javascript, através do uso de um iframe quando o javascript não está disponível, que é inserido nas páginas do site, tornando possível que a configuração das tags sejam realizadas via interface.


### **Posicionamento do Código - Google Tag Manager**

#### 1. Copie o seguinte JavaScript e cole-o o mais próximo da tag `<head>` de abertura possível em todas as páginas do seu site.

```html

<html>
  <head>
    <!-- Google Tag Manager -->
    <script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start': new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0], j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src='https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f); })(window,document,'script','dataLayer','GTM-XXXXXXX');</script>
    <!-- End Google Tag Manager -->
    //...
  </head>
```

#### 2. Copie o seguinte trecho e cole-o imediatamente após a marcação `<body>` de abertura em cada página do seu site.

```html
<body>
  <!-- Google Tag Manager (noscript) -->
  <noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-XXXXXXX" height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
  <!-- End Google Tag Manager (noscript) -->
  //...
  </body>
</html>
```

Link de referência: [Documentação Oficial Google Tag Manager](https://developers.google.com/tag-manager/quickstart)


## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />

> Caso o site já possua o Google Analytics instalado, será necessário a remoção do código de **todas as páginas do site**: <br />

```html

<script>
(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o), m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)})(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

ga('create', 'UA-XXXXXXXX-X', 'auto');
ga('send', 'pageview');
</script>

```

---

```html

<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=UA-XXXXXXX-X"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'UA-XXXXXXX-X');
</script>
```

---

## Overview e Descrições Técnicas

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

### Atributos HTML (Data Attributes)

> São atributos customizados inseridos nos elementos HTML da página, permitindo a inclusão de dados adicionais.

**Instalação**
1. Elementos: ```<div>Elemento</div>``` <br />
Todos os elementos do html que serão clicados, deverão ser mapeados recebendo os atributos com sua estrutura no item.

```html
<div 	
    data-gtm-event-category="[[exemplo:valor-categoria]]"
 	data-gtm-event-action="[[exemplo:valor-acao]]"
 	data-gtm-event-label="[[exemplo:valor-rotulo]]"
 >
</div>
```

#### Importante:
> Também devem ter os data-attributes `data-gtm-event-category`, `data-gtm-event-action` e `data-gtm-event-label`. Preenchidos conforme instruções específicas.

<br />

## Implementação


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
		'dimension1': '[[User ID]]'
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[User ID]]			| 'exemplo'				| Descrição										|

---

### Especificação de Micro-conversões:


**Item #1 - Tagbook:**<br />

- **Onde:** Descrição 1;
- **Quando:** Descrição 1;
- **Título ou nome do botão/link:** "Exemplo Link".

```html
<!-- Use se os atributos no elemento a ser clicado -->
<div
     data-gtm-event-category="" 
     data-gtm-event-action="" 
     data-gtm-event-label=""
>
Botão
</div>
```

| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[Váriavel]]			| 'exemplo'				| Descrição										|

<br />

**Cadastro Newsletter - Sucesso ou erro:**<br />

- **Onde:** No Callback do envio do e-mail de cadastro para receber newsletter.

```html
<script>
	dataLayer.push({
		'event': 'event',
		'eventCategory': '',
		'eventAction': '',
		'eventLabel': ''
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[Váriavel]]			| 'exemplo'				| Descrição										|

<br />

### Enhanced Ecommerce

**Na visualização de algum banner**<br />

- **Onde:** Em todas as páginas que estiver disponivel. 
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'promoView',
    'eventCategory': 'projeto:enhanced-ecommerce',
    'eventAction': 'promotionImpression',
'noInteraction': '1',
'ecommerce': {
    'promoView': {
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
| [[nome-promocao]] | 'maravilhoso-natal' e etc | Deve retornar o nome amigável do banner |
| [[arte-banner]] | 'www.exemplo.com' | URL do banner  |
| [[posicao-promocao]] | '1' e etc | Deve retornar a posição que o banner é exibido  |

<br />


**No clique dos banners**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'promoClick',
  'eventCategory': 'projeto:enhanced-ecommerce',
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
| [[nome-promocao]] | 'maravilhoso-natal' e etc | Deve retornar o nome amigável do banner |
| [[arte-banner]] | 'www.exemplo.com' | URL do banner  |
| [[posicao-promocao]] | '1' e etc | Deve retornar a posição que o banner é exibido  |


<br />


**Na visualização de uma vitrine de produtos**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'impressions',
  'eventCategory':'projeto:enhanced-ecommerce',
  'eventAction': 'productImpression',
  'noInteraction': '1',
  'ecommerce': {
    'impressions': [{
        'name': '[[nome-produto]]',
        'id': '[[id-produto]]',
        'list': '[[lista-produto]]',
        'variant': '[[variacao-produto]]',
        'position': '[[posicao-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'calca-masculina-super-skinny-em-jeans' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[lista-produto]] | 'calcas-jeans' | Nome da lista que o produto aparece |
| [[posicao-produto]] | '2' | Posição que o produto aparece em uma lista de produtos |
| [[variacao-produto]] | 'm' | Tamanho do produto |

<br />


**No clique de algum produto**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
    'event': 'click',
    'eventCategory': 'projeto:enhanced-ecommerce',
    'eventAction': 'productClick',
        'ecommerce': {
        'click': {
            'actionField': {'list': '[[lista-produto]]'},
            'products': [{
                'name': '[[nome-produto]]',
                'id': '[[id-produto]]',
                'price': '[[preco-produto]]',
                'brand': '[[marca-produto]]',
                'category': '[[categoria-produto]]',
                'position': '[[posicao-produto]]'
            }]
        }
    }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[lista-produto]] | 'calcas-jeans'| Nome da lista que o produto aparece|
| [[nome-produto]] | 'calca-masculina-super-skinny-em-jeans' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[marca-produto]] | 'samsumg' | Marca do produto |
| [[categoria-produto]] | 'masculino' | Categoria do produto |
| [[posicao-produto]] | '2' | Posição que o produto aparece em uma lista de produtos |

<br />


**Na visualização da página de detalhes do produto**<br />

- **Onde:** Na página de detalhe do produto
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'productDetail',
  'eventCategory': 'projeto:enhanced-ecommerce',
  'eventAction': 'productDetail',
  'noInteraction': '1',
  'ecommerce': {
    'detail': {
      'products': [{
        'name': '[[nome-produto]]',
        'id': '[[id-produto]]',
        'price': '[[preco-produto]]',
        'category': '[[categoria-produto]]',
        'variant': '[[variacao-produto]]',
      }]
    }
  }
 });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'calca-masculina-super-skinny-em-jeans' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[categoria-produto]] | 'masculino' | Categoria do produto |
| [[variacao-produto]] | 'm' | Tamanho do produto |

<br />


**Ao adicionar um produto ao carrinho**<br />

- **Onde:** Em todas as páginas que estiver disponivel
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'addToCart',
  'eventCategory':'projeto:enhanced-ecommerce',
  'eventAction': 'addToCart',
    'ecommerce': {
    'add': {
      'products': [{
        'name': '[[nome-produto]]',
        'id': '[[id-produto]]',
        'price': '[[preco-produto]]',
        'brand': '[[marca-produto]]',
        'category': '[[categoria-produto]]',
        'variant': '[[variacao-produto]]',
        'quantity': '[[quantidade-produto]]'
      }]
    }
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'calca-masculina-super-skinny-em-jeans' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[marca-produto]] | 'samsumg' | Marca do produto |
| [[categoria-produto]] | 'masculino' | Categoria do produto |
| [[variacao-produto]] | 'm' | Tamanho do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |

<br />


**Ao remover um produto do carrinho**<br />

- **Onde:** Na página da Sacola;
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'removeFromCart',
  'eventCategory': 'projeto:enhanced-ecommerce',
  'eventAction': 'removeFromCart',
    'ecommerce': {
    'remove': {
      'products': [{
        'name': '[[nome-produto]]',
        'id': '[[id-produto]]',
        'price': '[[preco-produto]]',
        'brand': '[[marca-produto]]',
        'category': '[[categoria-produto]]',
        'variant': '[[variacao-produto]]',
        'quantity': '[[quantidade-produto]]'
      }]
    }
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'calca-masculina-super-skinny-em-jeans' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[marca-produto]] | 'samsumg' | Marca do produto |
| [[categoria-produto]] | 'masculino' | Categoria do produto |
| [[variacao-produto]] | 'm' | Tamanho do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |

<br />


**No carregamento das etapas do checkout**<br />

- **Onde:** Na página do checkout
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'checkout',
  'eventCategory': 'projeto:enhanced-ecommerce',
  'eventAction': 'checkout',
  'noInteraction': '1',
  'ecommerce': {
    'checkout': {
      'actionField': {'step': '[[checkout-index]]'},
      'products': [{
        'name': '[[nome-produto]]',
        'id': '[[id-produto]]',
        'price': '[[preco-produto]]',
        'brand': '[[marca-produto]]',
        'category': '[[categoria-produto]]',
        'variant': '[[variacao-produto]]',
        'quantity': '[[quantidade-produto]]'
      }]
    }
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[checkout-index]] | '1-carrinho' | Página de carrinho de compras |
| [[checkout-index]] | '2-entrega' | Página de confirmação do endereço de entrega |
| [[checkout-index]] | '3-pagamento' | Página de seleção do método de pagamento |
| [[nome-produto]] | 'calca-masculina-super-skinny-em-jeans' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[marca-produto]] | 'samsumg' | Marca do produto |
| [[categoria-produto]] | 'masculino' | Categoria do produto |
| [[variacao-produto]] | 'm' | Tamanho do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |

<br />


**Ao selecionar uma opção de frete**<br />

- **Onde:** Na página de checkout
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'checkoutOption'',
  'eventCategory': 'enhanced-ecommerce',
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
  'eventCategory': 'enhanced-ecommerce',
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
  'eventCategory': 'projeto:enhanced-ecommerce',
  'eventAction': 'purchase',
  'noInteraction': '1',
  'ecommerce': {
    'purchase': {
      'actionField': {
        'id': '[[id-transacao]]',
        'revenue': '[[valor-total-transacao]]',
        'shipping': '[[frete-transacao]]'
        'tax': '[[taxa-transacao]]'
        'coupon': '[[coupon-transacao]]'
      },
      'products': [{
        'name': '[[nome-produto]]',
        'id': '[[id-produto]]',
        'price': '[[preco-produto]]',
        'brand': '[[marca-produto]]',
        'category': '[[categoria-produto]]',
        'variant': '[[variacao-produto]]',
        'quantity': '[[quantidade-produto]]'
      }]
    }
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[id-transacao]] |  '000011652' | ID único da transação |
| [[valor-total-transacao]] |  '139,99' | Valor total da transação incluindo frete e taxas |
| [[frete-transacao]] |  '0.00' | Valor do frete da transação |
| [[taxa-transacao]] |  '0.00' | Valor de taxas da transação |
| [[coupon-transacao]] | 'cupom-2018' | Cupom de desconto utilizado na transação - promoção nivel pedido |
| [[nome-produto]] | 'calca-masculina-super-skinny-em-jeans' | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | '139.99' | Preço do produto |
| [[marca-produto]] | 'samsumg' | Marca do produto |
| [[categoria-produto]] | 'masculino' | Categoria do produto |
| [[variacao-produto]] | 'm' | Tamanho do produto |
| [[quantidade-produto]] | '1' | Quantidade do produto |

<br />

---

> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>

