---
title: Adobe Target com Adobe Mobile Services SDK v4 para Android
description: O Adobe Target com Adobe Mobile Services SDK v4 para Android é o ponto de partida perfeito para desenvolvedores do Android que já estão usando o Adobe Mobile Services SDK v4 e desejam personalizar as experiências do aplicativo com o Adobe Target.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: d6cedd55dcc9c08d2d2ca5709e15fe5ea9fab8b8
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 2%

---


# Adobe Target com Adobe Mobile Services SDK v4 para Android - Visão geral

_Adobe Target com Adobe Mobile Services SDK v4 para_ Androidis é o ponto de partida perfeito para desenvolvedores Android que já estão usando o Adobe Mobile Services SDK v4 e desejam personalizar as experiências do aplicativo com o Adobe Target.

Um aplicativo de demonstração para Android é fornecido para você concluir as lições. Depois de concluir este tutorial, você deve estar pronto para o start implementando [!DNL Target] em seu próprio aplicativo Android!

Depois de concluir este tutorial, você será capaz de:

* Validar a configuração [Adobe Mobile Services SDK](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html)
* Implemente os seguintes tipos de solicitações [!DNL Target]:
   * Pré-busca de conteúdo [!DNL Target]
   * Agrupamento de vários [!DNL Target] locais (mboxes) em uma única solicitação
   * Bloquear solicitações (é executado antes da exibição do aplicativo)
   * Solicitações sem bloqueio (executadas em segundo plano)
   * Tempo real (sem armazenamento em cache)
   * Refetch de recuperação de cache
* Adicionar parâmetros a solicitações para personalização aprimorada
* Criar audiências e ofertas
* Personalizar layouts
* Implantar novos recursos com sinalizador de recursos

## Pré-requisitos

Nestas lições, presume-se que você:

* Tenha uma ID de Adobe e acesso de nível de aprovador à interface do Adobe Target (consulte as etapas de verificação abaixo)
* Conheça o código do cliente Adobe Target para que você possa fazer solicitações em sua própria conta. O Código do cliente é mostrado na interface do Adobe Target na   Configuração > Implementação > Editar tela de configurações do at.js
* Tenha acesso e esteja familiarizado com a [interface de usuário do Mobile Services](https://mobilemarketing.adobe.com)
* Tenha um IDE para o desenvolvimento de aplicativos móveis Android. Este tutorial apresenta [Android Studio](https://developer.android.com/studio/install) em várias etapas e capturas de tela

Se você não tiver o acesso necessário às soluções de Experience Cloud, entre em contato com o administrador do Experience Cloud.

Além disso, presume-se que você esteja familiarizado com o desenvolvimento do Android em Java. Você não precisa ser um especialista em Java para concluir as lições, mas você obterá mais deles se puder ler e entender o código confortavelmente.

### Verificar acesso ao Adobe Target

Esta lição requer acesso ao Adobe Target. Antes de prosseguir com as próximas etapas, verifique se você tem acesso ao Adobe Target, fazendo o seguinte:

1. Efetue login no [Adobe Experience Cloud](https://experience.adobe.com/)
1. Na tela inicial do Experience Cloud, clique em [!DNL Target]:
   ![Tela inicial Experience Cloud](assets/aec_homeScreen_clickTarget.png)
1. Você deve acessar a lista do Atividade no Adobe Target, como a figura abaixo, e deve ver se o usuário tem acesso no nível do Aprovador. Se você não conseguir acessar [!DNL Target] ou não puder verificar o acesso no nível do Aprovador, entre em contato com um dos Administradores do Experience Cloud do empresa, solicite esse acesso e retome este tutorial depois que ele for concedido:

   ![UI Adobe](assets/targetUI_approver.png)

## Sobre as lições

Nessas lições, você implementará o Adobe Target em um aplicativo de demonstração de viagem chamado &quot;We.Travel&quot; usando sua própria conta Adobe Target. Ao final do tutorial, você enviará mensagens personalizadas ao usuário com base no uso do aplicativo! As experiências finais de personalização serão as seguintes:

![Final do aplicativo We.Travel](assets/overview_final_result.jpg)

Depois de percorrer a implementação no aplicativo We.Travel, você poderá start usando [!DNL Target] em seu próprio aplicativo móvel.

Vamos começar!

**[PRÓXIMO : &quot;Baixe e atualize o aplicativo de amostra&quot; >](download-and-update-the-sample-app.md)**
