![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Analytics & Optimization <br />
> Documento de Especificação Técnica

<br />

## Instalação GTM - BP - Portal Médico
Última atualização: 11/08/2021 <br />
Em caso de dúvidas, entrar em contato com: [nathalia.paschotto@jellyfish.com](nathalia.paschotto@jellyfish.com)

<br />


## Instalação snippet GTM

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
})(window,document,'script','dataLayer','GTM-5K7SXZR');</script>
<!-- End Google Tag Manager -->


  </head>
```

#### 2. Copie o seguinte trecho e cole-o imediatamente após a marcação '<body>' de abertura em cada página do seu site.

```html
<body>
<!-- Google Tag Manager (noscript) -->
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-5K7SXZR"
height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
<!-- End Google Tag Manager (noscript) -->

  </body>
</html>
```

Link de referência: [Documentação Oficial Google Tag Manager](https://developers.google.com/tag-manager/quickstart)

---


<br />

> [nathalia.paschotto@jellyfish.com](nathalia.paschotto@jellyfish.com)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
