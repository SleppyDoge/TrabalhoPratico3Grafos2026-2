
# Marco 1 - Formulação do Problema

## 1. Resumo do problema

O problema escolhido foi o Flight Routes (CSES 1196), pertencente à classe de caminhos mínimos.

O objetivo é encontrar as k rotas de voo mais baratas entre as cidades de Syrjälä e Metsälä, considerando o custo total dos voos utilizados em cada rota.

Uma rota pode passar pela mesma cidade mais de uma vez. Além disso, rotas distintas que possuem o mesmo custo devem ser consideradas separadamente.

## 2. Entrada

A primeira linha contém três números inteiros:

- `n`: quantidade de cidades;
- `m`: quantidade de voos;
- `k`: quantidade de rotas mais baratas que devem ser encontradas.

As próximas `m` linhas apresentam três números inteiros (`a`, `b`, `c`), em que:

- `a`: cidade de origem do voo;
- `b`: cidade de destino do voo;
- `c`: preço do voo.

A cidade 1 representa Syrjälä e a cidade n representa Metsälä.

## 3. Saída

A saída deve apresentar k números inteiros correspondentes aos custos das k rotas mais baratas, em ordem não decrescente.

## 4. Objetivo

Encontrar os k menores custos de rotas entre a cidade 1 e a cidade n.

O custo total de uma rota é calculado pela soma dos pesos das arestas percorridas.

Portanto, o objetivo não é minimizar a quantidade de voos realizados, mas o custo total da viagem.

## 5. Restrições

| Restrição | Significado |
| --- | --- |
| 2 ≤ n ≤ 10⁵ | O grafo possui entre 2 e 100.000 cidades. |
| 1 ≤ m ≤ 2 × 10⁵ | Existem entre 1 e 200.000 voos. |
| 1 ≤ a, b ≤ n | As cidades de origem e destino devem possuir identificadores válidos. |
| 1 ≤ c ≤ 10⁹ | Cada voo possui um custo positivo de até 1 bilhão. |
| 1 ≤ k ≤ 10 | Devem ser encontradas entre 1 e 10 rotas de menor custo. |

O problema também garante a existência de pelo menos k rotas distintas entre a cidade de origem e a cidade de destino.

O número elevado de cidades e voos exige uma solução computacional eficiente.

## 6. Modelagem do grafo

O problema é modelado como um grafo direcionado e ponderado G = (V, E).

| Elemento do grafo | Representação no problema |
| --- | --- |
| Vértices (V) | Cidades |
| Arestas (E) | Voos entre cidades |
| Direção | Sentido do voo, da origem ao destino |
| Peso | Preço do voo |
| Vértice de origem (s) | Cidade 1 — Syrjälä |
| Vértice de destino (t) | Cidade n — Metsälä |

O grafo é direcionado porque a existência de um voo de uma cidade a para uma cidade b não garante a existência de um voo no sentido contrário.

O grafo é ponderado porque cada aresta possui um peso associado, correspondente ao preço do voo.

## 7. Família do problema

O problema pertence à família de caminhos mínimos em grafos direcionados e ponderados com pesos positivos.

Entretanto, diferentemente do problema tradicional de caminho mínimo, que busca apenas uma rota de menor custo, o Flight Routes exige encontrar as k rotas mais baratas, permitindo a repetição de vértices e considerando separadamente rotas distintas com custos iguais.

## Referências

- [CSES — Flight Routes (Problem 1196)](https://cses.fi/problemset/task/1196/)
- [Trabalho Prático 3 — Enunciado oficial](https://github.com/carubbi/RPG/blob/main/mat-didatico/trabalhos/T3.md)
- CARUBBI, Ricardo. Unidade 3 — Caminhos de Menor Custo
  (Shortest Paths). Material didático da disciplina de
  Resolução de Problemas com Grafos. UNIFOR, 2026.

