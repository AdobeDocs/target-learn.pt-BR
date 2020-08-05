---
title: Visão geral da API do Adobe Target
keywords: recommendations;adobe recommendations;premium;api;apis
description: A Adobe Target Recommendations inclui um conjunto dedicado de APIs que permitem gerenciar seu catálogo de produtos e/ou conteúdo recomendáveis; gerenciar seus algoritmos e campanhas de recomendações; e fornecer recomendações em objetos JSON, HTML ou XML a serem exibidos em Web, dispositivos móveis, email, IOT e outros canais.
kt: null
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: b66dbae616c9559f5d1b7bbedf2d9b383840973b
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---


# Visão geral da API do Adobe Target

As APIs do Adobe Target podem ser agrupadas de acordo com o tipo.

| Tipo de API | O que ele permite fazer | Link de download |
| --- | --- | --- |
| Admin | Crie, modifique e exclua atividades, audiências, ofertas e outros objetos (incluindo [!DNL Recommendations] entidades, critérios, designs e assim por diante). As [!DNL Recommendations] APIs são um tipo de API de administração.) | <UL><li>[Coleção Postman da API do administrador do Público alvo](https://developers.adobetarget.com/api/#admin-postman-collection)</li><li>[Coleção Recommendations API Postman](https://developers.adobetarget.com/api/recommendations/#section/Postman)</li></ul> |
| Entrega | Recupere conteúdo otimizado e personalizado de [!DNL Target] delivery para usuário final. | [Coleção Postman da API do Delivery do Público alvo](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection) |
| Relatório | Exporte os resultados da atividade e outros resultados do relatórios. | As APIs de Relatórios estão incluídas na coleção [Postman da API de administração de](https://developers.adobetarget.com/api/#admin-postman-collection)Públicos alvos. |
| Perfil | Recupere e modifique perfis de usuário armazenados no Adobe Target. | [Coleção Postman da API do Perfil do Público alvo](https://developers.adobetarget.com/api/#profiles) |

Observe a distinção entre APIs **de** administração (incluindo as [!DNL Recommendations] APIs), que permite configurar vários aspectos do Adobe Target, em comparação às APIs **de** delivery, que permitem recuperar o conteúdo. As APIs de administração exigem autenticação, enquanto as APIs de delivery não.

Para usar as Adobe Target Admin APIs, primeiro é necessário configurar a autenticação usando a E/S do Adobe.

[Próximo &quot;Configurar autenticação&quot; >](configure-io-target-integration.md)
