# Modelagem Conceitual de Banco de Dados

## 📚 Aula de 50 Minutos
**Tema:** Modelagem Conceitual de Banco de Dados - Entidades, Atributos, Relacionamentos e Cardinalidades

---

## 📋 Índice
1. [Objetivos da Aula](#objetivos-da-aula)
2. [Conteúdo Programático](#conteúdo-programático)
3. [Conceitos Fundamentais](#conceitos-fundamentais)
4. [Cronograma Sugerido](#cronograma-sugerido)
5. [Exemplos Práticos](#exemplos-práticos)
6. [Referências Bibliográficas](#referências-bibliográficas)

---

## 🎯 Objetivos da Aula

Ao final desta aula, o aluno será capaz de:

- ✅ Compreender o conceito de modelagem conceitual em banco de dados
- ✅ Identificar e descrever **entidades** em um sistema
- ✅ Reconhecer **atributos** e suas características
- ✅ Estabelecer **relacionamentos** entre entidades
- ✅ Determinar **cardinalidades** em relacionamentos
- ✅ Criar diagramas entidade-relacionamento (ER) básicos

---

## 📝 Conteúdo Programático

### 1. Introdução à Modelagem de Dados (5 min)
- O que é modelagem de dados?
- Níveis de abstração: Conceitual, Lógico e Físico
- Importância da modelagem conceitual
- Ferramenta: Diagrama Entidade-Relacionamento (DER)

### 2. Entidades (10 min)
- **Definição:** Objeto do mundo real que desejamos representar
- **Características:** Identificáveis e bem definidas
- **Tipos:**
  - Entidades Fortes: têm existência independente
  - Entidades Fracas: dependem de outras entidades
- **Representação:** Retângulo no DER

**Exemplo:**
```
┌─────────────────────┐
│     ESTUDANTE       │
└─────────────────────┘
```

### 3. Atributos (10 min)
- **Definição:** Propriedades descritivas de uma entidade
- **Tipos de Atributos:**
  - **Simples:** Não divisível (Nome, CPF)
  - **Composto:** Divisível em componentes (Endereço = Rua + Cidade + CEP)
  - **Monovalorado:** Um único valor (Data de Nascimento)
  - **Multivalorado:** Múltiplos valores (Telefones)
  - **Derivado:** Calculado a partir de outros (Idade = Data Atual - Data Nascimento)
  - **Identificador/Chave:** Identifica unicamente a entidade (Matrícula)

**Representação no DER:**
```
              ┌─────────────────────────┐
              │      ESTUDANTE          │
              └─────────────────────────┘
                      |
            ┌─────────┼─────────┐
            |         |         |
       Matrícula    Nome    Data_Nasc
         (PK)
```

- **Notação:**
  - Atributo em circulo: ○
  - Atributo chave: _Sublinhado_
  - Atributo multivalorado: Double oval ◎

### 4. Relacionamentos (15 min)
- **Definição:** Associação entre duas ou mais entidades
- **Características:** Nome, grau, tipo
- **Representação:** Losango no DER

**Exemplo Visual:**
```
┌─────────────┐           ┌──────────────┐
│ ESTUDANTE   │           │   DISCIPLINA │
└─────────────┘           └──────────────┘
      |                          |
      └──────────┬───────────────┘
                 |
            ◇ CURSA ◇
```

**Tipos de Relacionamentos:**
- Relacionamento 1:1 (Um para Um)
- Relacionamento 1:N (Um para Muitos)
- Relacionamento M:N (Muitos para Muitos)

### 5. Cardinalidades (10 min)
- **Definição:** Número mínimo e máximo de ocorrências de uma entidade em um relacionamento
- **Notação:** (mín, máx)

**Exemplos:**

| Tipo | Notação | Significado | Exemplo |
|------|---------|-------------|---------|
| Um para Um | 1:1 | Cada A relaciona com 1 B e vice-versa | Pessoa - CPF |
| Um para Muitos | 1:N | Um A com muitos B | Departamento - Empregado |
| Muitos para Muitos | M:N | Muitos A com muitos B | Estudante - Disciplina |

**Representação de Cardinalidade:**
```
    (1, 1)              (1, N)
      |                   |
┌──────────┐         ┌──────────┐
│   AUTOR  │────────│   LIVRO   │
└──────────┘         └──────────┘

Leitura: Um AUTOR escreve MUITOS LIVROS
         Um LIVRO é escrito por UM AUTOR
```

---

## 💡 Conceitos Fundamentais

### Entidade
Uma "coisa" do mundo real que queremos modelar.
- **Exemplo:** Aluno, Professor, Curso, Disciplina

### Atributo
Uma propriedade de uma entidade.
- **Exemplo:** Nome do aluno, Matrícula, Data de nascimento

### Relacionamento
Uma associação ou ligação entre entidades.
- **Exemplo:** Um aluno "CURSA" uma disciplina

### Cardinalidade
A quantidade de elementos envolvidos no relacionamento.
- **Exemplo:** Um professor ensina 1 ou mais disciplinas (1:N)

### Identificador (Chave Primária)
Um atributo que identifica unicamente uma entidade.
- **Exemplo:** Matrícula do aluno, CPF de uma pessoa

---

## ⏱️ Cronograma Sugerido (50 minutos)

| Tempo | Atividade |
|-------|-----------|
| 0-5 min | Introdução e contextualizando o tema |
| 5-15 min | Entidades: Conceito e exemplos |
| 15-25 min | Atributos: Tipos e características |
| 25-40 min | Relacionamentos e Cardinalidades |
| 40-45 min | Exemplos práticos integrados |
| 45-50 min | Conclusão e dúvidas |

---

## 🔍 Exemplos Práticos

### Exemplo 1: Sistema de Biblioteca

**Entidades:**
- LIVRO
- AUTOR
- MEMBRO (Leitor)

**Atributos:**
- LIVRO: ISBN (PK), Título, Ano Publicação, Editora
- AUTOR: ID_Autor (PK), Nome, Data Nascimento
- MEMBRO: ID_Membro (PK), Nome, Email, Telefone

**Relacionamentos e Cardinalidades:**
```
┌──────────┐                ┌────────┐
│  AUTOR   │──(1,N)──────────(1,N)──│ LIVRO │
└──────────┘                └────────┘
                                  |
                            (1,N) |
                                  |
                            ◇ EMPRESTA ◇
                                  |
                            (0,N) |
                                  |
                            ┌──────────┐
                            │ MEMBRO   │
                            └──────────┘
```

**Leitura:**
- Um AUTOR escreve MUITOS LIVROS
- Um LIVRO é escrito por UM AUTOR
- Um LIVRO é emprestado para MUITOS MEMBROS
- Um MEMBRO empresta MUITOS LIVROS

### Exemplo 2: Sistema Educacional

**Entidades:**
- ESTUDANTE
- DISCIPLINA
- PROFESSOR
- TURMA

**Relacionamentos:**
- ESTUDANTE **CURSA** DISCIPLINA (M:N)
- PROFESSOR **LECIONA** DISCIPLINA (1:N)
- DISCIPLINA **PERTENCE** TURMA (1:N)

---

## 📚 Referências Bibliográficas

1. **Elmasri, R.; Navathe, S. B.** *Sistemas de Banco de Dados*. Editora Pearson. 
   - Capítulos sobre modelagem conceitual e diagrama ER

2. **Date, C. J.** *An Introduction to Database Systems*. Editora Addison-Wesley.
   - Fundamentos de design de banco de dados

3. **Silberschatz, A.; Korth, H. F.; Sudarshan, S.** *Database System Concepts*. Editora McGraw-Hill.
   - Modelagem de dados e normalização

4. **Chen, P. P.** "The Entity-Relationship Model - Toward a Unified View of Data". 
   - ACM Transactions on Database Systems, 1976.
   - Artigo seminal sobre modelagem ER

---

## 🛠️ Atividades Sugeridas

### Atividade 1: Identificar Entidades (5 min)
Dado um cenário (ex: "Farmácia"), identifique as entidades principais.

### Atividade 2: Adicionar Atributos (5 min)
Para cada entidade, liste 3-5 atributos relevantes.

### Atividade 3: Definir Relacionamentos (5 min)
Desenhe as associações entre entidades.

### Atividade 4: Determinar Cardinalidades (5 min)
Para cada relacionamento, determine as cardinalidades.

---

## 📊 Dicas para Criar um Bom Modelo Conceitual

1. **Seja preciso:** Identifique todas as entidades relevantes
2. **Escolha bons nomes:** Use nomes descritivos e no singular
3. **Defina chaves:** Sempre tenha um identificador único
4. **Documente:** Explique escolhas não óbvias
5. **Valide:** Revise o modelo com os stakeholders
6. **Iteração:** Refine o modelo conforme necessário

---

## 📞 Dúvidas Frequentes

**P: Qual é a diferença entre atributo monovalorado e multivalorado?**
R: Monovalorado tem um valor (ex: CPF), multivalorado pode ter vários (ex: telefones).

**P: O que é uma entidade fraca?**
R: Uma entidade que depende de outra para existir (ex: Dependente depende de Empregado).

**P: Como represento um atributo derivado?**
R: Com tracejado ao redor do atributo ou especificado como "derivado".

---

## 🎓 Conclusão

A modelagem conceitual é a base para um banco de dados bem estruturado. Uma boa compreensão de entidades, atributos, relacionamentos e cardinalidades garante:
- ✅ Banco de dados bem organizado
- ✅ Menos redundância de dados
- ✅ Integridade referencial
- ✅ Fácil manutenção e escalabilidade

---

**Autor:** Aula preparada em 2026
**Disciplina:** Modelagem de Banco de Dados (MATAO 297)
**Duração:** 50 minutos
