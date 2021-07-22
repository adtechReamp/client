![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Analytics & Optmization <br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - BP - Central de Marcação Online
Última atualização: 20/05/2021 <br />
Em caso de dúvidas, entrar em contato com: [nathalia.paschotto@reamp.com.br](nathalia.paschotto@reamp.com.br) / [rodolfo.nogueira@reamp.com.br](rodolfo.nogueira@reamp.com.br)

<br />


[https://hospitalbp.centraldemarcacao.com.br/](https://hospitalbp.centraldemarcacao.com.br/)

<br />

<h3> INSTALAÇÃO DO GOOGLE TAG MANAGER</H3>

### **Posicionamento do Código - Google Tag Manager**

#### 1. Copie e cole o seguinte código abaixo o mais alto possível na tag '<head>' da página:.

```html

<html>
  <head>
 <!-- Google Tag Manager -->
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-K8W2XF3');</script>
<!-- End Google Tag Manager -->


  </head>
```

#### 2. Copie o seguinte trecho e cole-o imediatamente após a marcação '<body>' de abertura em cada página do seu site.

```html
<body>
<!-- Google Tag Manager (noscript) -->
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-K8W2XF3"
height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
<!-- End Google Tag Manager (noscript) -->

```

Link de referência: [Documentação Oficial Google Tag Manager](https://developers.google.com/tag-manager/quickstart)



<br />

---

<br />

> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
