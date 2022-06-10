---
title: Otimizar a implementação do Adobe Target
description: 'Obtenha uma visão geral da implementação e estrutura do Adobe Target. Saiba como entender e auditar a configuração de sua organização. Saiba mais sobre as técnicas comuns de solução de problemas e dicas sobre como criar um repositório de conhecimento para sua equipe. '
solution: Target
source-git-commit: fd679d3fc2c72b9852d8129adf8c1187bf22b25f
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 0%

---

# Otimizar a implementação do Adobe Target

Se você é novo em sua organização e deseja se familiarizar com o que está em vigor em uma prática de teste e otimização, este artigo ajuda a começar. Começaremos com uma visão geral da implementação e da estrutura do Adobe Target. Você aprenderá a entender e auditar a configuração de sua organização. Por fim, discutiremos técnicas comuns de solução de problemas e dicas sobre como criar um repositório de conhecimento para sua equipe.

O Adobe Target é uma ferramenta que permite testar e direcionar conteúdo exclusivo para visitantes diferentes. Para obter uma visão geral dos recursos disponíveis, [visite este guia](https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en).

## Implementação e estrutura do Target

Antes de mergulharmos no processo de implementação do Adobe Target ou em como ele é estruturado, é útil compreender primeiramente alguns fundamentos sobre o software.

O Adobe Target é uma ferramenta que permite o teste e o direcionamento de conteúdo único para visitantes diferentes sem alterar o código do site nativo. O Target altera temporariamente a experiência do usuário final, bem como rastreia o comportamento dos usuários depois de ver a alteração. O Target também oferece a capacidade de alterar a experiência para usuários finais com base em informações de perfil ou ações anteriores.

Há três tipos de atividades fundamentais do Target:

1. Teste A/B
2. Teste multivariado (MVT)
3. Teste de experiência

**O teste A/B** compara duas ou mais experiências para ver qual melhora mais conversões durante um período de teste pré-especificado. O teste A/B é um experimento altamente controlado com medidas de tráfego, divididas por porcentagens em vez de por uma regra, permitindo:

* para analisar os dados do teste.
* para obter insights sobre seu público.
* para determinar qual experiência tem o melhor desempenho.

**Teste multivariado** (MVT) compara combinações de ofertas entre elementos em uma página para ver qual combinação tem o melhor desempenho para um público-alvo específico. Esse teste também identifica qual elemento da página melhora mais conversões durante um período de teste pré-especificado. O MVT fornece:

* Uma maneira de exibir várias ofertas em vários elementos.
* Um método para testar a experiência exclusiva resultante em relação a uma meta específica.
* Insight sobre quais elementos têm o maior impacto negativo ou positivo nas interações do visitante.

**Teste de experiência** (Direcionamento experienciado) fornece conteúdo para um público-alvo específico com base em um conjunto de regras e critérios definidos pelo profissional de marketing. Esse método fornece uma maneira de direcionar conteúdo específico a um público-alvo específico com base em um conjunto de regras de alocação definidas.

Como funciona o Target?

Este é um exemplo de alto nível de como o Target funciona:

1. Um visitante solicita uma página do seu servidor e ela é exibida no navegador.
1. Um cookie próprio é definido no navegador do visitante para armazenar o comportamento.
1. A página chama o Adobe Target.
1. O conteúdo é exibido com base nas regras da atividade do usuário.
1. O Adobe Target captura métricas específicas, conforme definido na configuração da atividade, para medir o impacto das experiências de teste.

O Target é criado em uma &quot;mbox global&quot; que fornece a capacidade de afetar qualquer item na página. Esse recurso é implantado no carregamento da página como um link codificado para o arquivo at.js ou é entregue usando um Tag Manager, como o Adobe Launch.

## Entender sua implementação atual

Para entender sua implementação atual, o Adobe recomenda que você revise a implementação da interface do usuário do Target junto com o Gerenciador de tags e a implementação do Carregamento de página.

**Para revisar sua [!DNL Target] interface do usuário:**

1. Inicie sua revisão no [!DNL Target] IU:

   * Revise o [!DNL Target] pilha de tecnologia
   * Confirme os recursos disponíveis
   * Identificar onde a implantação está ativa

1. Analise as atividades para obter as práticas recomendadas:

   * Revisar campanhas históricas para a maturidade do programa

1. Desativar atividades antigas:

   * Arquivar e limpar [!DNL Target] ativo que não tem mais uso atual ou futuro

1. Revisar públicos-alvo.

1. Analise as definições do ambiente e os domínios associados.

1. Revisar scripts de perfil para aplicabilidade

   * Todos os scripts de perfil são executados em cada chamada de destino
   * Manter eficiência de chamada removendo scripts não aplicáveis

Para revisar o gerenciador de tags e o carregamento da página:

1. Confirme o seguinte no gerenciador de tags:

   * A implantação do [!DNL Target] Código JavaScript
   * A solução apropriada de ocultação de conteúdo
   * Defina as regras necessárias para preencher o [!DNL Target] chamadas com os parâmetros esperados

1. Confirme o seguinte durante o carregamento da página:

   * Correspondência de números de versão para o URL da solicitação e [!DNL Target] URL da solicitação
   * Valor preenchido da Experience Cloud ID (Corpo da nuvem)
   * Valores de integração esperados (corpo na nuvem)
   * Preenchido [!DNL Target] parâmetros nas páginas apropriadas

## [!DNL Target] atividades de auditoria

Para evitar a passagem manual de cada página para auditoria [!DNL Target] , use o Adobe Auditor para ajudar a entender o estado técnico atual de sua implementação. O Adobe Auditor é fornecido pelo ObservePoint e pode ser configurado para ser executado em um nível manual, para identificar problemas de implementação de alto nível no site.

O Adobe Auditor fornece:

* Um bom funcionamento do site
* Chamadas rápidas para problemas de implementação

A Adobe recomenda realizar auditorias manuais mensais para:

* Identificar páginas não marcadas
* Identificar versões inconsistentes
* Descubra versões desatualizadas
* Fornecer informações detalhadas que podem ser exportadas

## Solução de problemas comum

>[!NOTE]
>
>O Adobe recomenda instalar o Adobe Experience Platform Debugger.

Estas são as dicas gerais de solução de problemas ao inserir a Experiência:

### Cache e cookies**

* Limpar cache e cookies
* Tenha cuidado ao usar o modo privado (por exemplo: o modo privado no Firefox pode ser bloqueado [!DNL Target])

### Você está qualificado para a atividade?

* Verifique se você executou as mesmas etapas que o público-alvo usado na atividade
* Use `mboxTrace` ou tokens de resposta para verificar os valores do perfil e do segmento

### Dicas gerais de solução de problemas ao validar visual/funcional

Se estiverem na variável [!DNL Target] e você não verá a experiência visual esperada:

Verifique a [!DNL Target] resposta:

* Se o código não for executado:

1. Verificar atividades conflitantes
1. Entre em contato com o Atendimento ao cliente

* Se o código for executado:

1. Retrabalhe o código nesse cenário

## Manutenção de um repositório de conhecimento

Um repositório de conhecimento é uma plataforma online usada para documentar e compartilhar informações. O repositório de conhecimento contém informações específicas da sua implementação e pode conter informações específicas da equipe.

Idealmente, o repositório deve permitir a edição e o salvamento automático na plataforma. Depois de configurado inicialmente, é fácil manter-se atualizado. O conteúdo no Repositório de Conhecimento é preparado com base nas funções do usuário.

Os documentos típicos em um Repositório de Conhecimento incluem:

* **Documento de visão geral** - um documento utilizado para explicar claramente os objetivos, os objetivos, os processos e a estrutura dos programas
* **Repositório de ideias** - um documento usado para gerenciar e priorizar ideias potenciais que não estejam prontas para o processo de teste
* **Roteiro do programa** - um documento usado para gerenciar todos os aspectos das atividades de teste, uma vez que as ideias estejam prontas para iniciar o processo de teste
* **Documento do plano de atividade** - um documento usado para destacar as informações necessárias para criar e iniciar atividades
* **Documento do plano de atividade** - um documento utilizado para comunicar os resultados e as próximas etapas recomendadas às partes interessadas
* **Painel de programas** - um documento usado para acompanhar o desempenho do programa, a cadência e os benefícios de receita ao longo do tempo.

Para obter mais informações, consulte nossa [webinário](https://adobecustomersuccess.adobeconnect.com/p4p7xlp7dh42mp4/) com o Consultor Sênior, Wilder Freed.
