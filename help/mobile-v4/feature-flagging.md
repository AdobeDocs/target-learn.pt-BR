---
title: Sinalização de recurso
seo-title: Sinalização de recurso
description: O Adobe Target pode ser usado para experimentar recursos UX como cor, cópia, botões, texto e imagens e fornecer esses recursos a audiências específicas.
seo-description: O Adobe Target pode ser usado para experimentar recursos UX como cor, cópia, botões, texto e imagens e fornecer esses recursos a audiências específicas.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 1%

---


# Sinalização de recurso

Os proprietários de produtos de aplicativos móveis precisam de flexibilidade para implantar novos recursos em seus aplicativos sem precisar investir em várias versões de aplicativos. Eles também podem querer implantar recursos gradualmente em uma porcentagem da base de usuários, para testar a eficácia. O Adobe Target pode ser usado para experimentar recursos UX como cor, cópia, botões, texto e imagens e fornecer esses recursos a audiências específicas.

Nesta lição, criaremos uma oferta de &quot;sinalizador de recurso&quot; que pode ser usada como disparador para ativar recursos específicos do aplicativo.

## Objetivos de aprendizagem

Ao final desta lição, você poderá:

* Adicionar um novo local à solicitação de busca prévia em lote
* Criar uma [!DNL Target] atividade com uma oferta que será usada como sinalizador de recurso
* Carregue e valide a oferta do sinalizador de recursos no aplicativo

## Adicionar um novo local à solicitação de busca prévia à Atividade inicial

No aplicativo de demonstração das lições anteriores, adicionaremos um novo local chamado &quot;weTravel_feature_flag_recs&quot; à solicitação de busca prévia na Atividade inicial e o carregaremos na tela com um novo método Java.

>[!NOTE] Um dos benefícios do uso de uma solicitação de busca prévia é que adicionar uma nova solicitação não adiciona sobrecarga de rede adicional ou gera trabalho de carga adicional, já que a solicitação é empacotada dentro da solicitação de busca prévia

Primeiro, verifique se a constante weTravel_feature_flag_recs foi adicionada ao arquivo Constant.java:

![Adicionar constante sinalizador de recurso](assets/feature_flag_constant.jpg)

Este é o código:

```java
public static final String wetravel_feature_flag_recs = "wetravel_feature_flag_recs";
```

Agora, adicione o local à solicitação de busca prévia e carregue uma nova função chamada `processFeatureFlags()`:

![Código de sinalizador de recurso](assets/feature_flag_code.jpg)

Este é o código atualizado completo:

```java
public void targetPrefetchContent() {
    List<TargetPrefetchObject> prefetchList = new ArrayList<>();

    Map<String, Object> params1;
    params1 = new HashMap<String, Object>();
    params1.put("at_property", "7962ac68-17db-1579-408f-9556feccb477");

    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, params1));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, params1));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_feature_flag_recs, params1));

    Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
        @Override
        public void call(final Boolean status) {
            HomeActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    String cachingStatus = status ? "YES" : "NO";
                    System.out.println("Received Response from prefetch : " + cachingStatus);
                    engageMessage();
                    processFeatureFlags();
                    setUp();

                }
            });
        }};
    Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
}

public void processFeatureFlags() {
    Target.loadRequest(Constant.wetravel_feature_flag_recs, "", null, null, null,
            new Target.TargetCallback<String>(){
                @Override
                public void call(final String s) {
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            System.out.println("Feature Flags : " + s);
                            if(s != null && !s.isEmpty()) {
                                //enable or disable features
                            }
                        }
                    });
                }
            });
}
```

### Validar a solicitação de sinalizador de recurso

Depois que o código for adicionado, execute o Emulador na Atividade inicial e observe o Logcat para obter a resposta atualizada:

![Validar o local do sinalizador de recursos](assets/feature_flag_code_logcat.jpg)

## Criar uma Oferta JSON de sinalizador de recurso

Agora criaremos uma oferta JSON simples que atuará como um sinalizador ou acionador para uma audiência específica - a audiência que receberá a implantação do recurso em seu aplicativo. Na [!DNL Target] interface, crie uma nova oferta:

![Criar sinalizador de recurso Oferta JSON](assets/feature_flag_json_offer.jpg)

Vamos nomeá-lo &quot;Sinalizador de Recurso v1&quot; com o valor {&quot;enable&quot;:1}

![Oferta feature_flag_v1 JSON](assets/feature_flag_json_name.jpg)

## Criar uma atividade

Agora vamos criar uma atividade de teste A/B com essa oferta. Para obter etapas detalhadas sobre como criar uma atividade, consulte a lição anterior. A atividade só precisará de uma audiência para este exemplo. Em um cenário ao vivo, talvez você queira criar audiências personalizadas específicas para roll-outs de recursos específicos e, em seguida, definir a atividade para usar essas audiências. Neste exemplo, apenas alocaremos 50/50 de tráfego (50% para visitantes que visualizariam as atualizações de recursos e 50% para visitantes que visualizariam uma experiência padrão). Esta é a configuração da atividade:

1. Nomeie a Atividade como &quot;Sinalizador de recurso&quot;
1. Selecione o local &quot;weTravel_feature_flag_recs&quot;
1. Altere o conteúdo para a oferta JSON &quot;Sinalizador de recurso v1&quot;

   ![Configuração de Atividade do sinalizador de recurso](assets/feature_flag_activity.jpg)

1. Clique em **[!UICONTROL Adicionar experiência]** para adicionar a experiência B.
1. Deixe o local &quot;weTravel_feature_flag_recs&quot;
1. Deixe o conteúdo **** padrão para o conteúdo
1. Click **[!UICONTROL Next]** to advance to the [!UICONTROL Targeting] screen

   ![Configuração de Atividade do sinalizador de recurso](assets/feature_flag_activity_2.jpg)

1. Na tela [!UICONTROL Definição de metas] , verifique se o método de alocação [!UICONTROL de] tráfego está definido como a configuração padrão (Manual) e se cada experiência tem a alocação padrão de 50%. Selecione **[!UICONTROL Próximo]** para avançar para **[!UICONTROL Metas e configurações]**.

   ![Configuração de Atividade do sinalizador de recurso](assets/feature_flag_activity_3.jpg)

1. Defina o Objetivo **[!UICONTROL principal]** como **[!UICONTROL Conversão]**.
1. Defina a ação como **[!UICONTROL Visualizada uma mbox]**. Usaremos o local &quot;weTravel_context_dest&quot; (como esse local está na tela Confirmação, podemos usá-lo para ver se o novo recurso leva a mais conversões).
1. Clique em **[!UICONTROL Salvar e fechar]**.

   ![Configuração de Atividade do sinalizador de recurso](assets/feature_flag_activity_4.jpg)

Ativar a atividade.

## Validar a Atividade do sinalizador de recurso

Agora use o emulador para verificar a solicitação. Como definimos a definição de metas para 50% dos usuários, há 50% de resposta do sinalizador de recursos que contém o `{enable:1}` valor.

![Validação do sinalizador de recurso](assets/feature_flag_validation.jpg)

Se você não vir o `{enable:1}` valor, isso significa que você não foi direcionado para a experiência. Como um teste temporário, para forçar a oferta a mostrar, você poderia:

1. Desative a atividade.
1. Altere a alocação de tráfego para 100% na experiência do novo recurso.
1. Salve e reative.
1. Limpe os dados no emulador e reinicie o aplicativo.
1. A oferta agora deve retornar o `{enable:1}` valor.

Em um cenário ao vivo, a `{enable:1}` resposta pode ser usada para ativar uma lógica mais personalizada no aplicativo para exibir o conjunto de recursos específico que você deseja que mostre a audiência do público alvo.

## Conclusão 

Bom trabalho! Agora você tem as habilidades necessárias para implantar recursos em audiências específicas do usuário.
