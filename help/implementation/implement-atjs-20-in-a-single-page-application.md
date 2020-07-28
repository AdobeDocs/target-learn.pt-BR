---
title: Implementação do Adobe Target em SPA (Single Page Application)
seo-title: Implementação do Adobe Target em SPA (Single Page Application)
description: A versão mais recente da at.js fornece conjuntos de recursos avançados que fazem com que sua empresa execute personalização em tecnologias de próxima geração e cliente. Essa nova versão tem como foco a atualização da at.js para ter interações harmoniosas com aplicativos de página única (SPAs).
audience: developer
difficulty: 3
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: 37443ae4c1cdda387c8db0053201d520fa1ec224
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 8%

---


# Implementação do Adobe Target em SPA (Single Page Application)

The newest version of `at.js` provides rich feature sets that equip your business to execute personalization on next-generation, client-side technologies. This new version is focused on upgrading `at.js` to have harmonious interactions with single page applications (SPAs).

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## Como implementar o at.js 2.0 em um SPA

* Implemente `at.js` 2.0 em &lt;head> do aplicativo de página única.
* Implemente a `adobe.target.triggerView()` função sempre que a visualização for alterada em seu SPA. Várias técnicas podem ser empregadas para fazer isso, como acompanhar alterações de hash de URL, acompanhar eventos personalizados acionados pelo SPA ou incorporar o `triggerView()` código diretamente ao aplicativo. Você deve escolher a opção que funciona melhor para seu aplicativo de página única específico.
* O nome da visualização é o primeiro parâmetro da `triggerView()` função. Use nomes simples, claros e exclusivos para facilitar a seleção no Criador de experiências visuais do Público alvo.
* Você pode acionar visualizações em pequenas alterações de visualização, bem como em contextos não SPA, como meio caminho para baixo em uma página de rolagem infinita.
* `at.js` 2.0 e `triggerView()` pode ser implementado por meio de uma solução de gerenciamento de tags, como a Adobe Experience Platform Launch.

## Limitações do at.js 2.0

Esteja ciente das seguintes limitações do `at.js` 2.0 antes de atualizar:

* O rastreamento entre domínios não é compatível com `at.js` 2.0
* Os parâmetros de URL mboxOverride.browserIp e mboxSession não são suportados em `at.js` 2.0
* As funções herdadas mboxCreate, mboxDefine, mboxUpdate estão obsoletas em `at.js` 2.0. O conteúdo padrão será exibido e nenhuma solicitação de rede será feita.

## Código do rodapé da biblioteca usado no vídeo

O código abaixo foi adicionado à seção Rodapé da biblioteca da `at.js` biblioteca durante o vídeo. Ele é acionado quando o aplicativo é carregado pela primeira vez e, em seguida, em qualquer alteração de hash no aplicativo. Ele usa uma versão limpa do hash como nome da visualização e &quot;início&quot; quando o hash está vazio. Observe que para identificar o SPA, o código procura o texto &quot;response/&quot; no URL, que provavelmente precisará ser atualizado em seu site. Lembre-se também de que pode ser mais apropriado para o SPA desligar `triggerView()` de eventos personalizados ou incorporar o código diretamente ao aplicativo.

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

* [Como funciona o at.js 2.0 (diagramas de arquitetura)](understanding-how-atjs-20-works.md)
* [Usar o Visual Experience Composer para Aplicativos de Página Única (SPA)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [Atualização da documentação do at.js 1.x para o at.js 2.0](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/upgrading-from-atjs-1x-to-atjs-20.html)