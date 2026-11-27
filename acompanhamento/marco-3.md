# **Marco 3 — Algoritmo de Dijkstra**

## Estruturas de dados e estados iniciais

Para analisar a execução: nós iremos utilizar o código original de Dijkstra sem modificações.

Considerando a instância do Marco 2, temos:

- `g.V = 4`: quantidade de vértices.
- `s = 0`: vértice de origem, correspondente à cidade 1.
- `POSITIVE_INFINITY = 999999.0`: valor utilizado para representar uma distância inicialmente desconhecida.

As estruturas utilizadas pelo algoritmo são:

| Estrutura | Finalidade                                                                           |
| --------- | ------------------------------------------------------------------------------------ |
| `edgeTo`  | Armazena a aresta utilizada para chegar a cada vértice pelo menor caminho conhecido. |
| `distTo`  | Armazena as menores distâncias conhecidas a partir da origem.                        |
| `pq`      | Fila de prioridade que organiza os vértices pelo menor custo.                        |
| `g.adj`   | Armazena as arestas que saem de cada vértice.                                        |

O grafo utiliza índices começando em zero. Portanto, a cidade 1 corresponde ao vértice 0, a cidade 2 ao vértice 1, e assim sucessivamente.

### **Grafo utilizado**

```
0 → 1 (peso 1)
0 → 2 (peso 3)
1 → 2 (peso 2)
1 → 3 (peso 6)
2 → 1 (peso 8)
2 → 3 (peso 1)
```

## Acompanhamento da execução

O algoritmo começa removendo da fila de prioridade o vértice com a menor distância. Em seguida, executa o método `relax()` para verificar se existe um caminho mais barato até os vértices vizinhos.

**Estado inicial:**

```
edgeTo = [None, None, None, None]

distTo = [0, 999999, 999999, 999999]

pq = {0: 0}
```

### Iteração 1 — Processamento do vértice 0

O algoritmo remove o vértice 0 da fila e verifica suas arestas:

- 0 → 1: custo 1.
- 0 → 2: custo 3.

Como os dois vértices ainda possuem distância infinita, os valores são atualizados.

```
edgeTo = [None, (0→1), (0→2), None]

distTo = [0, 1, 3, 999999]

pq = {1: 1, 2: 3}
```

### Iteração 2 — Processamento do vértice 1

O algoritmo remove o vértice 1, que possui custo 1, e verifica suas arestas:

- 1 → 2: custo total 1 + 2 = 3.
- 1 → 3: custo total 1 + 6 = 7.

O caminho até o vértice 2 possui custo 3, igual ao valor que já estava armazenado. Como a condição do código utiliza `>`, não ocorre atualização.

Já o vértice 3 recebe o custo 7.

```
edgeTo = [None, (0→1), (0→2), (1→3)]

distTo = [0, 1, 3, 7]

pq = {2: 3, 3: 7}
```

### Iteração 3 — Processamento do vértice 2

O algoritmo remove o vértice 2, que possui custo 3, e verifica suas arestas:

- 2 → 1: custo total 3 + 8 = 11.
- 2 → 3: custo total 3 + 1 = 4.

O caminho até o vértice 1 não é atualizado, pois 11 é maior que 1.

Já o caminho até o vértice 3 é atualizado, pois 4 é menor que 7.

```
edgeTo = [None, (0→1), (0→2), (2→3)]

distTo = [0, 1, 3, 4]

pq = {3: 4}
```

### Iteração 4 — Processamento do vértice 3

O algoritmo remove o vértice 3 da fila.

Como ele não possui arestas de saída, nenhuma distância é atualizada. A fila fica vazia e o processamento termina.

```
edgeTo = [None, (0→1), (0→2), (2→3)]

distTo = [0, 1, 3, 4]

pq = {}
```

## Justificativa das decisões e resultado

Durante a execução, o algoritmo utiliza a fila de prioridade para sempre processar primeiro o vértice com a menor distância conhecida.

O método `relax()` compara o custo do caminho atual com o valor armazenado em `distTo`. Caso encontre um caminho de menor custo, atualiza a distância e a aresta correspondente em `edgeTo`.

Ao final, o menor caminho encontrado entre a cidade 1 e a cidade 4 é:

```
Cidade 1 → Cidade 3 → Cidade 4

Custo: 3 + 1 = 4
```

Resultado do Dijkstra:

```
Menor custo encontrado: 4
```


## Explicação mais detalhada do `def relax()` (um dos trechos de código do `dijkstra_sp.py`)

**Explicação:**

O método `relax()` verifica todas as arestas que saem do vértice recebido como parâmetro. Para cada aresta, identifica o vértice de destino e calcula o custo de chegar até ele passando pelo vértice atual.

A condição `if self.distTo[w] > self.distTo[v] + e.weight` verifica se o novo caminho é mais barato que o caminho anteriormente conhecido.

Se for, o algoritmo atualiza a distância em `distTo` e registra a aresta em `edgeTo`. Depois, verifica se o vértice já está na fila de prioridade: se estiver, sua prioridade é alterada com `change()`; caso contrário, ele é inserido com `insert()`.

Esse procedimento permite que o algoritmo atualize continuamente os menores custos encontrados até concluir o processamento do grafo.