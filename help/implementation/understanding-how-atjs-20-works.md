---
title: Como funciona o Adobe Target at.js 2.0
seo-title: Como funciona o Adobe Target at.js 2.0
description: O at.js 2.0 aprimora o suporte da Adobe Target para aplicativos de página única (SPA) e se integra a outras soluções de Experience Cloud. Este vídeo e os diagramas que o acompanham explicam como tudo se junta.
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


# Como funciona o Adobe Target at.js 2.0

`at.js` 2.0 aprimora o suporte da Adobe Target para aplicativos de página única (SPA) e integra-se a outras soluções de Experience Cloud. Este vídeo e os diagramas que o acompanham explicam como tudo se junta.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## Diagramas de arquitetura

![comportamento do at.js 2.0 no carregamento da página](assets/pageload.png)

1. A chamada retorna a ID de Experience Cloud (ECID). Se o usuário estiver autenticado, outra chamada sincronizará a ID do cliente.

1. `at.js` a biblioteca é carregada de forma síncrona e oculta o corpo do documento (também `at.js` pode ser carregada de forma assíncrona com um trecho opcional de pré-ocultação implementado na página).

1. A solicitação de carregamento da página é feita incluindo todos os parâmetros configurados, ECID, SDID e ID do cliente.

1. Os scripts de perfil são executados e alimentados na [!UICONTROL Loja de Perfis]. A Loja solicita audiências qualificadas da [!UICONTROL Biblioteca de Audiências] (por exemplo, audiências compartilhadas de [!DNL Analytics], Audience Manager etc). [!UICONTROL Os ] Atributos do cliente são enviados para o  [!UICONTROL Perfil ] Store em um processo em lote.
1. Com base no URL, nos parâmetros de solicitação e nos dados do perfil, [!DNL Target] decide quais Atividades e Experiências retornar ao visitante da página atual e visualizações futuras

1. Conteúdo direcionado enviado de volta para a página, incluindo opcionalmente valores de perfil para personalização adicional.

   O conteúdo direcionado na página atual é revelado o mais rápido possível sem cintilação do conteúdo padrão.

   O conteúdo direcionado para futuras visualizações de um aplicativo de página única é armazenado em cache no navegador, portanto, pode ser aplicado instantaneamente sem uma chamada de servidor adicional quando as visualizações são acionadas. (Consulte o diagrama a seguir para ver o comportamento `triggerView()`).

1. [!DNL Analytics] dados enviados da página para  [!UICONTROL Data ] CollectionServers
1. [!DNL Target]Os dados do são correspondidos aos dados do pela SDID, e processados no armazenamento de relatório do Analytics.[!DNL Analytics] [!DNL Analytics] os dados podem então ser visualizados nos relatórios A4T  [!DNL Analytics] e  [!DNL Target] por meio deles.

![comportamento do at.js 2.0 quando a função triggerView() é usada](assets/triggerview.png)

1. `adobe.target.triggerView()` é chamado no aplicativo de página única
1. O conteúdo direcionado para a exibição é lido do cache

1. O conteúdo direcionado é revelado o mais rápido possível sem oscilação do conteúdo padrão

1. A solicitação de notificação é enviada para a [!DNL Target] Loja de perfil para contar o visitante nas métricas de atividade e incremento
1. [!DNL Analytics] os dados são enviados do SPA para  [!UICONTROL Data ] CollectionServers

1. [!DNL Target] os dados são enviados do  [!DNL Target] backend para o  [!UICONTROL Data ] CollectionServers. Os dados do [!DNL Target] são correspondidos aos dados do [!DNL Analytics] pela SDID, e processados no armazenamento de relatório do [!DNL Analytics]. [!DNL Analytics] os dados podem então ser visualizados nos relatórios A4T  [!DNL Analytics] e  [!DNL Target] por meio deles.

## Recursos adicionais

* [Implementação do at.js 2.0 em um aplicativo de página única](implement-atjs-20-in-a-single-page-application.md)
* [Usar o Visual Experience Composer Adobe Target para aplicativos de página única (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [Como o at.js funciona na documentação](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/at-js/how-atjs-works.html)