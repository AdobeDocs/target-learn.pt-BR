---
title: Adobe Target com Adobe Mobile Services SDK v4 para Android
description: O Adobe Target com Adobe Mobile Services SDK v4 para Android é o ponto de partida perfeito para desenvolvedores Android que já estão usando o Adobe Mobile Services SDK v4 e desejam começar a personalizar experiências de aplicativo com o Adobe Target.
role: Desenvolvedor
level: Intermediário
topic: Móvel, Personalização
feature: Implementar dispositivos móveis, visão geral
doc-type: tutorial
kt: 3040
thumbnail: null
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 2%

---


# Adobe Target com Adobe Mobile Services SDK v4 para Android - Visão geral

_Adobe Target com Adobe Mobile Services SDK v4 para_ Androidis é o ponto de partida perfeito para desenvolvedores Android que já estão usando o Adobe Mobile Services SDK v4 e desejam começar a personalizar experiências de aplicativo com o Adobe Target.

Um aplicativo de demonstração para Android é fornecido para que você conclua as lições. Após concluir este tutorial, você deve estar pronto para começar a implementar [!DNL Target] em seu próprio aplicativo Android!

Depois de concluir este tutorial, você será capaz de:

* Validar a configuração do [Adobe Mobile Services SDK](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html)
* Implemente os seguintes tipos de solicitações [!DNL Target]:
   * Busca prévia do conteúdo [!DNL Target]
   * Aplique vários [!DNL Target] locais em lote (mboxes) em uma única solicitação
   * Bloquear solicitações (executadas antes da exibição do aplicativo)
   * Solicitações sem bloqueio (executadas em segundo plano)
   * Tempo real (sem armazenamento em cache)
   * Refetch de eliminação de cache
* Adicionar parâmetros a solicitações para personalização aprimorada
* Criar públicos-alvo e ofertas
* Personalizar layouts
* Implementar novos recursos com sinalizador de recursos

## Pré-requisitos

Nessas lições, presume-se que você:

* Ter uma ID do Adobe e acesso de nível de aprovador à interface do Adobe Target (consulte as etapas de verificação abaixo)
* Conheça o Código do cliente do Adobe Target para fazer solicitações em sua própria conta. O Código do cliente é mostrado na interface do Adobe Target na   Configuração > Implementação > Editar tela de configurações da at.js
* Ter acesso e estar familiarizado com a [interface do usuário do Mobile Services](https://mobilemarketing.adobe.com)
* Ter um IDE para desenvolvimento de aplicativos móveis Android. Este tutorial apresenta [Android Studio](https://developer.android.com/studio/install) em várias etapas e capturas de tela

Se você não tiver o acesso necessário às Soluções do Experience Cloud, entre em contato com o Administrador do Experience Cloud.

Além disso, presume-se que você esteja familiarizado com o desenvolvimento Android no Java. Não é necessário ser um especialista em Java para concluir as lições, mas você extrairá mais delas se ler e entender o código confortavelmente.

### Verificar o acesso ao Adobe Target

Esta lição requer acesso ao Adobe Target. Antes de seguir para as próximas etapas, verifique se você tem acesso ao Adobe Target fazendo o seguinte:

1. Faça logon no [Adobe Experience Cloud](https://experience.adobe.com/)
1. Na tela inicial do Experience Cloud, clique em [!DNL Target]:
   ![Tela inicial do Experience Cloud](assets/aec_homeScreen_clickTarget.png)
1. Você deve acessar a lista de Atividades no Adobe Target, conforme mostrado abaixo, e deve ver que seu usuário tem acesso no nível de Aprovador . Se você não conseguir acessar [!DNL Target] ou não puder verificar o acesso no nível do Aprovador, entre em contato com um dos administradores do Experience Cloud de sua empresa, solicite esse acesso e retome este tutorial depois que ele for concedido:

   ![Interface do usuário do Adobe](assets/targetUI_approver.png)

## Sobre as lições

Nestas lições, você implementará o Adobe Target em um aplicativo de demonstração chamado &quot;We.Travel&quot; usando sua própria conta Adobe Target. Ao final do tutorial, você enviará mensagens personalizadas para o usuário com base no uso do aplicativo! As experiências de personalização finais terão esta aparência:

![Aplicativo We.Travel final](assets/overview_final_result.jpg)

Após percorrer a implementação no aplicativo We.Travel, você poderá começar a usar [!DNL Target] em seu próprio aplicativo móvel.

Vamos começar!

**[PRÓXIMO : &quot;Baixe e atualize o aplicativo de exemplo&quot; >](download-and-update-the-sample-app.md)**
