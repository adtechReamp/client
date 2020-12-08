![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Technical Specification Document

<br />

## Data Layer and Data Attributes Implementation - Kimberly Clark
Last update: 08/12/2020 <br />
In case of any questions, contact: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Summary

- [Objective](#objective)
- [Implementation](#implementation)
- [Global Specifications](#global-specifications)
- [Global Dimensions](#global-dimensions)
- [General](#general)
- [Login](#login)
- [Register](#register)
- [Home](#home)
- [Product Page](#product-page)
- [Enhanced E-commerce](#enhanced-e-commerce)

## Objective

This document aims to instruct the implementation of the data layer and data attributes to use Google Analytics tracking resources for [https://xd.adobe.com/view/08130346-1762-4140-82d9-e661feaa6798-5d40/screen/7d36a398-6a5b-4dba-96ff-50d4e58f0dbf/](https://xd.adobe.com/view/08130346-1762-4140-82d9-e661feaa6798-5d40/screen/7d36a398-6a5b-4dba-96ff-50d4e58f0dbf/).

<br />

### **General description**

The Google Tag Manager snippet is a small piece of javascript or non-javascript code, using an iframe when javascript is not available, which is inserted in the website pages, making it possible for the tags to be configured via interface.


### **Code Positioning - Google Tag Manager**

#### 1. Copy the following JavaScript and paste it as close to the opening `<head>` tag as possible on all pages of your site.

```html

<html>
  <head>
    <!-- Google Tag Manager -->
    <script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start': new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0], j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src='https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f); })(window,document,'script','dataLayer','GTM-XXXXXXX');</script>
    <!-- End Google Tag Manager -->
    //...
  </head>
```

#### 2. Copy the following snippet and paste it immediately after the opening `<body>` tag on each page of your site.

```html
<body>
  <!-- Google Tag Manager (noscript) -->
  <noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-XXXXXXX" height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
  <!-- End Google Tag Manager (noscript) -->
  //...
  </body>
</html>
```

Reference Link: [Google's Official GTM documentation](https://developers.google.com/tag-manager/quickstart)


## Comments
> The values specified in brackets `[[]]` are dynamic variables and must be replaced by their respective values. <br />

> All values sent to Google Analytics must be sanitized, that is, without spaces, accents or special characters. <br />

> If the site already has Google Analytics installed, it will be necessary to remove the code from ** all pages of the site **: <br />

```html

<script>
(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o), m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)})(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

ga('create', 'UA-XXXXXXXX-X', 'auto');
ga('send', 'pageview');
</script>

```


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

## Implementation

### DataLayer

> It is an array of javascript objects used by Google Tag Manager to receive in its attributes, important data from the site.
To implement the dataLayer on the website, the developer can use different ways to fill in the data. These forms are dependent on the action established in the documentation and also on the level of interaction.

**Installation**<br />
Insert the data layer before the Google Tag Manager installation snippet. Example:

```html
<script>
	window.dataLayer = window.dataLayer || [];
	window.dataLayer = [{
		'atributo1': '[[value1]]',
		'atributo2': '[[value2]]'
	}];
</script>
```

OU

```html
<script>
	window.dataLayer = window.dataLayer || [];
	window.dataLayer.push({
		'atributo1': '[[value1]]',
		'atributo2': '[[value2]]'
	});
</script>
```

### HTML Attributes (Data Attributes)

> They are custom attributes inserted in the HTML elements of the page, allowing the inclusion of additional data.

**Installation**
1. Elements: ```<div>Element</div>``` <br />

All elements of the html that will be clicked, must be mapped receiving the attributes with their structure in the item.

```html
<div 	
    data-gtm-event-category="[[example:category-value]]"
 	data-gtm-event-action="[[example:action-value]]"
 	data-gtm-event-label="[[example:label-value]]"
 >
</div>
```

#### Important:
> They must also have the data-attributes `data-gtm-event-category`,` data-gtm-event-action` and `data-gtm-event-label`. Filled according to specific instructions.

<br />



### Global Specifications:

**General Items:**<br />
All information in brackets `[[]]` are dynamic variables that must be filled in with their respective values; <br />
All values sent to Google Analytics must be sanitized, that is, without spaces, accents or special characters; <br />
If the requested information is not available, return ´undefined´ typing.



### Global Dimensions:

**Custom dimensions for all pages:**<br />

A dataLayer push must be triggered when loading all pages on the site (Also consider all changes to Path, when the page content is changed but the page does not reload).<br />

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


| Variable 				| Example 				| Description 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[User ID]]			| '1234656'			    | Unique User ID defined after register.										|
| [[GA ClientID]]		| 'XXXXXXXXXX:XXXX:XX'	| Random Client ID generated by Google Analytics										|
| [[GTM-ID]]			| 'GTM-XXXXXX:XX'		| Container ID of the installed GTM.										|

---

### General

**On clicking the header itens.**<br />

- **Where:** On all pages where it's available.
    
```html
<div
   data-gtm-event-category='fem:general'
   data-gtm-event-action='click:header'
   data-gtm-event-label='[[header-item]]'
>Botão</div>
```


| Variable        | Example                               | Description                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[header-item]] | 'logo', 'idioma', 'perfil', 'menu'. | It should return the name of the header item clicked. |

<br />


**On clicking the footer itens.**<br />

- **Where:** On all pages where it's available.
    
```html
<div
   data-gtm-event-category='fem:general'
   data-gtm-event-action='click:footer'
   data-gtm-event-label='[[footer-item]]'
>Botão</div>
```


| Variable        | Example                               | Description                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[footer-item]] | 'logo', 'idioma', 'fale-com-a-gente', 'termos-e-condicoes' and etc. | It should return the name of the footer item clicked. |

<br />


**On selecting an item from the bars menu.**<br />

- **Where:** On all pages where it's available.
    
```html
<div
   data-gtm-event-category='fem:general'
   data-gtm-event-action='click:menu'
   data-gtm-event-label='[[menu-item]]'
>Botão</div>
```


| Variable       | Example                               | Description                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[menu-item]] |  'cuidado-diario', 'produtos', 'destaques' and etc. | It should return the name of the menu item clicked. |

<br />


**On selecting a language from the language menu.**<br />

- **Where:** On all pages where it's available.
    
```html
<div
   data-gtm-event-category='fem:general'
   data-gtm-event-action='click:language'
   data-gtm-event-label='[[language-name]]'
>Botão</div>
```


| Variable        | Example                               | Description                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[language-name]] | 'ingles', 'espanhol', 'portugues' and etc. | It should return the name of the selected language.  |

<br />


**On interaction with the filters.**<br />

- **Where:** On all pages where it's available.
    
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



| Variable        | Example                               | Description                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[filter-name]] | 'cuidados-diarios', 'fluxo-normal' and etc. | It should return the name of the selected filter tag.  |

<br />


**On clicking the backwards button.**<br />

- **Where:** On all pages where it's available.
    
```html
<div
   data-gtm-event-category='fem:general'
   data-gtm-event-action='click:button'
   data-gtm-event-label='backwards'
>Botão</div>
```



<br />


**On clicking the links in the breadcrumb.**<br />

- **Onde:** On all pages where it's available.
    
```html
<div
   data-gtm-event-category='fem:general'
   data-gtm-event-action='click:breadcrumb'
   data-gtm-event-label='[[breadcrumb-item]]'
>Botão</div>
```


| Variable        | Example                               | Description                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[breadcrumb-item]] | 'detaques', 'cuidados-diarios' and etc | It should return the name of the clicked link on the breadcrumb. |

<br />


### Login

**On clicking any button or link.**<br />

- **Where:** On the login page.
    
```html
<div
   data-gtm-event-category='fem:login'
   data-gtm-event-action='click:[[button-or-link]]'
   data-gtm-event-label='[[item-name]]'
>Botão</div>
```


| Variable        | Example                               | Description                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[button-or-link]] | 'botao' or 'link' | It should return the type of element clicked. |
| [[item-name]] | 'criar-uma-conta', 'esqueci-a-senha', 'entrar' and etc | It should return the name of the element clicked. |

<br />


**On filling the fields of the login form.**<br />

- **Where:** On the login page.
    
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



| Variable        | Example                               | Description                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[field-name]] | 'email', 'senha'  |  It should return the name of the filled field. |

<br />


**On the callback of the login attempt.**<br />

- **Where:** On the login page.
    
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



| Variable        | Example                               | Description                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[sucess-or-fail:error-tpe]] |  'sucesso', 'erro:senha-invalida', 'erro:perdeu-conexao' and etc. | It should return the success message or the fail one with the tye of error. |

<br />


### Register

**On clicking any button or link.**<br />

- **Where:** On the register page.
    
```html
<div
   data-gtm-event-category='fem:register'
   data-gtm-event-action='click:[[button-or-link]]'
   data-gtm-event-label='[[item-name]]'
>Botão</div>
```


| Variable        | Example                               | Description                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[button-or-link]] | 'botao' or 'link' | It should return the type of element clicked. |
| [[item-name]] | 'ja-possuo-uma-conta', 'registrar' and etc. | It should return the name of the element clicked.  |

<br />


**On filling the fields of the login form.**<br />

- **Where:** On the register page.
    
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



| Variable        | Example                               | Description                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[field-name]] | 'nome', 'email', 'senha' |  It should return the name of the filled field.  |

<br />


**On interaction with the checkbox.**<br />

- **Where:** On the register page.
    
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



| Variable        | Example                               | Description                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[checkbox-name]] | 'li-e-aceito-os-termos' e etc | It should return the name of the interacted checkbox. |

<br />


**Na tentiva de callback para logar**<br />

- **where:** On the register page.
    
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



| Variable        | Example                               | Description                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[sucess-or-fail:error-tpe]] | 'sucesso', 'erro:senha-invalida', 'erro:perdeu-conexao' and etc. | It should return the success message or the fail one with the tye of error.  |

<br />


### Home

**On clicking any link or button of the page.**<br />

- **where:** On the homepage.
    
```html
<div
   data-gtm-event-category='fem:home'
   data-gtm-event-action='click:[[button-or-link]]'
   data-gtm-event-label='[[item-name]]'
>Botão</div>
```


| Variable        | Example                               | Description                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[button-or-link]] | 'botao' ou 'link'   | It should return the type of element clicked. |
| [[item-name]] | 'clique-para-ver-mais', 'encontre-mais-produtos' and etc | It should return the name of the element clicked.  |

<br />


### Product Page

**On interaction with the questions.**<br />

- **Where:** On the product page.
    
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



| Variable        | Example                               | Description                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[question-name]] | 'qual-a-direnca-entre-o-intimus-com-abas-ou-sem-abas' and etc | It should return the name of the question clicked. |
| [[action]] | 'abriu' or 'fechou'. | It should return the name of the action done. |

<br />


**On viewing the content section.**<br />

- **Where:** On the product page.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'noInteraction': '1',
    'eventCategory': 'fem:pdp',
    'eventAction': 'viewed:section',
    'eventLabel': 'content'
  });
</script>
```




<br />


**On clicking a content card.**<br />

- **Where:** On the product page.
    
```html
<div
   data-gtm-event-category='fem:pdp'
   data-gtm-event-action='click:card'
   data-gtm-event-label='[[card-name]]'
>Botão</div>
```


| Variable        | Example                               | Description                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[card-name]] | 'some-content-card-title' | It should return the name of the card clicked.|

<br />


**On clicking the 'ver mais' button on a product.**<br />

- **Where:** On the product page.
    
```html
<div
   data-gtm-event-category='fem:pdp'
   data-gtm-event-action='click:button'
   data-gtm-event-label='ver-mais:[[product-name]]'
>Botão</div>
```


| Variable        | Example                               | Description                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[product-name]] | 'intimus-tripla-acao' e etc | Deve retornar o Name of the product. |

<br />


### Enhanced E-commerce

**On viewing a showcase/list of products.**<br />

- **Where:** On all pages where it's available.
    

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
        'name': '[[product-name]]',
        'id': '[[product-id]]',
        'list': '[[product-list]]',
        'price': '[[product-price]]',
        'brand': '[[product-brand]]',
        'category': '[[product-category]]',
        'position': '[[product-position]]'
    }]
  }
});
</script>
```

| Variable        | Example                               | Description                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[product-name]] | 'intimus-tripla-acao'  | Name of the product |
| [[product-id]] | 'i17mcjf106-771-2' | Product SKU |
| [[product-price]] | &quot;139,99&quot; | Product Price |
| [[product-category]] | 'absorvente' | Product Category |
| [[product-brand]] | 'intimus' | Product Brand |
| [[product-list]] | 'tampoes' | Name of the list in which the product is in |
| [[product-position]] | '1' | Position in which the product is on the list. |

<br />


**On clicking any product**<br />

- **Where:** On all pages where it's available.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
    'event': 'productClick',
    'eventCategory': 'fem:enhanced-ecommerce',
    'eventAction': 'productClick',
        'ecommerce': {
        'click': {
            'actionField': {'list': '[[product-list]]'},
            'products': [{
                'name': '[[product-name]]',
                'id': '[[product-id]]',
                'price': '[[product-price]]',
                'brand': '[[product-brand]]',
                'category': '[[product-category]]',
        'position': '[[product-position]]'
            }]
        }
    }
});
</script>
```

| Variable        | Example                               | Description                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[product-name]] | 'intimus-tripla-acao'  | Name of the product |
| [[product-id]] | 'i17mcjf106-771-2' | Product SKU |
| [[product-price]] | &quot;139,99&quot; | Product Price |
| [[product-category]] | 'absorvente' | Product Category |
| [[product-brand]] | 'intimus' | Product Brand |
| [[product-list]] | 'tampoes' | Name of the list in which the product is in |
| [[product-position]] | '1' | Position in which the product is on the list. |

<br />


**On viewing the product detail page of any product.**<br />

- **Where:** On the product detail page.
    

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
        'name': '[[product-name]]',
        'id': '[[product-id]]',
        'price': '[[product-price]]',
        'brand': '[[product-brand]]',
        'category': '[[product-category]]',
        'variant': '[[product-variant]]',
      }]
    }
  }
 });
</script>
```

| Variable        | Example                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[product-name]] | 'intimus-tripla-acao'  | Name of the product |
| [[product-id]] | 'i17mcjf106-771-2' | Product SKU |
| [[product-price]] | &quot;139,99&quot; | Product Price |
| [[product-category]] | 'absorvente' | Product Category |
| [[product-brand]] | 'intimus' | Product Brand |
| [[product-variant]] | 'com-abas' | Product Variant |

<br />


**On adding a product to the cart.**<br />

- **Where:** On all pages where it's available.
    

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
        'name': '[[product-name]]',
        'id': '[[product-id]]',
        'price': '[[product-price]]',
        'brand': '[[product-brand]]',
        'category': '[[product-category]]',
        'variant': '[[product-variant]]',
        'quantity': '[[product-quantity]]'
      }]
    }
  }
});
</script>
```

| Variable        | Example                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[product-name]] | 'intimus-tripla-acao'  | Name of the product |
| [[product-id]] | 'i17mcjf106-771-2' | Product SKU |
| [[product-price]] | &quot;139,99&quot; | Product Price |
| [[product-category]] | 'absorvente' | Product Category |
| [[product-variant]] | 'com-abas' | Product Variant |
| [[product-brand]] | 'intimus' | Product Brand |
| [[product-quantity]] | '2' | Product Quantity |

<br />


**On removing a product from the cart.**<br />

- **Where:** On the cart page.
    

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
        'name': '[[product-name]]',
        'id': '[[product-id]]',
        'price': '[[product-price]]',
        'brand': '[[product-brand]]',
        'category': '[[product-category]]',
        'variant': '[[product-variant]]',
        'quantity': '[[product-quantity]]'
      }]
    }
  }
});
</script>
```

| Variable        | Example                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[product-name]] | 'intimus-tripla-acao'  | Name of the product |
| [[product-id]] | 'i17mcjf106-771-2' | Product SKU |
| [[product-price]] | &quot;139,99&quot; | Product Price |
| [[product-category]] | 'absorvente' | Product Category |
| [[product-variant]] | 'com-abas' | Product Variant |
| [[product-brand]] | 'intimus' | Product Brand |
| [[product-quantity]] | '2' | Product Quantity |

<br />


**On loading of each checkout step.**<br />

- **Where:** On pages of the checkout process.
    

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
      'actionField': {'step': '[[checkout-step]]'},
      'products': [{
        'name': '[[product-name]]',
        'id': '[[product-id]]',
        'price': '[[product-price]]',
        'brand': '[[product-brand]]',
        'category': '[[product-category]]',
        'variant': '[[product-variant]]',
        'quantity': '[[product-quantity]]'
      }]
    }
  }
});
</script>
```

| Variable        | Example                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[checkout-index]] |  | Returns &quot;1&quot;, &quot;2&quot; or &quot;3&quot; according to the page the user is currently on.  |
| [[product-name]] | 'intimus-tripla-acao'  | Name of the product |
| [[product-id]] | 'i17mcjf106-771-2' | Product SKU |
| [[product-price]] | &quot;139,99&quot; | Product Price |
| [[product-category]] | 'absorvente' | Product Category |
| [[product-variant]] | 'com-abas' | Product Variant |
| [[product-brand]] | 'intimus' | Product Brand |
| [[product-quantity]] | '2' | Product Quantity |
| [[passo-checkout]] | 1' | Cart Page |
| [[passo-checkout]] | 2' | Shipping Information Page |
| [[passo-checkout]] | 3' | Payment Page |

<br />


**On choosing one of the payment and shipping options available.**<br />

- **Where:** On pages of the checkout process.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'checkoutOption',
  'eventCategory': 'fem:enhanced-ecommerce',
  'eventAction': 'checkoutOption',
  'eventLabel': '[[shipping-or-payment]]-method',
    'ecommerce': {
    'checkout_option': {
        'actionField':  {'step':'2','option':'shipping:[[selected-option]]:[[delivery-time]]'},
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
  'eventLabel': '[[shipping-or-payment]]-method',
    'ecommerce': {
    'checkout_option': {
        'actionField':  {'step':'3','option':'payment:[[selected-option]]'},
    }
  }
});
</script>
```


| Variable        | Example                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[selected-option]] | 'receber', 'retirar', 'cartao-de-credito', 'boleto' etc | It should return the name of the payment or shipping option selected. |
| [[delivery-time]] | 'em-ate-4-dias-uteis', 'pompeia-em-ate-2-dias' | Use this variable only for the shipping step. It should return the estimated delivery time for the selected shipping option. |
| [[shipping ou payment]] | 'shipping' ou 'payment' | It should return the name of the current checkout option. Eg: 'shipping' or 'payment'. |

<br />


**On completing a purchase.**<br />

- **Where:** On the thank you/order summary page.
    

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
        'id': '[[transaction-id]]',
        'revenue': '[[Transaction Revenue]]',
        'shipping': '[[Transaction Shipping]]'
        'tax': '[[transaction-tax]]'
        'coupon': '[[transaction-coupon]]'
      },
      'products': [{
        'name': '[[product-name]]',
        'id': '[[product-id]]',
        'price': '[[product-price]]',
        'brand': '[[product-brand]]',
        'category': '[[product-category]]',
        'variant': '[[product-variant]]',
        'quantity': '[[product-quantity]]'
      }]
    }
  }
});
</script>
```

| Variable        | Example                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[transaction-id]] | '000011652' | Unique ID of the transaction |
| [[Transaction Revenue]] | '139,99' | Total value of the transaction including taxes and shipping. |
| [[Transaction Shipping]] | '5.99' | Transaction shipping value |
| [[transaction-coupon]] | 'cupom-2020' | Name of coupon used in the transaction |
| [[transaction-tax]] | '2.99' | Transaction taxes value |
| [[product-name]] | 'intimus-tripla-acao'  | Name of the product |
| [[product-id]] | 'i17mcjf106-771-2' | Product SKU |
| [[product-price]] | &quot;139,99&quot; | Product Price |
| [[product-category]] | 'absorvente' | Product Category |
| [[product-variant]] | 'com-abas' | Product Variant |
| [[product-brand]] | 'intimus' | Product Brand |
| [[product-quantity]] | '2' | Product Quantity |

<br />


---

> In case of any questions, please contact: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script>
  document.querySelector('h1').style.display = 'none'
</script>
