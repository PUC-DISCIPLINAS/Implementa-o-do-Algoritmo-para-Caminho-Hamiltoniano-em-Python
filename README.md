Projeto HamiltonianPathFinder
Descrição do Projeto
O projeto HamiltonianPathFinder implementa em Python um algoritmo baseado em backtracking para encontrar Caminhos Hamiltonianos em grafos orientados ou não orientados. Um Caminho Hamiltoniano é um caminho que visita cada vértice do grafo exatamente uma vez. Este problema está relacionado a desafios clássicos da ciência da computação como o Problema do Caixeiro Viajante, sendo considerado de alta complexidade computacional.

Sobre o Algoritmo do Caminho Hamiltoniano
O algoritmo utiliza a técnica de backtracking, explorando todas as possibilidades de caminhos no grafo e retrocedendo quando percebe que um caminho atual não leva a uma solução válida.

Entrada: Um grafo representado por uma matriz de adjacência.

Saída: Um caminho que visita todos os vértices uma única vez (Caminho Hamiltoniano), se existir.

Como Executar o Projeto
1. Ambiente Virtual (Opcional, mas recomendado)
bash
Copiar
Editar
python3 -m venv .venv
source .venv/bin/activate  # Linux/macOS
.venv\Scripts\activate     # Windows
2. Instalar Dependências (somente se for utilizar visualização)
bash
Copiar
Editar
pip install matplotlib networkx
3. Executar o Script Principal
bash
Copiar
Editar
python main.py
4. Executar Visualização (Opcional)
bash
Copiar
Editar
python view.py
Explicação do Código (Linha a Linha)
Arquivo: main.py

python
Copiar
Editar
def is_safe(v, pos, path, graph):
    if graph[path[pos - 1]][v] == 0:
        return False
    if v in path:
        return False
    return True

def hamiltonian_path_util(graph, path, pos):
    if pos == len(graph):
        return True
    for v in range(1, len(graph)):
        if is_safe(v, pos, path, graph):
            path[pos] = v
            if hamiltonian_path_util(graph, path, pos + 1):
                return True
            path[pos] = -1
    return False

def hamiltonian_path(graph):
    path = [-1] * len(graph)
    path[0] = 0
    if not hamiltonian_path_util(graph, path, 1):
        return None
    return path
Relatório Técnico
Análise de Complexidade
Classes de Complexidade
Classe: NP-Completo

Justificativa: O problema de encontrar um Caminho Hamiltoniano pertence à classe NP-Completo, pois:

É possível verificar se uma solução é válida em tempo polinomial.

Não se conhece um algoritmo que resolva o problema em tempo polinomial.

Está diretamente relacionado ao Problema do Caixeiro Viajante (NP-Difícil).

Complexidade Assintótica
Pior Caso: O(n!)

Motivo: O algoritmo testa todas as permutações possíveis de vértices.

Aplicação do Teorema Mestre
O Teorema Mestre não é aplicável, pois o algoritmo não possui uma recorrência clássica de divisão e conquista, mas sim uma estrutura recursiva combinatória (backtracking com busca exaustiva).

Casos de Complexidade
Melhor Caso: O(n) — Quando a primeira combinação verificada já é válida.

Caso Médio: O(n!) — Tempo exponencial devido à natureza do problema.

Pior Caso: O(n!) — Quando o algoritmo precisa testar todas as possibilidades antes de concluir que não há solução.

Complexidade Ciclomática
Nós (N): 9

Arestas (E): 10

Componentes Conexos (P): 1

Cálculo: M = E - N + 2P = 10 - 9 + 2 = 3

A complexidade ciclomática é 3, indicando três caminhos independentes no fluxo de controle da função principal.

Visualização do Grafo
A visualização do grafo com destaque para o Caminho Hamiltoniano pode ser gerada com o arquivo view.py. Exemplo:


Conclusão
Este projeto demonstra a implementação eficiente de um algoritmo para detectar Caminhos Hamiltonianos utilizando Python. Apesar da complexidade elevada, a estratégia de backtracking permite encontrar soluções em grafos pequenos ou moderados. A visualização com NetworkX também facilita o entendimento do comportamento do algoritmo.


