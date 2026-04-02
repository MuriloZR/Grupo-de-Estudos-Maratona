# 📊 Aula: Complexidade de Algoritmos (Big-O)

## 🎯 Objetivo da Aula
- Entender o que é complexidade de tempo
- Aprender as principais notações Big-O
- Analisar códigos simples em C++
- Desenvolver intuição para programação competitiva

---

## 🤔 O que é Complexidade?

A **complexidade de tempo** mede **quantas operações** um algoritmo faz em função do tamanho da entrada `n`.

👉 Não medimos tempo em segundos, mas sim crescimento!

---

## 📈 Intuição Inicial

Se dobrarmos o tamanho da entrada:

| Complexidade | Crescimento |
|-------------|------------|
| O(1)        | constante |
| O(log n)    | cresce pouco |
| O(n)        | dobra |
| O(n log n)  | cresce mais |
| O(n²)       | quadruplica 😬 |

---

## 🔢 Principais Complexidades

### 🟢 O(1) — Constante

```cpp
int getFirst(vector<int>& v) {
    return v[0];
}
```

---

### 🔵 O(n) — Linear

```cpp
int sum(vector<int>& v) {
    int s = 0;
    for (int x : v) {
        s += x;
    }
    return s;
}
```

---

### 🟡 O(log n) — Logarítmica

```cpp
int binarySearch(vector<int>& v, int target) {
    int l = 0, r = v.size() - 1;
    while (l <= r) {
        int mid = (l + r) / 2;
        if (v[mid] == target) return mid;
        else if (v[mid] < target) l = mid + 1;
        else r = mid - 1;
    }
    return -1;
}
```

---

### 🟠 O(n log n)

```cpp
vector<int> v = {5, 2, 8, 1};
sort(v.begin(), v.end());
```

---

### 🔴 O(n²) — Quadrática

```cpp
int countPairs(vector<int>& v) {
    int n = v.size();
    int cnt = 0;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cnt++;
        }
    }
    return cnt;
}
```

---

## ⚠️ Regras Importantes

### 1. Ignore constantes

```cpp
for (int i = 0; i < n; i++) {}
for (int i = 0; i < 3*n; i++) {}
```

➡️ O(n)

---

### 2. Pegue o pior caso

```cpp
if (cond) {
    // O(n)
} else {
    // O(n²)
}
```

➡️ O(n²)

---

### 3. Loops aninhados multiplicam

```cpp
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {}
}
```

➡️ O(n²)

---

### 4. Loops sequenciais somam

```cpp
for (int i = 0; i < n; i++) {}
for (int i = 0; i < n; i++) {}
```

➡️ O(n)

---

## 🧠 Truques de Programação Competitiva

### ⏱ Limites comuns

| n máximo | Complexidade aceitável |
|----------|----------------------|
| 10⁶      | O(n) |
| 10⁵      | O(n log n) |
| 10³      | O(n²) |
| 20       | O(2ⁿ) |

---

### 🔍 Exemplo

```cpp
for (int i = 1; i <= n; i *= 2) {}
```

➡️ O(log n)

---

### 🔥 Exemplo clássico

```cpp
for (int i = 0; i < n; i++) {
    for (int j = i; j < n; j++) {}
}
```

➡️ O(n²)

---

## 🧪 Exercícios

### 1
```cpp
for (int i = 0; i < n; i++) {
    cout << i << endl;
}
```

### 2
```cpp
for (int i = 0; i < n; i++) {
    for (int j = 0; j < i; j++) {
        cout << i << j << endl;
    }
}
```

### 3
```cpp
for (int i = 0; i < n; i++) {
    for (int j = 1; j < n; j *= 2) {
        cout << i << j << endl;
    }
}
```

---
