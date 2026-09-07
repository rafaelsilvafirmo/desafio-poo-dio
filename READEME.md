# ☕ Desafio POO DIO — Bootcamp em Java

[![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)](https://www.java.com/)
[![Programação Orientada a Objetos](https://img.shields.io/badge/POO-Orientação%20a%20Objetos-6DB33F?style=for-the-badge)](https://www.dio.me/)
[![DIO](https://img.shields.io/badge/DIO-Desafio%20de%20Projeto-8A2BE2?style=for-the-badge)](https://www.dio.me/)

Projeto desenvolvido como parte de um **desafio de projeto da Digital Innovation One (DIO)**, com foco na aplicação prática dos principais conceitos de **Programação Orientada a Objetos (POO) em Java**.

A aplicação modela, de forma simplificada, uma plataforma de **Bootcamp**, representando cursos, mentorias, desenvolvedores, conteúdos e a progressão dos participantes.

---

## 📌 Sobre o projeto

O projeto consiste na criação de um pequeno domínio de negócio para representar um **Bootcamp de desenvolvimento de software**.

A aplicação permite:

- Criar cursos e mentorias;
- Associar conteúdos a um Bootcamp;
- Inscrever desenvolvedores em um Bootcamp;
- Controlar conteúdos inscritos;
- Registrar conteúdos concluídos;
- Calcular a experiência (XP) obtida pelos desenvolvedores;
- Trabalhar com diferentes tipos de conteúdo por meio de herança e polimorfismo.

O projeto foi desenvolvido com foco na compreensão da **modelagem de objetos e seus relacionamentos**, utilizando recursos nativos da linguagem Java.

---

## 🎯 Objetivos de aprendizagem

Durante a implementação, foram praticados conceitos fundamentais de Java e Programação Orientada a Objetos, entre eles:

- Classes e objetos;
- Abstração;
- Encapsulamento;
- Herança;
- Polimorfismo;
- Classes abstratas;
- Sobrescrita de métodos;
- Coleções da Java Collections Framework;
- `Set`;
- `LinkedHashSet`;
- `Optional`;
- `Iterator`;
- `LocalDate`;
- Manipulação e relacionamento entre objetos.

---

## 🧩 Modelagem do domínio

A estrutura principal do projeto é composta pelas seguintes entidades:

```text
                         ┌──────────────────────┐
                         │       Conteudo       │
                         │      <<abstract>>    │
                         ├──────────────────────┤
                         │ - titulo             │
                         │ - descricao          │
                         ├──────────────────────┤
                         │ + calcularXp()       │
                         └──────────┬───────────┘
                                    │
                         ┌──────────┴───────────┐
                         │                      │
              ┌──────────▼─────────┐  ┌─────────▼──────────┐
              │       Curso        │  │      Mentoria      │
              ├────────────────────┤  ├────────────────────┤
              │ - cargaHoraria     │  │ - data             │
              ├────────────────────┤  ├────────────────────┤
              │ + calcularXp()     │  │ + calcularXp()     │
              └────────────────────┘  └────────────────────┘


              ┌────────────────────┐
              │      Bootcamp      │
              ├────────────────────┤
              │ - nome             │
              │ - descricao        │
              │ - dataInicial      │
              │ - dataFinal        │
              │ - conteudos        │
              │ - devsInscritos    │
              └─────────┬──────────┘
                        │
                        │ contém
                        ▼
              ┌────────────────────┐
              │      Conteudo      │
              └────────────────────┘


              ┌─────────────────────────┐
              │           Dev           │
              ├─────────────────────────┤
              │ - nome                  │
              │ - conteudosInscritos    │
              │ - conteudosConcluidos   │
              ├─────────────────────────┤
              │ + inscreverBootcamp()   │
              │ + progredir()           │
              │ + calcularTotalXp()     │
              └─────────────────────────┘
```

---

## 🏗️ Estrutura do projeto

```text
desafio-poo-dio/
│
├── .vscode/
│
├── bin/
│
├── src/
│   ├── Main.java
│   │
│   └── br/
│       └── com/
│           └── dio/
│               └── desafio/
│                   └── dominio/
│                       ├── Bootcamp.java
│                       ├── Conteudo.java
│                       ├── Curso.java
│                       ├── Dev.java
│                       └── Mentoria.java
│
├── .gitignore
└── README.md
```

---

## 📚 Classes principais

### `Conteudo`

`Conteudo` é uma classe abstrata utilizada como base para os diferentes tipos de conteúdo existentes no Bootcamp.

Ela concentra atributos e comportamentos comuns, enquanto deixa a implementação do cálculo de XP para as classes especializadas.

```java
public abstract class Conteudo {
    private String titulo;
    private String descricao;

    public abstract double calcularXp();
}
```

---

### `Curso`

`Curso` é uma especialização de `Conteudo`.

Além dos atributos herdados, possui uma carga horária utilizada no cálculo de XP.

Exemplo de utilização no projeto:

```java
Curso curso1 = new Curso();
curso1.setTitulo("curso java");
curso1.setDescricao("descrição curso java");
curso1.setCargaHoraria(8);
```

Outro curso é criado para demonstrar que diferentes objetos podem compartilhar a mesma abstração:

```java
Curso curso2 = new Curso();
curso2.setTitulo("curso js");
curso2.setDescricao("descrição curso js");
curso2.setCargaHoraria(4);
```

---

### `Mentoria`

`Mentoria` também herda de `Conteudo`, mas possui uma data associada.

No programa principal, a data é definida utilizando `LocalDate`:

```java
Mentoria mentoria = new Mentoria();

mentoria.setTitulo("mentoria java");
mentoria.setDescricao("descrição mentoria java");
mentoria.setData(LocalDate.now());
```

---

### `Bootcamp`

`Bootcamp` representa o programa de formação.

No `Main`, são definidos seu nome e sua descrição e, posteriormente, os conteúdos são adicionados ao Bootcamp:

```java
Bootcamp bootcamp = new Bootcamp();

bootcamp.setNome("Bootcamp Java");
bootcamp.setDescricao("Bootcamp Java Developer");

bootcamp.getConteudos().add(curso1);
bootcamp.getConteudos().add(curso2);
bootcamp.getConteudos().add(mentoria);
```

O Bootcamp mantém os conteúdos disponíveis e os desenvolvedores inscritos.

---

### `Dev`

`Dev` representa um desenvolvedor participante do Bootcamp.

O desenvolvedor pode:

- Se inscrever em um Bootcamp;
- Consultar seus conteúdos inscritos;
- Progredir nos conteúdos;
- Consultar conteúdos concluídos;
- Calcular o XP acumulado.

Exemplo:

```java
Dev devFulano = new Dev();

devFulano.setNome("Fulano de Tal");
devFulano.inscreverBootcamp(bootcamp);
```

A progressão é simulada utilizando:

```java
devFulano.progredir();
devFulano.progredir();
```

E o XP total pode ser obtido com:

```java
devFulano.calcularTotalXp();
```

---

## 🧠 Conceitos de POO aplicados

### 1. Abstração

A classe `Conteudo` representa uma abstração para diferentes tipos de conteúdo.

Em vez de criar uma estrutura completamente independente para cada tipo, os elementos comuns são concentrados em uma classe base:

```java
public abstract class Conteudo
```

Isso permite que `Curso` e `Mentoria` compartilhem uma mesma estrutura conceitual.

---

### 2. Encapsulamento

Os atributos das classes são encapsulados utilizando modificadores de acesso, principalmente `private`.

O acesso e a alteração dos dados são realizados por meio de métodos, como:

```java
getTitulo()
setTitulo()
getDescricao()
setDescricao()
```

Isso ajuda a controlar o acesso ao estado interno dos objetos.

---

### 3. Herança

`Curso` e `Mentoria` são especializações de `Conteudo`.

A relação pode ser representada por:

```text
Conteudo
   ▲
   │
   ├── Curso
   │
   └── Mentoria
```

Na implementação:

```java
public class Curso extends Conteudo
```

e:

```java
public class Mentoria extends Conteudo
```

---

### 4. Polimorfismo

O método:

```java
calcularXp()
```

é definido na classe abstrata `Conteudo` e implementado pelas classes especializadas.

Isso permite que diferentes tipos de conteúdo apresentem comportamentos específicos mantendo uma interface comum.

---

## 🔄 Fluxo da aplicação

O fluxo demonstrado na classe `Main` pode ser resumido da seguinte maneira:

```text
1. Criar cursos
        │
        ▼
2. Criar mentoria
        │
        ▼
3. Criar Bootcamp
        │
        ▼
4. Adicionar conteúdos ao Bootcamp
        │
        ▼
5. Criar desenvolvedor
        │
        ▼
6. Inscrever desenvolvedor
        │
        ▼
7. Consultar conteúdos inscritos
        │
        ▼
8. Progredir nos conteúdos
        │
        ▼
9. Consultar conteúdos concluídos
        │
        ▼
10. Calcular XP
```

---

## 💻 Exemplo de execução

A classe `Main` cria dois desenvolvedores e simula diferentes níveis de progressão.

### Desenvolvedor 1

O primeiro desenvolvedor é inscrito no Bootcamp e conclui dois conteúdos:

```java
Dev devFulano = new Dev();
devFulano.setNome("Fulano de Tal");

devFulano.inscreverBootcamp(bootcamp);

devFulano.progredir();
devFulano.progredir();
```

Depois são exibidos:

```java
devFulano.getConteudosInscritos();
devFulano.getConteudosConcluidos();
devFulano.calcularTotalXp();
```

### Desenvolvedor 2

O segundo desenvolvedor também é inscrito no Bootcamp, mas conclui três conteúdos:

```java
Dev devCiclano = new Dev();
devCiclano.setNome("Ciclano de Tal");

devCiclano.inscreverBootcamp(bootcamp);

devCiclano.progredir();
devCiclano.progredir();
devCiclano.progredir();
```

Isso demonstra como diferentes objetos da mesma classe podem apresentar estados e resultados diferentes durante a execução.

---

## 🛠️ Tecnologias e recursos utilizados

![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)

- **Java**
- **Programação Orientada a Objetos**
- **Java Collections Framework**
- **`Set` / `LinkedHashSet`**
- **`Optional`**
- **`Iterator`**
- **`LocalDate`**
- **Git**
- **GitHub**

---

## ▶️ Como executar

### Pré-requisitos

Para executar o projeto, tenha instalado:

- Java JDK;
- Git;
- Uma IDE ou editor com suporte a Java.

### 1. Clone o repositório

```bash
git clone https://github.com/rafaelsilvafirmo/desafio-poo-dio.git
```

### 2. Acesse o diretório

```bash
cd desafio-poo-dio
```

### 3. Execute o projeto

Abra o projeto em sua IDE e execute a classe:

```text
src/Main.java
```

Também é possível compilar e executar o projeto diretamente utilizando o JDK.

---

## 📈 Principais aprendizados

Este projeto contribuiu para consolidar conhecimentos importantes para o desenvolvimento em Java, principalmente:

- Modelagem de um domínio utilizando classes;
- Criação e manipulação de objetos;
- Definição de responsabilidades;
- Relacionamento entre objetos;
- Abstração de comportamentos comuns;
- Encapsulamento do estado dos objetos;
- Reutilização por meio de herança;
- Polimorfismo através de métodos sobrescritos;
- Manipulação de coleções;
- Utilização da API de datas do Java;
- Organização de um projeto Java;
- Versionamento do código utilizando Git e GitHub.

---

## 🚀 Possíveis evoluções

O projeto pode ser utilizado como base para estudos e evoluções futuras.

Algumas possibilidades:

- [ ] Adicionar testes unitários com JUnit;
- [ ] Implementar tratamento de exceções;
- [ ] Adicionar validações aos objetos;
- [ ] Criar persistência de dados;
- [ ] Integrar um banco de dados;
- [ ] Criar uma API REST com Spring Boot;
- [ ] Implementar uma arquitetura em camadas;
- [ ] Criar DTOs;
- [ ] Adicionar documentação da API;
- [ ] Criar uma interface web para interação com o sistema.

---

## 🎓 Contexto do desafio

Este projeto foi desenvolvido como parte da jornada de aprendizagem da **Digital Innovation One (DIO)**, com o objetivo de aplicar conceitos de **Programação Orientada a Objetos em Java** em um cenário prático.

Mais do que implementar classes isoladamente, o desafio permite exercitar a capacidade de identificar entidades, seus atributos, comportamentos e relacionamentos dentro de um domínio.

---

## 📂 Repositório

🔗 **GitHub:**  
https://github.com/rafaelsilvafirmo/desafio-poo-dio

---

## 👨‍💻 Autor

**Rafael Silva Firmo**

Estudante de **Análise e Desenvolvimento de Sistemas**, com foco em desenvolvimento de software, Java e backend.

[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/rafaelsilvafirmo)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/rafael-silva-firmo/)

---

## 📄 Licença

Este projeto foi desenvolvido para fins educacionais como parte da jornada de estudos em **Java e Programação Orientada a Objetos**.
