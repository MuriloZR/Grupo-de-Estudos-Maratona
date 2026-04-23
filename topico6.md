# Tópico 06 — Estruturas de Dados: `map`, `set`, `stack` e `queue`

---

## Por que outras estruturas de dados?

O `std::vector` é versátil, mas nem sempre é a melhor ferramenta. Dependendo do problema, outras estruturas oferecem operações mais eficientes. Esta aula apresenta quatro estruturas da biblioteca padrão do C++, cada uma com um propósito bem definido.

| Estrutura | Cabeçalho | Ideia central |
|-----------|-----------|---------------|
| `std::stack` | `<stack>` | Pilha — o último a entrar é o primeiro a sair |
| `std::queue` | `<queue>` | Fila — o primeiro a entrar é o primeiro a sair |
| `std::set` | `<set>` | Coleção de elementos únicos, sempre ordenada |
| `std::map` | `<map>` | Coleção de pares chave-valor, ordenada pela chave |

---

## `std::pair` — Par de valores

Antes de entrar nas estruturas principais, vale conhecer o `std::pair`, pois ele aparece com frequência ao trabalhar com `std::map` e outras estruturas. Ele está disponível via `<utility>`, mas é incluído automaticamente pela maioria dos cabeçalhos da biblioteca padrão.

Um `std::pair` agrupa **dois valores de tipos potencialmente diferentes** em uma única unidade. Os valores são acessados por `.first` e `.second`.

```cpp
#include <utility>
#include <iostream>
#include <string>

int main() {
    std::pair<std::string, int> aluno = {"Alice", 95};

    std::cout << aluno.first  << std::endl;  // Alice
    std::cout << aluno.second << std::endl;  // 95

    // Modificando os valores
    aluno.second = 98;
    std::cout << aluno.second << std::endl;  // 98

    return 0;
}
```

`std::make_pair` é uma forma alternativa de criar um par sem precisar declarar os tipos explicitamente:

```cpp
auto coordenada = std::make_pair(10, 20);
std::cout << coordenada.first  << std::endl;  // 10
std::cout << coordenada.second << std::endl;  // 20
```

O `std::pair` é o tipo de cada elemento ao iterar sobre um `std::map` — por isso o padrão `par.first` para a chave e `par.second` para o valor aparece nos exemplos mais adiante neste arquivo.

---

## `std::stack` — Pilha de valores

Uma pilha segue o princípio **LIFO** — Last In, First Out (último a entrar, primeiro a sair). Pense em uma pilha de pratos: você só consegue pegar ou colocar pelo topo.

```
push(10) → [10]
push(20) → [10, 20]
push(30) → [10, 20, 30]
pop()    → [10, 20]       (30 foi removido)
top()    →  20            (elemento do topo)
```

### Operações principais

| Operação | Método | Complexidade |
|----------|--------|--------------|
| Adicionar no topo | `push(valor)` | `O(1)` |
| Remover do topo | `pop()` | `O(1)` |
| Consultar o topo | `top()` | `O(1)` |
| Verificar se vazia | `empty()` | `O(1)` |
| Número de elementos | `size()` | `O(1)` |

> `pop()` remove o elemento mas não o retorna. Para ler e remover, use `top()` seguido de `pop()`.

### Exemplo — invertendo uma palavra

```cpp
#include <iostream>
#include <stack>
#include <string>

int main() {
    std::string palavra = "hello";
    std::stack<char> pilha;

    // Empilha cada caractere
    for (char c : palavra) {
        pilha.push(c);
    }

    // Desempilha na ordem inversa
    std::string invertida = "";
    while (!pilha.empty()) {
        invertida += pilha.top();
        pilha.pop();
    }

    std::cout << invertida << std::endl;  // "olleh"

    return 0;
}
```

### Exemplo — verificando parênteses balanceados

Um uso clássico de pilhas é verificar se uma expressão tem parênteses corretamente abertos e fechados:

```cpp
#include <iostream>
#include <stack>
#include <string>

bool balanceado(const std::string& expr) {
    std::stack<char> pilha;

    for (char c : expr) {
        if (c == '(') {
            pilha.push(c);
        } else if (c == ')') {
            if (pilha.empty()) return false;
            pilha.pop();
        }
    }

    return pilha.empty();
}

int main() {
    std::cout << balanceado("(a + b) * (c - d)") << std::endl;  // 1 (true)
    std::cout << balanceado("((x + y)")           << std::endl;  // 0 (false)

    return 0;
}
```

---

## `std::queue` — Fila

Uma fila segue o princípio **FIFO** — First In, First Out (primeiro a entrar, primeiro a sair). Como uma fila de banco: quem chegou primeiro é atendido primeiro.

```
push(10) → [10]
push(20) → [10, 20]
push(30) → [10, 20, 30]
pop()    → [20, 30]       (10 foi removido — estava na frente)
front()  →  20            (elemento da frente)
back()   →  30            (elemento do fim)
```

### Operações principais

| Operação | Método | Complexidade |
|----------|--------|--------------|
| Adicionar no fim | `push(valor)` | `O(1)` |
| Remover da frente | `pop()` | `O(1)` |
| Consultar a frente | `front()` | `O(1)` |
| Consultar o fim | `back()` | `O(1)` |
| Verificar se vazia | `empty()` | `O(1)` |
| Número de elementos | `size()` | `O(1)` |

### Exemplo — simulando uma fila de atendimento

```cpp
#include <iostream>
#include <queue>
#include <string>

int main() {
    std::queue<std::string> fila;

    // Clientes chegando
    fila.push("Alice");
    fila.push("Bruno");
    fila.push("Carla");

    // Atendimento em ordem de chegada
    while (!fila.empty()) {
        std::cout << "Atendendo: " << fila.front() << std::endl;
        fila.pop();
    }

    return 0;
}
```

**Saída:**
```
Atendendo: Alice
Atendendo: Bruno
Atendendo: Carla
```

---

## Comparativo: `stack` vs `queue`

| | `std::stack` | `std::queue` |
|-|--------------|--------------|
| Princípio | LIFO | FIFO |
| Entrada | Pelo topo | Pelo fim |
| Saída | Pelo topo | Pela frente |
| Consulta | `top()` | `front()` e `back()` |
| Uso típico | Histórico de ações, recursão, parsers | Filas de espera, processamento em ordem |

---

## `std::set` — Conjunto

Um `std::set` armazena elementos **sem repetição** e **sempre em ordem crescente**. Inserir um elemento que já existe não causa erro — o elemento simplesmente é ignorado.

Internamente, o `std::set` é implementado como uma árvore binária de busca balanceada, o que garante `O(log n)` para inserção, remoção e busca.

### Operações principais

| Operação | Método | Complexidade |
|----------|--------|--------------|
| Inserir | `insert(valor)` | `O(log n)` |
| Remover | `erase(valor)` | `O(log n)` |
| Verificar se contém | `count(valor)` | `O(log n)` |
| Número de elementos | `size()` | `O(1)` |
| Verificar se vazio | `empty()` | `O(1)` |
| Limpar | `clear()` | `O(n)` |

> `count(valor)` retorna `1` se o elemento existe e `0` se não existe — funciona como um teste booleano.

### Exemplo — removendo duplicatas de um vetor

```cpp
#include <iostream>
#include <set>
#include <vector>

int main() {
    std::vector<int> v = {4, 1, 3, 1, 2, 4, 3, 5};
    std::set<int> s(v.begin(), v.end());

    std::cout << "Sem duplicatas, em ordem:" << std::endl;
    for (int x : s) {
        std::cout << x << " ";
    }
    std::cout << std::endl;
    // Saída: 1 2 3 4 5

    return 0;
}
```

### Exemplo — verificando elementos únicos

```cpp
#include <iostream>
#include <set>

int main() {
    std::set<std::string> presentes;

    presentes.insert("Ana");
    presentes.insert("Bruno");
    presentes.insert("Ana");    // ignorado — já existe

    std::cout << presentes.size() << std::endl;  // 2

    if (presentes.count("Bruno")) {
        std::cout << "Bruno está presente." << std::endl;
    }

    presentes.erase("Bruno");

    if (!presentes.count("Bruno")) {
        std::cout << "Bruno foi removido." << std::endl;
    }

    return 0;
}
```

---

## `std::map` — Mapa (dicionário)

Um `std::map` armazena pares **chave-valor**, onde cada chave é única. É equivalente a um dicionário: dado um termo (chave), você obtém sua definição (valor). As entradas ficam sempre ordenadas pela chave.

Assim como o `std::set`, é implementado como árvore binária de busca balanceada — todas as operações principais são `O(log n)`.

```
map["Alice"] = 95
map["Bruno"] = 87
map["Carla"] = 91

map["Alice"] → 95
```

### Operações principais

| Operação | Método | Complexidade |
|----------|--------|--------------|
| Inserir ou atualizar | `map[chave] = valor` | `O(log n)` |
| Acessar valor | `map[chave]` | `O(log n)` |
| Verificar se chave existe | `count(chave)` | `O(log n)` |
| Remover | `erase(chave)` | `O(log n)` |
| Número de pares | `size()` | `O(1)` |
| Verificar se vazio | `empty()` | `O(1)` |

> Usar `map[chave]` para uma chave que não existe **cria automaticamente** uma entrada com o valor padrão do tipo (0 para `int`, `""` para `string`). Use `count()` para verificar a existência antes de acessar, se isso for relevante.

### Exemplo — contando frequência de palavras

```cpp
#include <iostream>
#include <map>
#include <string>
#include <vector>

int main() {
    std::vector<std::string> palavras = {
        "banana", "maca", "banana", "laranja", "maca", "banana"
    };

    std::map<std::string, int> frequencia;

    for (const std::string& p : palavras) {
        frequencia[p]++;  // cria com 0 na primeira vez, depois incrementa
    }

    for (const auto& par : frequencia) {
        std::cout << par.first << ": " << par.second << std::endl;
    }

    return 0;
}
```

**Saída:**
```
banana: 3
laranja: 1
maca: 2
```

### Exemplo — agenda de contatos

```cpp
#include <iostream>
#include <map>
#include <string>

int main() {
    std::map<std::string, std::string> agenda;

    agenda["Alice"] = "(11) 99999-0001";
    agenda["Bruno"] = "(11) 99999-0002";
    agenda["Carla"] = "(11) 99999-0003";

    std::string nome = "Bruno";

    if (agenda.count(nome)) {
        std::cout << nome << ": " << agenda[nome] << std::endl;
    } else {
        std::cout << nome << " não encontrado." << std::endl;
    }

    agenda.erase("Bruno");
    std::cout << "Contatos restantes: " << agenda.size() << std::endl;  // 2

    return 0;
}
```

### Iterando sobre um `std::map`

Ao iterar, cada elemento é um `std::pair<chave, valor>`, acessado por `.first` e `.second`:

```cpp
std::map<std::string, int> notas;
notas["Alice"] = 95;
notas["Bruno"] = 87;
notas["Carla"] = 91;

for (const auto& par : notas) {
    std::cout << par.first << " → " << par.second << std::endl;
}
```

**Saída (em ordem alfabética pela chave):**
```
Alice → 95
Bruno → 87
Carla → 91
```

---

## `std::unordered_map` e `std::unordered_set`

O `std::map` e o `std::set` mantêm os elementos ordenados, o que custa `O(log n)` por operação. Quando a ordenação não importa e o que se quer é a maior velocidade possível, existem as versões **não ordenadas**:

| Estrutura | Cabeçalho | Ordenada | Complexidade média | Complexidade pior caso |
|-----------|-----------|----------|--------------------|------------------------|
| `std::map` | `<map>` | Sim | `O(log n)` | `O(log n)` |
| `std::unordered_map` | `<unordered_map>` | Não | `O(1)` | `O(n)` |
| `std::set` | `<set>` | Sim | `O(log n)` | `O(log n)` |
| `std::unordered_set` | `<unordered_set>` | Não | `O(1)` | `O(n)` |

Internamente, ambas usam uma **tabela hash**: a chave é processada por uma função de hash que determina diretamente a posição do elemento na memória, eliminando a necessidade de percorrer uma árvore. Isso resulta em `O(1)` em média, mas em casos de muitas colisões de hash o desempenho pode degradar para `O(n)` no pior caso.

### `std::unordered_map`

A interface é idêntica à do `std::map` — a diferença está apenas no desempenho e na ausência de ordenação.

```cpp
#include <iostream>
#include <unordered_map>
#include <string>

int main() {
    std::unordered_map<std::string, int> frequencia;

    frequencia["banana"]++;
    frequencia["maca"]++;
    frequencia["banana"]++;
    frequencia["banana"]++;

    std::cout << frequencia["banana"] << std::endl;  // 3
    std::cout << frequencia["maca"]   << std::endl;  // 1

    // A ordem de iteração NÃO é garantida
    for (const auto& par : frequencia) {
        std::cout << par.first << ": " << par.second << std::endl;
    }

    return 0;
}
```

> A saída da iteração pode variar entre execuções — a ordem dos elementos não é definida.

### `std::unordered_set`

Mesma ideia: funciona como `std::set`, mas sem garantia de ordenação e com `O(1)` em média.

```cpp
#include <iostream>
#include <unordered_set>

int main() {
    std::unordered_set<int> visitados;

    visitados.insert(42);
    visitados.insert(7);
    visitados.insert(42);  // ignorado

    std::cout << visitados.size()    << std::endl;  // 2
    std::cout << visitados.count(42) << std::endl;  // 1 (existe)
    std::cout << visitados.count(99) << std::endl;  // 0 (não existe)

    return 0;
}
```

### Quando usar cada versão

Use `std::map` / `std::set` quando:
- A ordem dos elementos importa
- Você precisa iterar em ordem crescente de chave
- O pior caso de desempenho precisa ser garantido (`O(log n)`)

Use `std::unordered_map` / `std::unordered_set` quando:
- A ordem não importa
- A prioridade é velocidade máxima nas operações de inserção, remoção e busca
- As chaves são tipos simples como `int` ou `std::string`

---

## Comparativo geral

| Estrutura | Ordenada | Elementos únicos | Acesso por chave | Complexidade média |
|-----------|----------|------------------|------------------|--------------------|
| `std::vector` | Não | Não | Por índice inteiro | `O(1)` acesso, `O(n)` busca |
| `std::stack` | — | Não | Somente o topo | `O(1)` |
| `std::queue` | — | Não | Somente frente e fim | `O(1)` |
| `std::set` | Sim | Sim | Não | `O(log n)` |
| `std::map` | Sim (pela chave) | Chaves únicas | Por chave arbitrária | `O(log n)` |
| `std::unordered_set` | Não | Sim | Não | `O(1)` |
| `std::unordered_map` | Não | Chaves únicas | Por chave arbitrária | `O(1)` |

---

## Resumo rápido

**`std::pair`** — use quando precisar armazenar dois valores na mesma variável: coordenadas de um ponto, acessar chave e elemento do `map`.

**`std::stack`** — use quando precisar de acesso apenas ao elemento mais recente (LIFO): histórico de ações, avaliação de expressões, backtracking.

**`std::queue`** — use quando precisar processar elementos na ordem em que chegaram (FIFO): filas de espera, processamento em lote, BFS em grafos.

**`std::set`** — use quando precisar garantir que não há duplicatas, precisar iterar em ordem crescente, ou quando o pior caso de desempenho precisa ser previsível.

**`std::map`** — use quando precisar associar uma informação a outra (chave → valor) com iteração em ordem crescente pela chave.

**`std::unordered_set`** — use quando precisar de unicidade e a maior velocidade possível, sem se importar com ordenação.

**`std::unordered_map`** — use quando precisar de associação chave → valor com a maior velocidade possível, sem se importar com ordenação.

---

## Referencias

- [cppreference.com — std::pair](https://en.cppreference.com/cpp/utility/pair)
- [cppreference.com — std::stack](https://en.cppreference.com/w/cpp/container/stack)
- [cppreference.com — std::queue](https://en.cppreference.com/w/cpp/container/queue)
- [cppreference.com — std::set](https://en.cppreference.com/w/cpp/container/set)
- [cppreference.com — std::map](https://en.cppreference.com/w/cpp/container/map)
- [cppreference.com — std::unordered_map](https://en.cppreference.com/w/cpp/container/unordered_map)
- [cppreference.com — std::unordered_set](https://en.cppreference.com/w/cpp/container/unordered_set)
- [LearnCpp.com — Containers](https://www.learncpp.com/cpp-tutorial/container-classes/)