# Modelagem Conceitual de Banco de Dados

## 📚 Bem-vindo à Aula de Modelagem de Banco de Dados!

Esta aula aborda os fundamentos essenciais da **modelagem conceitual de banco de dados**, um tema crucial para profissionais que trabalham com sistemas de informação, desenvolvimento de software e gestão de dados.

---

## 🎯 Objetivos da Aula (50 minutos)

Ao final desta aula, você será capaz de:

- ✅ Compreender o conceito e a importância da **modelagem conceitual**
- ✅ Identificar e caracterizar **entidades** em um banco de dados
- ✅ Reconhecer diferentes tipos de **atributos** e suas propriedades
- ✅ Mapear **relacionamentos** entre entidades
- ✅ Aplicar regras de **cardinalidade** em diagramas ER
- ✅ Analisar casos práticos de modelos conceituais

---

## 📖 Conteúdo Programático

### **Bloco 1: Conceitos Fundamentais (5 minutos)**

#### O que é Modelagem Conceitual?
A modelagem conceitual é a representação abstrata de como os dados estão organizados e relacionados em um banco de dados. Ela independe de qualquer sistema gerenciador de banco de dados (SGBD) específico.

**Importância:**
- Facilita a comunicação entre desenvolvedores e stakeholders
- Reduz inconsistências nos dados
- Previne problemas de design de banco de dados
- Documenta a estrutura lógica do sistema

#### Níveis de Abstração
```
┌─────────────────────────────────────┐
│ 1. MODELO CONCEITUAL (este nível)   │
│    Independente de implementação     │
├─────────────────────────────────────┤
│ 2. MODELO LÓGICO                    │
│    Estrutura de dados específica     │
├─────────────────────────────────────┤
│ 3. MODELO FÍSICO                    │
│    Implementação no SGBD             │
└─────────────────────────────────────┘
```

---

### **Bloco 2: Entidades (10 minutos)**

#### Definição
Uma **entidade** é um objeto do mundo real ou conceitual que queremos modelar e do qual desejamos armazenar informações.

#### Características das Entidades
- Representam coisas tangíveis (pessoas, produtos) ou abstratas (projetos, contratos)
- Possuem existência própria e distinguível
- São representadas por **retângulos** nos diagramas ER
- Cada entidade tem múltiplas instâncias (ocorrências)

#### Tipos de Entidades

| Tipo | Descrição | Exemplo |
|------|-----------|---------|
| **Forte** | Existe independentemente de outras | Departamento, Fornecedor |
| **Fraca** | Depende de outra entidade para existir | Dependente (depende de Empregado) |

#### Exemplo Prático - Caso de Uso: Gestão de Pessoal

```
┌─────────────────────────────────────┐
│        ENTIDADES DO SISTEMA         │
├─────────────────────────────────────┤
│ • contrato                          │
│ • empregado                         │
│ • departamento                      │
│ • dependente                        │
│ • fornecedores                      │
└─────────────────────────────────────┘
```

**Análise das Entidades:**

| Entidade | Tipo | Descrição |
|----------|------|-----------|
| **contrato** | Forte | Registra informações de contratos de trabalho |
| **empregado** | Forte | Dados dos colaboradores da organização |
| **departamento** | Forte | Estrutura organizacional da empresa |
| **dependente** | Fraca | Dependentes de cada empregado |
| **fornecedores** | Forte | Fornecedores de serviços/produtos |

---

### **Bloco 3: Atributos (10 minutos)**

#### Definição
**Atributos** são propriedades ou características que descrevem uma entidade.

#### Tipos de Atributos

##### 1. **Atributo Identificador (Chave Primária) - PK**
- Identifica unicamente cada ocorrência da entidade
- Representado com símbolo de chave (🔑) ou sublinhado
- Não pode ser nulo
- **Exemplo:** `cod_contrato`, `cod_emp_INT`, `cod_depto_INT`

##### 2. **Atributos Simples/Atômicos**
- Possuem um único valor
- Não podem ser decompostos
- **Exemplo:** `tipo VARCHAR(45)`, `sexo CHAR(1)`, `salario DECIMAL(10,2)`

##### 3. **Atributos Compostos**
- Podem ser decompostos em sub-atributos
- **Exemplo:** `endereco` (rua + número + bairro + cidade)
- **Exemplo:** `nome_completo` (nome + sobrenome)

##### 4. **Atributos Multivalorados**
- Podem possuir múltiplos valores para uma mesma instância
- Representados com linhas duplas no diagrama ER
- **Exemplo:** `telefone` (um empregado pode ter vários telefones)
- **Exemplo:** `email` (múltiplos emails)

##### 5. **Atributos Derivados/Calculados**
- Seu valor é calculado a partir de outros atributos
- Representados com linhas tracejadas
- Não são armazenados no banco (apenas calculados)
- **Exemplo:** `idade` (calculada a partir de data_nascimento)
- **Exemplo:** `tempo_empresa` (calculado de data_admissao)

##### 6. **Atributos de Relacionamento**
- Atributos que pertencem a um relacionamento, não a uma entidade
- Surgem especialmente em relacionamentos N:M

#### Exemplo de Atributos - Entidade "empregado"

```
empregado
├── 🔑 cod_emp (INT) - Identificador único
├── cod_depto (INT) - FK para departamento
├── nome (VARCHAR 50) - Atributo simples
├── sexo (CHAR 1) - Atributo simples
├── dt_nascimento (DATE) - Atributo simples
├── dt_admissao (DATE) - Atributo simples
├── civil (CHAR 1) - Atributo simples
├── salario (DECIMAL 10,2) - Atributo numérico
└── [Índices]
    ├── PRIMARY (cod_emp)
    └── UNIQUE (cod_emp)
```

#### Exemplo de Atributos - Entidade "departamento"

```
departamento
├── 🔑 cod_depto (INT) - Identificador único
├── nome (VARCHAR 50) - Atributo simples
└── [Índices]
    ├── PRIMARY (cod_depto)
    └── UNIQUE (cod_depto)
```

---

### **Bloco 4: Relacionamentos (10 minutos)**

#### Definição
Um **relacionamento** descreve como duas ou mais entidades se conectam e interagem.

#### Características
- Representados por **losangos** ou **conectores** nos diagramas ER
- Indicam associações entre entidades
- Possuem um **nome** que descreve a relação
- Podem ter **atributos próprios** (atributos de relacionamento)
- Possuem **grau** (número de entidades envolvidas)

#### Tipos de Relacionamentos

##### 1. **Relacionamento Um-para-Um (1:1)**
- Uma instância de A se relaciona com exatamente uma instância de B
- Raro em modelos reais
- **Exemplo:** Um empregado tem um contrato de trabalho

```
empregado (1) ──────────── (1) contrato
   |                           |
   └─── cada empregado tem ────┘
        exatamente um contrato
```

##### 2. **Relacionamento Um-para-Muitos (1:N)**
- Uma instância de A se relaciona com múltiplas instâncias de B
- Mais comum em modelos de dados
- **Exemplo:** Um departamento tem muitos empregados

```
departamento (1) ──────────── (N) empregado
      |                            |
      └── um departamento ────────┘
          pode ter vários
          empregados
```

##### 3. **Relacionamento Muitos-para-Muitos (N:M)**
- Múltiplas instâncias de A se relacionam com múltiplas instâncias de B
- Requer uma entidade intermediária (tabela de junção)
- **Exemplo:** Fornecedores fornecem produtos; produtos são fornecidos por múltiplos fornecedores

```
departamento (N) ──────────── (N) fornecedor
        |                           |
        └─ múltiplos depts ────────┘
           trabalham com
           múltiplos fornecedores
```

#### Exemplos do Caso Prático

| Entidades | Tipo | Cardinalidade | Descrição |
|-----------|------|---------------|-----------|
| **departamento ↔ empregado** | Funcional | 1:N | Um departamento tem vários empregados |
| **empregado ↔ dependente** | Funcional | 1:N | Um empregado tem vários dependentes |
| **empregado ↔ contrato** | Funcional | 1:1 | Um empregado tem um contrato |
| **departamento ↔ fornecedores** | Multivalorado | N:M | Um departamento trabalha com múltiplos fornecedores |

---

### **Bloco 5: Cardinalidade (7 minutos)**

#### Definição
**Cardinalidade** especifica quantas instâncias de uma entidade podem estar relacionadas com uma instância da outra entidade. Expressa as restrições de participação em um relacionamento.

#### Notações de Cardinalidade

##### Notação Chen (Mín, Máx)
```
(mín, máx) onde:
  mín = participação mínima (0 ou 1)
  máx = participação máxima (1 ou N)

Exemplos:
(0,1) - Zero ou um
(1,1) - Exatamente um
(0,N) - Zero ou mais
(1,N) - Um ou mais
```

##### Notação Crow's Foot (Pé de Corvo)
```
───── = Exatamente Um (1)
─○─ = Zero ou Um (0,1)
─<─ = Muitos (N)
─<○ = Zero ou Muitos (0,N)
```

#### Exemplos Práticos

**Exemplo 1: Departamento → Empregado**
```
departamento (1) ──────── (N) empregado
                ou
departamento (1,N) ──── (0,N) empregado

Significado:
- Um departamento TEM um ou mais empregados (1,N)
- Um empregado TRABALHA EM um departamento (0,N)
```

**Exemplo 2: Empregado → Dependente**
```
empregado (1) ──0──── (0,N) dependente

Significado:
- Um empregado PODE TER zero ou mais dependentes (0,N)
- Um dependente PERTENCE A um empregado (1,1)
```

**Exemplo 3: Departamento ↔ Fornecedores (N:M)**
```
departamento (N) ──────── (N) fornecedor

Tabela de Junção: fornecedores_para_departamento

Significado:
- Um departamento trabalha com múltiplos fornecedores
- Um fornecedor trabalha com múltiplos departamentos
```

---

## 🔍 Análise do Diagrama ER - Caso Prático

### Diagrama Conceitual Simplificado

```
           departamento ──(1:N)──── empregado ──(1:1)──── contrato
                |                       |
              (N:M)                   (1:N)
                |                       |
        fornecedores          dependente
                |
   fornecedores_para_
   departamento (tabela junção)
```

### Diagrama Conceitual Detalhado (Chen)

```
         ┌─────────────────────┐
         │    departamento     │
         ├─────────────────────┤
         │ 🔑 cod_depto (INT)  │
         │   nome (VARCHAR)    │
         └────────┬────────────┘
                  │ 1:N
                  │
         ┌────────▼────────┐
         │   TRABALHA EM   │◇────────┐
         └────────┬────────┘         │
                  │               (1:N)
                  │                  │
         ┌────────▼────────────────┐
         │     empregado          │
         ├────────────────────────┤
         │ 🔑 cod_emp (INT)       │
         │   nome (VARCHAR 50)    │
         │   sexo (CHAR 1)        │
         │   dt_nascimento (DATE) │
         │   dt_admissao (DATE)   │
         │   civil (CHAR 1)       │
         │   salario (DECIMAL)    │
         │   🗝️ cod_depto (FK)    │
         └────┬────────────┬──────┘
              │ 1:1        │ 1:N
              │            │
         ┌────▼───┐    ┌───▼──────────┐
         │contrato│    │ dependente   │
         ├────────┤    ├──────────────┤
         │🔑codes │    │🔑cod_dep(INT)│
         │tipo    │    │  cod_emp(FK) │
         │conta   │    │  nome (VC)   │
         └────────┘    │  dt_nasc(DT) │
                       │  sexo (CHAR) │
                       └──────────────┘

    ┌──────────────────────────────────────────┐
    │    fornecedores_para_departamento        │
    │           (Tabela de Junção)            │
    ├──────────────────────────────────────────┤
    │ 🔑🗝️ cod_fornecedor (FK)                 │
    │ 🔑🗝️ cod_depto (FK)                      │
    └──────────────────────────────────────────┘
```

### Descrição das Entidades

#### **1. CONTRATO**
- **Chave Primária:** `cod_contrato (INT)`
- **Atributos:**
  - `tipo (VARCHAR 45)` - Tipo de contrato (Efetivo, Temporário, etc.)
  - `conta (VARCHAR 45)` - Informações de conta
- **Relacionamento:** 1 empregado : 1 contrato (relação 1:1)
- **Índices:** PRIMARY KEY, UNIQUE

#### **2. EMPREGADO**
- **Chave Primária:** `cod_emp (INT)`
- **Chave Estrangeira:** `cod_depto (INT)` → referencia departamento
- **Atributos Simples:**
  - `nome (VARCHAR 50)` - Nome completo
  - `sexo (CHAR 1)` - Sexo (M/F)
  - `dt_nascimento (DATE)` - Data de nascimento
  - `dt_admissao (DATE)` - Data de admissão
  - `civil (CHAR 1)` - Estado civil
  - `salario (DECIMAL 10,2)` - Salário base
- **Relacionamentos:**
  - Pertence a 1 departamento (N:1)
  - Pode ter vários dependentes (1:N)
  - Possui 1 contrato (1:1)
- **Índices:** PRIMARY, UNIQUE em cod_emp

#### **3. DEPARTAMENTO**
- **Chave Primária:** `cod_depto (INT)`
- **Atributos:**
  - `nome (VARCHAR 50)` - Nome do departamento
- **Relacionamentos:**
  - Tem vários empregados (1:N)
  - Trabalha com múltiplos fornecedores (N:M via tabela junção)
- **Índices:** PRIMARY, UNIQUE em cod_depto

#### **4. DEPENDENTE (Entidade Fraca)**
- **Chaves:** 
  - `cod_dep (INT)` - Identificador local do dependente
  - `cod_emp (INT)` - Chave estrangeira para empregado (PK parcial)
- **Atributos:**
  - `nome (VARCHAR 50)` - Nome do dependente
  - `dt_nascimento (DATE)` - Data de nascimento
  - `sexo (CHAR 1)` - Sexo
- **Relacionamento:** Depende de 1 empregado (N:1)
- **Índices:** PRIMARY (cod_dep + cod_emp), FOREIGN KEY (cod_emp)

#### **5. FORNECEDORES**
- **Chave Primária:** `cod_fornecedor (INT)`
- **Atributos:**
  - `nome (VARCHAR 45)` - Nome da empresa
  - `cpnj (VARCHAR 45)` - CNPJ
  - `contato (VARCHAR 45)` - Contato principal
  - `email (VARCHAR 45)` - Email
  - `telefone (VARCHAR 14)` - Telefone de contato
- **Relacionamentos:** Trabalha com múltiplos departamentos (N:M)
- **Índices:** PRIMARY KEY

#### **6. FORNECEDORES_PARA_DEPARTAMENTO (Entidade de Junção)**
- **Tipo:** Tabela de junção para relacionamento N:M
- **Chaves Compostas (Primary Key):**
  - `fornecedores_cod_fornecedor (INT)` - FK
  - `departamento_cod_depto (INT)` - FK
- **Propósito:** Relacionar múltiplos fornecedores a múltiplos departamentos
- **Índices:** 
  - PRIMARY KEY (ambas as chaves)
  - FOREIGN KEY → fornecedores
  - FOREIGN KEY → departamento

---

## 📊 Matriz de Cardinalidade do Modelo

| Entidade 1 | Entidade 2 | Tipo | Cardinalidade | Descrição |
|---|---|---|---|---|
| departamento | empregado | Funcional | 1:N | Um departamento agrega vários empregados |
| empregado | contrato | Funcional | 1:1 | Um empregado possui um contrato |
| empregado | dependente | Funcional | 1:N | Um empregado pode ter vários dependentes |
| departamento | fornecedores | Multivalorado | N:M | Múltiplos departamentos trabalham com múltiplos fornecedores |

---

## 💡 Dicas Práticas para Modelagem

1. **Identifique as Entidades:** 
   - Pergunte-se: "Quais são as coisas principais que preciso armazenar?"
   - Procure por substantivos no requisito do sistema

2. **Defina os Atributos:** 
   - Para cada entidade, identifique suas características
   - Certifique-se de ter um identificador único (PK)
   - Sempre pergunte: "Que dados preciso armazenar?"

3. **Estabeleça Relacionamentos:** 
   - Determine como as entidades se conectam
   - Use verbos para nomear relacionamentos (ex: "trabalha em", "possui", "pertence a")

4. **Aplique Cardinalidade:** 
   - Para cada relacionamento, defina quantas instâncias podem estar envolvidas
   - Considere se a participação é obrigatória ou opcional

5. **Valide o Modelo:** 
   - Certifique-se de que ele representa corretamente o domínio do problema
   - Teste com exemplos reais

6. **Documente Decisões:** 
   - Registre o porquê de cada escolha de design
   - Use comentários descritivos

---

## 📚 Referências Bibliográficas

- **Chen, P. P.** (1976). "The Entity-Relationship Model - Toward a Unified View of Data". 
  - *ACM Transactions on Database Systems*, vol. 1, no. 1. 
  - Artigo seminal que introduziu o modelo ER

- **Elmasri, R. & Navathe, S. B.** (2016). *Fundamentals of Database Systems* (7ª ed.). 
  - Pearson Education.
  - Capítulos 3-5: Conceitos de modelagem, ER, e relacionamentos

- **Date, C. J.** (2015). *An Introduction to Database Systems* (12ª ed.). 
  - Addison-Wesley.
  - Capítulos sobre design relacional e modelagem

- **Silberschatz, A., Korth, H. F., & Sudarshan, S.** (2020). *Database System Concepts* (7ª ed.). 
  - McGraw-Hill.
  - Capítulos sobre modelagem conceitual e diagrama ER

- **Teorey, T. J., Lightstone, S. S., Nadeau, T. P., & Jagadish, H. V.** (2011). 
  - *Database Modeling and Design: Logical Design* (5ª ed.). Morgan Kaufmann.

- **Heuser, C. A.** (2009). *Projeto de Banco de Dados* (6ª ed.). 
  - Bookman Editora.
  - Modelagem conceitual e design de BD em português

---

## 🎓 Exercícios Práticos

### Exercício 1: Identificar Entidades
**Cenário:** Modelar um sistema de **gerenciamento de biblioteca**

**Instruções:**
Dado o caso de uma biblioteca, identifique as principais entidades necessárias para gerenciar:
- Livros e seus autores
- Membros que pegam emprestado
- Empréstimos e devoluções

**Solução Esperada:** 
```
Entidades:
- LIVRO
- AUTOR
- MEMBRO (ou LEITOR)
- EMPRÉSTIMO
- GÊNERO (opcional)
- EDITORA (opcional)
```

### Exercício 2: Definir Atributos
**Instruções:**
Para a entidade "LIVRO", defina:
1. Um identificador único (chave primária)
2. Pelo menos 5 atributos relevantes
3. Classifique cada atributo (simples, composto, multivalorado, etc.)

**Solução Esperada:** 
```
LIVRO
├── 🔑 isbn (VARCHAR 20) - Identificador único
├── titulo (VARCHAR 100) - Atributo simples
├── autor (VARCHAR 50) - Atributo simples
├── ano_publicacao (INT) - Atributo simples
├── editora (VARCHAR 50) - Atributo simples
├── categorias (VARCHAR) - Atributo multivalorado
└── data_aquisicao (DATE) - Atributo simples
```

### Exercício 3: Determinar Relacionamentos e Cardinalidade
**Instruções:**
Para o caso da biblioteca, estabeleça:
1. Todos os relacionamentos entre LIVRO, AUTOR e MEMBRO
2. A cardinalidade de cada relacionamento
3. Diagrama visual

**Solução Esperada:**
```
AUTOR (1) ──────── (N) LIVRO
                     |
                   (1,N)
                     |
MEMBRO ────────── EMPRÉSTIMO ────────── LIVRO
                   (atributo de relacionamento)
                   - data_empréstimo
                   - data_devolução
                   - multa

Cardinalidades:
- Um AUTOR escreve MUITOS LIVROS (1:N)
- Um LIVRO é escrito por UM AUTOR
- Um MEMBRO empresta MUITOS LIVROS (1:N - através de EMPRÉSTIMO)
- Um LIVRO pode ser emprestado para MUITOS MEMBROS (N:1 - através de EMPRÉSTIMO)
```

---

## ⏱️ Cronograma da Aula (50 minutos)

| Tempo | Duração | Atividade | Método |
|-------|---------|-----------|--------|
| 0:00 - 0:05 | 5 min | Introdução e contextualizando o tema | Apresentação |
| 0:05 - 0:15 | 10 min | Conceitos Fundamentais e Entidades | Exposição + Exemplos |
| 0:15 - 0:25 | 10 min | Atributos: Tipos e características | Exposição + Discussão |
| 0:25 - 0:35 | 10 min | Relacionamentos | Exposição + Diagramas |
| 0:35 - 0:42 | 7 min | Cardinalidades | Exposição + Exemplos |
| 0:42 - 0:48 | 6 min | Análise do Caso Prático | Análise de Diagrama |
| 0:48 - 0:50 | 2 min | Conclusão e dúvidas | Discussão |

---

## 🚀 Próximos Passos

- [ ] **Normalização de Banco de Dados** - 1FN, 2FN, 3FN, BCNF
- [ ] **Modelagem Lógica** - Transformação do modelo conceitual para relacional
- [ ] **Modelagem Física** - Implementação em SGBD específico (MySQL, PostgreSQL, Oracle)
- [ ] **Banco de Dados Não-Relacionais** - NoSQL, MongoDB, cassandra

---

## 📞 Dúvidas Frequentes

**P: Qual é a diferença entre atributo monovalorado e multivalorado?**
R: Um atributo monovalorado tem um único valor (ex: CPF), enquanto um multivalorado pode ter vários valores para a mesma instância (ex: múltiplos telefones).

**P: O que é uma entidade fraca?**
R: Uma entidade que depende de outra para existir e ser identificada. Exemplo: Dependente depende de Empregado. Sua chave primária inclui parte da chave da entidade forte.

**P: Como represento um atributo derivado?**
R: Com tracejado ao redor do atributo ou especificado explicitamente como "derivado". Exemplo: idade é derivada de data_nascimento.

**P: Quando usar uma tabela de junção (entidade de junção)?**
R: Quando você tem um relacionamento N:M entre duas entidades. A tabela de junção armazena as chaves estrangeiras de ambas as entidades.

---

## 🎓 Conclusão

A modelagem conceitual é a base para um banco de dados bem estruturado. Uma boa compreensão de **entidades**, **atributos**, **relacionamentos** e **cardinalidades** garante:

- ✅ Banco de dados bem organizado e escalável
- ✅ Menos redundância de dados
- ✅ Integridade referencial mantida
- ✅ Fácil manutenção e evolução
- ✅ Melhor performance nas consultas
- ✅ Documentação clara do sistema

---

## 📝 Informações da Aula

- **Título:** Modelagem Conceitual de Banco de Dados
- **Tema:** Entidades, Atributos, Relacionamentos e Cardinalidades
- **Duração:** 50 minutos
- **Disciplina:** Modelagem de Banco de Dados (MATAO 297)
- **Instituição:** victoricoma/mbd_matao_297
- **Data:** 2026-05-02
- **Versão:** 1.0

---

*Última atualização: 2026-05-02*
*Mantenha este material atualizado conforme novas práticas e padrões surgirem.*
