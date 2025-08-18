---
title: Otimizar a implementação do Adobe Target
description: Obtenha uma visão geral da implementação e estrutura do Adobe Target. Saiba como entender e auditar a configuração de sua organização. Saiba mais sobre as técnicas e dicas comuns de solução de problemas na criação de um repositório de conhecimento para sua equipe.
solution: Target
feature: Overview
role: Leader, User
exl-id: 49b69f41-0993-437c-bb69-84392be427df
source-git-commit: 20bd1eb17ef6e287f7b76e14f727456e12d6f115
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 0%

---

# Otimizar a implementação do Adobe Target

Se você é novo na organização e deseja se familiarizar com o que está em vigor a partir de uma prática de teste e otimização, este artigo ajuda a começar. Começaremos com uma visão geral da implementação e da estrutura do Adobe Target. Você aprenderá a entender e auditar a configuração de sua organização. Por fim, discutiremos técnicas comuns de solução de problemas e dicas sobre como criar um repositório de conhecimento para sua equipe.

O Adobe Target é uma ferramenta que permite testar e direcionar conteúdo exclusivo para visitantes diferentes. Para obter uma visão geral dos recursos disponíveis, [visite este guia](https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en).

## Implementação e estrutura do Target

Antes de analisarmos o processo de implementação do Adobe Target ou como ele é estruturado, é útil compreender alguns fundamentos sobre o software.

O Adobe Target é uma ferramenta que permite testar e direcionar conteúdo exclusivo para visitantes diferentes sem alterar o código nativo do site. O Target altera temporariamente a experiência do usuário final, além de rastrear o comportamento dos usuários após ver a alteração. O Target também oferece a capacidade de alterar a experiência para usuários finais com base em informações de perfil ou ações anteriores.

Há três tipos de atividades fundamentais do Target:

1. Teste A/B
2. Teste multivariado (MVT)
3. Teste de experiência

**O teste A/B** compara duas ou mais experiências para ver qual melhora mais conversões durante um período de teste pré-especificado. O teste A/B é um experimento altamente controlado com medições de tráfego, dividido por porcentagens em vez de por uma regra, que permite:

* para analisar os dados de teste.
* para obter insights sobre seu público-alvo.
* para determinar qual experiência tem o melhor desempenho.

O **Multivariate testing** (MVT) compara combinações de ofertas entre elementos em uma página para ver qual combinação tem o melhor desempenho para um público-alvo específico. Este teste também identifica qual elemento da página melhora mais conversões durante um período de teste pré-especificado. O MVT fornece:

* Uma maneira de exibir várias ofertas em vários elementos.
* Um método para testar a experiência exclusiva resultante em relação a uma meta específica.
* Insight para saber quais elementos têm mais impacto negativo ou positivo nas interações do visitante.

O **teste de experiência** (direcionamento experiente) fornece conteúdo a um público específico com base em um conjunto de regras e critérios definidos pelo profissional de marketing. Esse método oferece uma maneira de direcionar conteúdo específico a um público-alvo específico com base em um conjunto de regras de alocação definidas.

Como funciona o Target?

Este é um exemplo de alto nível de como o Target funciona:

1. Um visitante solicita uma página do seu servidor e ela é exibida no navegador.
1. Um cookie próprio é definido no navegador do visitante para armazenar o comportamento.
1. A página chama o Adobe Target.
1. O conteúdo é exibido com base nas regras da atividade do usuário.
1. O Adobe Target captura métricas específicas, conforme definido na configuração da atividade, para medir o impacto das experiências de teste.

O Target é construído em uma &quot;Mbox global&quot; que oferece a capacidade de afetar qualquer item na página. Esse recurso é implantado no carregamento da página como um link codificado para o arquivo at.js ou é entregue usando um Gerenciador de tags, como o Adobe Launch.

## Entenda sua implementação atual

Para entender sua implementação atual do, a Adobe recomenda que você revise sua implementação da interface do usuário do Target junto com seu Gerenciador de tags e implementação de carregamento de página.

**Para examinar a interface de usuário do [!DNL Target]:**

1. Comece sua análise na interface do usuário do [!DNL Target]:

   * Revise a pilha de tecnologia do [!DNL Target]
   * Confirmar os recursos disponíveis
   * Identificar onde a implantação está ativa

1. Atividades de análise para práticas recomendadas:

   * Revisar campanhas históricas de maturidade do programa

1. Desativar atividades antigas:

   * Arquivar e limpar o ativo [!DNL Target] que não tem mais uso atual ou futuro

1. Revise os públicos-alvo.

1. Revise as definições de ambiente e os domínios associados.

1. Revisar scripts de perfil quanto à aplicabilidade

   * Todos os scripts de perfil são executados em cada chamada de público alvo
   * Manter a eficiência da chamada removendo scripts não aplicáveis

Para revisar o gerenciador de tags e o carregamento de página:

1. Confirme o seguinte no gerenciador de tags:

   * A implantação do código JavaScript [!DNL Target] esperado
   * A solução apropriada para ocultação de conteúdo
   * Definir as regras necessárias para preencher as chamadas [!DNL Target] com os parâmetros esperados

1. Confirme o seguinte durante o carregamento da página:

   * Correspondência de números de versão para a URL de solicitação e a URL de solicitação [!DNL Target]
   * Valor da Experience Cloud ID preenchido (corpo da nuvem)
   * Apresentar os valores de integração esperados (corpo na nuvem)
   * Preencheu [!DNL Target] parâmetros nas páginas apropriadas

## [!DNL Target] atividades de auditoria

Para evitar percorrer manualmente cada página para auditar [!DNL Target] atividades, use o Adobe Auditor para ajudá-lo a entender o estado técnico atual de sua implementação. O Adobe Auditor é disponibilizado pelo ObservePoint e pode ser configurado para execução manual, a fim de identificar problemas de implementação de alto nível no site.

O Adobe Auditor fornece:

* Uma integridade de site alta
* Chamadas rápidas para problemas de implementação

A Adobe recomenda realizar auditorias manuais mensais para:

* Identificar páginas não marcadas
* Identificar versões inconsistentes
* Localizar versões desatualizadas
* Fornecer informações detalhadas que podem ser exportadas

## Solução de problemas comum

>[!NOTE]
>
>A Adobe recomenda instalar o Adobe Experience Platform Debugger.

Veja a seguir dicas gerais de solução de problemas ao entrar na Experience Platform:

### Cache e cookies**

* Limpeza de cache e cookies
* Tenha cuidado ao usar o modo privado (por exemplo: o modo privado no Firefox pode bloquear [!DNL Target])

### Você está qualificado para a atividade?

* Verifique se você executou as mesmas etapas que o público-alvo usou na atividade
* Use `mboxTrace` ou tokens de resposta para verificar valores de perfil e segmento

### Dicas gerais de solução de problemas ao validar visual/funcional

Se você estiver na experiência [!DNL Target] e não vir a experiência visual esperada:

Verifique a resposta [!DNL Target]:

* Se o código não for executado:

1. Verificar atividades conflitantes
1. Entre em contato com o Atendimento ao cliente

* Se o código for executado:

1. Retrabalhe o código nesse cenário

## Manutenção de um repositório de conhecimento

Um repositório de conhecimento é uma plataforma on-line usada para documentar e compartilhar informações. O repositório de conhecimento contém informações específicas para sua implementação e pode conter informações específicas da equipe.

Idealmente, o repositório deve permitir a edição e o salvamento automático na plataforma. Após a configuração inicial, é fácil mantê-lo e mantê-lo atualizado. O conteúdo no Repositório de conhecimento é preparado com base nas funções do usuário.

Os documentos típicos em um Repositório de conhecimento incluem:

* **Documento de visão geral** - um documento usado para explicar claramente as metas, os objetivos, os processos e a estrutura do programa
* **Repositório de ideação** - um documento usado para gerenciar e priorizar possíveis ideias que não estão prontas para o processo de teste
* **Roteiro do programa** - um documento usado para gerenciar todos os aspectos das atividades de teste quando as ideias estiverem prontas para iniciar o processo de teste
* **Documento do plano de atividade** - um documento usado para destacar informações necessárias para compilar e iniciar atividades
* **Documento do plano de atividade** - um documento usado para comunicar resultados e as próximas etapas recomendadas aos participantes
* **Painel de programas** - um documento usado para rastrear o desempenho do programa, a cadência e os benefícios da receita ao longo do tempo.

Para obter mais informações, consulte nosso [webinário](https://adobecustomersuccess.adobeconnect.com/p4p7xlp7dh42mp4/) com o consultor sênior, Wilder Freed.

Saiba mais sobre estratégia e liderança de pensamento na central de [Sucesso do cliente](https://experienceleague.adobe.com/docs/customer-success/customer-success/overview.html).
