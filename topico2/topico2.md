# Tópico 02 — Condicionais em C/C++
---

## O que são condicionais?

Condicionais permitem que o programa **tome decisões** com base em uma condição. Se a condição for verdadeira, um bloco de código é executado; caso contrário, outro bloco pode ser executado no lugar.

---

## Operadores Relacionais

Antes de escrever condicionais, precisamos saber comparar valores. O resultado de uma comparação é sempre `true` ou `false`.

| Operador | Significado | Exemplo | Resultado |
|----------|-------------|---------|-----------|
| `==` | Igual a | `5 == 5` | `true` |
| `!=` | Diferente de | `5 != 3` | `true` |
| `>` | Maior que | `7 > 3` | `true` |
| `<` | Menor que | `2 < 1` | `false` |
| `>=` | Maior ou igual | `5 >= 5` | `true` |
| `<=` | Menor ou igual | `4 <= 3` | `false` |

> Não confunda `=` (atribuição) com `==` (comparação)! Usar `=` dentro de uma condição é um erro clássico.

---

## Operadores Lógicos

Usados para **combinar** duas ou mais condições.

| Operador | Significado | Resultado |
|----------|-------------|-----------|
| `&&` | E (AND) — ambas verdadeiras | `true` só se as duas forem `true` |
| `\|\|` | OU (OR) — ao menos uma verdadeira | `true` se pelo menos uma for `true` |
| `!` | NÃO (NOT) — inverte o valor | `!true` → `false` |

```cpp
int idade = 20;
bool temCNH = true;

// && : as duas condições precisam ser verdadeiras
if (idade >= 18 && temCNH) {
    std::cout << "Pode dirigir." << std::endl;
}

// || : basta uma ser verdadeira
bool temIngresso = false;
bool estaNaLista = true;

if (temIngresso || estaNaLista) {
    std::cout << "Pode entrar." << std::endl;
}

// ! : inverte a condição
bool chovendo = false;

if (!chovendo) {
    std::cout << "Pode sair sem guarda-chuva." << std::endl;
}
```

---

## `if` / `else if` / `else`

A estrutura mais fundamental para tomada de decisão.

### Sintaxe

```cpp
if (condicao) {
    // executado se a condição for true
} else if (outra_condicao) {
    // executado se a condição anterior for false e esta for true
} else {
    // executado se nenhuma condição anterior for true
}
```

### Exemplo — Classificação de notas

```cpp
#include <iostream>

int main() {
    double nota;
    std::cout << "Digite sua nota: ";
    std::cin >> nota;

    if (nota >= 9.0) {
        std::cout << "Conceito A" << std::endl;
    } else if (nota >= 7.0) {
        std::cout << "Conceito B" << std::endl;
    } else if (nota >= 5.0) {
        std::cout << "Conceito C" << std::endl;
    } else {
        std::cout << "Reprovado" << std::endl;
    }

    return 0;
}
```

**Saída (para nota = 8.5):**
```
Conceito B
```

> O C++ avalia as condições **de cima para baixo** e executa apenas o primeiro bloco cuja condição for verdadeira. Os demais são ignorados.

---

### `if` sem chaves
laços de repetição
Se o bloco tiver apenas **uma linha**, as chaves são opcionais. Porém, usá-las é uma boa prática para evitar erros.

```cpp
// Válido, mas não recomendado para iniciantes:
if (x > 0)
    std::cout << "Positivo" << std::endl;

// Preferível, sempre use chaves:
if (x > 0) {
    std::cout << "Positivo" << std::endl;
}
```

---

## `switch`

O `switch` é uma alternativa ao `if/else if` quando se deseja comparar uma variável a **múltiplos valores fixos** (inteiros ou caracteres).

### Sintaxe

```cpp
switch (variavel) {
    case valor1:
        // código
        break;
    case valor2:
        // código
        break;
    default:
        // executado se nenhum case corresponder
        break;
}
```

> O `break` é essencial! Sem ele, a execução "cai" para o próximo `case` (comportamento chamado de *fall-through*).

### Exemplo — Dia da semana

```cpp
#include <iostream>

int main() {
    int dia;
    std::cout << "Digite o número do dia (1 a 7): ";
    std::cin >> dia;

    switch (dia) {
        case 1:
            std::cout << "Domingo" << std::endl;
            break;
        case 2:
            std::cout << "Segunda-feira" << std::endl;
            break;
        case 3:
            std::cout << "Terça-feira" << std::endl;
            break;
        case 4:
            std::cout << "Quarta-feira" << std::endl;
            break;
        case 5:
            std::cout << "Quinta-feira" << std::endl;
            break;
        case 6:
            std::cout << "Sexta-feira" << std::endl;
            break;
        case 7:
            std::cout << "Sábado" << std::endl;
            break;
        default:
            std::cout << "Dia inválido." << std::endl;
            break;
    }

    return 0;
}
```

### *Fall-through* intencional

Às vezes o *fall-through* é útil — quando vários `case`s devem executar o mesmo código:

```cpp
switch (dia) {
    case 1: // Domingo
    case 7: // Sábado
        std::cout << "Final de semana!" << std::endl; //Tanto o case 1 quanto o case 7 vão executar essa parte do código
        break;
    default:
        std::cout << "Dia útil." << std::endl;
        break;
}
```

---

## Operador Ternário

Uma forma compacta de escrever um `if/else` simples em uma única linha.

### Sintaxe

```cpp
variavel = (condicao) ? valor_se_true : valor_se_false;
```

### Exemplo

```cpp
int idade = 20;
std::string status = (idade >= 18) ? "maior de idade" : "menor de idade";
std::cout << "Você é " << status << "." << std::endl;
```

É equivalente a:

```cpp
std::string status;
if (idade >= 18) {
    status = "maior de idade";
} else {
    status = "menor de idade";
}
```

> Use o operador ternário com moderação, ele é ótimo para casos simples, mas pode prejudicar a legibilidade quando a lógica é mais complexa.

---

## Exemplo Completo

```cpp
#include <iostream>
#include <string>

int main() {
    double salario;
    int dependentes;

    std::cout << "Digite seu salário: ";
    std::cin >> salario;

    std::cout << "Digite o número de dependentes: ";
    std::cin >> dependentes;

    double aliquota;

    if (salario <= 2000.0) {
        aliquota = 0.0;
    } else if (salario <= 4000.0) {
        aliquota = 0.075;
    } else if (salario <= 8000.0) {
        aliquota = 0.15;
    } else {
        aliquota = 0.275;
    }

    double desconto = salario * aliquota;
    double deducaoDependentes = dependentes * 189.59;
    double impostoFinal = desconto - deducaoDependentes;

    if (impostoFinal < 0.0) {
        impostoFinal = 0.0;
    }

    std::string faixa = (aliquota == 0.0) ? "Isento" : "Tributável";

    std::cout << "\n--- Resumo ---" << std::endl;
    std::cout << "Situação: "      << faixa        << std::endl;
    std::cout << "Alíquota: "      << aliquota * 100 << "%" << std::endl;
    std::cout << "Imposto final: R$" << impostoFinal << std::endl;

    return 0;
}
```

---

## Resumo rápido

| Conceito | Quando usar |
|----------|-------------|
| `if / else` | Condição simples com dois caminhos |
| `if / else if / else` | Múltiplas condições encadeadas |
| `switch` | Comparar uma variável a vários valores fixos |
| Operador ternário `? :` | Atribuição condicional simples em uma linha |
| `&&` | Todas as condições precisam ser verdadeiras |
| `\|\|` | Basta uma condição ser verdadeira |
| `!` | Inverter o resultado de uma condição |

---

## Referências

- [cppreference.com — if statement](https://en.cppreference.com/w/cpp/language/if)
- [cppreference.com — switch statement](https://en.cppreference.com/w/cpp/language/switch)
- [LearnCpp.com — Condicionais](https://www.learncpp.com/cpp-tutorial/conditional-statements/)