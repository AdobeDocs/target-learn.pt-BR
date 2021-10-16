---
title: Como implementar o at.js 2.0 em um aplicativo de página única (SPA)
description: A Adobe Target at.js 2.0 fornece conjuntos de recursos avançados que fazem com que sua empresa execute personalização em tecnologias de próxima geração no lado do cliente. Siga estas etapas para implementar o at.js 2.0 em um aplicativo de página única (SPA).
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 955f0571-5791-4dbb-9931-e6d5c8bb42a7
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# Implementar o Adobe Target o at.js 2.0 em um aplicativo de página única (SPA)

O Adobe Target `at.js` 2.0 fornece conjuntos de recursos avançados que fazem com que sua empresa execute a personalização em tecnologias de próxima geração no lado do cliente. Essa versão tem como foco a atualização `at.js` para ter interações harmoniosas com aplicativos de página única (SPA).

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## Como implementar o at.js 2.0 em uma SPA

* Implemente `at.js` 2.0 no &lt;head> do Aplicativo de página única.
* Implemente a função `adobe.target.triggerView()` sempre que a exibição for alterada no SPA. Várias técnicas podem ser empregadas para fazer isso, como acompanhar alterações de hash de URL, ouvir eventos personalizados acionados por seu SPA ou incorporar o código `triggerView()` diretamente em seu aplicativo. Você deve escolher a opção que funciona melhor para seu aplicativo de página única específico.
* O nome da exibição é o primeiro parâmetro da função `triggerView()`. Use nomes simples, claros e exclusivos para facilitar a seleção no Visual Experience Composer do Target.
* Você pode acionar visualizações em pequenas alterações de visualização, bem como em contextos não SPA, como no meio de uma página de rolagem infinita.
* `at.js` O 2.0 e  `triggerView()` podem ser implementados por meio de uma solução de gerenciamento de tags, como o Adobe Experience Platform Launch.

## Limitações do at.js 2.0

Esteja ciente das seguintes limitações de `at.js` 2.0 antes de atualizar:

* O rastreamento entre domínios não é suportado em `at.js` 2.0
* Os parâmetros de URL mboxOverride.browserIp e mboxSession não são suportados em `at.js` 2.0
* As funções herdadas mboxCreate, mboxDefine, mboxUpdate estão obsoletas em `at.js` 2.0. O conteúdo padrão será exibido e nenhuma solicitação de rede será feita.

## Código do rodapé da biblioteca usado no vídeo

O código abaixo foi adicionado à seção Rodapé da biblioteca `at.js` durante o vídeo. Ele é acionado quando o aplicativo é carregado pela primeira vez e, em seguida, em qualquer alteração de hash no aplicativo. Ele usa uma versão limpa do hash como o nome da exibição e &quot;inicial&quot; quando o hash está vazio. Observe que para identificar o SPA, o código busca o texto &quot;response/&quot; no URL, que provavelmente precisará ser atualizado em seu site. Lembre-se também de que pode ser mais apropriado que seu SPA acione `triggerView()` de eventos personalizados ou incorporando o código diretamente no aplicativo.

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

* [Como entender o funcionamento da at.js 2.0 (diagramas de arquitetura)](understanding-how-atjs-20-works.md)
* [Usar o Adobe Target Visual Experience Composer para aplicativos de página única (VEC SPA)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [Atualização da documentação da at.js 1.x para at.js 2.0](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/upgrading-from-atjs-1x-to-atjs-20.html?lang=en)
