---
title: Como usar provedores de dados para integrar dados de terceiros
description: Este tutorial apresenta aos usuários os provedores de dados. Saiba como usar o recurso Provedores de dados para transmitir dados facilmente de terceiros para o Adobe Target.
role: User, Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: feature video
kt:
author: Daniel Wright
exl-id: 1892136e-14e3-4e52-8b1f-aee806d2f83a
TQID: 'https://experienceleague.adobe.com/XiUlJGHSFVxAMqdl6Y7hK9PoXOgiiUI43vrFeAj2Rpo'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
    internal-label: Audiences
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
    internal-label: Integrations
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
    internal-label: at.js
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
    internal-label: Experienced
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: d11449f8685d14c2bbd1e70f80711d4edab9d3a1
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 16%
---
# Usar provedores de dados para integrar dados de terceiros ao Adobe Target

[!UICONTROL Os Provedores de Dados] são um recurso que permite passar dados facilmente de terceiros para o Target.  Um terceiro pode ser um serviço de clima, um DMP ou até mesmo o seu próprio serviço Web. É possível então usar esses dados para criar públicos-alvo, conteúdo de direcionamento e enriquecer o perfil do visitante.

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## Como usar provedores de dados

1. O especialista em implementação adiciona o código antes da at.js (ou na seção Cabeçalho da biblioteca da at.js) que faz a chamada da API para terceiros, analisa a resposta e especifica com pares de nome/valor da resposta para enviar para [!DNL Target].
1. A at.js gerencia a cintilação e inclui os pares nome/valor como parâmetros personalizados na solicitação global do Target.
1. O profissional de marketing cria públicos-alvo na interface [!DNL Target] com base nesses parâmetros personalizados.
1. O profissional de marketing usa esses públicos para direcionar experiências, atividades e métricas, bem como para públicos-alvo de relatórios.

>[!NOTE]
>
>[!UICONTROL Provedores de dados] exigem at.js 1.3 ou superior

## Materiais de suporte

* [Implementar provedores de dados na at.js e no Adobe Target](implement-data-providers-to-integrate-third-party-data.md)
