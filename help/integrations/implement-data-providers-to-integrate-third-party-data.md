---
title: Implementação de provedores de dados para integrar dados de terceiros à Adobe Target
seo-title: Implementação de provedores de dados para integrar dados de terceiros à Adobe Target
description: Detalhes da implementação e exemplos de como usar o recurso Provedores de dados da Adobe Target para recuperar dados de provedores de dados de terceiros e passá-los na solicitação do Público alvo.
audience: developer
difficulty: 5
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: 37443ae4c1cdda387c8db0053201d520fa1ec224
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# Implemente [!UICONTROL Provedores de dados] para integrar dados de terceiros ao Adobe Target

Detalhes de implementação e exemplos de como usar o recurso [!UICONTROL Provedores de dados] da Adobe Target para recuperar dados de provedores de dados de terceiros e passá-los na solicitação de Público alvo.

>[!NOTE]
>
>[!UICONTROL Os ] provedores de dados exigem  `at.js` 1.3 ou superior

## Implementação dos componentes básicos dos provedores de dados

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

Uma rápida visão geral dos componentes básicos de `dataProvider` e como colocar o código na ordem correta.\
Um exemplo de trabalho com o código usado no vídeo pode ser encontrado aqui:
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## Integrar com uma API de terceiros

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

Um exemplo mais realista, integrando uma API do tempo.\
Um exemplo de trabalho com o código usado no vídeo pode ser encontrado aqui:
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## Integrar com vários provedores

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

Como incorporar dados de vários provedores à solicitação global [!DNL Target].\
Um exemplo de trabalho com o código usado no vídeo pode ser encontrado aqui:
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## Minimizar o impacto no carregamento da página

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

Minimize o impacto no tempo de carregamento da página armazenando dados em um objeto de armazenamento de sessão. Como alternativa, você pode passar os valores como parâmetros de perfil usando o prefixo `profile.` e passá-los na primeira solicitação [!DNL Target] da sessão. No entanto, você estaria limitado a passar cinquenta parâmetros de perfil por solicitação.

Um exemplo de trabalho com o código usado no vídeo pode ser encontrado aqui: [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## Materiais de suporte

* [Usar provedores de dados com a Adobe Target](use-data-providers-to-integrate-third-party-data.md)

* [Documentação dos provedores de dados](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)