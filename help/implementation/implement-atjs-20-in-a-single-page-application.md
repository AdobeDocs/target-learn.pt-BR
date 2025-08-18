---
title: Como implementar a at.js 2.0 em um aplicativo de página única (SPA)
description: A at.js 2.0 da Adobe Target fornece conjuntos de recursos avançados para sua empresa personalizar tecnologias de próxima geração no lado do cliente. Siga estas etapas para implementar a at.js 2.0 em um aplicativo de página única (SPA).
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 955f0571-5791-4dbb-9931-e6d5c8bb42a7
source-git-commit: fcd2273ba373dc2b3bc59a77f1925cdb7b2ed3ee
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Implementar a at.js 2.0 do Adobe Target em um aplicativo de página única (SPA)

O `at.js` 2.0 da Adobe Target fornece conjuntos de recursos avançados para sua empresa personalizar tecnologias de próxima geração no lado do cliente. Esta versão tem como foco a atualização do `at.js` para ter interações harmoniosas com aplicativos de página única (SPAs).

>[!VIDEO](https://video.tv.adobe.com/v/34798?quality=12&captions=por_br)

## Como implementar a at.js 2.0 em um SPA

* Implemente o `at.js` 2.0 no &lt;head> do seu Aplicativo de Página Única.
* Implemente a função `adobe.target.triggerView()` sempre que a exibição for alterada em seu SPA. Várias técnicas podem ser empregadas para fazer isso, como ouvir alterações de hash de URL, ouvir eventos personalizados acionados por seu SPA ou incorporar o código `triggerView()` diretamente no aplicativo. Você deve escolher a opção que funciona melhor para seu aplicativo de página única específico.
* O nome da exibição é o primeiro parâmetro da função `triggerView()`. Use nomes simples, claros e exclusivos para facilitar a seleção no Visual Experience Composer do Target.
* Você pode acionar exibições em pequenas alterações de exibição, bem como em contextos não SPA, como na metade de uma página de rolagem infinita.
* O `at.js` 2.0 e o `triggerView()` podem ser implementados por meio de uma solução de gerenciamento de marcas, como o Adobe Experience Platform Launch.

## Limitações da at.js 2.0

Esteja ciente das seguintes limitações do `at.js` 2.0 antes da atualização:

* O rastreamento entre domínios não tem suporte no `at.js` 2.0
* Os parâmetros de URL mboxOverride.browserIp e mboxSession não têm suporte no `at.js` 2.0
* As funções herdadas mboxCreate, mboxDefine e mboxUpdate foram descontinuadas em `at.js` 2.0. O conteúdo padrão será exibido e nenhuma solicitação de rede será feita.

## Código do rodapé da biblioteca usado no vídeo

O código abaixo foi adicionado à seção Rodapé da biblioteca da biblioteca `at.js` durante o vídeo. Ele é acionado quando o aplicativo é carregado pela primeira vez e, em seguida, em qualquer alteração de hash no aplicativo. Ele usa uma versão limpa do hash como o nome da exibição e &quot;inicial&quot; quando o hash está vazio. Observe que para identificar o SPA, o código procura pelo texto &quot;react/&quot; no URL, que provavelmente precisará ser atualizado no site. Lembre-se também de que pode ser mais apropriado para seu SPA acionar o `triggerView()` fora dos eventos personalizados ou incorporando o código diretamente no aplicativo.

```javascript
function sanitizeViewName(viewName) {
  if (viewName.startsWith('#')) {
    viewName = viewName.substr(1);
  }
  if (viewName.startsWith('/')) {
    viewName = viewName.substr(1);
  }
  return viewName;
}
function triggerView(viewName) {
  viewName = sanitizeViewName(viewName) || 'home';
  // Validate if the Target Libraries are available on your website
  if (typeof adobe != 'undefined' && adobe.target && typeof adobe.target.triggerView === 'function') {
    adobe.target.triggerView(viewName);
    console.log('AT: View triggered on page load: '+viewName)
  }
}
//fire triggerView when the SPA loads and when the hash changes in the SPA
if(window.location.pathname.indexOf('react/') >-1){
    triggerView(location.hash);
}
window.onhashchange = function() {
    if(window.location.pathname.indexOf('react/') >-1){
        triggerView(location.hash);
    }
}
```

## Recursos adicionais

* [Noções básicas sobre o funcionamento da at.js 2.0 (Diagramas de arquitetura)](understanding-how-atjs-20-works.md)
* [Usar o Visual Experience Composer do Adobe Target para aplicativos de página única (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
