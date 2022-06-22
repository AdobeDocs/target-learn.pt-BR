---
title: Início rápido para testes de personalização e criação de roteiro
description: Saiba mais sobre uma estrutura que pode ser usada para começar a validar atividades de personalização e criar um roteiro de personalização para executar por meio do Adobe Target e Adobe Analytics.
solution: Target,Analytics
exl-id: c0b6f9a0-7074-4e25-81e6-9781a54e2156
source-git-commit: 46f61d8f503f230a79b4072ea0d75edd41403708
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 0%

---

# Início rápido para testes de personalização e criação de roteiro

A personalização pode ser poderosa, mas deve ser validada por testes para garantir que realmente agregue valor. Testar é a estratégia mais eficaz para identificar quem, como e o que você deve personalizar.

À medida que iniciamos a segunda década do século XXI, organizações como a sua estão dividindo caminhos com estratégias ultrapassadas de definição de metas do consumidor e análises de dados imprecisas. Este é o advento da personalização, uma era em que os consumidores passaram a esperar nada menos do que uma experiência personalizada. A personalização no nível corporativo é um processo complexo e em constante mudança, mas quando feito de forma eficaz, maximizará a satisfação do cliente e aumentará substancialmente o ROI.

O artigo a seguir fornece uma estrutura que pode ser usada para começar a validar atividades de personalização e criar um roteiro de personalização para executar por meio do Adobe Target e Adobe Analytics. AdobeStart inclui:

1. **Identificar oportunidades de personalização** - utilize a análise de dados para identificar oportunidades de afetar os principais indicadores de desempenho do site, vinculados aos objetivos de negócios de sua organização.

1. **Desenvolver casos de uso** - defina os objetivos da sua atividade de personalização tendo em mente atributos específicos do visitante, seja explícito sobre como o conteúdo preparado melhorará a experiência do visitante, determinará antecipadamente qual será a aparência de sucesso e quais ações poderão ser tomadas dos aprendizados de teste.

1. **Criar um roteiro** - agregue uma lista e priorize os casos de uso de personalização, garanta que seus esforços estejam concentrados em atividades de alto valor; espera refinar e revisar casos de uso e roteiro com base em aprendizados.

1. **Projetar e executar** - crie e inicie as atividades do Adobe Target para fornecer conteúdo preparado para seus públicos-alvo prioritários.

1. **Realizar ações nos resultados** - analisar o desempenho da atividade e resumir os resultados da atividade, insights, recomendações e próximas etapas.

## Etapa 1: Identificar oportunidades de personalização{#personalization}

Esse é o ponto de partida onde você começa a formar o Roteiro de Personalização. Ao executar um programa de personalização bem-sucedido, é essencial se concentrar em seus principais objetivos de negócios e indicadores-chave de desempenho. Os esforços de personalização devem ser alinhados adequadamente para fornecer valor. Paul Morris, Adobe Business Consultor, afirma: &quot;Se tudo o que você faz se alimenta desses objetivos, seu programa tem grande probabilidade de gerar valor significativo. No entanto, se você tiver uma abordagem dispersa para os testes, provavelmente encontrará algumas vitórias, mas seu programa geral não terá quase o mesmo sucesso.&quot;

>[!NOTE]
>
>Se você não souber imediatamente quais são seus principais objetivos de negócios, é importante identificá-los o mais rápido possível. Certifique-se de:


* Estabeleça o alinhamento entre as metas de negócios e a hipótese acionável. Isso permitirá priorizar casos de uso que agreguem o maior valor à sua empresa.

* Torne suas metas mensuráveis para fins de rastreamento e correlacione ao impacto na receita.

* O alinhamento de cada oportunidade deve afetar uma única métrica de meta.

Às vezes, você pode ter objetivos que inicialmente também parecem intangíveis, como valor da marca ou fidelidade. É fundamental que você possa avaliá-los para usá-los como métricas de meta para atividades de Personalização. Normalmente, esses tipos de metas ainda podem ser alinhadas ao impacto na receita, como o valor do cliente vitalício ou os custos de aquisição.Conforme você avança, certifique-se de revisar o desempenho do programa em relação aos seus objetivos principais de negócios periodicamente, garantindo que o valor esteja sendo impulsionado pelo seu programa de Personalização.

Focalize a análise de dados para identificar áreas específicas do site que podem ser aprimoradas. O Adobe recomenda começar com Adobe Analytics para gerar casos de uso direcionados. Se você tiver uma equipe do Analytics em vigor, peça a ela para examinar o seguinte:

1. Tabelas de pré-formulário pessoais - um recurso de ideação que fornece detalhamentos ilimitados e pode ajudá-lo a responder quaisquer perguntas ou suposições que você possa ter.
1. Segmentação avançada - O IQ de segmentação permite comparar visitantes em diferentes seções do site.
1. Resenhas jornalísticas - Identifique quais partes do site se beneficiariam mais com a Personalização. Essas revisões permitem que você dê um passo para trás e navegue pelo seu site como um cliente faria.
1. Análise do concorrente - As chances são de que outras empresas enfrentem os mesmos desafios que você faz. Esta análise não se limita a empresas do mesmo setor.

A meta dessa etapa é gerar um insight acionável na forma de hipótese. Uma hipótese é uma previsão que você cria antes de executar um experimento. Ele afirma claramente o que está sendo mudado, o que você acredita que será o resultado e por que você acha que é o caso. Executar o experimento comprovará ou desaprovará sua hipótese. No final desta etapa, você deve ter um conjunto de hipóteses para oportunidades de personalização que melhorarão seu site e a satisfação do visitante.

## Etapa 2: Desenvolver casos de uso{#use-cases}

Comece com a hipótese gerada na Etapa 1 e desenvolva as atividades à sua volta. Agora é possível desenvolver as tabelas de pré-formulário criadas na Etapa 1A; cada um dos KPIs tem um conjunto de hipóteses, que se tornam testes individuais no Adobe Target. Se você estiver lutando para chegar a esse ponto, comece da maneira mais simples possível, por exemplo, concentrando-se nos visitantes que retornam ao seu site. Pense nas maneiras de adaptar sua página inicial aos seus visitantes recorrentes. Depois de ter seu conjunto de hipóteses, será necessário definir cada atividade para priorizar efetivamente cada caso de uso.

1. Defina os públicos-alvo de prioridade para os quais deseja fornecer conteúdo personalizado, tendo em conta os atributos exclusivos do visitante que definem quem são e o que desejam (por exemplo, cliente existente ou cliente potencial) Os desejos e as necessidades dos públicos-alvo de prioridade devem estar alinhados com os objetivos de negócios

1. Identifique o local específico na jornada do visitante, onde o conteúdo personalizado será o mais impactante. Concentre-se nas páginas em que você esperava visitantes de diversas personas ou visitantes com várias necessidades/intenções.

1. Comece a planejar algum trabalho de design de sua variante. O conteúdo deve ser cuidadosamente preparado com as necessidades e os desejos específicos do público-alvo, considerando onde eles estão na jornada. O conteúdo correto deve ser distinto e diferenciado.

## Etapa 3: Criar um roteiro, agregar e priorizar casos de uso

Agregue uma lista abrangente de oportunidades de personalização que captura, no mínimo, o local, a ideia e a prioridade das atividades de personalização.

A etapa de priorização é dividida em dois fatores:

**Valor:** Utilize pesquisa do setor, benchmarking e casos de uso semelhantes do passado para entender o valor esperado que cada uma de suas hipóteses pode gerar. Você deseja que seu valor seja vinculado diretamente a um dos seus Principais resultados de negócios (KBOs) e esteja em um formato padrão para que cada um dos casos de uso possa ser comparado um ao outro. O método mais comum é aplicar um valor monetário a cada caso de uso para comparação.

* Custo - Há um custo natural associado à criação de suas variantes de design no Target e, em seguida, à implantação potencial. Agora, é necessário estimar o custo associado a cada caso de uso. O custo inclui o tempo e os recursos necessários para criar experiências de teste, agendamento e análise de pós-teste.

A Adobe recomenda classificar cada um dos casos de uso em uma escala de 1 a 5; com 1 sendo simples e 5 sendo complexo. Agora você tem um conjunto de atividades priorizadas que pode ser testadas no Adobe Target. Essas atividades formarão a base das atividades de personalização anuais. O Adobe recomenda reavaliar regularmente o Roteiro de personalização. Os aprendizados de cada atividade devem influenciar as prioridades do seu roteiro prospetivo. Aprendizagem e recomendações serão mais impactantes se agirem em tempo hábil. As prioridades ao longo do ano podem mudar, mas a execução de uma metodologia iterativa garante que você sempre tenha um plano estratégico de ação em vigor e que possa acompanhar os objetivos de sua equipe e empresa.

## Etapa 4: Projetar e executar

Aproveitando a documentação criada para estrategizar o caso de uso de personalização, construa a Atividade de personalização no Target para fornecer conteúdo com curadoria para seus públicos-alvo prioritários. Verifique se o tipo de atividade, as configurações, as experiências e os recursos de relatórios estão alinhados com as metas do caso de uso. O design, o controle de qualidade e o lançamento de seu esforço de personalização são mais eficientes quando o cliente se enquadra nos processos da organização existente.

## Etapa 5: Realizar ações nos resultados

Depois que sua atividade de personalização tiver envolvido uma amostra representativa de visitantes, você poderá iniciar a análise aproveitando os insights para orientar as próximas etapas. Seja orientado por dados em sua análise, vinculando as recomendações à hipótese do caso de uso e ilustrando claramente o impacto nos objetivos dos negócios.

### Mais informações

Recomendamos que você assista a este vídeo, que discute cada uma dessas etapas: [https://adobecustomersuccess.adobeconnect.com/pvsqvdvunpai/](https://adobecustomersuccess.adobeconnect.com/pvsqvdvunpai/)

Saiba mais sobre estratégia e liderança de pensamento no [Sucesso do cliente](https://experienceleague.corp.adobe.com/docs/customer-success/customer-success/overview.html) cubo.