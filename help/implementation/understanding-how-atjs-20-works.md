---
title: Como a at.js 2.0 funciona?
description: A at.js 2.0 aprimora o suporte da Adobe Target para aplicativos de página única (SPA) e integra-se com outras soluções de Experience Cloud. Este vídeo e os diagramas que o acompanham explicam como tudo se une.
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 7f037665-88a7-469c-8df5-c82cb0f65382
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Noções básicas sobre o funcionamento da at.js 2.0 do Adobe Target

O `at.js` 2.0 aprimora o suporte da Adobe Target para aplicativos de página única (SPA) e integra-se com outras soluções de Experience Cloud. Este vídeo e os diagramas que o acompanham explicam como tudo se une.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## Diagramas de arquitetura

Comportamento do ![at.js 2.0 no carregamento da página](assets/pageload.png)

1. A chamada retorna a ID de Experience Cloud (ECID). Se o usuário for autenticado, outra chamada sincroniza a ID do cliente.

1. A biblioteca `at.js` é carregada de forma síncrona e oculta o corpo do documento (`at.js` também pode ser carregado de forma assíncrona com um trecho oculto previamente implementado na página).

1. A solicitação de Carregamento de página é feita, incluindo todos os parâmetros configurados, ECID, SDID e ID do cliente.

1. Os scripts de perfil executam e alimentam o [!UICONTROL Profile Store]. A Loja solicita públicos qualificados do [!UICONTROL Audience Library] (por exemplo, públicos compartilhados de [!DNL Analytics], Audience Manager, etc.). [!UICONTROL Customer Attributes] são enviados a [!UICONTROL Profile Store] em um processo em lote.
1. Com base na URL, parâmetros de solicitação e dados de perfil, [!DNL Target] decide quais Atividades e Experiências retornarão ao visitante para a página atual e para as exibições futuras

1. O conteúdo direcionado é enviado de volta para a página, opcionalmente incluindo valores de perfil para personalização adicional.

   O conteúdo direcionado na página atual é revelado o mais rápido possível sem cintilação do conteúdo padrão.

   O conteúdo direcionado para exibições futuras de um aplicativo de página única é armazenado em cache no navegador para que possa ser aplicado instantaneamente, sem uma chamada de servidor adicional, quando as exibições forem acionadas. (Veja o próximo diagrama para o comportamento de `triggerView()`).

1. Dados do [!DNL Analytics] enviados da página para os [!UICONTROL Data Collection] Servidores
1. Os dados do [!DNL Target] são correspondidos aos dados do Analytics pela SDID e processados no armazenamento de relatórios do [!DNL Analytics]. Os dados do [!DNL Analytics] podem ser exibidos em [!DNL Analytics] e [!DNL Target] pelos relatórios do A4T.

Comportamento do ![at.js 2.0 quando a função triggerView() é usada](assets/triggerview.png)

1. `adobe.target.triggerView()` é chamado no aplicativo de página única
1. O conteúdo direcionado para a exibição é lido do cache

1. O conteúdo direcionado é revelado o mais rápido possível sem cintilação do conteúdo padrão

1. A solicitação de notificação é enviada para [!DNL Target] [!UICONTROL Profile Store] para contar o visitante nas métricas de atividade e incremento
1. Os dados do [!DNL Analytics] são enviados do SPA para os [!UICONTROL Data Collection] servidores

1. Os dados do [!DNL Target] são enviados do back-end do [!DNL Target] para os Servidores do [!UICONTROL Data Collection]. Os dados do [!DNL Target] são correspondidos aos dados do [!DNL Analytics] por meio da SDID e processados no armazenamento de relatórios do [!DNL Analytics]. Os dados do [!DNL Analytics] podem ser exibidos em [!DNL Analytics] e [!DNL Target] pelos relatórios do A4T.

## Recursos adicionais

* [Implementar a at.js 2.0 em um aplicativo de página única](implement-atjs-20-in-a-single-page-application.md)
* [Usar o Visual Experience Composer do Adobe Target para aplicativos de página única (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
