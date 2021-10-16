---
title: Baixe e atualize o aplicativo de amostra We.Travel
description: 'O aplicativo de amostra We.Travel é pré-implementado com o SDK do Adobe Mobile Services v4. Você só precisa atualizá-lo para que ele aponte para suas próprias contas Experience Cloud Org e solução.   '
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 244bcf7a-b59b-4dd1-bd05-0a55ce7a7132
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# Baixe e atualize o aplicativo de amostra We.Travel

O aplicativo de amostra We.Travel é pré-implementado com o SDK do Adobe Mobile Services v4. Você só precisa atualizá-lo para que ele aponte para suas próprias contas de solução e organização do Experience Cloud.

## Objetivos de aprendizagem

Ao final desta lição, você poderá:

* Baixe e abra o aplicativo de amostra We.Travel no Android Studio
* Verifique e atualize as configurações do SDK do Mobile Services para [!DNL Target]

## Baixe o aplicativo We.Travel

* Baixe o [sample-app-android-SDKv4-Base-Version.zip](assets/sample-app-android-SDKv4-Base-Version.zip)
* Descomprima o arquivo zip
* Abra o aplicativo no Android Studio como um projeto existente (ignore quaisquer erros sobre &quot;Mapeamento de raiz VCS inválido&quot;)
* Execute o aplicativo em um emulador para confirmar se o aplicativo é criado e você pode ver a tela inicial
* Navegue pelo aplicativo e verifique se você pode concluir o processo de reserva (selecione qualquer opção de pagamento e clique em &quot;Continuar&quot; para ignorar a tela de faturamento!)

   ![Abra a tela ](assets/wetravel_homeScreen.png)![appConfirmation .](assets/wetravel_confirmationScreen.png)

## Verifique e atualize as configurações do SDK do Mobile Services para [!DNL Target]

O SDK do Adobe Mobile Services foi pré-instalado no aplicativo We.Travel [de acordo com a documentação](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=en). Agora, você atualizará a instalação para apontar para sua própria conta [!DNL Target].

Primeiro, crie um novo aplicativo na interface do usuário do Mobile Services:

1. Faça logon na interface [Adobe Mobile Services](https://mobilemarketing.adobe.com/).
1. Vá para [!UICONTROL Gerenciar aplicativos] e clique em **[!UICONTROL Adicionar]** para adicionar um novo aplicativo para usar com este tutorial (**[!UICONTROL Gerenciar aplicativos]** > **[!UICONTROL Adicionar]**).
1. Escolha um conjunto de relatórios do Analytics com dados de não produção, dê um nome ao aplicativo, selecione o tipo **[!UICONTROL Padrão]** e clique em **[!UICONTROL Salvar]**.
1. Depois que o aplicativo for adicionado, adicione seu [!DNL Target] Código do cliente na próxima tela na seção [!UICONTROL Opções do SDK do Target] (você pode encontrar o código do cliente na interface [!DNL Target] em **[!UICONTROL Configuração]** > **[!UICONTROL Implementação]** > **[!UICONTROL Editar configurações]**, ao lado do Download 0/> ).`at.js`
1. A configuração [!UICONTROL Tempo limite da solicitação] determina quanto tempo o aplicativo aguarda pela resposta do servidor [!DNL Target] antes de executar as instruções de tempo limite. Apenas deixe a configuração padrão.
1. Ative o [!UICONTROL Serviço de ID de visitante] e verifique se [!UICONTROL Organização] está selecionado no menu suspenso.
1. Salve as alterações clicando em **[!UICONTROL Salvar]** no lado superior direito da janela (não aquele nas opções [!UICONTROL Links universais], [!UICONTROL Links de aplicativo] ou [!UICONTROL Serviços de push]).
1. Role até a seção Downloads do SDK para aplicativos , na parte inferior da página, e baixe o arquivo de configuração:

   ![Baixar o arquivo de configuração](assets/config_file.jpg)

1. Substitua o arquivo `ADBMobileConfig.json` na pasta de ativos do projeto Android Studio (aplicativo > src > principal > ativos).

1. Agora, abra o arquivo `ADBMobileConfig.json` e verifique se ele contém as alterações esperadas, como seu [!DNL Target] Código do cliente e seus detalhes do Analytics:
   ![Baixar o arquivo de configuração](assets/client_code.jpg)

Se não vir suas configurações, confirme que você clicou no botão **[!UICONTROL Salvar]** correto na interface do [!UICONTROL Mobile Services] e copiou o arquivo para o local correto.

Parabéns! Você atualizou o SDK com seus detalhes de conta [!DNL Target]! Faremos uma validação adicional da configuração depois de adicionarmos solicitações [!DNL Target] na próxima lição.

**[PRÓXIMO : &quot;Adicionar solicitações do Target&quot; >](add-requests.md)**
