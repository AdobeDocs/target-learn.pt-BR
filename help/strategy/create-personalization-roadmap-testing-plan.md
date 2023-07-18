---
title: QuickStart para testes de personalização e criação de roteiro
description: Saiba mais sobre uma estrutura que você pode usar para começar a validar atividades de personalização e criar um roteiro de personalização para execução por meio do Adobe Target e do Adobe Analytics.
solution: Target,Analytics
level: Intermediate
role: Leader, Architect, Developer, Admin
exl-id: c0b6f9a0-7074-4e25-81e6-9781a54e2156
source-git-commit: 20bd1eb17ef6e287f7b76e14f727456e12d6f115
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 0%

---

# QuickStart para testes de personalização e criação de roteiro

A personalização pode ser eficiente, mas precisa ser validada por testes para garantir que realmente agrega valor. Testar é a estratégia mais eficaz para identificar quem, como e o que você deve personalizar.

À medida que nos lançamos na segunda década do século 21, organizações como a sua estão se separando de estratégias desatualizadas de direcionamento ao consumidor e análises de dados imprecisas. Este é o início da personalização, uma era em que os consumidores esperam nada menos do que uma experiência personalizada. A personalização no nível corporativo é um processo complexo e em constante mudança, mas quando feito de maneira eficaz, maximizará a satisfação do cliente e aumentará substancialmente o ROI.

O artigo a seguir fornece uma estrutura que você pode usar para começar a validar atividades de personalização e criar um roteiro de personalização para execução por meio do Adobe Target e do Adobe Analytics. A estrutura do Adobe QuickStart inclui:

1. **Identificar oportunidades de personalização** : aproveite a análise de dados para identificar oportunidades que afetem os indicadores-chave de desempenho em seu site, vinculados aos objetivos de negócios de sua organização.

1. **Desenvolver casos de uso** : defina objetivos de sua atividade de personalização com atributos específicos do visitante em mente, seja explícito sobre como o conteúdo preparado melhorará a experiência do visitante, estabeleça com antecedência a aparência do sucesso e quais ações podem ser executadas a partir dos aprendizados do teste.

1. **Criar um roteiro** : agregue uma lista e priorize casos de uso de personalização, verifique se seus esforços estão concentrados em atividades de alto valor; espere refinar e revisar casos de uso e roteiro com base em aprendizados.

1. **Projetar e executar** : crie e inicie as atividades do Adobe Target para fornecer conteúdo com curadoria para seus públicos-alvo prioritários.

1. **Tomar medidas em relação aos resultados** : analise o desempenho da atividade e resuma os resultados, os insights, as recomendações e as próximas etapas da atividade.

## Etapa 1: Identificar oportunidades de personalização{#personalization}

Esse é o ponto de partida para começar a formar o Roteiro de personalização. Ao executar um programa de personalização bem-sucedido, é essencial se concentrar em seus principais objetivos de negócios e indicadores-chave de desempenho. Os esforços de personalização devem ser alinhados de acordo para fornecer valor. Paul Morris, consultor de negócios do Adobe, afirma: &quot;Se tudo o que você fizer se enquadra nesses objetivos, é altamente provável que o seu programa gere valor significativo. No entanto, se você tiver uma abordagem dispersa para testes, provavelmente encontrará algumas vitórias, mas seu programa geral não será tão bem-sucedido.&quot;

>[!NOTE]
>
>Se você não souber imediatamente quais são seus principais objetivos de negócios, é importante identificá-los o mais rápido possível. Certifique-se de:


* Estabeleça alinhamento entre suas metas de negócios e sua hipótese acionável. Isso permitirá priorizar casos de uso que agreguem o maior valor à sua empresa.

* Torne suas metas mensuráveis para fins de rastreamento e correlacione-as ao impacto na receita.

* Alinhar cada oportunidade deve afetar uma única meta de métrica.

Às vezes, você pode ter objetivos que inicialmente também parecem intangíveis, como valor da marca ou fidelidade. É crucial poder medir esses itens para usá-los como métricas de meta para atividades de Personalização. Normalmente, esses tipos de metas ainda podem ser alinhados ao impacto na receita, como valor vitalício do cliente ou custos de aquisição.Conforme você avança, certifique-se de revisar o desempenho do programa em relação aos principais objetivos de negócios periodicamente para garantir que o valor esteja sendo retirado do seu programa de personalização.

Concentre a análise de dados para identificar áreas específicas do site que podem ser melhoradas. A Adobe recomenda começar pelo Adobe Analytics para gerar casos de uso direcionados. Se você tiver uma equipe do Analytics em funções, peça que ela verifique o seguinte:

1. Tabelas de pré-formulário pessoais - Um recurso de ideação que fornece detalhamentos ilimitados e pode ajudá-lo a responder a qualquer pergunta ou suposição que você possa ter.
1. Segmentação avançada - O Segmentation IQ permite comparar visitantes em diferentes seções do site.
1. Avaliações jurísticas - Identifique quais partes do site se beneficiariam mais da Personalização. Essas análises permitem que você dê um passo atrás e ande pelo seu site como um cliente faria.
1. Análise da concorrência — há chances de outras empresas enfrentarem os mesmos desafios que você enfrenta. Esta análise não se limita a empresas do mesmo setor.

O objetivo dessa etapa é gerar insights acionáveis na forma de uma hipótese. Uma hipótese é uma previsão criada antes da execução de um experimento. Ele indica claramente o que está sendo alterado, o que você acredita que o resultado será e por que você acha que é o caso. A execução do experimento comprovará ou desaprovará sua hipótese. No final desta etapa, você deve ter um conjunto de hipóteses para oportunidades de personalização que melhorarão o site e a satisfação do visitante.

## Etapa 2: desenvolver casos de uso{#use-cases}

Comece com a hipótese gerada na Etapa 1 e desenvolva suas atividades em torno dela. Agora é possível desenvolver as tabelas de pré-formulário criadas na Etapa 1A; cada um dos KPIs tem um conjunto de hipóteses, que então se tornam testes individuais no Adobe Target. Se você estiver com dificuldades para chegar a esse ponto, comece da maneira mais simples possível, por exemplo, com foco nos visitantes recorrentes que frequentam seu site. Pense sobre as maneiras de adaptar sua página inicial para seus visitantes recorrentes. Depois de ter o conjunto de hipóteses, será necessário definir cada atividade para priorizar efetivamente cada caso de uso.

1. Defina os públicos-alvo de prioridade aos quais você deseja fornecer conteúdo personalizado, tendo em mente os atributos de visitante únicos que definem quem eles são e o que eles querem (por exemplo, cliente existente versus cliente potencial). Os desejos e as necessidades dos públicos-alvo de prioridade devem se alinhar às suas metas de negócios

1. Identifique o local específico na jornada do visitante onde o conteúdo personalizado será mais impactante. Concentre-se em páginas em que você esperaria visitantes de diversos perfis ou visitantes com várias necessidades/intenções.

1. Comece a planejar algum trabalho de design da sua variante. O conteúdo deve ser cuidadosamente preparado com as necessidades específicas do público-alvo e os desejos em mente, considerando onde eles estão em sua jornada. O conteúdo correto deve ser distinto e diferenciado.

## Etapa 3: criar um roteiro, agregar e priorizar casos de uso

Agregue uma lista abrangente de oportunidades de personalização que capture, no mínimo, a localização, a ideia e a prioridade das atividades de personalização.

A etapa de Priorização é dividida em dois fatores:

**Valor:** Utilize pesquisas do setor, testes de desempenho e casos de uso semelhantes do passado para entender o valor esperado que cada uma de suas hipóteses pode gerar. Você quer que seu valor seja vinculado diretamente a um dos principais resultados de negócios (KBOs) e esteja em um formato padrão para que cada um dos casos de uso possa ser comparado entre si. O método mais comum é aplicar um valor monetário a cada caso de uso para comparação.

* Custo - Há um custo natural associado à criação das variantes de design no Target e, em seguida, à possível implantação. Agora, será necessário estimar o custo associado a cada caso de uso. O custo inclui o tempo e os recursos necessários para criar experiências de teste, programação e análise pós-teste.

A Adobe recomenda que você classifique cada um de seus casos de uso em uma escala de 1 a 5; sendo 1 simples e 5 complexo. Agora você tem um conjunto de atividades priorizadas que pode testar no Adobe Target. Essas atividades formarão a base de suas atividades anuais de personalização. A Adobe recomenda reavaliar o Roteiro de personalização regularmente. Os aprendizados de cada atividade devem influenciar suas prioridades de roteiro prospetivo. Os aprendizados e as recomendações terão mais impacto se forem abordados em tempo hábil. As prioridades ao longo do ano podem mudar, mas a execução de uma metodologia iterativa garante que você sempre tenha um plano estratégico de ação em vigor e que possa acompanhar os objetivos de sua equipe e da empresa.

## Etapa 4: projetar e executar

Aproveitando a documentação criada para criar estratégias para o caso de uso de personalização, crie a Atividade de personalização no Target para fornecer conteúdo preparado para seus públicos-alvo prioritários. Verifique se o tipo de atividade, as configurações, as experiências e os recursos de relatórios estão alinhados às metas do caso de uso. O design, o controle de qualidade e o lançamento de seu esforço de personalização são mais eficientes quando se enquadram em processos existentes da organização.

## Etapa 5: agir conforme os resultados

Depois que sua atividade de personalização engajar uma amostra representativa de visitantes, você poderá começar a análise aproveitando os insights para orientar as próximas etapas. Seja orientado por dados em sua análise, vinculando recomendações à sua hipótese de caso de uso e ilustrando claramente o impacto nos objetivos de negócios.

### Mais informações

Recomendamos que você assista a este vídeo, que discute cada uma destas etapas: [https://adobecustomersuccess.adobeconnect.com/pvsqvdvunpai/](https://adobecustomersuccess.adobeconnect.com/pvsqvdvunpai/)

Saiba mais sobre estratégia e liderança de pensamento na [Sucesso do cliente](https://experienceleague.adobe.com/docs/customer-success/customer-success/overview.html) hub.