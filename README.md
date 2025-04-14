# Projeto HamiltonianPath

## Descrição do Projeto

O projeto **HamiltonianPath** implementa em Python um algoritmo baseado em **backtracking** para determinar se existe um **Caminho Hamiltoniano** em um grafo, e caso exista, encontrar tal caminho.

Esse problema é um clássico da **Teoria dos Grafos**, sendo aplicado em áreas como otimização de rotas, circuitos eletrônicos, bioinformática e inteligência artificial.

---

## Sobre o Algoritmo de Caminho Hamiltoniano

Um **Caminho Hamiltoniano** é um caminho que passa **por todos os vértices do grafo exatamente uma vez**, sem repeti-los. Este projeto utiliza **backtracking** para percorrer as possibilidades de caminhos até encontrar (ou não) um caminho válido.

- **Entrada:** Lista de adjacência de um grafo.
- **Saída:** Lista com a sequência de vértices que formam um caminho Hamiltoniano, se existir.

---

## Como Executar o Projeto

### 1. Ambiente Virtual (Opcional, mas recomendado)

```bash
python3 -m venv .venv
source .venv/bin/activate  # Linux/macOS
.venv\Scripts\activate     # Windows
```

### 2. Instalar Dependências (Apenas se utilizar a visualização opcional)

```bash
pip install networkx matplotlib
```

### 3. Executar o Script Principal

```bash
python main.py
```

O programa imprimirá se há ou não um Caminho Hamiltoniano, e exibirá o caminho caso exista.

### 4. (Opcional) Visualizar o Caminho Hamiltoniano

```bash
python view.py
```

Isso abrirá uma janela com a visualização do grafo e o Caminho Hamiltoniano destacado.

---

## Explicação do Código (Linha a Linha)

Arquivo: **main.py**

```python
def hamiltonian_path(graph):
    n = len(graph)
    path = []

    def backtrack(current, visited):
        visited.add(current)
        path.append(current)

        if len(path) == n:
            return True

        for neighbor in graph[current]:
            if neighbor not in visited:
                if backtrack(neighbor, visited):
                    return True

        visited.remove(current)
        path.pop()
        return False

    for start_node in graph:
        path.clear()
        if backtrack(start_node, set()):
            return path

    return None


# Exemplo de grafo
graph = {
    0: [1, 2],
    1: [0, 2, 3],
    2: [0, 1, 3],
    3: [1, 2]
}

result = hamiltonian_path(graph)
if result:
    print("Caminho Hamiltoniano encontrado:", result)
else:
    print("Não existe Caminho Hamiltoniano no grafo.")
```

---

## Relatório Técnico

### Complexidade Assintótica

- **Pior caso:** O(n!) — onde n é o número de vértices.
- **Melhor caso:** O(n), se o primeiro caminho testado já for Hamiltoniano.
- **Caso médio:** Entre O(n) e O(n!) dependendo do grafo.

O problema pertence à classe **NP-Completo**, assim como o famoso **Problema do Caixeiro Viajante (TSP)**.

---

### Classes de Complexidade

#### 1. O problema está em NP

- Um Caminho Hamiltoniano pode ser **verificado** em tempo polinomial, bastando checar se a lista tem n vértices distintos e se cada vértice é adjacente ao próximo.

#### 2. O problema é NP-Completo

- O problema é **tão difícil quanto qualquer outro em NP**, e não se conhece um algoritmo polinomial para resolvê-lo em todos os casos.
- Está diretamente relacionado ao Problema do Caixeiro Viajante, que também é NP-Completo.

---

### Teorema Mestre

O **Teorema Mestre** não se aplica diretamente aqui, pois ele é usado para resolver **recorrências de algoritmos recursivos com estrutura de divisão e conquista** (como mergesort, quicksort ou Karatsuba).

Como o algoritmo de backtracking não segue esse padrão (não divide o problema igualmente e recursivamente), o Teorema Mestre **não é aplicável** neste caso.

---

### Análise dos Casos

| Caso       | Descrição                                                             | Complexidade         |
|------------|------------------------------------------------------------------------|----------------------|
| Melhor     | O caminho válido é encontrado logo no início                          | O(n)                 |
| Médio      | Parte das permutações são exploradas até encontrar a solução          | O(k), n < k < n!     |
| Pior       | Todas as permutações são testadas sem encontrar nenhuma válida        | O(n!)                |

---

## Visualização do Caminho Hamiltoniano

A imagem abaixo mostra um grafo com 4 vértices e o Caminho Hamiltoniano 0 → 1 → 2 → 3 destacado:

![hamiltonian_path_graph](https://github.com/user-attachments/assets/c1956701-2625-4d42-8e41-10fcbd645555)


---

## Conclusão

Este projeto apresenta uma implementação clara e funcional para resolver o problema do **Caminho Hamiltoniano** em Python, utilizando **backtracking**. Além da implementação, a documentação explica os fundamentos teóricos, complexidade e até visualiza o grafo com o caminho encontrado, facilitando a compreensão para estudos e aplicações práticas.
