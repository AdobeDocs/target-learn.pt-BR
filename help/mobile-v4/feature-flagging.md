---
title: Sinalização de recurso
description: O Adobe Target pode ser usado para experimentar recursos UX como cor, cópia, botões, texto e imagens e fornecer esses recursos para públicos específicos.
role: Desenvolvedor
level: Intermediário
topic: Móvel, Personalização
feature: Implementar dispositivos móveis
doc-type: tutorial
kt: 3040
thumbnail: null
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 1%

---


# Sinalização de recurso

Os proprietários de produtos de aplicativos móveis precisam da flexibilidade para implantar novos recursos em seus aplicativos sem precisar investir em várias versões de aplicativos. Eles também podem querer implantar recursos gradualmente em uma porcentagem da base de usuários, para testar a eficácia. O Adobe Target pode ser usado para experimentar recursos UX como cor, cópia, botões, texto e imagens e fornecer esses recursos para públicos específicos.

Nesta lição, criaremos uma oferta de &quot;sinalizador de recurso&quot; que pode ser usada como acionador para ativar recursos específicos do aplicativo.

## Objetivos de aprendizagem

Ao final desta lição, você poderá:

* Adicionar um novo local à solicitação de pré-busca em lote
* Crie uma atividade [!DNL Target] com uma oferta que será usada como um sinalizador de recurso
* Carregar e validar a oferta do sinalizador de recursos no seu aplicativo

## Adicionar um novo local à solicitação de pré-busca à atividade inicial

No aplicativo de demonstração das lições anteriores, adicionaremos um novo local chamado &quot;weTravel_feature_flag_recs&quot; à solicitação de pré-busca na Atividade inicial e o carregaremos na tela com um novo método Java.

>[!NOTE]
>
>Um dos benefícios de usar uma solicitação de pré-busca é que a adição de uma nova solicitação não adiciona nenhuma sobrecarga de rede adicional ou causa trabalho de carga adicional, pois a solicitação é empacotada dentro da solicitação de pré-busca

Primeiro, verifique se a constante weTravel_feature_flag_recs é adicionada no arquivo Constant.java :

![Adicionar constante sinalizador de recurso](assets/feature_flag_constant.jpg)

Este é o código:

```java
public static final String wetravel_feature_flag_recs = "wetravel_feature_flag_recs";
```

Agora, adicione o local à solicitação de pré-busca e carregue uma nova função chamada `processFeatureFlags()`:

![Código do sinalizador de recurso](assets/feature_flag_code.jpg)

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

## Criar uma oferta JSON de sinalizador de recurso

Agora criaremos uma oferta JSON simples que atuará como um sinalizador ou acionador para um público-alvo específico - o público-alvo que receberia a implantação do recurso em seu aplicativo. Na interface [!DNL Target], crie uma nova oferta:

![Criar oferta JSON de sinalizador de recurso](assets/feature_flag_json_offer.jpg)

Vamos nomeá-lo como &quot;Sinalizador de recurso v1&quot; com o valor {&quot;enable&quot;:1}

![oferta JSON feature_flag_v1](assets/feature_flag_json_name.jpg)

## Criar uma atividade

Agora vamos criar uma atividade de Teste A/B com essa oferta. Para obter etapas detalhadas sobre como criar uma atividade, consulte a lição anterior. A atividade só precisará de um público-alvo para este exemplo. Em um cenário ao vivo, você pode criar públicos-alvo personalizados específicos para implantações de recursos específicos e, em seguida, definir a atividade para usar esses públicos-alvo. Neste exemplo, vamos alocar o tráfego 50/50 (50% para visitantes que veriam as atualizações de recursos e 50% para visitantes que veriam uma experiência padrão). Esta é a configuração da atividade:

1. Nomeie a atividade como &quot;Sinalizador de recurso&quot;
1. Selecione o local &quot;weTravel_feature_flag_recs&quot;
1. Altere o conteúdo para a oferta JSON &quot;Sinalizador de recurso v1&quot;

   ![Configuração da atividade do sinalizador de recurso](assets/feature_flag_activity.jpg)

1. Clique em **[!UICONTROL Adicionar experiência]** para adicionar a experiência B.
1. Deixe o local &quot;weTravel_feature_flag_recs&quot;
1. Deixe **[!UICONTROL Conteúdo padrão]** para o conteúdo
1. Clique em **[!UICONTROL Avançar]** para avançar para a tela [!UICONTROL Direcionamento]

   ![Configuração da atividade do sinalizador de recurso](assets/feature_flag_activity_2.jpg)

1. Na tela [!UICONTROL Direcionamento], verifique se o método [!UICONTROL Alocação de tráfego] está definido como a configuração padrão (Manual) e se cada experiência tem a alocação padrão de 50%. Selecione **[!UICONTROL Next]** para avançar para **[!UICONTROL Metas e configurações]**.

   ![Configuração da atividade do sinalizador de recurso](assets/feature_flag_activity_3.jpg)

1. Defina a **[!UICONTROL Meta primária]** para **[!UICONTROL Conversão]**.
1. Defina a ação para **[!UICONTROL Visualizada uma Mbox]**. Usaremos a localização &quot;weTravel_context_dest&quot; (como essa localização está na tela Confirmação, podemos usá-la para ver se o novo recurso gera mais conversões).
1. Clique em **[!UICONTROL Salvar e fechar]**.

   ![Configuração da atividade do sinalizador de recurso](assets/feature_flag_activity_4.jpg)

Ativar a atividade.

## Validar a atividade do sinalizador de recursos

Agora use o emulador para monitorar a solicitação. Como definimos o direcionamento para 50% dos usuários, há 50% de usuários. Você verá que a resposta do sinalizador de recursos contém o valor `{enable:1}`.

![Validação do sinalizador de recurso](assets/feature_flag_validation.jpg)

Se você não vir o valor `{enable:1}`, significa que você não foi direcionado para a experiência. Como um teste temporário, para forçar a exibição da oferta, você pode:

1. Desative a atividade.
1. Altere a alocação de tráfego para 100% na nova experiência de recurso.
1. Salve e reative.
1. Limpe os dados no emulador e reinicie o aplicativo.
1. A oferta deve retornar o valor `{enable:1}`.

Em um cenário ao vivo, a resposta `{enable:1}` pode ser usada para ativar uma lógica mais personalizada no aplicativo para exibir o conjunto de recursos específico que você deseja mostrar ao público-alvo.

## Conclusão 

Bom trabalho! Agora você tem as habilidades necessárias para implantar recursos em públicos-alvo de usuários específicos.
