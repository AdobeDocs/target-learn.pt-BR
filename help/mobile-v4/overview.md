---
title: Adobe Target com Adobe Mobile Services SDK v4 para Android
description: O Adobe Target com o Adobe Mobile Services SDK v4 para Android é o ponto de partida perfeito para desenvolvedores do Android que já usam o Adobe Mobile Services SDK v4 e desejam começar a personalizar experiências de aplicativo com o Adobe Target.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile, Overview
doc-type: tutorial
kt: 3040
exl-id: 20f8ed4f-a86d-4c5e-9296-71a93724caa3
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 2%

---

# Adobe Target com Adobe Mobile Services SDK v4 para Android - Visão geral

O _Adobe Target com Adobe Mobile Services SDK v4 para Android_ é o ponto de partida perfeito para desenvolvedores do Android que já estão usando o Adobe Mobile Services SDK v4 e desejam começar a personalizar experiências de aplicativo com o Adobe Target.

Um aplicativo de demonstração do Android é fornecido para que você conclua as lições. Após concluir este tutorial, você deve estar pronto para começar a implementar o [!DNL Target] em seu próprio aplicativo Android!

Depois de concluir este tutorial, você será capaz de:

* Validar a configuração do [Adobe Mobile Services SDK](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=pt-BR)
* Implemente os seguintes tipos de solicitações [!DNL Target]:
   * Pré-busca de conteúdo [!DNL Target]
   * Vários locais (mboxes) do [!DNL Target] em lote em uma única solicitação
   * Bloquear solicitações (é executado antes da exibição do aplicativo)
   * Solicitações sem bloqueio (executadas em segundo plano)
   * Tempo real (sem armazenamento em cache)
   * Nova busca de cache
* Adicionar parâmetros a solicitações de personalização aprimorada
* Criar públicos e ofertas
* Personalizar layouts
* Implantar novos recursos com sinalização de recursos

## Pré-requisitos

Nessas lições, presume-se que você:

* Ter uma Adobe ID e acesso como aprovador à interface da Adobe Target (consulte as etapas de verificação abaixo)
* Conhecer o código de cliente do Adobe Target para fazer solicitações em sua própria conta. O código do cliente é mostrado na interface do Adobe Target na   Configuração > Implementação > Editar tela de configurações da at.js
* Ter acesso e se familiarizar com a [interface do usuário do Mobile Services](https://mobilemarketing.adobe.com/)
* Ter um IDE para desenvolvimento de aplicativos móveis Android. Este tutorial apresenta o [Android Studio](https://developer.android.com/studio/install) em várias etapas e capturas de tela

Se você não tiver o acesso necessário às Soluções da Experience Cloud, entre em contato com o administrador do Experience Cloud.

Além disso, presume-se que você esteja familiarizado com o desenvolvimento do Android em Java. Não é necessário ser um especialista em Java para concluir as lições, mas você extrairá mais delas se ler e entender o código confortavelmente.

### Verificar acesso ao Adobe Target

Esta lição requer acesso ao Adobe Target. Antes de seguir para as próximas etapas, verifique se você tem acesso ao Adobe Target fazendo o seguinte:

1. Faça logon no [Adobe Experience Cloud](https://experience.adobe.com/)
1. Na tela inicial do Experience Cloud, clique em [!DNL Target]:
   ![Tela inicial do Experience Cloud](assets/aec_homeScreen_clickTarget.png)
1. Você deve chegar à lista de Atividades no Adobe Target, como mostrado abaixo, e ver que seu usuário tem acesso como Aprovador. Se você não conseguir acessar [!DNL Target] ou não puder verificar o acesso no nível do Aprovador, contate um dos Administradores do Experience Cloud da sua empresa, solicite esse acesso e retome este tutorial depois que ele for concedido:

   ![INTERFACE DO USUÁRIO DO Adobe](assets/targetUI_approver.png)

## Sobre as lições

Nessas lições, você implementará o Adobe Target em um aplicativo de demonstração de viagem chamado &quot;We.Travel&quot; usando sua própria conta da Adobe Target. Ao final do tutorial, você entregará mensagens personalizadas ao usuário com base no uso do aplicativo! As experiências finais de personalização serão assim:

![Aplicativo We.Travel final](assets/overview_final_result.jpg)

Após percorrer a implementação no aplicativo We.Travel, você poderá começar a usar o [!DNL Target] em seu próprio aplicativo móvel.

Vamos começar!

**[NEXT: &quot;Baixar e atualizar o aplicativo de exemplo&quot; >](download-and-update-the-sample-app.md)**
