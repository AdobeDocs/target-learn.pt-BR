---
title: Práticas recomendadas de otimização
description: 'Saiba mais sobre seis princípios básicos de otimização do Adobe. '
solution: Target
source-git-commit: fd679d3fc2c72b9852d8129adf8c1187bf22b25f
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 0%

---

# Práticas recomendadas para otimização com o Adobe Target

Saiba mais sobre seis princípios básicos de otimização do Adobe.

Quando se trata de construir uma forte presença digital, há vários desafios que sua equipe enfrentará. Além disso, você tem a tarefa de envolver centenas, até milhares de clientes, além disso, seus clientes exibem uma variedade de comportamentos e preferências exclusivos que mudarão com o tempo, e cabe a você não apenas acompanhar essas alterações, mas antecipá-las e executar suas estratégias de forma eficiente e precisa. É uma corrida contra concorrentes em uma maratona de conteúdo perpétuo, exigindo iteração constante e a melhor tecnologia do setor.

Uma solução para esse desafio multifacetado é a otimização com o Adobe Target, o que garante que você tenha uma presença digital em evolução que seja relevante, valiosa e livre de atrito. A arquitetura técnica e os canais nos quais você implanta [!DNL Target] O varia bastante entre os clientes, no entanto, preparamos uma lista de práticas recomendadas e estratégias de otimização que cada equipe pode usar para aproveitar todos os recursos dessa ferramenta poderosa.

## Noções básicas sobre otimização

A otimização é definida como &quot;a ação de fazer o melhor ou mais eficaz uso de uma situação ou recurso&quot;. É a maneira mais eficiente de garantir que você tenha dados qualitativos que provarão que as mudanças que você está fazendo são valiosas. Para realmente otimizar, você deve ser capaz de medir o impacto e o valor de seus esforços. Caso contrário, as alterações feitas resultarão em maior custo, com ganhos mínimos. Para o conseguir de forma eficaz e eficiente, tem de começar pelo planeamento estratégico. Sem incluir um plano estratégico na sua otimização, você estaria apenas adivinhando.

### Seis princípios básicos de otimização

1. **Estratégizar**: Identifique oportunidades para atividades que estão alinhadas aos objetivos de negócios e que são baseadas em dados.
1. **Priorizar**: Classifique e programe atividades com base no alinhamento dos negócios, nível de esforço e impacto potencial.
1. **Design**: Crie visuais finalizados de experiências de atividades e desenvolva planos de atividades com critérios detalhados.
1. **Criar e executar**: Desenvolver atividade incluindo [!DNL Target] configuração, desenvolvimento de código e teste de controle de qualidade.
1. **Analisar**: Launch [!DNL Target] para produzir e monitorar o desempenho durante a atividade.
1. **Atuar e iterar**: Desenvolver recomendações com base no desempenho da atividade de teste ou personalização.

Sabendo que a alteração é uma constante, nossa estratégia de otimização deve ser um ciclo de execução iterativo para atender às necessidades em constante mudança dos clientes (consulte a Figura 1 abaixo).

![Otimização e personalização](assets/optimize-and-personalize.png)

_Figura 1 - Ciclo iterativo de otimização_

## Criar uma estratégia de otimização

O processo de desenvolvimento de uma estratégia de otimização pode ser dividido em: (1) Criar um plano de atividade de teste e (2) Entender os fundamentos da otimização.

1: O plano de atividades de ensaio deve ser documentado. Isso garante que você tenha um padrão mínimo de qualidade em relação ao aplicativo de atividade de teste. Seu plano de atividade de teste deve incluir:

* **Nome e descrição:** Nome da atividade intuitiva e descrição do foco do experimento. &quot;Como? O quê? Ao? Onde? Por quê?&quot;

* **Objetivo:** Finalidade da atividade e objetivo de negócios alinhado que está sendo projetado para impactar.

* **Hipótese:** Uma hipótese é uma previsão que você cria antes de executar um experimento. Ele claramente diz o que está sendo testado, o que você acredita que será o resultado e por que você acha que é o caso. Executar o experimento comprovará ou desaprovará sua hipótese.

Uma hipótese completa tem três partes:

* If _variável_
* Então _resultado_
* Porque _lógica_

* **Localização:** URL, seção da página e tipo de dispositivo.
* **Métrica de objetivo:** Como o sucesso será medido?
* **Métricas secundárias:** Outros KPIs (indicadores-chave de desempenho) valiosos para avaliar com o objetivo de compreender melhor as iterações de impacto e planejamento.
* **Público-alvo da atividade:** Descrição da filtragem de exposição de teste necessária.
* **Relatório de públicos-alvo:** Lista de descrições de subconjuntos de visitantes a serem usados para análise.
* **Conceitos de experiência:** Mockups, exemplos de wireframes e descrições.

**Nota geral:** Qualquer elemento de uma página da Web que possa gerar valor comercial ou fornecer informações valiosas sobre o comportamento do visitante pode ser testado. Alguns tipos comuns de atividades de teste incluem:

* Texto do título
* Texto do conteúdo
* Texto do botão
* Layout da página
* Fotografia
* Cor do botão
* Layout do elemento
* Remoção e adição de elementos
* Ordenação de navegação
* Taxonomia de navegação
* Realce da pesquisa

2: A segunda etapa da estratégia é entender os fundamentos da otimização, que inclui a compreensão dos próprios elementos de teste. Os elementos de teste da Otimização incluem:

    A. Valor do elemento
    
    Isso é feito recuando um passo para perguntar, por que um determinado elemento existe em seu site e o conteúdo serve um propósito específico? Essas perguntas são um bom ponto de partida se o site acabou de concluir uma reformulação ou se um novo recurso foi lançado recentemente. A tática usada para determinar o valor do elemento é chamada de Teste de inclusão/exclusão. O Teste de inclusão/exclusão fornece uma boa leitura do valor na página em que o elemento é exibido.
    
    B. Apresentação dos elementos
    
    É aqui que você pensa sobre a aparência geral do elemento e como isso afeta a apresentação geral da página. A tática usada para a apresentação é focar em fazer alterações impactantes no conteúdo e na página do elemento.
    
    C. Função do elemento
    
    Aqui perguntamos, o elemento na página está fazendo o que deveria fazer? A interação é bem-sucedida e está funcionando como planejado? A interação é natural ou um ponto de atrito? A tática usada para a função é criar experiências focadas na funcionalidade fácil de usar sem impacto adicional no custo.

## Otimização x personalização

Agora que analisámos e listámos os componentes da estratégia, é importante estabelecer uma distinção entre os esforços de otimização e os esforços de personalização. A otimização é a ação de fazer o melhor ou mais eficaz uso de uma situação ou recurso, enquanto a personalização é a ação de projetar ou produzir algo para atender às necessidades individuais de alguém.

Em um alto nível:

* A otimização é focada em testes para descobrir o que é mais eficiente e tem melhor desempenho para TODAS as pessoas que interagem com sua presença digital.
* A personalização está testando o que é mais eficiente e de melhor desempenho para alguns daqueles que interagem com sua presença digital.

Ao se concentrar na Otimização, as atividades de teste mais comuns são:

* **Teste A/B:** Teste em tempo real de duas ou mais páginas ou elementos de página uns contra os outros para obter um insight quantitativo sobre a preferência do cliente.
* **Teste multivariado:** Comparação de combinações de ofertas entre elementos em uma página para ver qual combinação tem o melhor desempenho. Além disso, o teste multivariado identificará qual elemento da página melhora mais conversões.

Ao se concentrar na personalização, você provavelmente verá as mesmas atividades de teste que na Otimização, mas elas são direcionadas para públicos-alvo mais específicos. Por exemplo, em testes A/B, você provavelmente adicionará páginas e públicos nas experiências para aprimorar sua personalização.

A personalização também inclui o tipo de atividade de teste Direcionamento de experiência, que fornece conteúdo para públicos-alvo específicos com base em um conjunto de regras e critérios definidos. À medida que você começa a crescer e a se aprofundar na Personalização, é também aqui que você aproveitará alguns dos recursos premium do Target, como:

* Tipo de atividades do Automated Personalization
* Tipo de atividades de recomendação

## Otimização antes da personalização

Dada a compreensão acima, o Adobe recomenda Otimizar antes de Personalizar e promover a Personalização de modo amplo a granular. Para madurar as atividades de personalização, de amplo para granular, você começará a usar um estilo de personalização one-to-many (amplo) (usando testes A/B) e passará para o estilo de personalização one-to-one (granular) (usando atividades de personalização automatizada).

Para obter mais informações, ouça [webinar sobre compreensão e otimização da implementação do Adobe Target](https://adobecustomersuccess.adobeconnect.com/pkfafpzd9yarmp4/), com a consultora de negócios Katie Cozby.
