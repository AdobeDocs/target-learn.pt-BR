---
title: Adicionar solicitações do Adobe Target
description: O Adobe Mobile Services SDK (v4) fornece métodos e funcionalidades do Adobe Target que permitem personalizar seu aplicativo com experiências diferentes para usuários diferentes.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 88a5be3f-d61f-43e7-997a-574ef56122ed
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '1785'
ht-degree: 0%

---

# Adicionar solicitações do Adobe Target

O Adobe Mobile Services SDK (v4) fornece métodos e funcionalidades do Adobe Target que permitem personalizar seu aplicativo com experiências diferentes para usuários diferentes. Normalmente, uma ou mais solicitações são feitas pelo aplicativo à Adobe Target para recuperar o conteúdo personalizado e medir o impacto desse conteúdo.

Nesta lição, você preparará o aplicativo We.Travel para personalização implementando [!DNL Target] solicitações.

## Pré-requisitos

[baixe e atualize o aplicativo de exemplo](download-and-update-the-sample-app.md).

## Objetivos de aprendizagem

No final desta lição, você poderá:

* Armazenar em cache várias ofertas de [!DNL Target] (ou seja, conteúdo personalizado) usando uma solicitação de pré-busca em lote
* Carregar locais [!DNL Target] previamente buscados
* Carregar um local [!DNL Target] em tempo real (sem busca prévia)
* Limpar locais previamente buscados do cache
* Validar solicitações pré-buscadas e em tempo real

## Terminologia

Abaixo está uma da terminologia principal do Target que será usada no restante deste tutorial.

* **Solicitação:** uma solicitação de rede para os servidores do Adobe Target
* **Oferta:** um trecho de código ou outro conteúdo baseado em texto, definido na interface do usuário do [!DNL Target] (ou com a API), que é entregue na resposta. Normalmente JSON quando [!DNL Target] é usado em aplicativos móveis nativos.
* **Local:** um nome definido pelo usuário fornecido para uma solicitação, usado na interface [!DNL Target] para associar ofertas a solicitações específicas
* **Solicitação em Lote:** uma única solicitação que inclui várias localizações
* **Solicitação de pré-busca:** uma única solicitação que recupera ofertas e as armazena em cache na memória para uso futuro no aplicativo
* **Solicitação de pré-busca de lote:** uma única solicitação que pré-busca ofertas para vários locais
* **Público-alvo:** um grupo de visitantes definido na interface do [!DNL Target] ou compartilhado com o [!DNL Target] a partir de outros aplicativos da Adobe (por exemplo, &quot;visitantes do iPhone X&quot;, &quot;visitantes na Califórnia&quot;, &quot;Primeiro aplicativo aberto&quot;)
* **Atividade:** uma construção [!DNL Target], definida na interface do usuário [!DNL Target] (ou com a API) que vincula locais, ofertas e públicos para criar uma experiência personalizada

## Adicionar uma solicitação de pré-busca de lote

A primeira solicitação que implementaremos no We.Travel é uma solicitação de pré-busca em lote com dois locais [!DNL Target] na tela inicial. Em uma lição posterior, configuraremos ofertas para esses locais que exibem mensagens para ajudar a orientar novos usuários durante o processo de reserva.

Uma solicitação de pré-busca busca obtém o mínimo possível de conteúdo [!DNL Target] ao armazenar em cache a resposta do servidor do Adobe Target (oferta). Uma solicitação de pré-busca em lote recupera e armazena em cache várias ofertas, cada uma associada a um local diferente. Todos os locais de busca prévia são armazenados em cache no dispositivo para uso futuro na sessão do usuário. Ao buscar previamente vários locais na tela inicial, podemos recuperar ofertas para usar posteriormente enquanto o visitante navega pelo aplicativo. Consulte a [documentação de busca prévia](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html?lang=pt-BR) para obter mais detalhes sobre os métodos de busca prévia.

### Adicionar a solicitação de pré-busca de lote

Vamos atualizar o controlador HomeActivity (o código-fonte da tela inicial), que está localizado em app > main > java > com.wetravel > Controller. Adicionaremos os dois blocos de código mostrados em vermelho:

Começaremos com o controlador HomeActivity (o código-fonte da tela inicial), que está localizado em app > main > java > com.wetravel > Controller.

Adicionaremos os dois blocos de código mostrados em vermelho:

![Código de pré-busca de HomeActivity](assets/homeactivity.jpg)

Role para baixo até o final do código de HomeActivity e adicione o código fornecido abaixo após a função `setHeader()` e *substituindo* a função `onResume()` atual:

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

O IDE provavelmente avisará que você não tem as classes [!DNL Target] importadas no arquivo. Certifique-se de importar as classes [!DNL Target] na parte superior do controlador HomeActivity, como mostrado em vermelho abaixo:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

![Importar as classes de destino](assets/import.jpg)

Você provavelmente também verá erros para &quot;não é possível encontrar a variável de símbolo wetravel_engage_home&quot; e &quot;não é possível encontrar a variável de símbolo wetravel_engage_search&quot;. Adicione esses ao arquivo `Constant.java` (em app > src > main > java > com > wetravel > Utils):

```java
public static final String wetravel_engage_home = "wetravel_engage_home";
public static final String wetravel_engage_search = "wetravel_engage_search";
```

![Adicionar os nomes de localização ao arquivo Constant.java](assets/constants.jpg)

### Explicação do código de solicitação de pré-busca em lote

| Código | Descrição |
|--- |--- |
| `targetPrefetchContent()` | Uma função definida pelo usuário (não parte da SDK) que usa métodos [!DNL Target] para recuperar e armazenar em cache dois locais [!DNL Target]. |
| `prefetchContent()` | O método SDK [!DNL Target] que envia a solicitação de pré-busca |
| `Constant.wetravel_engage_home` | Nome do local [!DNL Target] previamente buscado que exibirá o conteúdo da oferta na tela inicial |
| `Constant.wetravel_engage_search` | Nome do local [!DNL Target] previamente buscado que exibirá seu conteúdo de oferta na Tela de Resultados da Pesquisa. Como esse é um segundo local na busca prévia, essa solicitação de busca prévia é chamada de &quot;solicitação em lote de busca prévia&quot;. |
| setUp() | Uma função definida pelo usuário que renderiza a tela inicial do aplicativo após as ofertas de [!DNL Target] serem buscadas previamente |

### Sobre assíncrono vs. síncrono

Com o código que acabamos de implementar, a solicitação de pré-busca é feita como uma chamada síncrona de bloqueio, antes da renderização da tela inicial. Quando colamos o novo código no controlador HomeActivity, movemos a execução da função `setUp()` da função `onResume()` para depois da solicitação do Target. Isso pode ser benéfico em cenários em que você deseja personalizar o conteúdo quando o aplicativo é aberto pela primeira vez, pois garante que o conteúdo personalizado dos servidores do Target retorne (ou atinja o tempo limite) antes que a primeira tela seja renderizada. Para permitir que as solicitações sejam carregadas de forma assíncrona (em segundo plano), basta chamar `setUp()` na função `onCreate()`.

### Validar a solicitação de pré-busca de lote

Recrie o aplicativo e abra o Emulador do Android. (As capturas de tela a seguir usam o Pixel 2 no Android Q versão 9+, API nível 29). A resposta da busca prévia deve informar &quot;resposta recebida da busca prévia&quot;:

Quando a tela inicial é renderizada, a solicitação de pré-busca deve ser carregada. Com o Logcat, filtre por [!DNL "Target"] para ver a solicitação e a resposta:

![Validar as solicitações na Tela Inicial](assets/prefetch_validation.jpg)

Se você não estiver vendo uma resposta bem-sucedida, verifique as configurações no arquivo `ADBMobileConfig.json` e a sintaxe de código no arquivo HomeActivity.

Dois locais agora são armazenados em cache no dispositivo. Os nomes de locais serão carregados com lentidão na interface do [!DNL Target], onde podem ser selecionados em vários menus suspensos quando você os usa em uma atividade.

### Adicionar solicitações de carga para cada local armazenado em cache

Agora que os locais são previamente buscados e suas respostas armazenadas em cache no dispositivo, vamos adicionar o método `Target.loadRequest()` que recupera o conteúdo da oferta do cache para que você possa usá-lo para atualizar seu aplicativo. Adicionaremos um novo método personalizado chamado `engageMessage()` que será executado com a solicitação de pré-busca. `engageMessage()` chamará `Target.loadRequest()`. `engageMessage()` é executado antes de `setUp()` para garantir que a solicitação de carregamento seja chamada antes da configuração da tela.

Primeiro, adicione a chamada e o método `engageMessage()` para a localização wetravel_engage_home na HomeActivity:

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

Agora adicione a chamada e o método `engageMessage()` para o local wetravel_engage_search na SearchBusActivity. Observe que a chamada `engageMessage()` é definida no método `onResume()` antes da chamada para `setUpSearch()`, para que seja executada antes que a tela seja configurada:

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

Como você acabou de adicionar métodos Target ao SearchBusActivity, certifique-se de importar as classes [!DNL Target]:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

## Adicionar uma solicitação em tempo real

A próxima solicitação que adicionaremos ao aplicativo será uma solicitação em tempo real na tela Thank You. Por &quot;tempo real&quot;, queremos dizer que a solicitação será feita e a resposta será aplicada imediatamente (não armazenada em cache para depois). Em uma lição posterior, criaremos uma experiência usando essa solicitação, que é personalizada para o destino da viagem do usuário.

Vamos adicionar uma solicitação em tempo real na tela Thank You. No arquivo ThankYouActivity, faremos as alterações mostradas em vermelho:
![Adicionar um local em tempo real na tela de agradecimento](assets/thankyou.jpg)

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
![Adicionar um local em tempo real na tela de agradecimento](assets/thankyou2.jpg)

Adicionar este bloco de código após a função `filterRecommendationBasedOnOffer()`:

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

Como você acabou de adicionar métodos do Target ao ThankYouActivity, certifique-se de importar as classes do Target:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

### Explicação do código targetLoadRequest()

| Código | Descrição |
|--- |--- |
| `targetLoadRequest()` | Uma função definida pelo usuário (não parte da SDK) que aciona `Target.loadRequest()`, que carrega e exibe o local wetravel_context_dest |
| `Target.loadRequest()` | O método SDK que faz a solicitação ao servidor do Target |
| Constant.wetravel_context_dest | O nome da localização atribuído à solicitação que será usada posteriormente quando criarmos a atividade na interface [!DNL Target] |
| `filterRecommendationBasedOnOffer()` | Uma função definida pelo usuário no aplicativo que obtém a oferta da localização da resposta do Target e decide como o aplicativo deve ser alterado com base no conteúdo da oferta |
| `recommandations.addAll()` | Uma função definida pelo usuário no aplicativo que era executada por padrão quando a tela Obrigado foi carregada, mas que agora é executada após a resposta do Target ter sido recebida e analisada por `filterRecommendationBasedOnOffer()` |

Essa foi uma atualização mais sofisticada que fizemos no aplicativo com a solicitação que adicionamos à tela inicial, portanto, vamos analisar o que fizemos:

1. Interrompemos o comportamento anterior do aplicativo de mostrar três promoções padrão, comentando as linhas de código
1. Pedimos ao aplicativo para executar uma nova função, que nomeamos arbitrariamente targetLoadRequest
1. Definimos a função `targetLoadRequest` para fazer uma solicitação ao Target usando o método Target.loadRequest e executar imediatamente a função `filterRecommendationBasedOnOffer()` quando a resposta de oferta [!DNL Target] for recebida
1. A função `filterRecommendationBasedOnOffer()` interpreta a resposta e decide quais promoções devem ser aplicadas à tela

Este é um padrão de uso muito comum ao usar [!DNL Target] em aplicativos móveis.  É muito eficiente, na medida em que você pode personalizar quase qualquer aspecto do seu aplicativo móvel. Também requer coordenação entre o código do aplicativo e as ofertas que definiremos posteriormente na interface [!DNL Target]. Devido a essa coordenação, alguns casos de uso de personalização podem exigir que você atualize seu aplicativo na loja de aplicativos para iniciar a atividade.

### Validar a solicitação em tempo real

Abra o Android Emulator e percorra todas as etapas para reservar uma viagem: Início > Resultados da pesquisa no ônibus > Seleção de assentos, Opções de pagamento (qualquer opção de pagamento com dados em branco funcionará).

Na tela final Thank You (Obrigado), assista Logcat pela resposta. A resposta deve informar &quot;O conteúdo padrão foi retornado para &quot;wetravel_context_dest&quot;:

![Adicionar um local em tempo real na tela de agradecimento](assets/thankyou_validation.jpg)

## Limpando locais previamente buscados do cache

Pode haver situações em que os locais previamente buscados precisem ser apagados durante uma sessão. Por exemplo, quando ocorre uma reserva, faz sentido limpar os locais em cache, já que o usuário agora está &quot;envolvido&quot; e entende o processo de reserva. Se reservarem outra viagem durante a sessão, não precisarão dos locais originais na tela inicial e na tela de resultados da pesquisa para orientar sua reserva. Faria mais sentido limpar os locais do cache e buscar previamente novas ofertas para, talvez, uma segunda reserva com desconto ou outro cenário relevante. A lógica pode ser adicionada à tela inicial e à tela de resultados da pesquisa para buscar previamente novos locais se uma reserva tiver ocorrido durante a sessão.

Neste exemplo, simplesmente limparemos os locais previamente buscados para a sessão quando ocorrer uma reserva. Isso é feito chamando a função `Target.clearPrefetchCache()`. Defina a função dentro da função `targetLoadRequest()` como mostrado abaixo:

```java
Target.clearPrefetchCache()
```

![Limpar Locais Buscados previamente do Cache](assets/clearPrefetch.jpg)

Parabéns! Seu aplicativo agora tem a estrutura para personalização. Na próxima lição, aprimoraremos nossos recursos de personalização adicionando parâmetros a esses locais.

**[NEXT: &quot;Adicionar Parâmetros&quot; >](add-parameters.md)**
