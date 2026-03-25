# Tópico 01 — Tipos de Variáveis, `std::cin` e `std::cout` em C++
---

##  O que é uma variável?

Uma variável é um espaço na memória do computador onde podemos armazenar um valor. Em C++, toda variável precisa ter um **tipo** declarado antes de ser usada.

```cpp
tipo nome_da_variavel = valor_inicial;
```
> Se a variável não for inicializada, ela conterá "lixo" de memória até que o valor dentro dela seja sobrescrito

---

##  Tipos Primitivos de Variáveis

### Inteiros

| Tipo | Tamanho típico | Intervalo aproximado |
|------|---------------|----------------------|
| `int` | 4 bytes | -2.147.483.648 (-2³¹) a 2.147.483.647 (2³¹ - 1) |
| `short` | 2 bytes | -32.768 a 32.767 |
| `long` | 4 ou 8 bytes | Depende da plataforma, mas é sempre maior ou igual ao `int` |
| `long long` | 8 bytes | ±9,2 × 10¹⁸ ( ± 9,2 quintilhões) |

> Use `unsigned` antes do tipo para aceitar apenas valores não-negativos, dobrando o limite positivo. Ex: `unsigned int`.

```cpp
int idade = 20;
long long populacaoMundial = 8000000000LL; //LL indica que é long long
unsigned int pontos = 150;
```

---

### Números de Ponto Flutuante (decimais)

| Tipo | Tamanho típico | Precisão |
|------|---------------|----------|
| `float` | 4 bytes | ~7 dígitos |
| `double` | 8 bytes | ~15 dígitos |
| `long double` | 12 ou 16 bytes | ~18–19 dígitos |

```cpp
float altura = 1.75f;   // 'f' indica que é float
double pi = 3.14159265358979;
```

> Prefira `double` quando precisar de mais precisão nos cálculos.

---

### Caracteres e Booleanos

| Tipo | Tamanho típico | O que armazena |
|------|---------------|----------------|
| `char` | 1 byte | Um único caractere (tabela ASCII) |
| `bool` | 1 byte | `true` ou `false` |

```cpp
char letra = 'A';
bool aprovado = true;
bool reprovado = false;
```

> Atenção: `char` usa aspas **simples** `' '`, enquanto `std::string` usa aspas **duplas** `" "`.

---

### Texto — `std::string`

Para trabalhar com cadeias de caracteres (texto), usamos `std::string`, que requer a inclusão do cabeçalho `<string>`:

```cpp
#include <string>

std::string nome = "João";
std::string curso = "Ciência da Computação";
```

---

## Saída de dados — `std::cout` ou `printf`

`std::cout` (de *character output*) é usado para **exibir informações na tela**.

```cpp
#include <iostream>

using namespace std;

int main() {
    cout << "Olá, mundo!" << endl;
    return 0;
}
```

### Operador `<<` (inserção)

O operador `<<` "empurra" dados para a saída. Podemos encadear múltiplos valores:

```cpp
std::string nome = "Ana";
int idade = 21;

std::cout << "Nome: " << nome << ", Idade: " << idade << std::endl;
```

**Saída:**
```
Nome: Ana, Idade: 21
```

### `std::endl` vs `'\n'`

| | Comportamento |
|-|---------------|
| `std::endl` | Quebra de linha **+** limpa o buffer de saída |
| `'\n'` | Apenas quebra de linha (mais rápido) |

```cpp
std::cout << "Linha 1\n";
std::cout << "Linha 2" << std::endl;
```

### `Printf`
Também é usado para exibir informações na tela, mas é mais simples (não possui operadores especiais)

```cpp
#include <iostream>

using namespace std;

int main() {
    printf("Olá mundo!\n");
    return 0;
}
```

#### Para exibir variáveis

```cpp
#include <iostream>

using namespace std;

int main() {
    int idade = 21;
    string nome = "João";

    printf("Nome: %s, Idade: %d\n", nome.c_str(), idade);
    return 0;
}
```
**Saída:**
```
Nome: João, Idade: 21
```

---

## Entrada de dados — `std::cin` ou `scanf`

`std::cin` (de *character input*) é usado para **ler dados digitados pelo usuário**.

```cpp
#include <iostream>

using namespace std;

int main() {
    int numero;
    cout << "Digite um número: ";
    cin >> numero;
    cout << "Você digitou: " << numero << endl;
    return 0;
}
```

### Operador `>>` (extração)

O operador `>>` "extrai" dados da entrada e armazena na variável. Também pode ser encadeado:

```cpp
int a, b;
std::cout << "Digite dois números: ";
std::cin >> a >> b;
std::cout << "Soma: " << a + b << std::endl;
```

### Lendo uma linha inteira com `std::getline`

`std::cin >>` para na leitura ao encontrar um espaço. Para ler uma frase completa, use `std::getline`:

```cpp
#include <iostream>
#include <string>

using namespace std;

int main() {
    string nomeCompleto;
    cout << "Digite seu nome completo: ";
    getline(cin, nomeCompleto);
    cout << "Olá, " << nomeCompleto << "!" << endl;
    return 0;
}
```

> **Cuidado:** Ao misturar `std::cin >>` com `std::getline`, pode ocorrer um problema com o caractere `'\n'` que fica no buffer. Nesse caso, use `std::cin.ignore()` antes do `std::getline`.

### `scanf`
Também serve para ler dados digitados pelo usuário, é mais simples (não possui operadores especiais), mas é um pouco mais "chato" de usar, e limitado, em relação ao `std::cin`

```cpp
#include <iostream>

using namespace std;

int main() {
    int numero;
    printf("Digite um número: ");

    scanf("%d", &numero);

    printf("Você digitou: %d\n", numero);
    return 0;
}
```

---

## Estrutura básica de um programa em C++

```cpp
#include <iostream>  // necessário para cin e cout
#include <string>    // necessário para string

using namespace std;

int main() {
    // Declaração de variáveis
    string nome;
    int idade;
    double altura;

    // Entrada de dados
    cout << "Digite seu nome: ";
    cin >> nome;

    cout << "Digite sua idade: ";
    cin >> idade;

    cout << "Digite sua altura: ";
    cin >> altura;

    // Saída de dados
    cout << "\n--- Dados informados ---" << endl;
    cout << "Nome:   " << nome   << endl;
    cout << "Idade:  " << idade  << " anos" << endl;
    cout << "Altura: " << altura << " m" << endl;

    return 0;
}
```
---

## Resumo rápido

| Conceito | Como usar |
|----------|-----------|
| Declarar variável | `tipo nome = valor;` |
| Inteiro | `int x = 10;` |
| Decimal | `double y = 3.14;` |
| Caractere | `char c = 'A';` |
| Booleano | `bool b = true;` |
| Texto | `std::string s = "olá";` |
| Imprimir na tela | `std::cout << valor;` |
| Ler do teclado | `std::cin >> variavel;` |
| Ler linha inteira | `std::getline(std::cin, variavel);` |
| Quebra de linha | `'\n'` ou `std::endl` |

---

## Referências

- [cppreference.com — Tipos fundamentais](https://en.cppreference.com/w/cpp/language/types)
- [cppreference.com — std::cout](https://en.cppreference.com/w/cpp/io/cout)
- [cppreference.com — std::cin](https://en.cppreference.com/w/cpp/io/cin)
- [cplusplus.com](https://cplusplus.com/)