![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - LPs - Simples de tratar - Conecta Consulta
Última atualização: 08/04/2021 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Implementação](#implementa%c3%a7%c3%a3o)
- [Especificações Globais](#especifica%c3%a7%c3%b5es-globais)
- [Dimensões Globais](#dimens&otilde;es-globais)
- [Geral-LPs](#geral-lps)



## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referente a <b> LPs de hipotireoidismo - simples de tratar <b>



<br />

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

## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />

---

## Implementação

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
	Texto do elemento
</div>
```

#### Importante:
> Também devem ter os data-attributes `data-gtm-event-category`, `data-gtm-event-action` e `data-gtm-event-label`. Preenchidos conforme instruções específicas.

<br />

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
		'dimension1': '[[[GA ClientID]]',
		'dimension2': '[[GTM-ID]]]',
		'dimension3': '[[resposta]]'
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[GA ClientID]]	| 'XXXXXXXXXX:XXXX:XX'	| ID aleatório do Google Analytics										|
| [[GTM-ID]]		| 'GTM-xxxxxxx'		| ID do container do GTM instalado no ambiente										|


---

### Geral LPs

**Quando: Ao clicar no logo do header.**<br />

- **Onde:** Nas Lps de hipotireoidismo simples de tratar.
    

```html
<!-- Use se os atributos no elemento a ser clicado -->
<div
     data-gtm-event-category="[[nome-lp]]:simples-de-tratar" 
     data-gtm-event-action="clique:header" 
     data-gtm-event-label="logo"
>
Botão
</div>
```

| Variável 				| Exemplo 				| Descrição 									|
| :--------------	| :-------------- | :--------------------------	|
| [[nome-lp]]	  | 'lp1-hipotireoidismo' e 'lp2-hipotireoidismo'.  | Deve retornar o nome da lp. |


<br />


**Quando: Ao clicar em um dos elementos do footer.**<br />

- **Onde:** Nas Lps de hipotireoidismo simples de tratar.
    

```html
<!-- Use se os atributos no elemento a ser clicado -->
<div
     data-gtm-event-category="[[nome-lp]]:simples-de-tratar" 
     data-gtm-event-action="clique:footer" 
     data-gtm-event-label="[[nome-item]]"
>
Botão
</div>
```

| Variável 				| Exemplo 				| Descrição 									|
| :--------------	| :-------------- | :--------------------------	|
| [[nome-lp]]	  | 'lp1-hipotireoidismo' e 'lp2-hipotireoidismo'.  | Deve retornar o nome da lp. |
| [[nome-item]]	  | 'logo', 'cadastre-se', 'entre' e etc | Deve retornar o nome do item clicado no footer. |

<br />

**Quando: No clique dos botões de cada seção**<br />

- **Onde:** Nas Lps de hipotireoidismo simples de tratar.
    

```html
<!-- Use se os atributos no elemento a ser clicado -->
<div
     data-gtm-event-category="[[nome-lp]]:simples-de-tratar" 
     data-gtm-event-action="clique:botao" 
     data-gtm-event-label="[[nome-botao]]:[[nome-secao]]"
>
Botão
</div>
```

| Variável 				| Exemplo 				| Descrição 									|
| :--------------	| :-------------- | :--------------------------	|
| [[nome-lp]]	  	| 'lp1-hipotireoidismo'e 'lp2-hipotireoidismo'.  | Deve retornar o nome da lp. |
| [[nome-botao]]	| 'faca-sua-pre-avaliacao-agora', 'quero-responder-ao-questionario-agora!', 'tenho-sintomas-e-quero-fazer-a-pre-avaliacao!' e etc | Deve retornar o nome do botão clicado. |
| [[nome-secao]]	| 'entenda-como-e-simples-de-tratar', 'tem-duvidas-do-que-esta-sentindo-tem-relacai-a-tireoide','qual-especialidade-medica-devo-procurar', 'sintomas-comun' e etc | Deve retornar o nome da seção do botão clicado.  |

<br />


> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
