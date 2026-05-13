---
title: Práticas recomendadas de otimização
description: Saiba mais sobre os seis conceitos básicos da Adobe sobre otimização e como aplicá-los.
solution: Target
role: Leader, Developer, Admin
feature: Overview
level: Beginner
exl-id: dd29faea-bb67-4128-b261-fa407ba7158c
TQID: https://experienceleague.adobe.com/4M13hg8c1kxAmsBaiSfyvV3XEXLxV5lHEy299YGBvII
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
  - id: f8667931-f646-4dd3-af2a-b9d0cb8098ad
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 1254
ht-degree: 0%

---

# Práticas recomendadas de otimização com o Adobe Target

Saiba mais sobre os seis conceitos básicos da Adobe sobre otimização e como aplicá-los.

Quando se trata de construir uma forte presença digital, há vários desafios que sua equipe enfrentará. Você não tem apenas a tarefa de envolver centenas, até milhares de clientes, além disso, seus clientes exibem uma variedade de comportamentos e preferências únicos que mudarão com o tempo, e cabe a você não apenas acompanhar essas alterações, mas antecipá-las e executar suas estratégias com eficiência e precisão. É uma corrida contra os concorrentes em uma maratona de conteúdo perpétua, exigindo iteração constante e a melhor tecnologia do setor.

Uma solução para esse desafio multifacetado é a otimização com o Adobe Target, que garante uma presença digital em evolução relevante, valiosa e sem atrito. A arquitetura técnica e os canais nos quais você implanta o [!DNL Target] variarão consideravelmente entre os clientes. No entanto, preparamos uma lista de práticas recomendadas e estratégias de otimização que cada equipe pode usar para aproveitar todos os recursos dessa poderosa ferramenta.

## Noções básicas sobre otimização

A otimização é definida como &quot;a ação de fazer o melhor ou mais eficaz uso de uma situação ou recurso&quot;. É a maneira mais eficiente de garantir que você tenha dados qualitativos que provarão que as alterações que você está fazendo são valiosas. Para otimizar de fato, você deve ser capaz de medir o impacto e o valor de seus esforços. Caso contrário, as alterações feitas resultarão em custo mais alto, com ganho mínimo. Para conseguir isso de maneira eficaz e eficiente, você deve começar com o planejamento estratégico. Sem incluir um plano estratégico em sua otimização, você simplesmente estaria chutando.

### Seis fundamentos da otimização

1. **Criar uma estratégia**: identifique oportunidades para atividades alinhadas aos objetivos de negócios e que sejam baseadas em dados.
1. **Priorizar**: classifique e agende atividades com base no alinhamento de negócios, no nível de esforço e no impacto potencial.
1. **Design**: crie visuais finalizados das experiências da atividade e desenvolva planos de atividade com critérios detalhados.
1. **Criar e executar**: desenvolver atividade incluindo configuração de [!DNL Target], desenvolvimento de código e teste de controle de qualidade.
1. **Analisar**: inicie a atividade [!DNL Target] para produzir e monitorar o desempenho durante a atividade.
1. **Agir e iterar**: desenvolva recomendações com base no desempenho da atividade de teste ou personalização.

Sabendo que a mudança é uma constante, nossa estratégia de otimização deve ser um ciclo de execução iterativo para atender às necessidades em constante mudança de seus clientes (consulte a Figura 1 abaixo).

![Otimização e personalização](assets/optimize-and-personalize.png)

_Figura 1 - Ciclo Iterativo de Otimização_

## Criação de uma estratégia de otimização

O processo de desenvolvimento de uma estratégia de otimização pode ser dividido em: (1) Criar um plano de atividade de teste e (2) Entender os conceitos básicos de otimização.

1: O plano de atividade de teste deve ser documentado. Isso garante que você tenha um padrão mínimo de qualidade quando se trata do aplicativo de atividade de teste. Seu plano de atividade de teste deve incluir:

* **Nome e descrição:** nome de atividade intuitiva e descrição do foco do experimento. &quot;Como? O quê? Quando? Onde? Por quê?&quot;

* **Objetivo:** a finalidade da atividade e o objetivo comercial alinhado que está sendo projetado para impactar.

* **Hipótese:** Uma hipótese é uma previsão criada antes da execução de um experimento. Ele indica claramente o que está sendo testado, o que você acredita que o resultado será e por que você acha que é o caso. A execução do experimento comprovará ou desaprovará sua hipótese.

Uma hipótese completa tem três partes:

* Se _variável_
* Então _resultado_
* Porque _lógica_

* **Local:** URL, seção de página e tipo de dispositivo.
* **Métrica de objetivo:** Como o sucesso será medido?
* **Métricas secundárias:** outros KPIs (indicadores-chave de desempenho) valiosos a serem avaliados com o objetivo de entender melhor as iterações de impacto e planejamento.
* **Público-alvo da atividade:** Descrição da filtragem de exposição de teste necessária.
* **Relatórios de Públicos-alvo:** Lista de descrições de subconjuntos de visitantes a serem usados para análise.
* **Conceitos de experiência:** modelos, exemplos wireframes e descrições.

**Observação geral:** todos os elementos de uma página da Web que podem agregar valor comercial ou fornecer insight valiosas ao comportamento do visitante podem ser testados. Alguns tipos comuns de atividades de teste incluem:

* Texto do título
* Texto do conteúdo
* Texto do botão
* Layout da página
* Fotografia
* Cor do botão
* Layout do elemento
* Remoção e adição de elementos
* Ordem de navegação
* Taxonomia de navegação
* Ênfase de pesquisa

2: O segundo estágio da estratégia é Entender as noções básicas de otimização, que inclui a compreensão dos próprios elementos de teste. Os elementos de teste da Otimização incluem:

    A Valor do elemento
    
    Isso é feito voltando atrás para perguntar por que um determinado elemento existe no site e por que o conteúdo serve a um propósito específico? Essas perguntas são um bom ponto de partida se o site acabou de concluir um novo design ou se um novo recurso foi lançado recentemente. A tática usada para determinar o valor do elemento é chamada de Teste de inclusão/exclusão. O Teste de Inclusão/Exclusão fornece uma boa leitura do valor na página em que o elemento é exibido.
    
    B. Apresentação do elemento
    
    Aqui é onde você deve pensar sobre a aparência geral do elemento e como isso afeta a apresentação geral da página. A tática usada para a apresentação é concentrar-se em fazer alterações impactantes de conteúdo e página de elemento.
    
    C. Função do elemento
    
    Aqui perguntamos: o elemento na página está fazendo o que deve? A interação foi bem-sucedida e está funcionando como esperado? A interação é natural ou um ponto de atrito? A tática usada para a função é criar experiências focadas em funcionalidades fáceis de usar, sem impacto adicional no custo.

## Otimização vs. personalização

Agora que analisamos e listamos os componentes da estratégia, é importante fazer uma distinção entre os esforços de Otimização e os esforços da Personalization. Otimização é a ação de fazer o melhor ou mais eficaz uso de uma situação ou recurso, enquanto o Personalization é a ação de projetar ou produzir algo para atender às necessidades individuais de alguém.

Em um alto nível:

* O foco da otimização são os testes para descobrir o que é mais eficiente e o melhor desempenho para TODOS que interagem com a sua presença digital.
* A Personalization está testando para descobrir o que é mais eficiente e o melhor desempenho para ALGUNS dos que interagem com a sua presença digital.

Ao se concentrar na Otimização, as atividades de teste mais comuns são:

* **Teste A/B:** teste em tempo real de duas ou mais páginas ou elementos de página entre si para obter insight quantitativo em preferência do cliente.
* **Teste multivariado:** Comparação de combinações de ofertas entre elementos em uma página para ver qual combinação tem o melhor desempenho. Além disso, o teste multivariado identificará qual elemento da página melhora mais conversões.

Ao se concentrar no Personalization, provavelmente você verá as mesmas atividades de teste que no Otimization, mas elas são direcionadas para públicos mais específicos. Por exemplo, no teste A/B, é provável que você adicione páginas e públicos-alvo nas experiências para aprimorar o Personalization.

O Personalization também inclui o tipo de atividade de teste de Direcionamento de experiência, que fornece conteúdo a públicos-alvo específicos com base em um conjunto de regras e critérios definidos. À medida que você começa a crescer e se aprofundar no Personalization, também é aqui que você aproveitará alguns dos recursos premium do Target, como:

* Tipo de atividades do Automated Personalization
* Tipo de atividades de recomendação

## Otimização antes da personalização

Dado o entendimento acima, a Adobe recomenda que você Otimize antes de Personalizar e promova o Personalization de amplo para granular. Para amadurecer as atividades do Personalization de amplo a granular, você começará a usar um estilo de personalização de um para muitos (amplo) (usando o teste A/B) e, em seguida, passará para um estilo de personalização de um para um (granular) (usando as atividades de Personalização automatizada).

Para obter mais informações, leia o [QuickStart para testes de personalização e criação de roteiro](https://experienceleague.adobe.com/en/perspectives/quickstart-for-personalization-testing-and-roadmap-creation).

Saiba mais sobre estratégia e liderança de pensamento no hub [Perspectivas](https://experienceleague.adobe.com/en/perspectives).
