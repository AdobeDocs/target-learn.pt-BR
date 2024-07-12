---
title: O que é a API do Adobe Recommendations?
description: Este tutorial orienta os desenvolvedores na prática usando as APIs do Adobe Target Recommendations para configurar e gerenciar catálogos e critérios personalizados do Recommendations, bem como usar a API de entrega para recuperar o conteúdo das recomendações.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 10f80056-fb71-4362-86bc-d161f596cb91
source-git-commit: 542ff406fc24df54a2f1b007422492341ea46507
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 2%

---

# Visão geral da API do Adobe Recommendations

As APIs relevantes para [!DNL Recommendations] incluem [APIs de administrador](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) que permitem:

* Gerencie seu catálogo de produtos ou conteúdo recomendáveis
* Gerencie seus algoritmos e atividades do [!DNL Recommendations]

Usando a [!DNL Target] [API de entrega](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) com o Recommendations, você também pode:

* Recupere recomendações em objetos JSON, HTML ou XML para que elas possam ser exibidas na Web, em dispositivos móveis, em emails, na Internet das Coisas (IOT) e em outros canais.

## Descrição do tutorial

Este tutorial orienta os desenvolvedores pela prática do uso das APIs do [!DNL Recommendations] para configurar e gerenciar catálogos e critérios personalizados do [!DNL Recommendations], além de usar a API de entrega para recuperar o conteúdo das recomendações. Ao final deste tutorial, você será capaz de:

* Configurar e gerenciar entidades usando a API do Recommendations
* Configurar e gerenciar critérios personalizados usando a API do Recommendations
* Entenda como usar o Recommendations com a API de entrega para usar os resultados das recomendações em dispositivos não HTML

## Público-alvo

Este tutorial destina-se a desenvolvedores novos nas APIs do Target ou nas APIs do Recommendations.

## Pré-requisitos

O uso das APIs de administrador do Target requer [configuração de autenticação de Adobe](https://experienceleague.adobe.com/docs/target-dev/developer/api/configure-authentication.html?lang=pt-BR){target="_blank"}. Verifique se você configurou este tutorial antes de iniciá-lo.

## Recursos

Observe os seguintes recursos, que são necessários para entender este tutorial e segui-lo com êxito:

| Recurso | Detalhes |
| --- | --- |
| Postman | Obtenha o [aplicativo Postman](https://www.postman.com/downloads/) para seu sistema operacional. O Postman Basic é gratuito com a criação da conta. Embora não seja necessário para usar as APIs do Adobe Target em geral, o Postman facilita os fluxos de trabalho da API, e a Adobe Target fornece várias coleções do Postman para ajudar a executar suas APIs e saber como elas operam. O restante deste tutorial pressupõe conhecimento prático do Postman. Para obter ajuda, consulte a [documentação do Postman](https://learning.getpostman.com/). |
| Referências | A familiaridade com os seguintes recursos é assumida durante o restante deste tutorial:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentação do Target Adobe I/O](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentação da API do Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[Próximo &quot;Gerenciar seu Catálogo do Recommendations&quot; >](https://experienceleague.adobe.com/docs/target-dev/developer/api/recommendations-api/manage-catalog.html){target="_blank"}
