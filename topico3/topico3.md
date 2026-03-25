# Aula 03 — Laços de Repetição em C++
---

## O que são laços de repetição?

Laços (ou *loops*) permitem que um bloco de código seja **executado várias vezes** sem precisar reescrevê-lo. A repetição continua enquanto uma condição for verdadeira, ou por um número determinado de vezes.

C++ oferece três estruturas de repetição: `for`, `while` e `do while`.

---

## `for`

Ideal quando se sabe **quantas vezes** o laço deve repetir. Reúne em uma linha só a inicialização, a condição e o incremento.

### Sintaxe

```cpp
for (inicializacao; condicao; incremento) {
    // código repetido enquanto a condição for true
}
```

| Parte | O que faz | Quando executa |
|-------|-----------|----------------|
| `inicializacao` | Declara e define a variável de controle | Uma única vez, no início |
| `condicao` | Verifica se o laço continua | Antes de cada iteração |
| `incremento` | Atualiza a variável de controle | Após cada iteração |

### Exemplo — Contando de 1 a 5

```cpp
#include <iostream>

int main() {
    for (int i = 1; i <= 5; i++) {
        std::cout << i << std::endl;
    }
    return 0;
}
```

**Saída:**
```
1
2
3
4
5
```

### Exemplo — Contando de forma decrescente

```cpp
for (int i = 10; i >= 1; i--) {
    std::cout << i << " ";
}
std::cout << std::endl;
```

**Saída:**
```
10 9 8 7 6 5 4 3 2 1
```

### Exemplo — Somando os N primeiros números

```cpp
#include <iostream>

int main() {
    int n;
    std::cout << "Digite N: ";
    std::cin >> n;

    int soma = 0;
    for (int i = 1; i <= n; i++) {
        soma += i;  // equivalente a: soma = soma + i
    }

    std::cout << "Soma de 1 a " << n << " = " << soma << std::endl;
    return 0;
}
```

---

## `while`

Ideal quando **não se sabe antecipadamente** quantas vezes o laço vai repetir. A condição é verificada **antes** de cada iteração.

### Sintaxe

```cpp
while (condicao) {
    // código repetido enquanto a condição for true
}
```

> Se a condição já for falsa na primeira verificação, o bloco **nunca é executado**.

### Exemplo — Validação de entrada

```cpp
#include <iostream>

int main() {
    int senha;

    std::cout << "Digite a senha: ";
    std::cin >> senha;

    while (senha != 1234) {
        std::cout << "Senha incorreta. Tente novamente: ";
        std::cin >> senha;
    }

    std::cout << "Acesso liberado!" << std::endl;
    return 0;
}
```

### Exemplo — Leitura até valor sentinela

Um **valor sentinela** é um valor especial que sinaliza o fim da entrada.

```cpp
#include <iostream>

using namespace std;

int main() {
    int valor;
    int soma = 0;
    int quantidade = 0;

    cout << "Digite números (0 para encerrar):" << endl;
    cin >> valor;

    while (valor != 0) {
        soma += valor;
        quantidade++;
        cin >> valor;
    }

    if (quantidade > 0) {
        cout << "Média: " << (double)soma / quantidade << endl;
    } else {
        cout << "Nenhum número informado." << endl;
    }

    return 0;
}
```

---

## `do while`

Semelhante ao `while`, mas a condição é verificada **depois** de cada iteração. Isso garante que o bloco seja executado **pelo menos uma vez**.

### Sintaxe

```cpp
do {
    // código executado ao menos uma vez
} while (condicao);
```

> Não esqueça do ponto e vírgula `;` após o `while`.

### Exemplo — Menu de opções

```cpp
#include <iostream>

int main() {
    int opcao;

    do {
        std::cout << "\n--- Menu ---" << std::endl;
        std::cout << "1. Iniciar"    << std::endl;
        std::cout << "2. Configurar" << std::endl;
        std::cout << "0. Sair"       << std::endl;
        std::cout << "Escolha: ";
        std::cin >> opcao;

        switch (opcao) {
            case 1: std::cout << "Iniciando..." << std::endl; break;
            case 2: std::cout << "Configurando..." << std::endl; break;
            case 0: std::cout << "Saindo..." << std::endl; break;
            default: std::cout << "Opção inválida." << std::endl; break;
        }

    } while (opcao != 0);

    return 0;
}
```

> O `do while` é o mais natural para menus, pois o menu precisa aparecer ao menos uma vez antes de qualquer verificação.

---

## `break` e `continue`

Duas palavras-chave que alteram o fluxo normal de um laço.

### `break` — interrompe o laço imediatamente

```cpp
for (int i = 1; i <= 10; i++) {
    if (i == 5) {
        break;  // sai do laço quando i chega em 5
    }
    std::cout << i << " ";
}
// Saída: 1 2 3 4
```

### `continue` — pula para a próxima iteração

```cpp
for (int i = 1; i <= 10; i++) {
    if (i % 2 == 0) {
        continue;  // ignora os pares e vai para o próximo i
    }
    std::cout << i << " ";
}
// Saída: 1 3 5 7 9
```

---

## Laço infinito

Um laço sem condição de parada roda para sempre. Geralmente é combinado com `break` para controlar a saída.

```cpp
while (true) {
    int x;
    std::cout << "Digite um número positivo: ";
    std::cin >> x;

    if (x > 0) {
        std::cout << "Válido!" << std::endl;
        break;
    }

    std::cout << "Número inválido, tente novamente." << std::endl;
}
```

---

## Laços Aninhados

É possível colocar um laço dentro de outro. O laço interno completa **todas as suas iterações** a cada iteração do laço externo.

### Exemplo — Tabuada completa

```cpp
#include <iostream>

int main() {
    for (int i = 1; i <= 10; i++) {
        std::cout << "Tabuada do " << i << ":" << std::endl;
        for (int j = 1; j <= 10; j++) {
            std::cout << i << " x " << j << " = " << i * j << std::endl;
        }
        std::cout << std::endl;
    }
    return 0;
}
```

### Exemplo — Triângulo de asteriscos

```cpp
int linhas = 5;

for (int i = 1; i <= linhas; i++) {
    for (int j = 1; j <= i; j++) {
        std::cout << "* ";
    }
    std::cout << std::endl;
}
```

**Saída:**
```
*
* *
* * *
* * * *
* * * * *
```

---

## Exemplo Completo

Programa que lê N números e exibe o maior, o menor e a média:

```cpp
#include <iostream>

using namespace std;

int main() {
    int n;
    cout << "Quantos números você vai digitar? ";
    cin >> n;

    if (n <= 0) {
        cout << "Quantidade inválida." << endl;
        return 1;
    }

    double valor, soma = 0;
    double maior, menor;

    cout << "Digite o 1º número: ";
    cin >> valor;
    maior = menor = soma = valor;

    for (int i = 2; i <= n; i++) {
        cout << "Digite o " << i << "º número: ";
        cin >> valor;

        soma += valor;

        if (valor > maior) maior = valor;
        if (valor < menor) menor = valor;
    }

    cout << "\n--- Resultados ---" << endl;
    cout << "Maior: "  << maior    << endl;
    cout << "Menor: "  << menor    << endl;
    cout << "Média: "  << soma / n << endl;

    return 0;
}
```

---

## Resumo rápido

| Laço | Quando usar | Condição verificada |
|------|-------------|---------------------|
| `for` | Número de repetições conhecido | Antes de cada iteração |
| `while` | Número de repetições desconhecido | Antes de cada iteração |
| `do while` | Deve executar ao menos uma vez | Depois de cada iteração |

| Palavra-chave | Efeito |
|---------------|--------|
| `break` | Encerra o laço imediatamente |
| `continue` | Pula para a próxima iteração |

---

## Referências

- [cppreference.com — for](https://en.cppreference.com/w/cpp/language/for)
- [cppreference.com — while](https://en.cppreference.com/w/cpp/language/while)
- [cppreference.com — do-while](https://en.cppreference.com/w/cpp/language/do)
- [LearnCpp.com — Loops](https://www.learncpp.com/cpp-tutorial/introduction-to-loops-and-while-statements/)