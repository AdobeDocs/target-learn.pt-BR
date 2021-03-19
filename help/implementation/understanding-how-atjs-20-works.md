---
title: Como funciona a at.js 2.0?
description: O at.js 2.0 aprimora o suporte da Adobe Target para aplicativos de página única (SPA) e integra-se com outras soluções do Experience Cloud. Este vídeo e os diagramas que o acompanham explicam como tudo se une.
role: Desenvolvedor
level: Intermediário
topic: SPA, arquitetura, desenvolvimento
feature: Implementação
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 21%

---


# Noções básicas sobre o funcionamento da at.js 2.0 no Adobe Target

`at.js` 2.0 aprimora o suporte da Adobe Target para aplicativos de página única (SPA) e integra-se com outras soluções do Experience Cloud. Este vídeo e os diagramas que o acompanham explicam como tudo se une.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## Diagramas de arquitetura

![Comportamento do at.js 2.0 no carregamento da página](assets/pageload.png)

1. A chamada retorna Experience Cloud ID (ECID). Se o usuário estiver autenticado, outra chamada sincroniza a ID do cliente.

1. `at.js` A biblioteca é carregada de forma síncrona e oculta o corpo do documento (também `at.js` pode ser carregado de forma assíncrona com um trecho opcional de pré-ocultação implementado na página).

1. A solicitação de Carregamento de página é feita incluindo todos os parâmetros configurados, ECID, SDID e ID do cliente.

1. Os scripts de perfil executam e fazem o feed no [!UICONTROL Armazenamento de perfil]. A Loja solicita públicos qualificados da [!UICONTROL Biblioteca de público-alvo] (por exemplo, públicos-alvo compartilhados de [!DNL Analytics], Audience Manager etc). [!UICONTROL Os ] atributos do cliente são enviados para o  [!UICONTROL Profile ] Store em um processo em lote.
1. Com base no URL, nos parâmetros de solicitação e nos dados do perfil, [!DNL Target] decide quais Atividades e Experiências retornarão ao visitante para a página atual e para as exibições futuras

1. O conteúdo direcionado foi enviado de volta à página, incluindo, opcionalmente, valores de perfil para personalização adicional.

   O conteúdo direcionado na página atual é revelado o mais rápido possível sem cintilação do conteúdo padrão.

   O conteúdo direcionado para futuras exibições de um aplicativo de página única é armazenado em cache no navegador, portanto, pode ser aplicado instantaneamente, sem uma chamada de servidor adicional, quando as exibições forem acionadas. (Consulte o diagrama a seguir para conhecer o comportamento `triggerView()`).

1. [!DNL Analytics] dados enviados da página para o  [!UICONTROL Data ] CollectionServers
1. [!DNL Target]Os dados do são correspondidos aos dados do pela SDID, e processados no armazenamento de relatório do Analytics.[!DNL Analytics] [!DNL Analytics] Os dados podem ser exibidos no  [!DNL Analytics] e  [!DNL Target] por meio dos relatórios do A4T.

![O comportamento da at.js 2.0 quando a função triggerView() é usada](assets/triggerview.png)

1. `adobe.target.triggerView()` é chamado no aplicativo de página única
1. O conteúdo direcionado para a exibição é lido do cache

1. O conteúdo direcionado é revelado o mais rápido possível sem oscilação do conteúdo padrão

1. A solicitação de notificação é enviada para a [!DNL Target] Loja de perfil para contar o visitante nas métricas de atividade e incremento
1. [!DNL Analytics] Os dados são enviados do SPA para o  [!UICONTROL Data ] CollectionServers

1. [!DNL Target] Os dados são enviados do  [!DNL Target] backend para o  [!UICONTROL Data ] CollectionServers. Os dados do [!DNL Target] são correspondidos aos dados do [!DNL Analytics] pela SDID, e processados no armazenamento de relatório do [!DNL Analytics]. [!DNL Analytics] Os dados podem ser exibidos no  [!DNL Analytics] e  [!DNL Target] por meio dos relatórios do A4T.

## Recursos adicionais

* [Implementar a at.js 2.0 em um aplicativo de página única](implement-atjs-20-in-a-single-page-application.md)
* [Usar o Adobe Target Visual Experience Composer para aplicativos de página única (VEC SPA)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [Como a at.js funciona na documentação](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/at-js/how-atjs-works.html)