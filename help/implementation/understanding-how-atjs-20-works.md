---
title: Como funciona o Adobe Target.js 2.0
seo-title: Como funciona o Adobe Target.js 2.0
description: O at.js 2.0 aprimora o suporte a Adobe Target para aplicativos de página única (SPA) e se integra a outras soluções de Experience Cloud. Este vídeo e os diagramas que o acompanham explicam como tudo se junta.
audience: developer
difficulty: 3
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: 37443ae4c1cdda387c8db0053201d520fa1ec224
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 20%

---


# Como funciona o Adobe Target.js 2.0

`at.js` 2.0 aprimora o suporte ao Adobe Target para aplicativos de página única (SPA) e integra-se a outras soluções de Experience Cloud. Este vídeo e os diagramas que o acompanham explicam como tudo se junta.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## Diagramas de arquitetura

![comportamento do at.js 2.0 no carregamento da página](assets/pageload.png)

1. A chamada retorna a ID de Experience Cloud (ECID). Se o usuário estiver autenticado, outra chamada sincronizará a ID do cliente.

1. `at.js` a biblioteca é carregada de forma síncrona e oculta o corpo do documento (`at.js` também pode ser carregada de forma assíncrona com um trecho opcional de pré-ocultação implementado na página).

1. A solicitação de carregamento da página é feita incluindo todos os parâmetros configurados, ECID, SDID e ID do cliente.

1. Profile scripts execute and feed into the [!UICONTROL Profile Store]. The Store requests qualified audiences from the [!UICONTROL Audience Library] (e.g. audiences shared from [!DNL Analytics], Audience Manager, etc). [!UICONTROL Os Atributos] do cliente são enviados para a Loja de [!UICONTROL Perfis] em um processo em lote.
1. Based on URL, request parameters, and profile data, [!DNL Target] decides which Activities and Experiences to return to the visitor for the current page and future views

1. Conteúdo direcionado enviado de volta para a página, incluindo opcionalmente valores de perfil para personalização adicional.

   O conteúdo direcionado na página atual é revelado o mais rápido possível sem cintilação do conteúdo padrão.

   O conteúdo direcionado para futuras visualizações de um aplicativo de página única é armazenado em cache no navegador, portanto, pode ser aplicado instantaneamente sem uma chamada de servidor adicional quando as visualizações são acionadas. (Consulte o diagrama a seguir para ver o `triggerView()` comportamento).

1. [!DNL Analytics] dados enviados da página para os servidores de coleta [!UICONTROL de] dados
1. [!DNL Target]Os dados do são correspondidos aos dados do pela SDID, e processados no armazenamento de relatório do Analytics.[!DNL Analytics] [!DNL Analytics] os dados podem então ser visualizados tanto [!DNL Analytics] como [!DNL Target] por meio de relatórios A4T.

![comportamento do at.js 2.0 quando a função triggerView() é usada](assets/triggerview.png)

1. `adobe.target.triggerView()` é chamado no aplicativo de página única
1. O conteúdo direcionado para a exibição é lido do cache

1. O conteúdo direcionado é revelado o mais rápido possível sem oscilação do conteúdo padrão

1. A solicitação de notificação é enviada para a [!DNL Target] Loja de perfil para contar o visitante nas métricas de atividade e incremento
1. [!DNL Analytics] os dados são enviados do SPA para os Servidores de Coleta [!UICONTROL de] Dados

1. [!DNL Target] os dados são enviados do back-end [!DNL Target] para os Servidores de Coleta [!UICONTROL de] Dados. Os dados do [!DNL Target] são correspondidos aos dados do [!DNL Analytics] pela SDID, e processados no armazenamento de relatório do [!DNL Analytics]. [!DNL Analytics] os dados podem então ser visualizados tanto [!DNL Analytics] como [!DNL Target] por meio de relatórios A4T.

## Recursos adicionais

* [Implementação do at.js 2.0 em um aplicativo de página única](implement-atjs-20-in-a-single-page-application.md)
* [Usar o Visual Experience Composer para Aplicativos de Página Única (SPA)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [Como o at.js funciona na documentação](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/at-js/how-atjs-works.html)