# Aula 05 — Notação Big O e Complexidade de Algoritmos

> Revisão dos conceitos abordados em aula. Guarde este material como referência!

---

## O que é complexidade de algoritmos?

Quando escrevemos um programa, geralmente existem várias formas de resolver o mesmo problema. A **complexidade de algoritmos** é uma forma de medir e comparar o desempenho dessas soluções — não em segundos de relógio, mas em termos de **quanto o tempo de execução ou o uso de memória cresce conforme a entrada aumenta**.

Existem dois tipos de complexidade:

- **Complexidade de tempo** — quantas operações o algoritmo executa em função do tamanho da entrada
- **Complexidade de espaço** — quanta memória extra o algoritmo utiliza em função do tamanho da entrada

Nesta aula, o foco é a complexidade de tempo.

---

## Por que não medir em segundos?

Medir o tempo real de execução depende de fatores externos: velocidade do processador, carga do sistema, linguagem de programação, compilador, etc. Um algoritmo lento pode parecer rápido em um computador potente, e vice-versa.

A complexidade nos dá uma medida **independente de hardware**, focando no comportamento do algoritmo conforme o tamanho da entrada — representado pela letra **n** — cresce.

---

## Notação Big O

A **notação Big O** descreve o **pior caso** de crescimento de um algoritmo. Ela responde à pergunta: *no máximo, quantas operações esse algoritmo realiza para uma entrada de tamanho n?*

Escrevemos como `O(f(n))`, onde `f(n)` é uma função que descreve esse crescimento. Alguns exemplos comuns, do mais eficiente para o menos eficiente:

| Notação | Nome | Exemplo |
|---------|------|---------|
| `O(1)` | Constante | Acessar um elemento de um vetor pelo índice |
| `O(log n)` | Logarítmica | Busca binária |
| `O(n)` | Linear | Percorrer um vetor inteiro |
| `O(n log n)` | Linear-logarítmica | `std::sort` |
| `O(n²)` | Quadrática | Bubble Sort, Selection Sort |
| `O(2ⁿ)` | Exponencial | Força bruta para subconjuntos |
| `O(n!)` | Fatorial | Força bruta para permutações |

> Na notação Big O, **constantes e termos menores são ignorados**. Por exemplo, um algoritmo que realiza `3n + 5` operações é classificado como `O(n)`, pois o que importa é como ele cresce conforme `n` aumenta, não os fatores constantes.

---

## Complexidade O(1) — Constante

O algoritmo executa sempre o mesmo número de operações, independentemente do tamanho da entrada.

```cpp
// Acessar um elemento de um vetor pelo índice é sempre uma única operação,
// não importa se o vetor tem 10 ou 10 milhões de elementos.
int primeiro = v[0];
int ultimo   = v[n - 1];
```

Outros exemplos: atribuição de variável, operações aritméticas simples, `push_back` no `std::vector` (em média).

---

## Complexidade O(n) — Linear

O número de operações cresce proporcionalmente ao tamanho da entrada. Se `n` dobra, o tempo dobra.

```cpp
// Percorre todos os n elementos exatamente uma vez.
int soma = 0;
for (int i = 0; i < n; i++) {
    soma += v[i];
}
```

Outros exemplos: busca linear, imprimir todos os elementos de um vetor, copiar um vetor.

---

## Complexidade O(n²) — Quadrática

Geralmente aparece quando há **dois laços aninhados**, cada um percorrendo a entrada. Se `n` dobra, o tempo quadruplica.

```cpp
// Para cada elemento (laço externo), percorre todos os outros (laço interno).
// Total de operações: n × n = n²
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        // operação
    }
}
```

O **Bubble Sort** visto na aula anterior é um exemplo clássico de `O(n²)`:

```cpp
for (int i = 0; i < n - 1; i++) {
    for (int j = 0; j < n - 1 - i; j++) {
        if (v[j] > v[j + 1]) {
            int temp = v[j];
            v[j]     = v[j + 1];
            v[j + 1] = temp;
        }
    }
}
```

Mesmo que o laço interno reduza a cada iteração, o número total de comparações ainda cresce quadraticamente — por isso a classificação é `O(n²)`.

---

## Complexidade O(log n) — Logarítmica

A cada passo, o algoritmo **descarta metade** dos elementos restantes. Isso faz com que o número de operações cresça muito lentamente mesmo para entradas enormes.

O exemplo clássico é a **busca binária**, que só funciona em vetores já ordenados:

```cpp
// Retorna o índice do elemento alvo, ou -1 se não encontrado.
int buscaBinaria(int v[], int n, int alvo) {
    int esquerda = 0;
    int direita  = n - 1;

    while (esquerda <= direita) {
        int meio = (esquerda + direita) / 2;

        if (v[meio] == alvo) {
            return meio;          // encontrou
        } else if (v[meio] < alvo) {
            esquerda = meio + 1;  // descarta metade esquerda
        } else {
            direita = meio - 1;   // descarta metade direita
        }
    }

    return -1;
}
```

Para um vetor de 1 bilhão de elementos, a busca binária precisa de no máximo **30 comparações**. A busca linear precisaria de até 1 bilhão.

---

## Complexidade O(n log n) — Linear-logarítmica

É a complexidade dos algoritmos de ordenação eficientes, como **Merge Sort**, **Quick Sort** e o `std::sort` da biblioteca padrão do C++. É significativamente melhor que `O(n²)` para entradas grandes.

```cpp
#include <algorithm>
#include <vector>

std::vector<int> v = {5, 3, 8, 1, 4};
std::sort(v.begin(), v.end());  // O(n log n)
```

---

## Comparando na prática

A tabela abaixo mostra o número aproximado de operações para diferentes tamanhos de entrada:

| n | O(1) | O(log n) | O(n) | O(n log n) | O(n²) |
|---|------|----------|------|------------|-------|
| 10 | 1 | 3 | 10 | 33 | 100 |
| 100 | 1 | 7 | 100 | 664 | 10.000 |
| 1.000 | 1 | 10 | 1.000 | 9.966 | 1.000.000 |
| 1.000.000 | 1 | 20 | 1.000.000 | 19.931.568 | 10¹² |

A diferença entre `O(n²)` e `O(n log n)` para `n = 1.000.000` é a diferença entre algo que termina em segundos e algo que levaria anos.

---

## Regras para calcular a complexidade

### Laços simples

Um laço que percorre `n` elementos contribui com `O(n)`:

```cpp
for (int i = 0; i < n; i++) { ... }  // O(n)
```

### Laços aninhados

Laços aninhados se multiplicam:

```cpp
for (int i = 0; i < n; i++) {        // O(n)
    for (int j = 0; j < n; j++) {    // O(n)
        ...
    }
}
// Complexidade total: O(n × n) = O(n²)
```

### Blocos sequenciais

Blocos em sequência somam, e mantém-se apenas o termo dominante:

```cpp
for (int i = 0; i < n; i++) { ... }  // O(n)
for (int i = 0; i < n; i++) { ... }  // O(n)
// Total: O(n) + O(n) = O(2n) → simplifica para O(n)
```

### Constantes são descartadas

```cpp
for (int i = 0; i < 3 * n; i++) { ... }  // O(3n) → O(n)
```

---

## Busca linear vs busca binária — comparação direta

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

// O(n) — percorre elemento por elemento
int buscaLinear(const std::vector<int>& v, int alvo) {
    for (int i = 0; i < v.size(); i++) {
        if (v[i] == alvo) return i;
    }
    return -1;
}

// O(log n) — requer vetor ordenado
int buscaBinaria(const std::vector<int>& v, int alvo) {
    int esquerda = 0;
    int direita  = v.size() - 1;

    while (esquerda <= direita) {
        int meio = (esquerda + direita) / 2;
        if      (v[meio] == alvo) return meio;
        else if (v[meio] <  alvo) esquerda = meio + 1;
        else                      direita  = meio - 1;
    }
    return -1;
}

int main() {
    std::vector<int> v = {1, 3, 5, 7, 9, 11, 13, 15, 17, 19};

    std::cout << buscaLinear(v, 13)  << std::endl;  // 6
    std::cout << buscaBinaria(v, 13) << std::endl;  // 6

    return 0;
}
```

Para este vetor de 10 elementos a diferença é irrelevante. Para um vetor de 1 bilhão de elementos ordenados, a busca linear pode fazer 1 bilhão de comparações, enquanto a binária faz no máximo 30.

---

## Resumo rápido

| Complexidade | Comportamento | Exemplo |
|--------------|---------------|---------|
| `O(1)` | Não depende de n | Acesso por índice |
| `O(log n)` | Divide o problema pela metade a cada passo | Busca binária |
| `O(n)` | Cresce proporcionalmente a n | Busca linear, soma de vetor |
| `O(n log n)` | Levemente pior que linear | `std::sort` |
| `O(n²)` | Dois laços aninhados sobre n | Bubble Sort |
| `O(2ⁿ)` | Dobra a cada elemento adicionado | Força bruta de subconjuntos |

**Regras práticas:**
- Constantes e termos menores são ignorados: `O(3n + 5)` → `O(n)`
- Laços aninhados se multiplicam: dois laços de `n` → `O(n²)`
- Blocos sequenciais somam, e prevalece o maior: `O(n) + O(n²)` → `O(n²)`
- Prefira `O(n log n)` a `O(n²)` sempre que possível para entradas grandes

---

## Referencias

- [Big O Cheat Sheet](https://www.bigocheatsheet.com/)
- [cppreference.com — std::sort](https://en.cppreference.com/w/cpp/algorithm/sort)
- [cppreference.com — std::binary_search](https://en.cppreference.com/w/cpp/algorithm/binary_search)
- [Introduction to Algorithms — Cormen et al.](https://mitpress.mit.edu/9780262046305/introduction-to-algorithms/)