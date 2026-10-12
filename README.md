# Discount Strategy Analysis: Fixed vs. Progressive Discounts

## Sobre o projeto

Este projeto analisa duas estratégias promocionais para um e-commerce de eletrônicos: desconto fixo e desconto progressivo.

O objetivo é investigar como o volume de usuários, a taxa de conversão e o ticket médio podem influenciar o faturamento de uma campanha promocional de quatro horas.

A pergunta que orienta o estudo é:

**Os descontos progressivos realmente aumentam o faturamento ou apenas atraem mais clientes que gastam menos?**

Este case faz parte do meu processo de aprendizado em análise de dados e aplicação de conceitos de probabilidade e estatística a problemas de negócio.

## Contexto do problema

A campanha acontece das 18h às 22h e considera duas estratégias:

- **Desconto fixo:** 15% durante toda a campanha.
- **Desconto progressivo:** descontos de 10%, 12%, 15% e 17% ao longo das quatro horas.

### Dados disponíveis

| Variável | Valor |
|---|---:|
| Usuários esperados — desconto fixo | 60.000 |
| Usuários esperados — desconto progressivo | 80.000 |
| Taxa média de conversão | 2% |
| Ticket médio sem desconto | R$ 350,00 |
| Duração da campanha | 4 horas |

## Metodologia

### 1. Cálculo do ticket médio

O primeiro passo foi calcular o ticket médio após a aplicação de cada desconto.

A fórmula utilizada foi:

`ticket_medio = ticket_original * (1 - desconto)`

Para o cenário fixo, com desconto de 15%:

`350 * (1 - 0.15) = R$ 297,50`

Para o cenário progressivo, os tickets médios estimados são:

| Desconto | Ticket médio |
|---|---:|
| 10% | R$ 315,00 |
| 12% | R$ 308,00 |
| 15% | R$ 297,50 |
| 17% | R$ 290,50 |

### 2. Estimativa de pedidos e faturamento

Para cada período, utilizei as seguintes fórmulas:

`pedidos = usuarios * taxa_conversao`

`faturamento = pedidos * ticket_medio`

Como não havia dados históricos sobre a distribuição horária dos usuários, adotei hipóteses explícitas para construir uma primeira simulação.

No cenário fixo, distribuí os 60.000 usuários igualmente entre as quatro horas, resultando em 15.000 usuários por hora.

No cenário progressivo, considerei uma distribuição crescente de 10%, 20%, 30% e 40% do público total ao longo da campanha.

Essa distribuição foi definida como uma hipótese de trabalho para representar o possível aumento de interesse conforme o desconto cresce. Ela não foi estimada a partir de dados observados.

### 3. Resultados da simulação inicial

| Indicador | Desconto fixo | Desconto progressivo |
|---|---:|---:|
| Usuários | 60.000 | 80.000 |
| Pedidos esperados | 1.200 | 1.600 |
| Faturamento estimado | R$ 357.000,00 | R$ 477.680,00 |

Na primeira comparação, o cenário progressivo apresentou um faturamento estimado R$ 120.680,00 maior, equivalente a aproximadamente 33,8% acima do cenário fixo.

Entretanto, essa diferença não pode ser atribuída exclusivamente aos descontos: o cenário progressivo também considera 20.000 usuários adicionais.

### 4. Comparação com o mesmo volume de usuários

Para isolar melhor o efeito dos descontos, realizei uma segunda simulação com 60.000 usuários nos dois cenários, mantendo a distribuição horária relativa do cenário progressivo.

Nessa comparação, os resultados foram:

| Indicador | Desconto fixo | Desconto progressivo |
|---|---:|---:|
| Usuários | 60.000 | 60.000 |
| Pedidos esperados | 1.200 | 1.200 |
| Faturamento estimado | R$ 357.000,00 | R$ 358.260,00 |

A diferença foi de R$ 1.260,00, aproximadamente 0,35%.

Esse resultado sugere que, sob as hipóteses adotadas, o faturamento é muito semelhante quando o volume de usuários é mantido constante.

A simulação não permite concluir qual estratégia é superior na prática. Para isso, seria necessário avaliar como cada estratégia realmente influencia o tráfego, a conversão e o comportamento de compra.

## Dificuldades e aprendizados

Comecei este projeto realizando os cálculos manualmente, utilizando papel para estruturar os cenários e compreender a relação entre desconto, ticket médio, conversão e faturamento.

Uma das principais dificuldades foi definir como os usuários deveriam ser distribuídos ao longo das quatro horas da campanha.

Inicialmente, considerei utilizar a distribuição normal para o cenário de desconto fixo. Ao revisar os cálculos, percebi que precisava definir melhor os parâmetros estatísticos e os intervalos de tempo antes de utilizar essa distribuição para estimar o volume de usuários.

Também considerei a distribuição beta como uma possibilidade para representar proporções ou taxas variáveis. Ainda preciso aprofundar meus conhecimentos para determinar qual distribuição probabilística seria mais adequada a cada variável do problema.

Optei por começar com uma simulação simples, com premissas explícitas, para construir uma base de entendimento antes de avançar para modelos mais complexos.

Esse processo me ajudou a perceber que um cálculo pode estar matematicamente correto e, ainda assim, produzir uma conclusão limitada quando as hipóteses utilizadas não são suficientes para responder à pergunta de negócio.

## Limitações

- A distribuição de usuários por hora foi definida por hipótese, não por dados históricos.
- A taxa de conversão foi considerada constante em todos os períodos e cenários.
- O ticket médio foi ajustado proporcionalmente ao desconto, assumindo que o valor de R$ 350,00 representa a mesma base de compra em todos os períodos.
- O modelo não considera custos, margens, estoque, alterações no mix de produtos ou efeitos sobre o lucro.
- Os resultados são estimativas determinísticas baseadas nos valores esperados, não previsões observadas ou intervalos de confiança.

## Próximos passos

- [ ] Implementar os cálculos em Python com Pandas e NumPy.
- [ ] Criar gráficos para comparar usuários, pedidos, ticket médio e faturamento por hora.
- [ ] Investigar distribuições probabilísticas adequadas para modelar contagens de usuários e taxas de conversão.
- [ ] Realizar análises de sensibilidade para diferentes volumes de usuários e taxas de conversão.
- [ ] Avaliar a inclusão de margens e custos para comparar também a rentabilidade das estratégias.
- [ ] Investigar como dados históricos ou testes A/B poderiam validar as hipóteses do modelo.

## Tecnologias e conceitos

**Tecnologias planejadas:** Python, Pandas, NumPy e Matplotlib.

**Conceitos:** análise de cenários, probabilidade, distribuições estatísticas, taxa de conversão, ticket médio, faturamento e análise de sensibilidade.

## Considerações finais

Este projeto representa o início de um processo de aprendizado sobre como utilizar dados e modelos estatísticos para apoiar decisões de negócio.

Mais do que buscar uma resposta definitiva, meu objetivo é construir uma análise reproduzível, compreender as limitações das hipóteses adotadas e aprimorar progressivamente a modelagem.

A próxima etapa será transformar os cálculos manuais em um notebook Python, permitindo validar os resultados, explorar diferentes cenários e documentar a evolução da análise.
