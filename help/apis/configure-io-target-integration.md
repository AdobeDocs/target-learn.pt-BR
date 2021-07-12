---
title: Como configurar a autenticação para APIs do Adobe Target
description: Este tutorial orienta os desenvolvedores pelas etapas necessárias para gerar tokens de autenticação para interagir com as APIs do Adobe Target com êxito. Siga estas etapas para usar o Console do desenvolvedor do Adobe para gerar e testar o token de acesso do portador, que é necessário para usar as APIs do Target.
role: Developer, Admin, Architect
level: Intermediate
topic: Personalização, administração, integrações, desenvolvimento
feature: APIs/SDKs, Administração e configuração
doc-type: tutorial
kt: null
thumbnail: null
author: Judy Kim
exl-id: 8a1e93e4-67b2-4942-a8da-fc0f2cbb2df2
source-git-commit: ee9aac0144e35abf32c5d8eafe10a013bf30d8d3
workflow-type: tm+mt
source-wordcount: '1892'
ht-degree: 2%

---

# Configurar autenticação para APIs do Adobe Target

As APIs de administrador do Adobe Target, incluindo [!DNL Recommendations] APIs de administrador, são protegidas por autenticação para garantir que somente usuários autorizados as usem para acessar o Adobe Target. Use o [Console do Desenvolvedor do Adobe](https://console.adobe.io/) para gerenciar essa autenticação para todas as soluções da Adobe Experience Cloud, incluindo [!DNL Target].

Esta lição aborda as etapas preliminares necessárias para gerar tokens de autenticação necessários para interagir com as APIs do Adobe Target com êxito. Nas seções a seguir, você:

1. Crie um projeto (anteriormente chamado de integração) no Console do desenvolvedor do Adobe.
2. Exporte detalhes do projeto para o Postman.
3. Gere um token de acesso ao portador.
4. Teste o token de acesso do portador.

## Pré-requisitos

| Recurso | Detalhes |
| --- | --- |
| Postman | Para concluir essas etapas com sucesso, obtenha o [Aplicativo Postman](https://www.postman.com/downloads/) para seu sistema operacional. O Postman Basic é gratuito com a criação de contas. Embora não seja necessário para usar as APIs do Adobe Target em geral, o Postman facilita os fluxos de trabalho da API e o Adobe Target fornece várias coleções de Postman para ajudar a executar suas APIs e aprender como elas operam. O resto deste tutorial assume conhecimento prático de Postman. Para obter ajuda, consulte a [documentação do Postman](https://learning.getpostman.com/). |
| Referências | A familiarização com os seguintes recursos é assumida no restante deste tutorial:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentação do Target Adobe I/O](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentação da API do Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

## Criar um projeto do Adobe I/O

Nesta seção, você acessará o Console do desenvolvedor do Adobe e criará um projeto para [!DNL Adobe Target]. Para obter mais informações, consulte a [documentação sobre projetos](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects.md).

<!--1. Generate your private key and public certificate, per the [documentation on authentication](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWTCertificate.md). //<!--as described in **Step 1** of [How to set up Adobe IO: Authentication - Step by Step](https://helpx.adobe.com/marketing-cloud-core/kb/adobe-io-authentication-step-by-step.html). After completing Step 1, return to this tutorial and resume with Step 2, below. // The outcome of this step should be the creation of a `private.key` file and a `certificate_pub.crt` file. Return to this tutorial once you have generated these two files.-->

1. No [Adobe Admin Console](https://adminconsole.adobe.com/), verifique se sua conta de usuário do Adobe recebeu acesso ao nível [Administrador de produto](https://helpx.adobe.com/enterprise/using/admin-roles.html) e [Desenvolvedor](https://helpx.adobe.com/enterprise/using/manage-developers.html) para [!DNL Target].

2. No [Console do Desenvolvedor do Adobe](https://console.adobe.io/), selecione a Organização do Experience Cloud para a qual deseja criar essa integração. (Observe que é provável que você só tenha acesso a uma única organização do Experience Cloud.)

   ![configure-io-target-create-project2.png](assets/configure-io-target-createproject2.png)

3. Clique em **[!UICONTROL Criar novo projeto]**.

   ![configure-io-target-create-project3.png](assets/configure-io-target-createproject3.png)

4. Clique em **[!UICONTROL Adicionar API]** para adicionar uma REST API ao seu projeto para acessar serviços e produtos do Adobe.

   ![Adicionar API](assets/configure-io-target-createproject4.png)

5. Selecione **[!DNL Adobe Target]** como o serviço do Adobe com o qual deseja integrar. Clique no botão **[!UICONTROL Next]** que aparece.

   ![configure-io-target-create-project5](assets/configure-io-target-createproject5.png)

6. Selecione uma opção para associar chaves públicas e privadas à integração da conta de serviço que você está criando para o Target. Para este tutorial, selecione **[!UICONTROL Opção 1: Gere um par de chaves]** e clique em **[!UICONTROL Generate keypair]**.
   ![configure-io-target-create-project6](assets/configure-io-target-createproject6.png)

7. Observe os resultados! Conforme instruído, anote o arquivo de configuração baixado automaticamente (`config`), que contém a chave privada. Clique em **[!UICONTROL Avançar]**.
   ![configure-io-target-create-project7](assets/configure-io-target-createproject7.png)
8. No sistema de arquivos, verifique o local de `config`, que é o arquivo de configuração compactado criado na etapa anterior. Novamente, esse arquivo `config` contém sua chave privada, que será necessária posteriormente. A localização exata em seu sistema de arquivos pode diferir da mostrada aqui.
   ![configure-io-target-create-project8](assets/configure-io-target-createproject8.png)
9. De volta ao Console do desenvolvedor do Adobe, selecione os [perfis de produto](https://helpx.adobe.com/enterprise/using/manage-products-and-profiles.html) correspondentes às propriedades em que você está usando [!DNL Recommendations]. (Se não estiver usando propriedades, selecione a opção Espaço de trabalho padrão.) Clique em **[!UICONTROL Salvar API configurada]**.
   ![configure-io-target-create-project9](assets/configure-io-target-createproject9.png)

10. Clique em **[!UICONTROL Criar integração]**. Você deve receber uma mensagem temporária indicando que sua API foi configurada com êxito.

11. Como etapa final, renomeie seu projeto com um nome mais significativo do que o `Project 1` original. Para fazer isso, navegue até o projeto usando o caminho de navegação como mostrado, clique em **[!UICONTROL Editar projeto]** para acessar o modal **[!UICONTROL Editar projeto] e renomeie o projeto.

![configure-io-target-create-project11](assets/configure-io-target-createproject11.png)

>[!NOTE]
> 
>Neste tutorial, nomeamos o projeto como &quot;Integração do Target&quot;. Se você desejar usar o projeto para mais do que apenas o Adobe Target, convém nomeá-lo adequadamente. Por exemplo, você pode optar por nomeá-lo como &quot;APIs do Adobe&quot; ou &quot;APIs do Experience Cloud&quot;, já que ele pode ser usado com outras soluções na Adobe Experience Cloud.

## Exportar detalhes do projeto

Agora que você tem um projeto do Adobe que pode usar para acessar [!DNL Target], é necessário enviar detalhes desse projeto junto com as solicitações da API do Adobe. Esses detalhes são necessários para interagir com várias APIs do Adobe, incluindo várias [!DNL Target] APIs. Por exemplo, os detalhes de integração incluem informações de autorização e autenticação exigidas pelas [!DNL Target] APIs de administração. Portanto, para usar as APIs com o Postman, é necessário inserir esses detalhes no Postman.

Há muitas maneiras de especificar os detalhes do seu projeto no Postman, mas nesta seção, aproveitamos alguns recursos e coleções pré-construídos. Primeiro (nesta seção), você exportará os detalhes da sua integração para um ambiente Postman. Em seguida (na seção a seguir), você gerará um token de acesso do portador para conceder acesso aos recursos de Adobe necessários.

>[!NOTE]
>
>Para obter instruções de vídeo aplicáveis a qualquer solução de Experience Cloud, incluindo [!DNL Target], consulte [Usar Postman com APIs de Experience Platform](https://docs.adobe.com/content/help/en/platform-learn/tutorials/apis/postman.html). As seguintes seções são relevantes para as APIs [!DNL Target]:
>
> 1. Exportar detalhes de integração do Adobe I/O para o Postman
> 2. Gerar um token de acesso com o Postman

>
> 
Essas etapas também são fornecidas abaixo.

1. Ainda no [Console do Desenvolvedor do Adobe](https://console.adobe.io/), navegue para exibir as credenciais **[!UICONTROL Conta de Serviço (JWT)]** do seu novo projeto. Use a navegação à esquerda ou a seção **[!UICONTROL Credenciais]**, conforme mostrado.
   ![JWT1](assets/configure-io-target-jwt1.png)
Em detalhes  **[!UICONTROL de Credencial]**, observe que você pode visualizar suas chaves  **públicas,** a ID do  **cliente** e outras informações relacionadas à sua conta de serviço.
   ![JWT1a](assets/configure-io-target-jwt1a.png)
2. Clique em para navegar até as informações sobre a API **[!UICONTROL Adobe Target]**. Use a navegação à esquerda ou a seção **[!UICONTROL Connected products and services]**, conforme mostrado.
   ![JWT2](assets/configure-io-target-jwt2.png)
3. Clique em **[!UICONTROL Baixar para Postman]** > **[!UICONTROL Conta de serviço (JWT)]** para criar um arquivo JSON capturando suas informações de autenticação para um ambiente Postman.
   ![JWT3](assets/configure-io-target-jwt3.png)
Anote o arquivo JSON em seu sistema de arquivos.
   ![JWT3a](assets/configure-io-target-jwt3a.png)
4. No Postman, clique no ícone de engrenagem para gerenciar seus ambientes e clique em **Importar** para importar o arquivo JSON (ambiente).
   ![JWT4](assets/configure-io-target-jwt4.png)
5. Escolha seu arquivo e clique em **Open**.
   ![JWT5](assets/configure-io-target-jwt5.png)
6. No modal Postman **Gerenciar ambientes**, clique no nome do ambiente recém-importado para inspecioná-lo. (O nome do ambiente pode ser diferente do mostrado aqui. Edite o nome conforme desejado. Ela não precisa necessariamente corresponder ao nome do Adobe project.)
   ![JWT6](assets/configure-io-target-jwt6.png)
7. Observe que `CLIENT_SECRET` e `API_KEY` (juntamente com outras variáveis) têm seus valores preenchidos previamente, obtidos da integração, conforme definido no Console do desenvolvedor do Adobe. (A variável Postman `CLIENT_SECRET` deve corresponder à credencial de Adobe `CLIENT SECRET`, conforme exibida no Console do desenvolvedor, e `API_KEY` no Postman também deve corresponder a `CLIENT ID` no Console do desenvolvedor.) Por outro lado, as notas `PRIVATE_KEY`, `JWT_TOKEN` e `ACCESS_TOKEN` estão em branco. Vamos começar fornecendo o valor `PRIVATE_KEY`.
   ![JWT7](assets/configure-io-target-jwt7.png)

   >[!NOTE]
   >
   >**Surpresa!**
   >
   >Teste de pop! Você consegue se lembrar onde está sua chave privada?
   >Está certo, está no arquivo `config` baixado anteriormente do Console do Desenvolvedor do Adobe!

8. No sistema de arquivos, abra o arquivo `config` e abra o arquivo de chave `private`.
   ![JWT8](assets/configure-io-target-jwt8.png)
9. Selecione e copie todo o conteúdo do arquivo de chave `private`.
   ![JWT9](assets/configure-io-target-jwt9.png)
10. No Postman, cole o valor da chave privada nos campos **VALOR INICIAL** e **VALOR ATUAL**.
   ![JWT10](assets/configure-io-target-jwt10.png)
11. Clique em **[!UICONTROL Atualizar]** e feche o modal Ambientes.


## Gerar o token de acesso do portador

Nesta seção, você gera o token de acesso do portador, que é necessário para autenticar sua interação com APIs do Adobe Target. Para gerar o token de acesso do portador, é necessário enviar os detalhes de integração (estabelecidos nas seções anteriores) para o [Adobe Identity Management Service (IMS)](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/AuthenticationGuide.md). Há algumas maneiras diferentes de fazer isso, mas neste tutorial, criamos uma solicitação de POST bespoke para a API IMS. Só brincando. Neste tutorial, aproveitamos uma coleção Postman contendo uma chamada IMS pré-criada que torna o processo direto e fácil. Depois de importar a coleção, você pode reutilizá-la sempre que necessário para gerar novos tokens não apenas para o Adobe Target, mas também para outras APIs do Adobe.

1. Navegue até o [Adobe Identity Management Service API de exemplo de chamadas](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims).
   ![token1](assets/configure-io-target-generatetoken1.png)
2. Clique na coleção **Postman de geração de token de acesso ao Adobe I/O**.
   ![token2](assets/configure-io-target-generatetoken2.png)
3. Obtenha o JSON bruto para esta coleção clicando em **Raw** e copiando o JSON resultante para a área de transferência. (Como alternativa, você pode salvar o JSON bruto como um arquivo .json.)
   ![token3](assets/configure-io-target-generatetoken3.png)
4. No Postman, importe a coleção colando e enviando o JSON bruto da área de transferência. (Como alternativa, você pode fazer upload do arquivo .json que você salvou.) Clique em **Continuar**.
   ![token4](assets/configure-io-target-generatetoken4.png)
5. Selecione o **[!UICONTROL IMS: Gerar JWT + Auth por meio de solicitação de Token de usuário]** na coleção Postman de geração de token de acesso ao Adobe I/O, verifique se o ambiente está selecionado e clique em **Enviar** para gerar o token.

   ![token5](assets/configure-io-target-generatetoken5.png)

   >[!NOTE]
   >
   >Esse token de acesso do portador será válido por 24 horas. Envie a solicitação novamente sempre que precisar gerar um novo token.

6. Abra o modal Gerenciar ambientes novamente e selecione o ambiente.
   ![token6](assets/configure-io-target-jwt11.png)
7. Observe que os valores `ACCESS_TOKEN` e `JWT_TOKEN` agora estão preenchidos.
   ![token7](assets/configure-io-target-generatetoken7.png)

>[!NOTE]
>
>P: Preciso usar a coleção Postman de geração de token de acesso ao Adobe I/O para gerar o JSON Web Token (JWT) e o token de acesso do portador?
>
>A: Não! A coleção Adobe I/O Access Token Generation Postman está disponível como uma conveniência para gerar mais facilmente o JWT e o token de acesso ao portador no Postman. Como alternativa, você pode usar recursos no Console do desenvolvedor do Adobe para gerar manualmente o token de acesso do portador.

## Teste o token de acesso do portador

Neste exercício, você usará seu novo token de acesso do portador enviando uma solicitação de API que recupera uma lista de atividades da sua conta [!DNL Target]. Uma resposta bem-sucedida indica que o projeto do Adobe e a autenticação estão funcionando como esperado para usar a API.

1. Importe as [APIs de administrador do Adobe Target Postman Collection](https://developers.adobetarget.com/api/#admin-postman-collection). Siga todos os prompts até que a coleção seja importada no Postman.
   ![testtoken1](assets/configure-io-target-testtoken0.png)
1. Expanda a coleção e observe a solicitação **[!UICONTROL List activities]**.
   ![testtoken1](assets/configure-io-target-testtoken1.png)
1. Observe que variáveis como `{{access_token}}` estão inicialmente por resolver. Você pode resolver isso de várias maneiras diferentes, por exemplo, você pode definir uma nova variável de coleção chamada `{{access_token}}`, mas neste tutorial, você alterará a solicitação da API para aproveitar o ambiente Postman que estava usando anteriormente. Isso permitirá que o ambiente continue a servir como uma consolidação única e consistente de todas as variáveis comuns entre as APIs do Adobe.
   ![testtoken2](assets/configure-io-target-testtoken2.png)
1. Digite para substituir `{{access_token}}` por `{{ACCESS_TOKEN}}`.
   ![testtoken3](assets/configure-io-target-testtoken3.png)
1. Digite para substituir `{{api_key}}` por `{{API_KEY}}`.
   ![testtoken4](assets/configure-io-target-testtoken4.png)
1. Digite para substituir `{{tenant}}` por `{{TENANT_ID}}`. Observação `{{TENANT_ID}}` ainda não foi reconhecida.
   ![testtoken4](assets/configure-io-target-testtoken4a.png)
1. Abra o modal Gerenciar ambientes e selecione o ambiente.
   ![JWT11](assets/configure-io-target-jwt11.png)
1. Digite para adicionar uma nova variável de ambiente `{{TENANT_ID}}`. Copie e cole o valor da ID do locatário nos campos **VALOR INICIAL** e **VALOR ATUAL** para a nova variável de ambiente `TENANT_ID`.

   ![testtoken5](assets/configure-io-target-testtoken5.png)

   >[!NOTE]
   >
   >A ID do locatário é diferente de seu [!DNL Target] `clientcode`. A ID do locatário existe no URL quando você está conectado a [!DNL Target]. Para obter sua ID do locatário, faça logon no [!DNL Adobe Experience Cloud], abra [!DNL Target] e clique no cartão [!DNL Target]. Use o valor da ID do locatário, conforme observado no subdomínio do URL.
   >
   >Por exemplo, se o URL quando conectado ao Adobe Target for
   >
   >`<https://mycompany.experiencecloud.adobe.com/...>`
   >
   >então sua ID do locatário é &quot;minha empresa&quot;.

1. Envie sua solicitação após verificar se você selecionou o ambiente correto. Você deve receber uma resposta contendo sua lista de atividades.
   ![testtoken6](assets/configure-io-target-testtoken6.png)

Parabéns! Depois de verificar a autenticação do Adobe, é possível usá-la para interagir com as APIs do Adobe Target (bem como com outras APIs do Adobe). Por exemplo, você pode [Usar APIs do Recommendations](https://docs.adobe.com/content/help/en/target-learn/recommendations-api-tutorial/recs-api-overview.html) para criar ou gerenciar recomendações.
