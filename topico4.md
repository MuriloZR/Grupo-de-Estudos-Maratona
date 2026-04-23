# Tópico 04 — Vetores em C e C++

---

## O que é um vetor?

Imagine que você precisa armazenar a nota de 50 alunos. Criar 50 variáveis separadas seria inviável. Um **vetor** (ou *array*) resolve isso: é uma estrutura que armazena **múltiplos valores do mesmo tipo** em sequência na memória, acessíveis por um índice.

```
notas[0]  notas[1]  notas[2]  notas[3]  notas[4]
  7.5       8.0       6.5       9.0       5.0
```

> Em C++, os índices sempre começam em **0**, não em 1.

---

## Arrays estilo C (também funcionam em C++)

Os tópicos a seguir cobrem arrays no estilo da linguagem C, suportados nativamente em C++. São de tamanho fixo e definido em tempo de compilação.

---

## Declaração e Inicialização

### Declarando um vetor

```cpp
tipo nome[tamanho];
```

```cpp
int numeros[5];       // vetor de 5 inteiros (valores indefinidos)
double notas[10];     // vetor de 10 doubles
char vogais[5];       // vetor de 5 caracteres
```

> Um vetor declarado sem inicialização contém **lixo de memória**. Sempre inicialize antes de usar.

### Inicializando na declaração

```cpp
int numeros[5] = {10, 20, 30, 40, 50};
double notas[] = {7.5, 8.0, 6.5, 9.0, 5.0};  // tamanho deduzido automaticamente
int zeros[5] = {0};                            // todos os elementos inicializados com 0
```

### Atribuindo valores individualmente

```cpp
int numeros[3];
numeros[0] = 10;
numeros[1] = 20;
numeros[2] = 30;
```

---

## Acessando Elementos

Cada elemento é acessado pelo seu **índice** entre colchetes.

```cpp
int notas[5] = {7, 8, 6, 9, 5};

std::cout << notas[0] << std::endl;  // 7 (primeiro elemento)
std::cout << notas[4] << std::endl;  // 5 (último elemento)

notas[2] = 10;  // altera o terceiro elemento para 10
```

> Acessar um índice fora do tamanho do vetor (ex: `notas[5]` em um vetor de 5 elementos) causa **comportamento indefinido** — um dos erros mais comuns em C++. O compilador não avisa!

---

## Percorrendo um Vetor com `for`

A forma mais comum de trabalhar com vetores é combiná-los com laços.

### Lendo e exibindo

```cpp
#include <iostream>

int main() {
    int notas[5];

    // Leitura
    for (int i = 0; i < 5; i++) {
        std::cout << "Digite a nota " << i + 1 << ": ";
        std::cin >> notas[i];
    }

    // Exibição
    std::cout << "\nNotas digitadas:" << std::endl;
    for (int i = 0; i < 5; i++) {
        std::cout << "Aluno " << i + 1 << ": " << notas[i] << std::endl;
    }

    return 0;
}
```

### Calculando a soma e a média

```cpp
int valores[5] = {4, 8, 15, 16, 23};
int soma = 0;

for (int i = 0; i < 5; i++) {
    soma += valores[i];
}

double media = (double)soma / 5;
std::cout << "Soma: "  << soma  << std::endl;
std::cout << "Média: " << media << std::endl;
```

### Encontrando o maior e o menor elemento

```cpp
int v[6] = {3, 7, 1, 9, 4, 6};
int maior = v[0];
int menor = v[0];

for (int i = 1; i < 6; i++) {
    if (v[i] > maior) maior = v[i];
    if (v[i] < menor) menor = v[i];
}

std::cout << "Maior: " << maior << std::endl;  // 9
std::cout << "Menor: " << menor << std::endl;  // 1
```

---

## Tamanho de um Vetor

Em C++, não existe uma função nativa que retorne o tamanho de um array. Uma forma comum é usar `sizeof`:

```cpp
int v[] = {10, 20, 30, 40, 50};
int tamanho = sizeof(v) / sizeof(v[0]);  // 20 / 4 = 5

std::cout << "Tamanho: " << tamanho << std::endl;
```

> Por isso, é uma boa prática armazenar o tamanho em uma constante:

```cpp
const int TAM = 5;
int notas[TAM];

for (int i = 0; i < TAM; i++) {
    std::cin >> notas[i];
}
```

---

## Operações com vetores

Arrays estilo C não possuem métodos. As operações exigem que você escreva o algoritmo do zero.

#### Invertendo um vetor

Não existe função nativa para inverter um array estilo C. A abordagem manual usa dois índices que caminham das extremidades para o centro, trocando os elementos:

```cpp
int v[6] = {1, 2, 3, 4, 5, 6};
int inicio = 0;
int fim = 5;

while (inicio < fim) {
    int temp    = v[inicio];
    v[inicio]   = v[fim];
    v[fim]      = temp;
    inicio++;
    fim--;
}
// v agora é: {6, 5, 4, 3, 2, 1}
```

#### Buscando um elemento (busca linear)

Também não há função nativa para busca em arrays estilo C. O algoritmo percorre o vetor elemento por elemento até encontrar o alvo:

```cpp
int v[5] = {10, 30, 50, 70, 90};
int alvo = 50;
int posicao = -1;  // -1 indica "não encontrado"

for (int i = 0; i < 5; i++) {
    if (v[i] == alvo) {
        posicao = i;
        break;
    }
}

if (posicao != -1) {
    std::cout << "Encontrado na posição " << posicao << std::endl;
} else {
    std::cout << "Elemento não encontrado." << std::endl;
}
```

#### Ordenando um vetor (Bubble Sort)

Não existe ordenação nativa para arrays estilo C. O **Bubble Sort** é o algoritmo mais simples para implementar do zero: compara pares de elementos adjacentes e os troca se estiverem fora de ordem, repetindo até o vetor estar ordenado.

```cpp
int v[5] = {5, 3, 8, 1, 4};
int n = 5;

for (int i = 0; i < n - 1; i++) {
    for (int j = 0; j < n - 1 - i; j++) {
        if (v[j] > v[j + 1]) {
            int temp = v[j];
            v[j]     = v[j + 1];
            v[j + 1] = temp;
        }
    }
}
// v agora é: {1, 3, 4, 5, 8}
```

---

## `std::vector` (existe apenas em C++)

Os arrays estilo C têm uma limitação importante: seu tamanho precisa ser definido em tempo de compilação e não pode mudar. O `std::vector` resolve isso — é um array dinâmico que **cresce e encolhe em tempo de execução**, oferecendo uma série de métodos utilitários.

Para usá-lo, inclua o cabeçalho `<vector>`:

```cpp
#include <vector>
```

### Declaração e inicialização

```cpp
std::vector<int> numeros;                     // vetor vazio
std::vector<int> notas(5);                    // 5 elementos inicializados com 0
std::vector<int> valores(5, 10);              // 5 elementos inicializados com 10
std::vector<int> primos = {2, 3, 5, 7, 11};  // inicialização direta
```

### Adicionando e removendo elementos

```cpp
std::vector<int> v;

v.push_back(10);  // adiciona 10 ao final  → {10}
v.push_back(20);  // adiciona 20 ao final  → {10, 20}
v.push_back(30);  // adiciona 30 ao final  → {10, 20, 30}

v.pop_back();     // remove o último elemento → {10, 20}
```

### Acessando elementos

O acesso por índice funciona da mesma forma que nos arrays estilo C:

```cpp
std::vector<int> v = {10, 20, 30, 40, 50};

std::cout << v[0]      << std::endl;  // 10
std::cout << v.front() << std::endl;  // 10 — primeiro elemento
std::cout << v.back()  << std::endl;  // 50 — último elemento
```

### Tamanho e verificações

```cpp
std::vector<int> v = {1, 2, 3};

std::cout << v.size()  << std::endl;  // 3 — número de elementos
std::cout << v.empty() << std::endl;  // 0 (false) — vetor não está vazio

v.clear();  // remove todos os elementos
std::cout << v.empty() << std::endl;  // 1 (true)
```

### Percorrendo com `for`

Como o `std::vector` conhece seu próprio tamanho via `.size()`, o laço fica mais seguro:

```cpp
std::vector<double> notas = {7.5, 8.0, 6.5, 9.0, 5.0};

for (int i = 0; i < notas.size(); i++) {
    std::cout << "Nota " << i + 1 << ": " << notas[i] << std::endl;
}
```

Também é possível usar o **range-based for**, uma forma mais moderna e legível:

```cpp
for (double nota : notas) {
    std::cout << nota << std::endl;
}
```

### Exemplo — leitura dinâmica sem tamanho fixo

Uma das grandes vantagens do `std::vector` é não exigir que o tamanho seja definido antecipadamente:

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numeros;
    int valor;

    std::cout << "Digite números (0 para encerrar):" << std::endl;
    std::cin >> valor;

    while (valor != 0) {
        numeros.push_back(valor);
        std::cin >> valor;
    }

    std::cout << "Você digitou " << numeros.size() << " números." << std::endl;

    int soma = 0;
    for (int n : numeros) {
        soma += n;
    }

    std::cout << "Soma: " << soma << std::endl;

    return 0;
}
```
### Operações com `std::vector`

Ao usar `std::vector` em conjunto com o cabeçalho `<algorithm>`, grande parte das operações ganham versões prontas e otimizadas.
> Grande parte dos algoritmos presentes em `<algorithm>` também funcionam com arrays padrões do C

#### Invertendo — `std::reverse`

```cpp
#include <algorithm>
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5, 6};
std::reverse(v.begin(), v.end());
// v agora é: {6, 5, 4, 3, 2, 1}
```

#### Buscando — `std::find`

Retorna um iterador apontando para o elemento encontrado, ou `v.end()` caso não exista:

```cpp
#include <algorithm>
#include <vector>

std::vector<int> v = {10, 30, 50, 70, 90};
int alvo = 50;

auto it = std::find(v.begin(), v.end(), alvo);

if (it != v.end()) {
    std::cout << "Encontrado na posição " << it - v.begin() << std::endl;
} else {
    std::cout << "Elemento não encontrado." << std::endl;
}
```

#### Ordenando — `std::sort`

Usa um algoritmo eficiente internamente (geralmente Introsort), muito mais rápido que o Bubble Sort para vetores grandes:

```cpp
#include <algorithm>
#include <vector>

std::vector<int> v = {5, 3, 8, 1, 4};
std::sort(v.begin(), v.end());
// v agora é: {1, 3, 4, 5, 8}
```

> Na prática, prefira sempre as funções de `<algorithm>` ao invés de implementar esses algoritmos do zero. A implementação manual é apresentada aqui para fins didáticos, para que você entenda o que realmente acontece.

---


### Comparativo: array estilo C vs `std::vector`

| Característica | Array estilo C | `std::vector` |
|----------------|---------------|---------------|
| Tamanho | Fixo (definido na compilação) | Dinâmico (muda em execução) |
| Saber o tamanho | `sizeof` manual | `.size()` |
| Adicionar elementos | Não é possível | `.push_back()` |
| Remover elementos | Não é possível | `.pop_back()` |
| Verificar se vazio | Não disponível | `.empty()` |
| Recomendado para | Situações simples e de baixo nível | Uso geral em C++ moderno |

---

## Exemplo Completo

Programa que lê as notas de uma turma, calcula a média e indica quais alunos foram aprovados:

```cpp
#include <iostream>
#include <vector>
#include <string>

int main() {
    int n;
    std::cout << "Quantos alunos? ";
    std::cin >> n;

    std::vector<std::string> nomes(n);
    std::vector<double> notas(n);
    double soma = 0;

    // Leitura
    for (int i = 0; i < n; i++) {
        std::cout << "Nome do aluno " << i + 1 << ": ";
        std::cin >> nomes[i];
        std::cout << "Nota de " << nomes[i] << ": ";
        std::cin >> notas[i];
        soma += notas[i];
    }

    double mediaTurma = soma / n;

    // Resultados
    std::cout << "\n--- Resultados ---" << std::endl;
    for (int i = 0; i < n; i++) {
        std::string situacao = (notas[i] >= 6.0) ? "Aprovado" : "Reprovado";
        std::cout << nomes[i] << ": " << notas[i] << " — " << situacao << std::endl;
    }

    std::cout << "\nMedia da turma: " << mediaTurma << std::endl;

    return 0;
}
```

---

## Resumo rápido

**Arrays estilo C:**

| Operação | Sintaxe |
|----------|---------|
| Declarar | `tipo nome[tamanho];` |
| Inicializar | `int v[3] = {1, 2, 3};` |
| Acessar elemento | `v[indice]` |
| Alterar elemento | `v[indice] = valor;` |
| Tamanho com constante | `const int TAM = 5;` |
| Tamanho com sizeof | `sizeof(v) / sizeof(v[0])` |
| Percorrer | `for (int i = 0; i < TAM; i++)` |

**`std::vector`:**

| Operação | Sintaxe |
|----------|---------|
| Declarar | `std::vector<tipo> nome;` |
| Inicializar | `std::vector<int> v = {1, 2, 3};` |
| Adicionar ao final | `v.push_back(valor);` |
| Remover do final | `v.pop_back();` |
| Acessar elemento | `v[indice]` |
| Tamanho | `v.size()` |
| Verificar se vazio | `v.empty()` |
| Limpar | `v.clear()` |
| Percorrer | `for (int i = 0; i < TAM; i++)` ou `for (int x : v)` ou usando iteradores |

---

## Erros Comuns

- **Índice fora dos limites** — acessar `v[n]` em um vetor de tamanho `n` (o último índice válido é `n-1`)
- **Usar lixo de memória** — ler um array estilo C não inicializado
- **Confundir tamanho com último índice**, um vetor de tamanho 5 tem índices de 0 a **4**
- **Usar `=` para copiar arrays estilo C**, `a = b` não funciona, é preciso copiar elemento a elemento (com `std::vector` isso funciona normalmente)

---

## Referências

- [cppreference.com — Arrays](https://en.cppreference.com/w/cpp/language/array)
- [cppreference.com — std::vector](https://en.cppreference.com/w/cpp/container/vector)
- [LearnCpp.com — Arrays](https://www.learncpp.com/cpp-tutorial/introduction-to-arrays-part-i/)
- [LearnCpp.com — std::vector](https://www.learncpp.com/cpp-tutorial/introduction-to-stdvector-and-list-constructors/)
- [LearnCpp.com — Sorting](https://www.learncpp.com/cpp-tutorial/sorting-an-array-using-selection-sort/)