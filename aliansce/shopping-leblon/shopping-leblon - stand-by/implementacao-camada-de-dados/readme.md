![Jellyfish](https://github.com/adtechReamp/client/blob/main/Jellyfish-Logo-Blue-01.jpg?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - Shopping Leblon
Última atualização: 23/06/2022 <br />
Em caso de dúvidas, entrar em contato com: [ao.br@jellyfish.com](ao.br@jellyfish.com)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Implementação](#implementa%c3%a7%c3%a3o)
- [Geral](#geral)
- [Home](#home)
- [O Shopping](#o-shopping)
- [Cinema](#cinema)
- [Teatro](#teatro)
- [Lojas](#lojas)
- [Gastronomia](#gastronomia)
- [Planeje sua visita](#planeje-sua-visita)
- [Servicos](#servicos)
- [Fale Conosco](#fale-conosco)
- [Solar](#solar)
- [Enhanced E-commerce](#enhanced-e-commerce)


## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referentes ao ambiente de [https://shoppingleblon.com.br/](https://shoppingleblon.com.br/).

<br />

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
---

<h3 align="center"> Ajustes e implementações que devem ser realizadas </h3>


### Especificacoes Globais:

**Itens Gerais:**<br />
Todas as informações entre colchetes `[[  ]]` são variáveis dinâmicas que devem ser preenchidas com seus respectivos valores; <br />
Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais; <br />
Caso a informação solicitada não estiver disponível retornar tipagem ´undefined´.



### Dimensoes Globais:

**Dimensões Customizadas para todas as páginas:**<br />
Deve ser disparado um push de dataLayer no momento de carregamento de todas as páginas do site (Considerar também todas as trocas de Path, quando o conteúdo da página é alterado mas a página não recarrega).<br />


```html
<script>
	window.dataLayer = window.dataLayer || [];
	dataLayer.push({
		'dimension1': '[[User ID]]',
		'dimension3': '[[GTM ID]]',
        'dimension4': '[[Nome Loja]]',
        'dimension5': '[[Nome Ambiente]]',
   		'dimension6': '[[Genero Filme]]',
    	'dimension7': '[[Posicao Banner]]',
    	'dimension8': '[[CPF]]',
        'dimension9': '[[SKU Produto]]',
        'dimension10': '[[Email]]',
        'emailAllIn': '[[emailAllIn]]'
	
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[User ID]]			| '1234656'			    | ID definido após o cadastro e login								
| [[GTM ID]]			| 'GTM-NM5JRBW'		| ID do container do GTM instalado no ambiente e sua versao										|
| [[Nome Loja]] | 'concept', 'marisa' e etc | Deve retornar o nome da loja  
| [[Nome Ambiente]] | 'caxias', 'carioca', 'bangu', 'grande-rio' e etc. | Deve retornar o nome do shopping  
| [[Genero Filme]] | 'acao', 'romance', 'comedia' e etc. | Deve retornar o genero do filme  
| [[Posicao Banner]]   | '0', '1', '2' e etc. | Deve retornar a posicao do banner   
| [[CPF]]   | 'ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad' | Deve retornar o CPF do usuário hasheado em SHA256   
| [[SKU Produto]] | '45632187', '45612302' etc. | Deve retornar o sku do produto  
| [[Email]]   | 'ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad' | Deve retornar o email do usuário hasheado em SHA256   |
| [[emailAllIn]]   | 'jsdkjskdj' | Deve retornar o email do usuário criptografado em 2048, em todas as páginas apos ele logar ou se cadastrar    |


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
| [[nome-item]] | 'login', 'carrinho', 'logo' e etc. | Deve retornar o nome do item clicado no Header. |


<br />

**Quando:Ao clicar em um dos elementos do footer.**<br />

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
| [[secao]] | 'o-shopping', 'ajuda', 'politicas' e etc. | Deve retornar o nome da secao do footer.    |
| [[nome-item]] |  'instagram', 'cinema', 'solar' e etc. | Deve retornar o nome do item clicado no Footer.    |


<br />

**Quando: Ao clicar em um dos itens do menu.**<br />

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
| [[item-menu]] | 'compre-agora', 'o-shopping', 'lojas', 'cinema' e etc. | Deve retornar o nome do item clicado no menu. |


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
| [[termo-buscado]] | 'sorveteria', 'ad-studio', 'celulares' e etc. | Deve retornar o termo buscado.    |


<br />

### Home

**Quando:** Ao clicar nos cards.<br />

- **Onde:** Na página home.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:home',
    'eventAction': 'clique:card',
    'eventLabel': '[[nome-card]]'
  });
</script>

```
| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-card]] | 'solar', 'lojas', 'gastronomia' e etc. | Deve retornar o nome do card clicado.    |


<br />

**Quando:** Ao clicar nos links ou botões.<br />
- **Onde:** Na página home.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:home',
    'eventAction': 'clique:[[nome-item]]',
    'eventLabel': '[[nome-secao]]:[[texto-item]]'
  });
</script>

```
| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-item]] | 'botao', 'link' e etc. | Deve retornar qual elemento foi clicado.    |
| [[nome-secao]] | 'lojas-online', 'gastronomia', 'lojas-online', 'programa-de-relacionamento-do-shopping-leblon' ou 'acontece-no-shopping'. | Deve retornar o nome da seção onde houve a interação.    |
| [[texto-item]] | 'livraria-da-travessa', 'saiba-mais', 'compre-agora, 'arrecadacao-de-agasalhos' e etc. | Deve retornar o titulo (ou texto) de onde houve a interação.    |

<br />

---

### O Shopping

**Quando:** Ao clicar nos links<br />

- **Onde:** Na página Cinema.

```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:o-shopping',
    'eventAction': 'clique:link',
    'eventLabel': '[[nome-link]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| ['nome-link'] | 'offices-do-shopping-leblon', 'responsabilidade-social', `regras-de-convivencia` e etc | Deve retornar o nome do link clicado |


<br />

---

### Cinema

**Quando:** Ao clicar no botao "comprar" de cada filme. <br />
- **Onde:** Na página Cinema.


```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:cinema',
    'eventAction': 'clique:botao:comprar',
    'eventLabel': '[[nome-filme]]:[[data]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| ['nome-filme'] | 'batman', 'top-gun:maverick', 'lightyear', e etc. | Deve retornar o nome do filme interagido. |
| ['data'] | '27/06', '28/06', '29/06', e etc. | Deve retornar a data escolhida. |

<br />

**Quando:** No clique dos botões ou ícones de cada filme.<br />
- **Onde:** Na página Cinema.


```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:cinema',
    'eventAction': 'clique:[[botao-ou-icone]]',
    'eventLabel': '[[nome-filme]]:[[nome-item]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| ['botao-ou-icone'] | 'botao' ou 'icone' | Deve retornar se a iteracao ocorreu em um item ou botao.  |
| ['nome-filme'] | 'batman', 'top-gun:maverick', 'lightyear', e etc. | Deve retornar o nome do filme interagido. |
| ['nome-item'] | 'trailer', 'comprar',  | Deve retornar se a iteracao ocorreu em um item ou botao.  |

<br />

**Quando:** No clique do modal "outros horarios do dia"<br />
- **Onde:** Na página Cinema.


```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:cinema',
    'eventAction': 'clique:modal-horario',
    'eventLabel': '[[nome-filme]]:[[status]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| ['nome-filme'] | 'batman', 'top-gun:maverick', 'lightyear', e etc. | Deve retornar o nome do filme interagido. |
| ['status'] | 'abriu' ou 'fechou' | Deve retornar se o modal foi aberto ou fechado. |

<br />

---

### Teatro

**Quando:** Ao clicar na imagem da peça ou no link "Mais Detalhes".<br />
- **Onde:** Na página Teatro.


```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:teatro',
    'eventAction': 'clique:link',
    'eventLabel': '[[nome-filme]]:detalhes'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| ['nome-peca'] | 'o-misterio-da-irma-vap', 'historias-do-porchat' e etc. | Deve retornar o nome da peça interagida. |

<br />

**Quando:** Ao clicar no botao "comprar" de cada peça. <br />
- **Onde:** Na página Teatro.


```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:teatro',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-peca]]:comprar'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| ['nome-peca'] | 'o-misterio-da-irma-vap', 'historias-do-porchat' e etc. | Deve retornar o nome da peça interagida. |

<br />

---

### Lojas


**Quando:** Na interação com os filtros<br />
- **Onde:** Na página Lojas.
    
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
| ['nome-filtro'] | 'segmento', 'a-z' e etc. | Deve retornar o nome do filtro. |
| ['item-filtrado'] | 'aliemntacao', 'artigos-diversos' e etc. | Deve retornar termo filtrado. |
<br />

**Quando:** Ao clicar nas lojas. <br />
- **Onde:** Na página Lojas.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:lojas',
    'eventAction': 'clique:loja',
    'eventLabel': '[[nome-loja]]'
  });
</script>
```
| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| ['nome-loja'] | 'abreu', 'abraccio' e etc. | Deve retornar o nome da loja clicada. |
<br />

**Quando:** Ao clicar nos botoes das lojas. <br />
- **Onde:** Na página Lojas.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:lojas',
    'eventAction': 'clique:botao:loja',
    'eventLabel': '[[nome-loja]]:[[nome-botao]]'
  });
</script>
```
| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| ['nome-loja'] | 'abreu', 'abraccio' e etc. | Deve retornar o nome da loja clicada. |
| ['nome-botao'] | 'whatsapp', 'app-delivery', 'site-da-loja' e etc. | Deve retornar o texto do botao da loja clicada. |

<br />

---

### Gastronomia

**Quando:** Na interação com os filtros<br />
- **Onde:** Na página de Gastronomia.

```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:gastronomia',
    'eventAction': 'interacao:filtro',
    'eventLabel': '[[nome-filtro]]:[[item-filtrado]]'
  });
</script>
```
| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| ['nome-filtro'] | 'segmento', 'a-z' e etc. | Deve retornar o nome do filtro. |
| ['item-filtrado'] | 'aliemntacao', 'artigos-diversos' e etc. | Deve retornar termo filtrado. |
<br />

**Quando:** Ao clicar nas lojas.<br />
- **Onde:** Na página de Gastronomia.

```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:gastronomia',
    'eventAction': 'clique:loja',
    'eventLabel': '[[nome-loja]]'
  });
</script>

```
| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| ['nome-loja'] | 'abreu', 'abraccio' e etc. | Deve retornar o nome da loja clicada. |
<br />

**Quando:** Ao clicar nos botões das lojas<br />
- **Onde:** Na página de Gastronomia.

```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:gastronomia',
    'eventAction': 'clique:botao:loja',
    'eventLabel': '[[nome-loja]]:[[nome-botao]]'
  });
</script>
```
| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| ['nome-loja'] | 'abreu', 'abraccio' e etc. | Deve retornar o nome da loja clicada. |
| ['nome-botao'] | 'app-delivery', 'site-da-loja', 'compre-agora' e etc. | Deve retornar o nome do botão clicado. |

<br />

---

### Planeje sua visita

**Quando:** Nos cliques dos botões/links<br />
- **Onde:** Na página Planeje sua visita.

```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:planeje-sua-visita',
    'eventAction': 'clique:[[botao-ou-link]]',
    'eventLabel': '[[nome-item]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[botao-ou-link]] |  'botao' ou 'link' | Deve retornar se a interação ocorreu em um botão ou um link.  |
| [[nome-item]] |  'acessar-listagem-de-servicos', 'offices-do-shopping-leblon', 'responsabilidade-social' e etc | Deve retornar o titulo do item interagido.  |

<br />

---

### Servicos
**Quando:**  Nos cliques dos botões<br />

- **Onde:** Na página Serviços.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:servicos',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] |  'pagar-estacionamento', 'compre-agora' e etc | Deve retornar o nome do botão clicado.  |


<br />

---

### Fale Conosco

**Quando:** Nos cliques dos botões<br />
- **Onde:** Na página fale conosco.

```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:fale-conosco',
    'eventAction': 'clique:[[botao-ou-link]]',
    'eventLabel': '[[nome-item]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-item]] |  'meus-pedidos', 'prazo-de-entrega', 'nossas-lojas', 'o-shopping-e-pet-friendly?', 'enviar', e etc. | Deve retornar o titulo do item clicado.  |

<br />

**Quando:** Na interação com os campos do formulário<br />
- **Onde:** Na página fale conosco.

```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:fale-conosco',
    'eventAction': 'interacao:campo:formulario',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-item]] |  'nome', 'email', 'cpf', 'mensagem' e etc. | Deve retornar o nome do campo preenchido.  |

<br />

**Quando:** Na tentativa de callback do envio do formulario<br />
- **Onde:** Na página fale conosco.

```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:fale-conosco',
    'eventAction': 'callback',
    'eventLabel': '[[status]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]] |  'sucesso', 'erro:cpf-invalido', 'erro:campo-email-obrigatorio' e etc. | Deve retornar a mensagem de sucesso ou o tipo de erro.  |

<br />
---

### Solar

**Quando:** Ao clicar nos botões ou links<br />
- **Onde:** Na página Solar.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:solar',
    'eventAction': 'clique[[botao-ou-link]]',
    'eventLabel': '[[nome-item]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-item]] | 'faca-parte', 'enviar', 'politica-de-privacidade', 'lounge', 'shopping-leblon' e etc | Deve retornar o nome do item interagido.  |

<br />

**Quando:** Na interação com os campos do formulário<br />

- **Onde:** Na página Solar.

<b> Deve ser ajustado a taxonomia dos campos (Tagbook aba de validação site em homologação - linha 60) </b>

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:solar',
    'eventAction': 'interacao:campo:formulario',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] | 'nome', 'cpf' e etc | Deve retornar o nome do campo preenchido.  |


<br />

**Quando:** Na tentativa de callback do envio de formulario<br />

- **Onde:** Na página Solar.

<b> Deve ser ajustado a taxonomia dos campos (Tagbook aba de validação site em homologação - linha 60) </b>

    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'shopping-leblon:solar',
    'eventAction': 'callback',
    'eventLabel': '[[status]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]] | 'sucesso', 'erro:campo-nome-obrigatorio', 'erro:campo-email-nao-preenchido' e etc | Deve retornar o nome do campo preenchido.  |


<br />

---
### Enhanced E-commerce

**Na visualização de algum banner ou ads**<br />

- **Onde:** Em todas as páginas que estiver disponivel. 
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'promotionImpression',
    'eventCategory': 'shopping-leblon:enhanced-ecommerce',
    'eventAction': 'promotionImpression',
'noInteraction': '1',
'ecommerce': {
    'promoView': {
      'promotions': [{
        'id': '[[promotion-id]]',
        'name': '[[promotion-name]]',
        'position': '[[p´romotion-position]]'
      }]
    }
  }
  });
</script>
```



| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[promotion-id]] |'banner123' e etc | ID único do Banner |
| [[promotion-name]] | 'polos-diferenciadas' | Deve retornar o nome amigável do banner |
| [[promotion-position]] | '1' e etc | Deve retornar a posição que o banner é exibido  |

<br />


**No clique dos banners ou ads**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'promotionClick',
  'eventCategory': 'shopping-leblon:enhanced-ecommerce',
  'eventAction': 'promotionClick',
    'ecommerce': {
    'promoClick': {
      'promotions': [{
        'id': '[[promotion-id]]',
        'name': '[[promotion-name]]',
        'position': '[[promotion-position]]',
      }]
    }
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[promotion-id]] |'banner123' e etc | ID único do Banner |
| [[promotion-name]] | 'polos-diferenciadas' | Deve retornar o nome amigável do banner |
| [[promotion-position]] | '1' e etc | Deve retornar a posição que o banner é exibido  |

<br />

**Na visualização de uma lista de produtos**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'productImpression',
  'eventCategory': 'shopping-leblon:enhanced-ecommerce',
  'eventAction': 'productImpression',
  'noInteraction': '1',
  'ecommerce': {
    'impressions': [{
        'name': '[[product-name]]',
        'id': '[[product-id]]',
        'price':' [[product-price]]',
        'category': '[[product-category]]',
        'brand': '[[product-brand]]',
        'list': '[[product-list]]',
        'position': '[[product-position]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[product-name]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[product-id]] | 'i17mcjf106-771-2' | SKU do produto |
| [[product-price]] | '139.99' | Preço do produto |
| [[product-category]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[product-brand]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[product-list]] | 'moda-masculina' e etc' | Nome da lista que o produto aparece |
| [[product-position]] | '2' | Posição que o produto aparece em uma lista de produtos |

<br />


**No clique de algum produto**<br />

- **Onde:** Em todas as páginas que estiver disponivel.
    

```html
<script>
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
    'event': 'productClick',
    'eventCategory': 'shopping-leblon:enhanced-ecommerce',
    'eventAction': 'productClick',
        'ecommerce': {
        'click': {
            'actionField': {'list': '[[lista-produto]]'},
             'products': [{
               'name': '[[product-name]]',
               'id': '[[product-id]]',
               'price':' [[product-price]]',
               'category': '[[product-category]]',
               'brand': '[[product-brand]]',
               'list': '[[product-list]]',
               'position': '[[product-position]]',
               'coupon': '[[product-cupom]]',
               'dimension4': '[[nome-loja]]'
    }]
  }
});
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[product-name]] | 'chinelo-metalizado-ouro' e etc' | Nome do produto |
| [[product-id]] | 'i17mcjf106-771-2' | SKU do produto |
| [[product-price]] | '139.99' | Preço do produto |
| [[product-category]] | calcados', 'vestuario', 'alimentacao' e etc | Categoria do produto |
| [[product-brand]] | 'marisa', 'rayban' e etc | Marca do produto |
| [[product-list]] | 'moda-masculina' e etc' | Nome da lista que o produto aparece |
| [[product-position]] | '2' | Posição que o produto aparece em uma lista de produtos |
| [[product-cupom]] | '25%' e etc' | Desconto do produto |
| [[nome-loja]] | '12kj3h', '3io5lk4' e etc | Deve retornar o nome(ID) da loja que vende o produto. |

<br />


---

> Em caso de dúvidas, entrar em contato com: [ao.br@jellyfish.com](ao.br@jellyfish.com)


<script> document.querySelector('h1').style.display = 'none' </script>
