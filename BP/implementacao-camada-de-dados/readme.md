![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - BP - A Beneficiência Portuguesa de São Paulo
Última atualização: 19/07/2021 <br />
Em caso de dúvidas, entrar em contato com: [nathalia.paschotto@reamp.com.br](nathalia.paschotto@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [LP indique seus pacientes](#lp-indique-seus-pacientes)



## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referente ao ambiente:

[https://www.bp.org.br/indique-seus-pacientes](https://www.bp.org.br/indique-seus-pacientes)

<br />





---

## Overview e Descrições Técnicas

### Camada de dados (DataLayer)

> É um array de objetos javascript utilizado pelo Google Tag Manager para receber em seus atributos, dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação.

## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />

---

### LP indique seus pacientes 

**Quando: Na interação com os campo do formúlario .**<br />

- **Onde:**  Na nova LP de médicos referenciadores.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'indique-seus-pacientes',
    'eventAction': 'interacao:formulario',
    'eventLabel': 'preencheu:campo:[[nome-campo]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]]| 'nome','e-mail','telefone', 'crm', e etc. |  Retornar o nome do campo preenchido.|


<br />

*Quando: Na interação com os filtros do formúlario .**<br />

- **Onde:**  Na nova LP de médicos referenciadores.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'indique-seus-pacientes',
    'eventAction': 'interacao:formulario:filtro-especialidade',
    'eventLabel': 'selecionou:filtro:[[nome-filtro]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-filtro]]| 'cardiologia','geriatria','nefrologia' e etc. |  Retornar o nome do filtro preenchido.|


<br />

**Quando: Ao interagir com o checkbox.**<br />

- **Onde:**  Na nova LP de médicos referenciadores.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'indique-seus-pacientes',
    'eventAction': 'interacao:checkbox-formulario',
    'eventLabel': '[[acao]]:[[nome-check]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[acao]] | 'marcou' e 'desmarcou' |  Deve retornar o tipo de ação realizada.  |
| [[[nome-check]]|  'concordo-em-receber-informações-sobre-a-bp-e-estou-ciente-sobre-a-politica-de-privacidade' e 'quero-receber-a-newsletter-da-bp-sobre-novidades-e-eventos'.| Deve retornar o nome do checkbox interagido.|


<br />


**Quando:   Na tentativa de callback de envio do formulário.**<br />

- **Onde:**  Na nova LP de médicos referenciadores.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'indique-seus-pacientes',
    'eventAction': 'callback:envio-formulario',
    'eventLabel': '[[status]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|[[status]]| :  'sucesso', 'erro:email-invalido', 'pagina-indisponivel-no-momento' e etc.|  Retornar a mensagem de sucesso ou tipo de erro. |





<br />

---

<br />

> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
