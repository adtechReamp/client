![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)
teste
> Adtech<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - Kimberly Clark
Última atualização: 04/12/2020 <br />
Em caso de dúvidas, entrar em contato com: [paulo.benachio@reamp.com.br](paulo.beneachio@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Implementação](#implementa%c3%a7%c3%a3o)
- [Especificações Globais](#especifica%c3%a7%c3%b5es-globais)
- [Dimensões Globais](#dimens&otilde;es-globais)
- [General](#general)
- [Login](#login)
- [Register](#register)
- [Home](#home)
- [Product Page](#product-page)
- [Enhanced E-commerce](#enhanced-e-commerce)

## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados e de data attributes para utilização de recursos de monitoramento do Google Analytics referentes ao ambiente de [https://xd.adobe.com/view/08130346-1762-4140-82d9-e661feaa6798-5d40/screen/7d36a398-6a5b-4dba-96ff-50d4e58f0dbf/](https://xd.adobe.com/view/08130346-1762-4140-82d9-e661feaa6798-5d40/screen/7d36a398-6a5b-4dba-96ff-50d4e58f0dbf/).

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

## Implementação

### Camada de dados (DataLayer)

> É um array de objetos javascript utilizado pelo Google Tag Manager para receber em seus atributos, dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação.

**Instalação**<br />
Inserir a camada de dados antes do snippet de instalação do Google Tag Manager. Exemplo:

```html
<script>
	window.dataLayer = window.dataLayer || [];
	window.dataLayer = [{
		'atributo1': '[[valor1]]',
		'atributo2': '[[valor2]]'
	}];
</script>
```

OU

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
		'dimension3': '[[GTM-ID]]'
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[User ID]]			| '1234656'			    | ID único de usuário defeinido após o cadastro										|
| [[GA ClientID]]		| 'XXXXXXXXXX:XXXX:XX'	| ID aleatório do Google Analytics										|
| [[GTM-ID]]			| 'GTM-XXXXXX:XX'		| ID do container do GTM instalado no ambiente										|

---

### General

**When: On clicking the header itens.**<br />

- **Onde:** Where: On all pages where it's available.
    
```html
<div
   data-gtm-event-category='fem:general'
   data-gtm-event-action='click:header'
   data-gtm-event-label='[[header-item]]'
>Botão</div>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[header-item]] | 'logo', 'idioma', 'perfil', 'menu'. | It should return the name of the header item clicked. |

<br />


**When: On clicking the footer itens.**<br />

- **Onde:** Where: On all pages where it's available.
    
```html
<div
   data-gtm-event-category='fem:general'
   data-gtm-event-action='click:footer'
   data-gtm-event-label='[[footer-item]]'
>Botão</div>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[footer-item]] | 'logo', 'idioma', 'fale-com-a-gente', 'termos-e-condicoes' and etc. | It should return the name of the footer item clicked. |

<br />


**When: On selecting an item from the bars menu.**<br />

- **Onde:** Where: On all pages where it's available.
    
```html
<div
   data-gtm-event-category='fem:general'
   data-gtm-event-action='click:menu'
   data-gtm-event-label='[[menu-item]]'
>Botão</div>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[menu-item]] |  'cuidado-diario', 'produtos', 'destaques' and etc. | It should return the name of the menu item clicked. |

<br />


**When: On selecting a language from the language menu.**<br />

- **Onde:** Where: On all pages where it's available.
    
```html
<div
   data-gtm-event-category='fem:general'
   data-gtm-event-action='click:language'
   data-gtm-event-label='[[language-name]]'
>Botão</div>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[language-name]] | 'ingles', 'espanhol', 'portugues' and etc. | It should return the name of the selected language.  |

<br />


**When: On interaction with the filters.**<br />

- **Onde:** Where: On all pages where it's available.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'fem:general',
    'eventAction': 'interaction:filter',
    'eventLabel': '[[filter-name]]'
  });
</script>
```



| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[filter-name]] | 'cuidados-diarios', 'fluxo-normal' and etc. | It should return the name of the selected filter tag.  |

<br />


**When: On clicking the backwards button.**<br />

- **Onde:** Where: On all pages where it's available.
    
```html
<div
   data-gtm-event-category='fem:general'
   data-gtm-event-action='click:button'
   data-gtm-event-label='backwards'
>Botão</div>
```



<br />


**When: On clicking the links in the breadcrumb.**<br />

- **Onde:** Where: On all pages where it's available.
    
```html
<div
   data-gtm-event-category='fem:general'
   data-gtm-event-action='click:breadcrumb'
   data-gtm-event-label='[[breadcrumb-item]]'
>Botão</div>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[breadcrumb-item]] | 'dstaques', 'cuidados-diarios' and etc | It should return the name of the clicked link on the breadcrumb. |

<br />


### Login

**When: On clicking any button or link.**<br />

- **Onde:** Where: On the login page.
    
```html
<div
   data-gtm-event-category='fem:login'
   data-gtm-event-action='click:[[button-or-link]]'
   data-gtm-event-label='[[item-name]]'
>Botão</div>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[button-or-link]] | 'botao' ou 'link' | It should return the type of element clicked. |
| [[item-name]] | 'criar-uma-conta', 'esqueci-a-senha', 'entrar' and etc | It should return the name of the element clicked. |

<br />


**When: On filling the fields of the login form.**<br />

- **Onde:** Where: On the login page.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'fem:login',
    'eventAction': 'filled:field',
    'eventLabel': '[[field-name]]'
  });
</script>
```



| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[field-name]] | 'email', 'senha'  |  It should return the name of the filled field. |

<br />


**When: On the callback of the login attempt.**<br />

- **Onde:** Where: On the login page.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'login',
    'eventCategory': 'fem:login',
    'eventAction': 'send:callback',
    'eventLabel': '[[sucess-or-fail:error-tpe]]'
  });
</script>
```



| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[sucess-or-fail:error-tpe]] |  'sucesso', 'erro:senha-invalida', 'erro:perdeu-conexao' and etc. | It should return the success message or the fail one with the tye of error. |

<br />


### Register

**When: On clicking any button or link.**<br />

- **Onde:** Where: On the register page.
    
```html
<div
   data-gtm-event-category='fem:register'
   data-gtm-event-action='click:[[button-or-link]]'
   data-gtm-event-label='[[item-name]]'
>Botão</div>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[button-or-link]] | 'botao' ou 'link' | It should return the type of element clicked. |
| [[item-name]] | 'ja-possuo-uma-conta', 'registrar' and etc. | It should return the name of the element clicked.  |

<br />


**When: On filling the fields of the login form.**<br />

- **Onde:** Where: On the register page.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'fem:register',
    'eventAction': 'filled:field',
    'eventLabel': '[[field-name]]'
  });
</script>
```



| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[field-name]] | 'nome', 'email', 'senha' |  It should return the name of the filled field.  |

<br />


**On interaction with the checkbox.**<br />

- **Onde:** On the register page.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'fem:register',
    'eventAction': 'interaction:checkbox',
    'eventLabel': '[[checkbox-name]]'
  });
</script>
```



| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[checkbox-name]] | 'li-e-aceito-os-termos' e etc | It should return the name of the interacted checkbox. |

<br />


**Na tentiva de callback para logar**<br />

- **Onde:** On the register page.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'fem:register',
    'eventAction': 'envio:callback',
    'eventLabel': '[[sucess-or-fail:error-tpe]]'
  });
</script>
```



| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[sucess-or-fail:error-tpe]] | 'sucesso', 'erro:senha-invalida', 'erro:perdeu-conexao' and etc. | It should return the success message or the fail one with the tye of error.  |

<br />


### Home

**When: On clicking any link or button of the page.**<br />

- **Onde:** Where: On the homepage.
    
```html
<div
   data-gtm-event-category='fem:home'
   data-gtm-event-action='click:[[button-or-link]]'
   data-gtm-event-label='[[item-name]]'
>Botão</div>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[button-or-link]] | 'botao' ou 'link'   | It should return the type of element clicked. |
| [[item-name]] | 'clique-para-ver-mais', 'encontre-mais-produtos' and etc | It should return the name of the element clicked.  |

<br />


### Product Page

**When: On interaction with the questions.**<br />

- **Onde:** Where: On the product page.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'fem:pdp',
    'eventAction': 'interaction:questions',
    'eventLabel': '[[question-name]]:[[action]]'
  });
</script>
```



| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[question-name]] | 'qual-a-direnca-entre-o-intimus-com-abas-ou-sem-abas' and etc | It should return the name of the question clicked. |
| [[action]] | 'abriu' or 'fechou'. | It should return the name of the action done. |

<br />


**When: On viewing the content section.**<br />

- **Onde:** Where: On the product page.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'fem:pdp',
    'eventAction': 'viewed:section',
'noInteraction': '1',
    'eventLabel': 'content'
  });
</script>
```




<br />


**When: On clicking a content card.**<br />

- **Onde:** Where: On the product page.
    
```html
<div
   data-gtm-event-category='fem:pdp'
   data-gtm-event-action='click:card'
   data-gtm-event-label='[[card-name]]'
>Botão</div>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[card-name]] | 'some-content-card-title' | It should return the name of the card clicked.|

<br />


**When: On clicking the 'ver mais' button on a product.**<br />

- **Onde:** Where: On the product page.
    
```html
<div
   data-gtm-event-category='fem:pdp'
   data-gtm-event-action='click:button'
   data-gtm-event-label='ver-mais:[[product-name]]'
>Botão</div>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[product-name]] | 'intimus-tripla-acao' e etc | Deve retornar o nome do produto. |

<br />


### Enhanced E-commerce

**Na visualização de uma vitrine de produtos**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'productImpressions',
  'eventCategory':'fem:enhanced-ecommerce',
  'eventAction': 'productImpression',
  'noInteraction': '1',
  'ecommerce': {
    'impressions': [{
        'name': '[[nome-produto]]',
        'id': '[[id-produto]]',
        'list': '[[lista-produto]]',
        'price': '[[preco-produto]]',
        'brand': '[[marca-produto]]',
        'category': '[[categoria-produto]]',
        'position': '[[posicao-produto]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-produto]] | 'intimus-tripla-acao'  | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | &quot;139,99&quot; | Preço do produto |
| [[categoria-produto]] | 'absorvente' | Categoria do produto |
| [[marca-produto]] | 'intimus' | Marca do produto |
| [[lista-produto]] | 'tampoes' | Nome da lista que o produto aparece |
| [[posicao-produto]] | '1' | Posição que o produto aparece em uma lista de produtos |

<br />


**No clique de algum produto**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
    'event': 'productClick',
    'eventCategory': 'fem:enhanced-ecommerce',
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
| [[nome-produto]] | 'intimus-tripla-acao'  | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | &quot;139,99&quot; | Preço do produto |
| [[categoria-produto]] | 'absorvente' | Categoria do produto |
| [[marca-produto]] | 'intimus' | Marca do produto |
| [[lista-produto]] | 'tampoes' | Nome da lista que o produto aparece |
| [[posicao-produto]] | '1' | Posição que o produto aparece em uma lista de produtos |

<br />


**Na visualização da página de detalhes do produto**<br />

- **Onde:** Na página de detalhe do produto
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'productDetail',
  'eventCategory': 'fem:enhanced-ecommerce',
  'eventAction': 'productDetail',
  'noInteraction': '1',
  'ecommerce': {
    'detail': {
      'products': [{
        'name': '[[nome-produto]]',
        'id': '[[id-produto]]',
        'price': '[[preco-produto]]',
        'brand': '[[marca-produto]]',
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
| [[nome-produto]] | 'intimus-tripla-acao'  | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | &quot;139,99&quot; | Preço do produto |
| [[categoria-produto]] | 'absorvente' | Categoria do produto |
| [[marca-produto]] | 'intimus' | Marca do produto |
| [[variacao-produto]] | 'com-abas' | Tamanho do produto |

<br />


**Ao adicionar um produto ao carrinho**<br />

- **Onde:** Em todas as páginas que estiver disponivel
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'addToCart',
  'eventCategory':'fem:enhanced-ecommerce',
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
| [[nome-produto]] | 'intimus-tripla-acao'  | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | &quot;139,99&quot; | Preço do produto |
| [[categoria-produto]] | 'absorvente' | Categoria do produto |
| [[variacao-produto]] | 'com-abas' | Tamanho do produto |
| [[marca-produto]] | 'intimus' | Marca do produto |
| [[quantidade-produto]] | '2' | Quantidade do produto |

<br />


**Ao remover um produto do carrinho**<br />

- **Onde:** Na página da sacola
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'removeFromCart',
  'eventCategory': 'fem:enhanced-ecommerce',
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
| [[nome-produto]] | 'intimus-tripla-acao'  | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | &quot;139,99&quot; | Preço do produto |
| [[categoria-produto]] | 'absorvente' | Categoria do produto |
| [[variacao-produto]] | 'com-abas' | Tamanho do produto |
| [[marca-produto]] | 'intimus' | Marca do produto |
| [[quantidade-produto]] | '2' | Quantidade do produto |

<br />


**No carregamento das etapas do checkout**<br />

- **Onde:** Na página do checkout
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'checkout',
  'eventCategory': 'fem:enhanced-ecommerce',
  'eventAction': 'checkout',
  'noInteraction': '1',
  'ecommerce': {
    'checkout': {
      'actionField': {'step': '[[passo-checkout]]'},
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
| [[checkout-index]] |  | Retornar &quot;1&quot; ou &quot;2&quot; ou &quot;3&quot; de acordo com a página que o usuário está.  |
| [[nome-produto]] | 'intimus-tripla-acao'  | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | &quot;139,99&quot; | Preço do produto |
| [[categoria-produto]] | 'absorvente' | Categoria do produto |
| [[variacao-produto]] | 'com-abas' | Tamanho do produto |
| [[marca-produto]] | 'intimus' | Marca do produto |
| [[quantidade-produto]] | '2' | Quantidade do produto |
| [[passo-checkout]] | 1' | Página de carrinho de compras |
| [[passo-checkout]] | 2' | Página de confirmação do endereço de entrega |
| [[passo-checkout]] | 3' | Página de seleção do método de pagamento |

<br />


**Ao escolher uma forma de pagamento e entrega**<br />

- **Onde:** Na página do checkout
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'checkoutOption',
  'eventCategory': 'fem:enhanced-ecommerce',
  'eventAction': 'checkoutOption',
  'eventLabel': '[[shipping ou payment]]-method',
    'ecommerce': {
    'checkout_option': {
        'actionField':  {'step':'2','option':'shipping:[[opcao escolhida]]:[[previsao-entrega]]'},
    }
  }
});
</script>
```

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'checkoutOption',
  'eventCategory': 'fem:enhanced-ecommerce',
  'eventAction': 'checkoutOption',
  'eventLabel': '[[shipping ou payment]]-method',
    'ecommerce': {
    'checkout_option': {
        'actionField':  {'step':'3','option':'payment:[[opcao escolhida]]'},
    }
  }
});
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[opcao escolhida]] | 'receber', 'retirar', 'cartao-de-credito', 'boleto' etc | Deve retornar o nome da opção de pagamento ou entrega escolhida. |
| [[previsao-entrega]] | 'em-ate-4-dias-uteis', 'pompeia-em-ate-2-dias' | Usar essa variável apenas para etapa de entrega. Retorna as informações de forma de entrega. |
| [[shipping ou payment]] | 'shipping' ou 'payment' | Deve retornar o nome da etapa do checkout. |

<br />


**Na finalização da compra**<br />

- **Onde:** Na página de resumo do pedido
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'purchase',
  'eventCategory': 'fem:enhanced-ecommerce',
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
| [[id-transacao]] | '000011652' | ID único da transação |
| [[valor-total-transacao]] | '139,99' | Valor total da transação incluindo frete e taxas |
| [[frete-transacao]] | '5.99' | Valor do frete da transação |
| [[coupon-transacao]] | 'cupom-2020' | Cupom de desconto utilizado na transação - promoção nivel pedido |
| [[taxa-transacao]] | '2.99' | Valor de taxas da transação |
| [[nome-produto]] | 'intimus-tripla-acao'  | Nome do produto |
| [[id-produto]] | 'i17mcjf106-771-2' | SKU do produto |
| [[preco-produto]] | &quot;139,99&quot; | Preço do produto |
| [[categoria-produto]] | 'absorvente' | Categoria do produto |
| [[variacao-produto]] | 'com-abas' | Tamanho do produto |
| [[marca-produto]] | 'intimus' | Marca do produto |
| [[quantidade-produto]] | '2' | Quantidade do produto |

<br />


---

> Em caso de dúvidas, entrar em contato com: [paulo.benachio@reamp.com.br](paulo.benachio@reamp.com.br)

<br />

<script>
  document.querySelector('h1').style.display = 'none'
</script>
