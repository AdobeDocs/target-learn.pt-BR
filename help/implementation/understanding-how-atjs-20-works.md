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
source-wordcount: '412'
ht-degree: 22%

---

# Noções básicas sobre o funcionamento da at.js 2.0 do Adobe Target

`at.js` A versão 2.0 aprimora o suporte da Adobe Target para aplicativos de página única (SPA) e integra-se com outras soluções de Experience Cloud. Este vídeo e os diagramas que o acompanham explicam como tudo se une.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## Diagramas de arquitetura

![Comportamento da at.js 2.0 no carregamento da página](assets/pageload.png)

1. A chamada retorna a ID de Experience Cloud (ECID). Se o usuário for autenticado, outra chamada sincroniza a ID do cliente.

1. `at.js` A biblioteca é carregada de forma síncrona e oculta o corpo do documento (`at.js` O também pode ser carregado de forma assíncrona com uma opção de pré-ocultação de trecho implementada na página).

1. A solicitação de Carregamento de página é feita, incluindo todos os parâmetros configurados, ECID, SDID e ID do cliente.

1. Os scripts de perfil executam e fazem o feed na [!UICONTROL Loja de perfis]. A Loja solicita públicos qualificados da [!UICONTROL Biblioteca de público-alvo] (por exemplo, públicos-alvo compartilhados de [!DNL Analytics], Audience Manager, etc.). [!UICONTROL Atributos do cliente] são enviados para [!UICONTROL Loja de perfis] em um processo em lote.
1. Com base no URL, parâmetros de solicitação e dados de perfil, [!DNL Target] decide quais Atividades e Experiências retornarão ao visitante para a página atual e para as exibições futuras

1. O conteúdo direcionado é enviado de volta para a página, opcionalmente incluindo valores de perfil para personalização adicional.

   O conteúdo direcionado na página atual é revelado o mais rápido possível sem cintilação do conteúdo padrão.

   O conteúdo direcionado para exibições futuras de um aplicativo de página única é armazenado em cache no navegador para que possa ser aplicado instantaneamente, sem uma chamada de servidor adicional, quando as exibições forem acionadas. (Consulte o próximo diagrama para `triggerView()` comportamento).

1. [!DNL Analytics] dados enviados da página para a [!UICONTROL Coleta de dados] Servidores
1. [!DNL Target]Os dados do são correspondidos aos dados do pela SDID, e processados no armazenamento de relatório do Analytics.[!DNL Analytics] [!DNL Analytics] os dados podem ser exibidos em [!DNL Analytics] e [!DNL Target] pelos relatórios do A4T.

![Comportamento da at.js 2.0 quando a função triggerView() é usada](assets/triggerview.png)

1. `adobe.target.triggerView()` é chamado no aplicativo de página única
1. O conteúdo direcionado para a exibição é lido do cache

1. O conteúdo direcionado é revelado o mais rápido possível sem oscilação do conteúdo padrão

1. A solicitação de notificação é enviada para a [!DNL Target] Loja de perfil para contar o visitante nas métricas de atividade e incremento
1. [!DNL Analytics] Os dados do são enviados do SPA para o [!UICONTROL Coleta de dados] Servidores

1. [!DNL Target] Os dados do são enviados do [!DNL Target] back-end para o [!UICONTROL Coleta de dados] Servidores. Os dados do [!DNL Target] são correspondidos aos dados do [!DNL Analytics] pela SDID, e processados no armazenamento de relatório do [!DNL Analytics]. [!DNL Analytics] os dados podem ser exibidos em [!DNL Analytics] e [!DNL Target] pelos relatórios do A4T.

## Recursos adicionais

* [Implementar a at.js 2.0 em um aplicativo de página única](implement-atjs-20-in-a-single-page-application.md)
* [Usar o Visual Experience Composer do Adobe Target para aplicativos de página única (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
