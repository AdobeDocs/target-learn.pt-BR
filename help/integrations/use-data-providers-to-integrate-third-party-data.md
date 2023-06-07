---
title: Como usar provedores de dados para integrar dados de terceiros
description: Este tutorial apresenta aos usuários os provedores de dados. Saiba como usar o recurso Provedores de dados para transmitir dados facilmente de terceiros para o Adobe Target.
role: User, Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: feature video
kt: null
author: Daniel Wright
exl-id: 1892136e-14e3-4e52-8b1f-aee806d2f83a
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 25%

---

# Usar provedores de dados para integrar dados de terceiros ao Adobe Target

[!UICONTROL Os provedores de dados são uma função que permite passar dados de terceiros facilmente para o Target.]  Um terceiro pode ser um serviço de clima, um DMP ou até mesmo o seu próprio serviço Web. É possível então usar esses dados para criar públicos-alvo, conteúdo de direcionamento e enriquecer o perfil do visitante.

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## Como usar provedores de dados

1. O especialista em implementação adiciona o código antes da at.js (ou na seção Cabeçalho da biblioteca da at.js) que faz a chamada da API para o terceiro, analisa a resposta e especifica com pares de nome/valor da resposta para enviar para o [!DNL Target].
1. A at.js gerencia a cintilação e inclui os pares nome/valor como parâmetros personalizados na solicitação global do Target.
1. O profissional de marketing cria públicos-alvo na [!DNL Target] com base nesses parâmetros personalizados.
1. O profissional de marketing usa esses públicos para direcionar experiências, atividades e métricas, bem como para públicos-alvo de relatórios.

>[!NOTE]
>
>[!UICONTROL Provedores de dados] requer at.js 1.3 ou superior

## Materiais de suporte

* [Implementar provedores de dados na at.js e no Adobe Target](implement-data-providers-to-integrate-third-party-data.md)
