---
title: Como usar tokens de resposta e eventos personalizados do at.js
description: Saiba como usar Tokens de resposta e Eventos personalizados do at.js para compartilhar informações de perfil do Target com sistemas de terceiros.
role: Developer
level: Experienced
topic: Personalization, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: d6ce5367-a453-4e6c-8545-9fa676977f04
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 3%

---

# Usar Tokens de resposta e Eventos personalizados do at.js com o Adobe Target

Os Tokens de resposta e os Eventos personalizados do `at.js` permitem que você compartilhe informações de perfil do [!DNL Target] com sistemas de terceiros. Qualquer objeto no perfil de visitante do [!DNL Target], incluindo atributos de perfil personalizados, informações geográficas, detalhes de atividades e perfis internos, pode ser adicionado à resposta do [!DNL Target], na qual você pode usar o JavaScript personalizado para integrar-se a terceiros.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## Como usar Tokens de resposta e Eventos personalizados do at.js

1. Determine de quais dados você precisa, a partir de [!DNL Target]
1. Ative os Tokens de resposta para os dados necessários, invertendo o botão de alternância na tela Configurar->Tokens de resposta
1. Determine qual ouvinte de eventos você precisa usar
1. Escreva o JavaScript necessário para ouvir o evento do Adobe Target, leia os tokens de resposta e faça o que for necessário para a integração
1. Implante o ouvinte de eventos JavaScript usando uma ação de código personalizado no Launch após a ação &quot;Carregar o Target&quot; ou adicione-o à seção Rodapé da biblioteca da at.js na tela Configuração ->Implementação e salve um novo arquivo da at.js
1. Controle de qualidade e publique sua integração

## Recursos adicionais

* [Use o Experience Cloud Debugger com o Adobe Target](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [Documentação do token de resposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)
* [Uso de provedores de dados no Adobe Target](use-data-providers-to-integrate-third-party-data.md)
