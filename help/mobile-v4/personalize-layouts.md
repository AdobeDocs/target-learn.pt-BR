---
title: Personalizar Layouts
description: Nesta lição final, criamos duas atividades de personalização no Target para nossos Públicos-alvo. Saiba como carregar e exibir as atividades no aplicativo e validar se o conteúdo é exibido na hora certa nos locais certos.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
author: Daniel Wright
exl-id: a9f033d9-9f72-4154-88f5-d36423a404d0
TQID: https://experienceleague.adobe.com/Ku3bhBHqeS5xdaAVtjPELQJ2fu-GdNWqTweOTILSqsI
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 1074
ht-degree: 1%

---

# Personalizar Layouts

Agora é hora de unir tudo e criar as experiências personalizadas. Uma _Atividade_ é o mecanismo [!DNL Target] que vincula os locais, os públicos e as ofertas, de forma que, quando a solicitação for feita pelo aplicativo, [!DNL Target] responda com o conteúdo personalizado. Criaremos duas atividades de personalização em [!DNL Target] e validaremos se o conteúdo personalizado é exibido para o usuário certo na hora certa e no local certo.

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Atividades de build no Adobe Target
* Validar as atividades no aplicativo de amostra

## Criar atividades no Adobe Target

Saiba como criar atividades Engage Users e Contextual Offers.

### Primeira atividade - &quot;Envolver usuários&quot;

Aqui está um resumo da atividade que criaremos:

| Público-alvo | Localizações | Ofertas |
|---|---|---|
| Novos usuários de aplicativos móveis | wetravel_engage_home, wetravel_engage_search | Página inicial: Envolver novos usuários, Pesquisar: Envolver novos usuários |
| Retornando usuários do aplicativo móvel | wetravel_engage_home, wetravel_engage_search | Página inicial: usuários recorrentes, default_content |

Na interface [!DNL Target], faça o seguinte:

1. Selecione **[!UICONTROL Atividades]** > **[!UICONTROL Criar Atividade]** > **[!UICONTROL Direcionamento De Experiência]**.

   ![Criar atividade](assets/activity_create_1.jpg)

1. Clique em **[!UICONTROL Aplicativo móvel]**.
1. Selecione o **[!UICONTROL Compositor do formulário]**.
1. Selecione o espaço de trabalho (o mesmo espaço de trabalho usado nas lições anteriores).
1. Selecione sua Propriedade (a mesma propriedade usada nas lições anteriores).
1. Clique em **[!UICONTROL Avançar]**.

   ![Criar atividade](assets/activity_create_2.jpg)

1. Altere o título da atividade para **[!UICONTROL Envolver Usuários]**.
1. Selecione as **[!UICONTROL reticências]** > **[!UICONTROL Alterar público]**.
   ![Novos Usuários de Aplicativos Móveis Alteram Público-Alvo](assets/activity_create_3.jpg)
1. Defina o público como **[!UICONTROL Novos usuários de aplicativos móveis]**.
1. Clique em **[!UICONTROL Concluído]**.
   ![Novo público-alvo de usuários de aplicativos móveis](assets/activity_create_4.jpg)

1. Altere a localização para _wetravel_ engage_home_.
1. Selecione a seta suspensa ao lado de Conteúdo padrão e selecione **[!UICONTROL Alterar oferta do HTML]**.

   ![Novo público-alvo de usuários de aplicativos móveis](assets/activity_create_5.jpg)

1. Selecione a oferta **[!UICONTROL Página inicial: Envolver novos usuários]**.
1. Selecione **[!UICONTROL Concluído]**.

   ![Novo público-alvo de usuários de aplicativos móveis](assets/activity_create_6.jpg)

1. Selecione **[!UICONTROL Adicionar Local]**.
   ![Novo público-alvo de usuários de aplicativos móveis](assets/activity_create_7.jpg)

1. Selecione o local _wetravel_ engage_search_.
1. Altere a oferta do HTML.

   ![Novo público-alvo de usuários de aplicativos móveis](assets/activity_create_8.jpg)

1. Selecione a oferta **[!UICONTROL Pesquisar: Envolver Novos Usuários]**.
1. Clique em **[!UICONTROL Concluído]**.

   ![Novo público-alvo de usuários de aplicativos móveis](assets/activity_create_9.jpg)

Você acabou de conectar um público-alvo a locais e ofertas, criando a experiência personalizada para os Novos usuários de aplicativos móveis! A experiência agora deve ficar assim:

![Experiência Final](assets/activity_engage_users_a_final.jpg)

Agora crie uma experiência para Usuários de aplicativos móveis que retornam:

1. Selecione **[!UICONTROL Adicionar segmentação por experiência]** à esquerda.
1. Selecione o Público-alvo **[!UICONTROL Usuários de Aplicativos Móveis Recorrentes]**.
1. Selecione **[!UICONTROL Concluído]**.
   ![Retornando o Público-alvo de Usuários de Aplicativos Móveis](assets/activity_create_11.jpg)

Agora use o mesmo processo usado anteriormente para configurar a nova experiência. A configuração da experiência de usuários de aplicativos móveis recorrentes deve ser semelhante a:

![Final de Usuários de Aplicativo Móvel Retornados](assets/activity_engage_users_b_final.jpg)

Vamos prosseguir para a próxima tela da configuração:

1. Clique em **[!UICONTROL Avançar]** para avançar para a tela **[!UICONTROL Direcionamento]**.
1. Use as configurações padrão para direcionamento. Se você tiver experiências com públicos sobrepostos (por exemplo, _Usuários de Nova York_ e _Usuários pela primeira vez_), poderá organizar a ordem de prioridade nesta tela.
1. Clique em **[!UICONTROL Avançar]** para avançar para **[!UICONTROL Metas e Configurações]**.

   ![Atividade Engage Users - Padrão de direcionamento](assets/activity_engage_users_targeting.jpg)

Agora vamos concluir a configuração da atividade:

1. Defina a **[!UICONTROL Meta primária]** para **[!UICONTROL Conversão]**.
1. Defina a ação como **[!UICONTROL Visualizou uma mbox]** > _wetravel_ context_dest_ (como esse local está na tela de confirmação, podemos usá-lo para medir conversões).

   ![Envolver Atividade dos Usuários - Metas](assets/activity_create_12.jpg)

1. Mantenha todas as outras configurações na tela de acordo com os padrões.
1. Clique em **[!UICONTROL Salvar e fechar]** para salvar a Atividade.
1. Ative a **[!UICONTROL Atividade]** na próxima tela.

![Público-alvo da Experiência B](assets/activity_create_13.jpg)

Nossa primeira atividade está ativa e pronta para ser testada.

### Segunda atividade - &quot;Ofertas contextuais&quot;

Aqui está um resumo da segunda atividade que criaremos:

| Público-alvo | Localização | Ofertas |
| --- | --- | --- |
| Destino: San Diego | wetravel_context_dest | Promoção para San Diego |
| Destino: Los Angeles | wetravel_context_dest | Promoção para Los Angeles |

Repita o mesmo processo acima para a próxima atividade - &quot;Ofertas contextuais&quot;. A configuração final de ambas as experiências é mostrada abaixo:

#### San Diego

![Ofertas contextuais - Experiência A](assets/activity_contextual_a_final.jpg)

#### Los Angeles

![Ofertas contextuais - Experiência B](assets/activity_contextual_b_final.jpg)

Na etapa Metas e configurações, alteraremos a Meta principal para o local na tela de confirmação de reserva:

1. Nas **[!UICONTROL Configurações de Relatórios]**, defina a **[!UICONTROL Meta Primária]** como **[!UICONTROL Conversão]**.
1. Defina a ação como **[!UICONTROL Visualizou uma mbox]** > _wetravel_ context_dest_ (nesta atividade, esta métrica não tem significado, pois este também é o mesmo local que fornece a experiência).
1. Clique em **[!UICONTROL Salvar e fechar]**.

![Ofertas contextuais - Experiência](assets/activity_create_14.jpg)

Ative a Atividade na próxima tela.

Agora, nossa segunda atividade está ativa e pronta para ser testada.

## Validar a oferta inicial

Execute o Emulador e observe a primeira oferta a ser exibida na parte inferior da tela inicial. Se você for um usuário recorrente com 5 ou mais inicializações de aplicativo, verá a oferta _bem-vindo de volta_ exibida. Se você for um novo usuário (menos de 5 inicializações de aplicativo), verá a mensagem _novo usuário_:

![Validar Oferta Inicial](assets/layout_home_validate.jpg)

Se a nova oferta de usuário não for exibida, tente apagar os dados para o emulador. Isso redefinirá as inicializações do aplicativo para 1 na próxima vez que você iniciar. Isso é feito em **[!UICONTROL Ferramentas]** > **[!UICONTROL Gerenciador AVD]**. Talvez seja necessário reiniciar o Android Studio também, se o Logcat não funcionar corretamente:

![Limpar Emulador](assets/layout_home_validate_avd_wipe.jpg)

Você também pode validar a resposta no Logcat filtrando por _wetravel_ engage_home_:

![Validar Oferta Inicial - Logcat](assets/layout_home_validate_logcat.jpg)

## Validar a oferta de pesquisa

Selecione **[!UICONTROL San Jose]** como sua **[!UICONTROL Partida]** e **[!UICONTROL San Diego]** como seu **[!UICONTROL Destino]** e clique em **[!UICONTROL Localizar Barramento]** para procurar os barramentos disponíveis.

Na tela de resultados, você deve ver a mensagem _usar filtros_. Se você for um usuário recorrente com 5 ou mais inicializações do aplicativo, nenhuma mensagem será exibida aqui, pois o conteúdo padrão está definido para este local (que está em branco):

![Validar Oferta De Pesquisa](assets/layout_search_validate.jpg)

## Validar as ofertas contextuais na tela de agradecimento

Agora, continue com o processo de reserva:

* Selecione um barramento na tela de resultados.
* Selecione um assento na tela de check-out.
* Selecione **[!UICONTROL Cartão de Crédito]** na tela de pagamento (deixe as informações de pagamento em branco - nenhuma reserva será feita).

Como San Diego foi selecionado como destino, você deve ver o banner de oferta _DJ SAM_ na tela de confirmação:

![Validar oferta de contexto - San Diego](assets/layout_context_san_diego.jpg)

Agora selecione **[!UICONTROL Concluído]** e tente outra reserva com Los Angeles como destino. A tela de confirmação deve exibir o banner _Universal Studios_:

![Validar Oferta de Contexto - Los Angeles](assets/layout_context_los_angeles.jpg)

## Conclusão

Parabéns! Isso conclui a parte principal do tutorial do Adobe Target SDK 4.x para Android. Agora você tem as habilidades para implementar a personalização em aplicativos Android! Você pode consultar esta documentação e o aplicativo de demonstração como uma referência para seus projetos futuros.

Próximo: A Sinalização de recurso é outro recurso que pode ser implementado com o Adobe Target no Android. Para saber mais sobre a sinalização de recursos, confira a próxima lição.

**[PRÓXIMO: Sinalização de Recurso >](feature-flagging.md)**
