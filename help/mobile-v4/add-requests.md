---
title: Adicionar solicitações do Adobe Target
description: 'O SDK do Adobe Mobile Services (v4) fornece métodos e funcionalidades da Adobe Target que permitem personalizar seu aplicativo com experiências diferentes para usuários diferentes.   '
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
source-wordcount: '1810'
ht-degree: 0%

---


# Adicionar solicitações do Adobe Target

O SDK do Adobe Mobile Services (v4) fornece métodos e funcionalidades do Adobe Target que permitem personalizar seu aplicativo com diferentes experiências para usuários diferentes. Normalmente, uma ou mais solicitações são feitas do aplicativo para a Adobe Target para recuperar o conteúdo personalizado e medir o impacto desse conteúdo.

Nesta lição, você preparará o aplicativo We.Travel para personalização implementando solicitações [!DNL Target].

## Pré-requisitos

Certifique-se de [baixar e atualizar o aplicativo de amostra](download-and-update-the-sample-app.md).

## Objetivos de aprendizagem

Ao final desta lição, você poderá:

* Armazene em cache várias [!DNL Target] ofertas (ou seja, conteúdo personalizado) usando uma solicitação de pré-busca em lote
* Carregar locais [!DNL Target] pré-buscados
* Carregar um local [!DNL Target] em tempo real (sem busca prévia)
* Limpar locais pré-buscados do cache
* Validar solicitações pré-buscadas e em tempo real

## Terminologia

Abaixo está uma parte da terminologia principal do Target que usaremos no restante deste tutorial.

* **Solicitação:**  uma solicitação de rede para os servidores da Adobe Target
* **Oferta:**  um snippet de código ou outro conteúdo baseado em texto, definido na interface do  [!DNL Target] usuário (ou com API), que é entregue na resposta. Geralmente, JSON quando [!DNL Target] é usado em aplicativos móveis nativos.
* **Localização:**  um nome definido pelo usuário fornecido a uma solicitação, usado na  [!DNL Target] interface para associar ofertas a solicitações específicas
* **Solicitação em lote:**  uma única solicitação que inclui vários locais
* **Solicitação de busca prévia:**  uma única solicitação que recupera ofertas e as armazena em cache na memória para uso futuro no aplicativo
* **Solicitação de pré-busca em lote:**   uma única solicitação que busca previamente ofertas para vários locais
* **Público-alvo:**  um grupo de visitantes definidos na  [!DNL Target] interface ou compartilhados com  [!DNL Target] a partir de outros aplicativos do Adobe (por exemplo, &quot;Visitantes do iPhone X&quot;, &quot;visitantes na Califórnia&quot;, &quot;Primeiro aplicativo aberto&quot;)
* **Atividade:**  uma  [!DNL Target] construção, definida na interface do  [!DNL Target] usuário (ou com API) que vincula locais, ofertas e públicos-alvo para criar uma experiência personalizada

## Adicionar uma solicitação de pré-busca em lote

A primeira solicitação que implementaremos no We.Travel é uma solicitação de pré-busca em lote com dois locais [!DNL Target] na Tela inicial. Em uma lição posterior, vamos configurar ofertas para esses locais que exibem mensagens para ajudar a orientar novos usuários durante o processo de reserva.

Uma solicitação de busca prévia busca conteúdo [!DNL Target] o mínimo possível, armazenando a resposta do servidor do Adobe Target em cache (oferta). Uma solicitação de pré-busca em lote recupera e armazena em cache várias ofertas, cada uma associada a um local diferente. Todos os locais pré-buscados são armazenados em cache no dispositivo para uso futuro na sessão do usuário. Ao realizar uma busca prévia em vários locais na tela inicial, podemos recuperar ofertas para uso posteriormente, à medida que o visitante navega pelo aplicativo. Consulte a [documentação de pré-busca](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-mob-target-prefetch-android.html) para obter mais detalhes sobre os métodos de pré-busca.

### Adicionar a solicitação de pré-busca em lote

Vamos atualizar o controlador HomeActivity (o código-fonte da tela inicial), que está localizado em app > main > java > com.weTravel > Controller. Adicionaremos os dois blocos de código mostrados em vermelho:

Começaremos com o controlador HomeActivity (o código-fonte da tela inicial), que está localizado em app > main > java > com.weTravel > Controller.

Adicionaremos os dois blocos de código mostrados em vermelho:

![Código de pré-busca da HomeActivity](assets/homeactivity.jpg)

Role para baixo até o final do código do HomeActivity e adicione o código fornecido abaixo após a função `setHeader()` e *substituindo* a função `onResume()` atual:

```java
@Override
protected void onResume() {
    super.onResume();
    targetPrefetchContent();
}

public void targetPrefetchContent() {
    List<TargetPrefetchObject> prefetchList = new ArrayList<>();
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, null));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, null));
    Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
        @Override
        public void call(final Boolean status) {
            HomeActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    String cachingStatus = status ? "YES" : "NO";
                    System.out.println("Received Response from prefetch : " + cachingStatus);
                    setUp();

                }
            });
        }};
    Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
}
```

Seu IDE provavelmente avisará que você não tem as classes [!DNL Target] importadas no arquivo. Certifique-se de importar as classes [!DNL Target] na parte superior do controlador HomeActivity, conforme mostrado em vermelho abaixo:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

![Importar as classes de destino](assets/import.jpg)

Você provavelmente também verá erros para &quot;não é possível encontrar a variável de símbolo weTravel_engagement_home&quot; e &quot;não é possível encontrar a variável de símbolo weTravel_involved_search&quot;. Adicione-os ao arquivo `Constant.java` (em app > src > main > java > com > weTravel > Utils):

```java
public static final String wetravel_engage_home = "wetravel_engage_home";
public static final String wetravel_engage_search = "wetravel_engage_search";
```

![Adicionar os nomes de localização ao arquivo Constant.java](assets/constants.jpg)

### Explicação do código de solicitação de pré-busca em lote

| Código | Descrição |
|--- |--- |
| `targetPrefetchContent()` | Uma função definida pelo usuário (não parte do SDK) que usa métodos [!DNL Target] para recuperar e armazenar em cache dois locais [!DNL Target]. |
| `prefetchContent()` | O método do SDK [!DNL Target] que envia a solicitação de pré-busca |
| `Constant.wetravel_engage_home` | Nome do local [!DNL Target] pré-buscado que exibirá seu conteúdo de oferta na tela inicial |
| `Constant.wetravel_engage_search` | Nome do local [!DNL Target] pré-buscado que exibirá seu conteúdo de oferta na tela Resultados da pesquisa. Como esse é um segundo local na pré-busca, essa solicitação de pré-busca é chamada de &quot;solicitação em lote de pré-busca&quot;. |
| setUp() | Uma função definida pelo usuário que renderiza a tela inicial do aplicativo depois que as ofertas [!DNL Target] são buscadas previamente |

### Sobre assíncrono versus síncrono

Com o código que acabamos de implementar, a solicitação de pré-busca é feita como uma chamada de bloqueio síncrona, antes da renderização da tela inicial. Quando colamos o novo código no controlador HomeActivity, movemos a execução da função `setUp()` da função `onResume()` para depois da solicitação do Target. Isso pode ser benéfico em cenários em que você deseja personalizar o conteúdo quando o aplicativo é aberto pela primeira vez, pois garante que o conteúdo personalizado dos servidores do Target retorne (ou atinja o tempo limite) antes da renderização da primeira tela. Para permitir que as solicitações sejam carregadas de forma assíncrona (em segundo plano), em vez disso, chame `setUp()` dentro da função `onCreate()` .

### Validar a solicitação de pré-busca em lote

Recrie o aplicativo e abra o emulador de Android. (As capturas de tela a seguir usam o Pixel 2 no Android Q versão 9+, nível de API 29). A resposta da busca prévia deve informar &quot;resposta da busca prévia recebida&quot;:

Quando a tela Início é renderizada, a solicitação de pré-busca deve ser carregada. Com o Logcat, filtre por [!DNL "Target"] para ver a solicitação e a resposta:

![Validar as solicitações na tela inicial](assets/prefetch_validation.jpg)

Se você não estiver vendo uma resposta bem-sucedida, verifique as configurações no arquivo `ADBMobileConfig.json` e a sintaxe de código no arquivo HomeActivity.

Agora, dois locais são armazenados em cache no dispositivo. Os nomes de localização serão carregados lentamente em breve na interface [!DNL Target], onde podem ser selecionados em vários menus suspensos quando você os usa em uma atividade.

### Adicionar solicitações de carregamento para cada localização em cache

Agora que as localizações são buscadas previamente e suas respostas são armazenadas em cache no dispositivo, vamos adicionar o método `Target.loadRequest()` que recupera o conteúdo da oferta do cache para que você possa usá-lo para atualizar seu aplicativo. Adicionaremos um novo método personalizado chamado `engageMessage()` que será executado com a solicitação de pré-busca. `engageMessage()` chamará  `Target.loadRequest()`. `engageMessage()` é executado antes  `setUp()` para garantir que a solicitação de carregamento seja chamada antes da configuração da tela.

Primeiro, adicione a chamada `engageMessage()` e o método para o local weTravel_engagement_home no HomeActivity:

![Adicionar primeira solicitação de carregamento](assets/wetravel_engage_home_loadRequest.jpg)

Este é o código atualizado:

```java
    public void targetPrefetchContent() {
        List<TargetPrefetchObject> prefetchList = new ArrayList<>();
        Map<String, Object> params1;
        params1 = new HashMap<String, Object>();
        params1.put("at_property", "your at_property value goes here");
        prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, params1));
        prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, params1));
        Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
            @Override
            public void call(final Boolean status) {
                HomeActivity.this.runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        String cachingStatus = status ? "YES" : "NO";
                        System.out.println("Received Response from prefetch : " + cachingStatus);
                        engageMessage();
                        setUp();
                    }
                });
            }};
        Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
    }
    public void engageMessage() {
        Target.loadRequest(Constant.wetravel_engage_home, "", null, null, null,
            new Target.TargetCallback<String>(){
                @Override
                public void call(final String s) {
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            System.out.println("Engage Message : " + s);
                            if(s != null && !s.isEmpty()) Utility.showToast(getApplicationContext(), s);
                        }
                    });
                }
            });
    }
```

Agora, adicione a chamada e o método `engageMessage()` para o local weTravel_engagement_search no SearchBusActivity. Observe que a chamada `engageMessage()` é definida no método `onResume()` antes da chamada para `setUpSearch()` para que seja executada antes da tela ser configurada:

![Adicionar segunda solicitação de carregamento](assets/wetravel_engage_search_loadRequest.jpg)

Este é o código atualizado:

```java
    @Override
    public void onResume() {
        super.onResume();
        engageMessage();
        setUpSearch();
    }
    public void engageMessage() {
        Target.loadRequest(Constant.wetravel_engage_search, "", null, null, null,
                new Target.TargetCallback<String>(){
                    @Override
                    public void call(final String s) {
                        runOnUiThread(new Runnable() {
                            @Override
                            public void run() {
                                System.out.println("Engage Message : " + s);
                                if(s != null && !s.isEmpty()) Utility.showToast(getApplicationContext(), s);
                            }
                        });
                    }
                });
    }
```

Como acabou de adicionar métodos do Target à SearchBusActivity, certifique-se de importar as classes [!DNL Target]:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

## Adicionar uma solicitação em tempo real

A próxima solicitação que adicionaremos ao aplicativo será em tempo real na tela de agradecimento. Por &quot;tempo real&quot;, significa que a solicitação será feita e a resposta será aplicada imediatamente (não armazenada em cache para mais tarde). Em uma lição posterior, criaremos uma experiência usando essa solicitação, que é personalizada para o destino de viagem do usuário.

Então vamos adicionar uma solicitação em tempo real na tela Obrigado. No arquivo ThankYouActivity, faremos as alterações mostradas em vermelho:
![Adicionar um local em tempo real na Tela de agradecimento](assets/thankyou.jpg)

Role até o final do arquivo ThankYouActivity. Comente as três linhas na função `getRecommandations()` e adicione a invocação da função `targetLoadRequest()`:

```java
// AppDialogs.dialogLoaderHide();
// recommandations.addAll(recommandation.recommandations);
// recommandationbAdapter.notifyDataSetChanged();
```

Adicione esta linha de código à função `getRecommandations()`:

```java
targetLoadRequest(recommandation.recommandations);
```

Agora, precisamos definir a função `targetLoadRequest()`:
![Adicionar um local em tempo real na Tela de agradecimento](assets/thankyou2.jpg)

Adicione este bloco de código após a função `filterRecommendationBasedOnOffer()`:

```java
public void targetLoadRequest(final ArrayList<Recommandation> recommandations) {
    Target.loadRequest(Constant.wetravel_context_dest, "", null, null, null, new Target.TargetCallback<String>() {
        @Override
        public void call(final String response) {
            try {
                runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        AppDialogs.dialogLoaderHide();
                        filterRecommendationBasedOnOffer(recommandations, response);
                        recommandationbAdapter.notifyDataSetChanged();
                    }
                });
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    });
}
```

Como você acabou de adicionar métodos do Target à Atividade de agradecimento, certifique-se de importar as classes do Target :

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

### Explicação do código targetLoadRequest()

| Código | Descrição |
|--- |--- |
| `targetLoadRequest()` | Uma função definida pelo usuário (não parte do SDK) que aciona `Target.loadRequest()` que carrega e exibe o local weTravel_context_dest |
| `Target.loadRequest()` | O método do SDK que faz a solicitação para o servidor do Target |
| Constant.wetravel_context_dest | O nome do local atribuído à solicitação que usaremos posteriormente quando criarmos a atividade na interface [!DNL Target] |
| `filterRecommendationBasedOnOffer()` | Uma função definida pelo usuário no aplicativo que obtém a oferta da localização da resposta do Target e decide como o aplicativo deve ser alterado com base no conteúdo da oferta |
| `recommandations.addAll()` | Uma função definida pelo usuário no aplicativo que era executada por padrão quando a tela de agradecimento era carregada, mas agora é executada após a resposta do Target ser recebida e analisada por `filterRecommendationBasedOnOffer()` |

Essa foi uma atualização mais sofisticada que fizemos no aplicativo com a solicitação que adicionamos à tela inicial, então vamos levar um momento para revisar o que fizemos:

1. Interrompemos o comportamento anterior do aplicativo de mostrar três promoções padrão, comentando as linhas do código
1. Dissemos ao aplicativo para executar uma nova função, chamada arbitrariamente de targetLoadRequest
1. Definimos a função `targetLoadRequest` para fazer uma solicitação ao Target usando o método Target.loadRequest e executar imediatamente a função `filterRecommendationBasedOnOffer()` quando a resposta da oferta [!DNL Target] for recebida
1. A função `filterRecommendationBasedOnOffer()` interpreta a resposta e decide quais promoções devem ser aplicadas à tela

Este é um padrão de uso muito comum ao usar [!DNL Target] em aplicativos móveis.  Ele é muito poderoso, na medida em que você pode personalizar quase qualquer aspecto do seu aplicativo móvel. Também requer coordenação entre o código do aplicativo e as ofertas que definiremos posteriormente na interface [!DNL Target]. Devido a essa coordenação, alguns casos de uso de personalização podem exigir a atualização do aplicativo na loja de aplicativos para iniciar a atividade.

### Validar a solicitação em tempo real

Abra o emulador de Android e percorra todas as etapas para reservar uma viagem: Home > Bus Search Results > Seat Selection, Payment Options (qualquer opção de pagamento com dados em branco funcionará).

Na tela de agradecimento final, assista Logcat para obter a resposta. A resposta deve ler &quot;O conteúdo padrão foi retornado para &quot;weTravel_context_dest&quot;:

![Adicionar um local em tempo real na tela de agradecimento](assets/thankyou_validation.jpg)

## Limpando Locais Pré-buscados do Cache

Pode haver situações em que os locais pré-buscados precisam ser apagados durante uma sessão. Por exemplo, quando ocorre uma reserva, faz sentido limpar os locais em cache, pois o usuário agora está &quot;engajado&quot; e entende o processo de reserva. Se reservarem outra viagem durante a sessão, não precisarão dos locais originais na tela inicial e na tela de resultados da pesquisa para orientar sua reserva. Seria mais sensato limpar os locais do cache e pré-buscar novas ofertas para talvez um segundo agendamento com desconto ou outro cenário relevante. A lógica pode ser adicionada à tela inicial e à tela de resultados da pesquisa para buscar previamente novos locais se uma reserva tiver ocorrido durante a sessão.

Neste exemplo, apenas apagaremos os locais pré-buscados da sessão quando uma reserva ocorrer. Isso é feito ao chamar a função `Target.clearPrefetchCache()` . Defina a função dentro da função `targetLoadRequest()`, conforme mostrado abaixo:

```java
Target.clearPrefetchCache()
```

![Limpar Locais Pré-buscados do Cache](assets/clearPrefetch.jpg)

Parabéns! Seu aplicativo agora tem a estrutura para personalização. Na próxima lição, aprimoraremos nossos recursos de personalização adicionando parâmetros a esses locais.

**[PRÓXIMO : &quot;Adicionar parâmetros&quot; >](add-parameters.md)**
