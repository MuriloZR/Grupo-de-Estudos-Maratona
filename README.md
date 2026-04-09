# Introdução à Programação em C++

Material de apoio das aulas de **Introdução à Programação** para calouros.  
Cada pasta corresponde a uma aula e contém um arquivo de revisão com exemplos práticos.

---

## Conteúdo Programático

| Tópico | Tema | Material |
|------|------|----------|
| 01 | Tipos de variáveis, `std::cin` e `std::cout` | [Tópico 1](./topico1/topico1.md) |
| 02 | Condicionais: `if`, `else`, `switch` | [Tópico 2](./topico2/topico2.md) |
| 03 | Laços de repetição: `for`, `while`, `do while` | [Tópico 3](./topico3/topico3.md) |
| 04 | Vetores: arrays padrões e `std::vector` | [Tópico 4](./topico4/topico4.md) |
| 05 | Complexidade e notação Big O | [Tópico 5](./topico5/topico5.md) |

> Novos Tópicos serão adicionados ao longo do tempo.

**Links para exercícios podem ser encontrados [aqui](./questoes.md)**
> Os links abrem na aba atual do seu navegador, eu recomendo clilar no link do exercício com o botão direito e abrir numa nova aba, pra não ter que ficar voltando para essa paǵina toda hora que quiserem consultar o material novamente

---

## Como usar este repositório

Você pode navegar pelo material de duas formas:

**Pelo GitHub** — clique diretamente nos links da tabela acima para ler as revisões no navegador.

**Clonando localmente** — para ter o material offline:

```bash
git clone https://github.com/MuriloZR/Grupo-de-Estudos-Maratona.git
```

---

## Pré-requisitos

Para compilar e rodar os exemplos de código presentes nas revisões, você precisa de um compilador C++. As opções mais comuns são:

- **g++** (Linux/macOS): geralmente já instalado, ou disponível via gerenciador de pacotes
- **MinGW / g++** (Windows): assista [Como Instalar e Configurar o GCC no Windows](https://youtu.be/daD-X5AQ7e8?si=NjD4ZmXwdPlokS1S)
- **Editores Recomendados**: VS Code, Zed Editor, Neovim, Sublime Text

Para compilar um arquivo `.cpp`:

```bash
g++ nome_do_seu_arquivo.cpp -o nome_do_executavel
./nome_do_executavel
```

---

## Referências Gerais

- [cppreference.com](https://en.cppreference.com/) ou [cplusplus.com](https://cplusplus.com/) — documentação completa da linguagem
- [LearnCpp.com](https://www.learncpp.com/) — tutorial gratuito e completo de C++
- [Geeks for Geeks](https://www.geeksforgeeks.org/) — algoritmos, conceitos, informações gerais
- [Compiler Explorer](https://godbolt.org/) — teste código C++ direto no navegador