![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - ProMatre 
Última atualização: 24/06/2021 <br />
Em caso de dúvidas, entrar em contato com: [nathalia.paschotto@reamp.com.br](nathalia.paschotto@reamp.com.br)

<br />

## Sumário

- [Fale Conosco](#fale-conosco)
- [Artigos](#artigos)



## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referente ao ambiente:

[https://dev.promatresp.com.br/](https://dev.promatresp.com.br/)

<br />


Link de referência: [Documentação Oficial Google Tag Manager](https://developers.google.com/tag-manager/quickstart)


## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />



## Overview e Descrições Técnicas

### Camada de dados (DataLayer)

> É um array de objetos javascript utilizado pelo Google Tag Manager para receber em seus atributos, dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação.

## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />

> Tudo que estiver como geral, deverá ter a mesma nomencratura no elemento do site. (em todas as páginas onde estiver o mesmo elemento)

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

### Fale Conosco

**Quando:   Na tentativa de callback de envio do formulário.**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'pro-matre:fale-conosco',
    'eventAction': 'callback:envio-formulario',
    'eventLabel': '[[status]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[status]]| :  'sucesso', 'erro:email-invalido', 'pagina-indisponivel-no-momento' e etc.|  Retornar a mensagem de sucesso ou tipo de erro. |


<br />

### Artigos


**Quando:   Ao ser reconhecido o último "</p>" ou "</div>" do artigo dentro dos botões "continuar lendo".**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'leituraCompleta',
    'eventCategory': 'pro-matre:geral',
    'eventAction': 'leitura-artigo',
    'eventLabel': 'leitura-completa:[[titulo-artigo]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[titulo-artigo]]| :  'plano-particular', 'o-que-e-o-plano-particular?', 'humanizacao' e etc.|  Retornar o titulo do artigo. |


<br />


---

<br />

> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
