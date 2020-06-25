---
title: Criar Audiências e Ofertas no Adobe Target
seo-title: Criar Audiências e Ofertas no Adobe Target
description: 'Nesta lição, construiremos audiências e ofertas para os três locais que implementamos nas lições anteriores. Eles serão usados para exibir experiências personalizadas na próxima lição.   '
seo-description: Nesta lição, construiremos audiências e ofertas para os três locais que implementamos nas lições anteriores. Eles serão usados para exibir experiências personalizadas na próxima lição.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 1%

---


# Criar Audiências e Ofertas no Adobe Target

Nesta lição, iremos para a [!DNL Target] interface e construiremos audiências e ofertas para os três locais que implementamos nas lições anteriores.

## Objetivos de aprendizagem

Ao final desta lição, você poderá:

* Criar públicos-alvo no Adobe Target
* Criar ofertas no Adobe Target

Mais especificamente, nesta lição criaremos audiências e ofertas necessárias para realizar os casos de uso de personalização definidos no início do tutorial. Queremos usar as telas Início e Pesquisa para ajudar os usuários do aplicativo a reservar suas viagens, e queremos usar a tela Agradecimentos para exibir algumas promoções relevantes com base no destino do usuário. Esta é uma tabela que representa o que construiremos nesta lição para cada localização:

| Localização | Público-alvo | Oferta |
| --- | --- | --- |
| weTravel_engagement_home | Novos usuários do aplicativo móvel | &quot;Selecione sua Origem e destino para procurar as rotas de barramento disponíveis&quot; |
| weTravel_engagement_search | Novos usuários do aplicativo móvel | &quot;Use filtros para restringir seus resultados de pesquisa&quot; |
| weTravel_engagement_home | Retorno de usuários de aplicativos móveis | &quot;Bem-vindo de volta! Use o código promocional BACK30 durante o check-out para obter um desconto de 10%.&quot; |
| weTravel_engagement_search | Retorno de usuários de aplicativos móveis | conteúdo padrão |
| weTravel_context_dest | Destino: San Diego | &quot;DJ&quot; |
| weTravel_context_dest | Destino: Los Angeles | &quot;Universal&quot; |

## Selecione seu espaço de trabalho

Se sua empresa usar Propriedades e Espaços de trabalho para estabelecer limites para personalizar aplicativos e sites, e você implementou o parâmetro at_property na última lição, você deve primeiro verificar se está na Workspace correta antes de continuar com esta lição. Se você não usar Propriedades e Espaços de trabalho, ignore essa etapa. Selecione o Espaço de trabalho usado na lição anterior para copiar o valor at_property:

![Exemplo da área de trabalho](assets/workspace.jpg)

## Criar Audiências

Agora vamos criar as audiências que usaremos para personalizar o aplicativo.

### Criar uma Audiência para novos usuários

Audiências Adobe Target são usadas para identificar grupos específicos de visitantes. As Ofertas podem então ser direcionadas para esses grupos específicos. Para os dois primeiros locais, usaremos uma audiência &quot;Novos usuários&quot;:

1. Clique em **[!UICONTROL Audiência]** no menu de navegação superior.
1. Click the **[!UICONTROL Create Audience]** button.
   ![Criar uma nova Audiência de usuário](assets/audience_new_mobile_app_users_1.jpg)

1. Digite **[!UICONTROL New Mobile App Users]** como nome da audiência.
1. Selecione **[!UICONTROL Adicionar regra]**.
1. Selecione uma regra **[!UICONTROL Personalizada]** .
   ![Criar uma nova Audiência de usuário](assets/audience_new_mobile_app_users_2.jpg)

1. Selecione **[!UICONTROL a.Launches]**.
1. Select **[!UICONTROL is less than]**.
1. Enter **5**.
1. Salve a nova audiência.
   ![Criar uma nova Audiência de usuário](assets/audience_new_mobile_app_users_3.jpg)

### Criar uma Audiência para usuários recorrentes

Siga as mesmas etapas listadas acima para criar uma audiência para usuários recorrentes.

1. Nomeie a audiência como Usuários __ do aplicativo móvel recorrente.
1. Usar **[!UICONTROL a.Launches é maior ou igual a 5]** como regra personalizada.
1. Salve a nova audiência.

   ![Criar uma Audiência de usuário recorrente](assets/audience_returning_mobile_app_users.jpg)

>[!NOTE] Todas as medições de ciclo de vida e dimensões coletadas no SDK [!DNL Target] móvel são precedidas por &quot;a&quot; (por exemplo, a.Launches) e estão disponíveis na opção &quot;Personalizado&quot; do menu suspenso e podem ser usadas para criar o audiência.

### Crie uma Audiência para os usuários que reservam uma viagem para San Diego

Em seguida, criaremos algumas audiências para alguns dos destinos oferecidos pelo aplicativo We.Travel. Na última lição, passamos o destino como um parâmetro de localização na solicitação de localização weTravel_context_dest. Esse parâmetro está disponível na opção &quot;Personalizado&quot; do menu suspenso.

>[!NOTE] Se um parâmetro que você está esperando ver na lista suspensa Personalizado não aparecer na [!DNL Target] interface, verifique se ele está sendo passado na solicitação. Se você verificou que está na solicitação, mas não carregou lento na [!DNL Target] interface, basta digitar o nome do parâmetro e pressionar enter para continuar definindo sua audiência

1. Nomeie o _destino da audiência: San Diego_.
1. Use uma regra personalizada com esta definição: _locationDest contém San Diego_.
1. Salve a nova audiência.

   ![Criar Audiência &quot;San Diego&quot;](assets/audience_locationDest_san_diego.jpg)

### Criar uma Audiência para usuários que reservam uma viagem para Los Angeles

1. Nomeie o _destino da audiência: Los Angeles_
1. Use uma regra personalizada com esta definição: _locationDest contém Los Angeles_
1. Salve a nova audiência.

![Criar Audiência &quot;Los Angeles&quot;](assets/audience_locationDest_los_angeles.jpg)

## Crie ofertas

Agora, vamos criar ofertas para exibir essas mensagens. Como lembrete, as ofertas são trechos de código/conteúdo, que são fornecidos na [!DNL Target] resposta. Eles são criados com mais frequência na interface do [!DNL Target] usuário, mas também podem ser criados por meio da API ou da integração dos Fragmentos de experiência com o Adobe Experience Manager. Em aplicativos móveis, as ofertas JSON são comuns. Neste tutorial, estaremos usando ofertas HTML, que podem ser usadas para fornecer qualquer conteúdo de texto simples (incluindo JSON) ao aplicativo.

### Criar a Oferta para novos usuários

Primeiro, vamos criar ofertas para as mensagens para novos usuários:

1. Clique em **[!UICONTROL Oferta]** no menu de navegação superior.
1. Clique em **[!UICONTROL Criar]**.
1. Selecione Oferta **** HTML.

   ![Criar Oferta inicial](assets/offer_home_1.jpg)

1. Dê um nome para a _página inicial da oferta: Envolva novos usuários_.
1. Digite _Selecionar origem e destino para pesquisar os barramentos_ disponíveis como código.
1. Salve a nova oferta.

   ![Criar Oferta HTML inicial](assets/offer_home_2.jpg)

### Criar a Oferta para usuários recorrentes

Agora vamos criar uma oferta para usuários recorrentes (a segunda oferta será o conteúdo padrão, que será exibido como nada):

1. Dê um nome para a _página inicial da oferta: Retornando usuários_.
1. Digite _Welcome de volta! Use o código promocional BACK30 durante o check-out para obter um desconto de 10%._ como o código HTML.
1. Salve a nova oferta.

   ![Criar Oferta HTML inicial](assets/offer_home_returning_users.jpg)

### Crie a Oferta de San Diego

Quando &quot;DJ&quot; for retornado para a atividade Obrigado, a lógica na função filterRecommendationBasedOnOffer() exibirá um banner para &quot;Rock Night with DJ SAM&quot;:

1. Nomeie a _Promoção da oferta para San Diego_.
1. Digite _DJ_ como o código HTML.
1. Salve a nova oferta.

![Criar Oferta &quot;San Diego&quot;](assets/offer_san_diego.jpg)

### Criar Oferta para usuários indo para Los Angeles

Quando &quot;Universal&quot; for retornado para a atividade Obrigado, a lógica na função filterRecommendationBasedOnOffer() exibirá um banner para &quot;Universal Studios&quot; será exibida:

1. Nomeie a _Promoção da oferta para Los Angeles_.
1. Digite _Universal_ como o código HTML.
1. Salve a nova oferta.

![Criar Oferta &quot;Los Angeles&quot;](assets/offer_los_angeles.jpg)

## Conclusão 

Agora temos nossas Audiências e Ofertas. Na próxima lição, criaremos atividades que unem os locais, as audiências e as ofertas para criar experiências personalizadas!

**[PRÓXIMO : &quot;Personalizar layouts&quot; >](personalize-layouts.md)**
