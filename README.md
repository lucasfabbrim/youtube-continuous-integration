# Java CI - Build and Test

Este repositório utiliza **GitHub Actions** para automatizar a compilação e execução de testes do projeto Java sempre que houver um **Pull Request** para a branch `main`.

## 📌 Como funciona este workflow?

O workflow está definido no arquivo `.github/workflows/continuous-integration.yml`. Ele é ativado automaticamente quando um **Pull Request** é criado para a branch `main`.

Ele executa as seguintes etapas:

### **1️⃣ Checkout do código**
Faz o download do repositório para o runner do GitHub Actions.
```yaml
- name: Checkout code
  uses: actions/checkout@v4
```

### **2️⃣ Configuração do JDK 17**
Baixa e configura o **Java Development Kit (JDK) 17** usando a distribuição **Temurin**.
```yaml
- name: Set up JDK 17
  uses: actions/setup-java@v4
  with:
    distribution: 'temurin'  # Eclipse Temurin (ex-Adoptium)
    java-version: '17'
    cache: 'maven'  # Habilita cache para dependências Maven
```

### **3️⃣ Construção e Testes com Maven**
Executa os testes automatizados do projeto usando o **Maven**.
```yaml
- name: Build and test with Maven
  run: mvn clean test
```

---

## 📂 Estrutura do Workflow
```yaml
name: Java CI - Build and Test

on:
  pull_request:
    branches: [ main ]

jobs:
  build:
    name: Build and Test with Maven
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4
      
      - name: Set up JDK 17
        uses: actions/setup-java@v4
        with:
          distribution: 'temurin'
          java-version: '17'
          cache: 'maven'

      - name: Build and test with Maven
        run: mvn clean test
```

