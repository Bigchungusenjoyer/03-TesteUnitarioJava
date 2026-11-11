# 🧪 Laboratório: Testes Unitários e TDD com Java e JUnit

> **Disciplina:** Qualidade de Software  
> **Duração estimada:** 2h  
> **Pré-requisitos:** Conta no GitHub, noções básicas de Java

---

## 📋 Sumário

1. [Objetivos de Aprendizagem](#-objetivos-de-aprendizagem)
2. [Revisão Teórica — Testes Unitários](#-revisão-teórica--testes-unitários)
3. [Revisão Teórica — TDD](#-revisão-teórica--tdd)
4. [Preparação do Ambiente](#️-preparação-do-ambiente)
5. [Estrutura do Repositório](#-estrutura-do-repositório)
6. [Parte 1 — Exemplo do Construtor da Conta Bancária](#-parte-1--exemplo-do-construtor-da-conta-bancária)
7. [Parte 2 — Exercício: Crie os Demais Testes](#-parte-2--exercício-crie-os-demais-testes)
8. [Referência Rápida — JUnit 5](#-referência-rápida--junit-5)
9. [Entregáveis](#-entregáveis)

---

## 🎯 Objetivos de Aprendizagem

Ao final desta atividade, você será capaz de:

- Explicar o que são testes unitários e por que são importantes para a qualidade de software.
- Aplicar o ciclo **Red → Green → Refactor** da metodologia TDD.
- Escrever testes unitários em Java utilizando o framework **JUnit 5** (Jupiter).
- Usar as anotações `@Test` e `@ParameterizedTest` para diferentes cenários de teste.
- Executar testes de forma interativa dentro do VS Code.
- Organizar um projeto de testes seguindo as convenções do ecossistema Java/Maven.

---

## 📖 Revisão Teórica — Testes Unitários

### O que é um Teste Unitário?

Um **teste unitário** é um trecho de código que verifica o comportamento de uma **unidade isolada** do sistema — geralmente um método ou função. O objetivo é garantir que cada parte do código funcione corretamente de forma independente.

### Características de um bom teste unitário

| Característica | Descrição |
|---|---|
| **Rápido** | Executa em milissegundos |
| **Isolado** | Não depende de banco de dados, rede ou outros testes |
| **Repetível** | Produz o mesmo resultado toda vez que é executado |
| **Auto-verificável** | O resultado é "passou" ou "falhou" — sem inspeção manual |
| **Oportuno** | Escrito no momento certo (idealmente antes do código, no TDD) |

> Essas características formam o acrônimo **F.I.R.S.T** (Fast, Isolated, Repeatable, Self-validating, Timely).

### O padrão AAA (Arrange-Act-Assert)

Todo teste unitário segue uma estrutura de três etapas:

```
Arrange  →  Preparar os dados e objetos necessários
Act      →  Executar a ação que será testada
Assert   →  Verificar se o resultado é o esperado
```

Exemplo concreto em Java com JUnit 5:

```java
@Test
void construtor_DadosValidos_CriaContaCorretamente() {
    // Arrange & Act
    var conta = new Conta("Maria", 100);

    // Assert
    assertEquals("Maria", conta.getTitular());
    assertEquals(100, conta.getSaldo());
    assertTrue(conta.isAtiva());
}
```

### Por que escrever testes unitários?

- **Detecção precoce de bugs:** encontra erros antes que cheguem à produção.
- **Documentação viva:** os testes descrevem o comportamento esperado do código.
- **Refatoração segura:** é possível alterar o código com confiança de que nada quebrou.
- **Redução de custo:** quanto mais cedo um defeito é encontrado, mais barato é corrigi-lo.

### Convenções de nomenclatura

Usaremos o padrão `metodo_Cenario_ResultadoEsperado`:

```
construtor_DadosValidos_CriaContaCorretamente
depositar_ValorNegativo_LancaIllegalArgumentException
sacar_SaldoInsuficiente_LancaIllegalStateException
```

Isso torna os relatórios de teste autoexplicativos.

---

## 🔄 Revisão Teórica — TDD

### O que é TDD?

**Test-Driven Development** (Desenvolvimento Guiado por Testes) é uma metodologia onde os testes são escritos **antes** do código de produção. Foi popularizada por Kent Beck como parte das práticas de Extreme Programming (XP).

### O Ciclo Red → Green → Refactor

```
┌──────────────────────────────────────┐
│                                      │
│   🔴 RED                             │
│   Escreva um teste que FALHE         │
│                                      │
│          │                           │
│          ▼                           │
│                                      │
│   🟢 GREEN                           │
│   Escreva o código MÍNIMO para       │
│   o teste PASSAR                     │
│                                      │
│          │                           │
│          ▼                           │
│                                      │
│   🔵 REFACTOR                        │
│   Melhore o código mantendo          │
│   todos os testes passando           │
│                                      │
│          │                           │
│          └──────── ↩ Repita ─────────┘
│
└──────────────────────────────────────┘
```

Detalhando cada etapa:

| Etapa | O que fazer | Tempo |
|---|---|---|
| 🔴 **Red** | Escrever um teste para um comportamento que ainda não existe. O teste deve **falhar**. | 1–3 min |
| 🟢 **Green** | Escrever o código **mínimo** necessário para que o teste passe. Não otimize ainda. | 1–5 min |
| 🔵 **Refactor** | Melhorar a estrutura do código (eliminar duplicação, renomear variáveis, simplificar lógica) sem alterar o comportamento. Todos os testes devem continuar passando. | 1–5 min |

### Benefícios do TDD

- **Design emergente:** o código nasce com responsabilidades claras e interfaces bem definidas.
- **Cobertura de testes alta por padrão:** se todo código nasce de um teste, a cobertura é naturalmente alta.
- **Feedback imediato:** erros são detectados em segundos, não em dias.
- **Confiança ao mudar código:** a suíte de testes funciona como uma rede de segurança.

### TDD NÃO é:

- ❌ Escrever o código e depois os testes (isso é "test-after").
- ❌ Escrever todos os testes de uma vez e depois todo o código.
- ❌ Uma garantia de que o software está livre de bugs (mas reduz muito o risco).

---

## ⚙️ Preparação do Ambiente

### Passo 1 — Fork do repositório

1. Acesse o repositório original no GitHub.
2. Clique no botão **"Fork"** (canto superior direito).
3. Selecione sua conta pessoal como destino.

### Passo 2 — Abrir no GitHub Codespaces

1. No seu fork, clique no botão verde **"<> Code"**.
2. Selecione a aba **"Codespaces"**.
3. Clique em **"Create codespace on main"**.
4. Aguarde o ambiente ser carregado (2–3 minutos na primeira vez).

> 💡 A configuração do repositório usa a imagem de desenvolvimento Java 21 e instala as extensões do VS Code, incluindo o **Test Runner for Java**. A primeira criação do ambiente pode levar alguns minutos.

> ⏱️ Depois que o Codespace abrir, aguarde a importação do projeto Maven/Java terminar antes de usar a view **Testing**.

### Passo 3 — Verificar o ambiente

Abra o terminal integrado (`` Ctrl + ` ``) e, na pasta raiz do repositório, execute:

```bash
java --version
./mvnw test
```

Confirme que `java --version` exibe Java 21.x e que a suíte inicial termina com `BUILD SUCCESS` e **8 testes executados, 0 falhas e 0 erros**. Só comece os passos Red depois desse checkpoint verde. O `pom.xml` exige Java 21; uma versão anterior pode causar `release version 21 not supported`, que é incompatibilidade de ambiente e não Red.

> 💡 O repositório inclui o **Maven Wrapper** (`mvnw`, `mvnw.cmd` e `.mvn/wrapper`). No Codespaces, use `./mvnw`; a criação do ambiente garante a permissão de execução e roda esse checkpoint. Na primeira chamada, o script pode baixar o JAR do Wrapper, a distribuição Maven e as dependências; é necessária conexão com o Maven Central. No estado inicial, `ContaTest` tem seis métodos de teste e executa oito casos por causa do teste parametrizado.

### Diagnóstico: ambiente ou Red?

| Sinal | Interpretação | O que fazer |
|---|---|---|
| `Permission denied` ao executar `./mvnw` | O script não iniciou; ainda não é resultado de teste. | Na raiz, execute `chmod +x mvnw` e tente novamente. |
| `release version 21 not supported` | Maven está usando um JDK anterior ao exigido. | Confira `java --version` e `JAVA_HOME`; selecione JDK 21 e reabra o terminal. |
| Wrapper/dependências não baixam ou há erro de conexão | O build não conseguiu preparar o ambiente. | Verifique a conexão ao Maven Central e tente de novo. |
| `No tests matching pattern` / nenhum teste encontrado | O filtro não corresponde a um teste existente; nenhum comportamento foi exercitado. | Rode `./mvnw test` ou ajuste o filtro após criar o teste. |
| O teste executou e apontou o resultado/comportamento esperado incorreto | O código foi executado, mas o contrato ainda não é atendido. | Antes da implementação ou da próxima mudança, isso pode ser o Red previsto; após Green, investigue implementação ou teste. |
| `UnsupportedOperationException` no método ainda não implementado | Red esperado somente no passo guiado que chama aquele método. | Confirme que é o teste novo previsto; implemente o mínimo e rode-o novamente. |

Uma falha de compilação, de descoberta de testes ou de download não é Red: para contar como Red, o teste precisa executar e demonstrar a falta do comportamento que acabou de ser especificado.

### Passo 4 — Conhecer o Test Explorer

A extensão **Test Runner for Java** permite executar testes de forma visual:

1. Clique no ícone de tubo de ensaio (🧪) na barra lateral esquerda do VS Code.
2. Você verá a árvore de testes organizados por pacote e classe.
3. Clique no botão ▶️ ao lado de um teste para executá-lo individualmente.
4. Use o botão ▶️ no topo para executar todos os testes.

Se a view **Testing** não mostrar os testes depois da importação:

1. Aguarde a importação do projeto Java terminar. Em um Codespace recém-criado, isso pode levar alguns minutos mesmo após o terminal já estar disponível.
2. Verifique se o workspace abriu em modo **Standard** para Java.
3. Abra a Paleta de Comandos e execute **Java: Import Java Projects in Workspace**.
4. Se ainda não aparecer, execute **Java: Clean Java Language Server Workspace** e recarregue a janela.

O workspace já está configurado para abrir em modo **Standard** e importar o Maven automaticamente. A view visual é conveniência; o terminal é a referência para saber se os testes passaram.

> **Falha esperada de TDD não é falha do ambiente:** na Parte 2, o teste novo falha porque o método ainda lança `UnsupportedOperationException`. Erros como compilador incompatível, dependências que não baixam ou falha ao iniciar o Wrapper devem ser resolvidos antes de interpretar o resultado como Red.

Você também pode executar testes pelo terminal:

```bash
# Executar todos os testes
./mvnw test

# Executar com mais detalhes
./mvnw test -Dsurefire.printSummary=true

# Filtrar os testes do construtor, já disponíveis no projeto
./mvnw test -Dtest="ContaTest#construtor*"
```

---

## 📁 Estrutura do Repositório

```
tdd-junit-java/
├── .devcontainer/
│   └── devcontainer.json              ← Configuração do Codespaces
├── .github/workflows/
│   └── java-tests.yml                 ← Testes automáticos com Java 21
├── .mvn/wrapper/
│   └── maven-wrapper.properties       ← Configuração do Maven Wrapper
├── mvnw                               ← Script do Maven Wrapper para Linux/macOS
├── mvnw.cmd                           ← Script do Maven Wrapper para Windows
├── .vscode/
│   └── extensions.json                ← Extensões recomendadas
├── src/
│   ├── main/java/contabancaria/
│   │   └── Conta.java                ← Classe de produção (construtor implementado)
│   └── test/java/contabancaria/
│       └── ContaTest.java             ← Testes (exemplo do construtor + você escreverá o restante)
├── pom.xml                            ← Configuração Maven (dependências e build)
├── .gitignore
└── README.md                          ← Este roteiro
```

---

### Distribuição sugerida do tempo (2 horas)

| Tempo | Etapa e checkpoint |
|---|---|
| 10 min | Preparar o ambiente e obter o checkpoint inicial verde: Java 21 e 8 casos aprovados. |
| 15 min | Revisar AAA, JUnit e os testes do construtor prontos no repositório. |
| 25 min | Fazer os dois ciclos guiados de `depositar`: valor válido e valor zero. |
| 20 min | Testar `sacar`, um cenário por ciclo; conferir saldo preservado nas rejeições. |
| 20 min | Testar `encerrar` e, em seguida, operações numa conta encerrada. |
| 20 min | Testar `transferir` com sucesso, validações e estados preservados nas duas contas. |
| 10 min | Executar a suíte completa, conferir pelo menos 15 casos e preparar a entrega. |

O núcleo obrigatório são os cenários da matriz e todos os checkpoints Red → Green. A extração de validação duplicada é a etapa de refatoração; se o tempo acabar, não pule testes para forçá-la.

## 🟢 Parte 1 — Exemplo do Construtor da Conta Bancária

> **Objetivo:** Entender a estrutura de um teste unitário com JUnit 5 observando os testes já prontos do construtor. O ciclo TDD executável está na Parte 2.

### 1.1 Analisar o código de produção

Abra o arquivo `src/main/java/contabancaria/Conta.java` e observe o construtor da classe `Conta`. Ele já está implementado com as seguintes regras:

- O titular não pode ser nulo ou vazio (lança `IllegalArgumentException`).
- O saldo inicial não pode ser negativo (lança `IllegalArgumentException`).
- A conta é criada como ativa.

Os demais métodos (`depositar`, `sacar`, `transferir`, `encerrar`) ainda **não estão implementados** — lançam `UnsupportedOperationException`. É você quem vai implementá-los usando TDD na Parte 2.

### 1.2 Analisar os testes do construtor

Abra `src/test/java/contabancaria/ContaTest.java` e analise os testes prontos para o Construtor:

- `construtor_DadosValidos_CriaContaCorretamente` — teste básico com `@Test` que verifica titular, saldo e status ativo.
- `construtor_SemSaldoInicial_CriaContaComSaldoZero` — testa o valor padrão do saldo.
- `construtor_TitularNulo_LancaIllegalArgumentException` — testa cenário de exceção.
- `construtor_TitularVazio_LancaIllegalArgumentException` — outro cenário de exceção.
- `construtor_SaldoNegativo_LancaIllegalArgumentException` — valida regra de negócio.
- `construtor_VariosValoresValidos_CriaContaCorretamente` — teste parametrizado com `@ParameterizedTest` e `@CsvSource`.

### 1.3 Executar os testes do construtor

No terminal, execute:

```bash
./mvnw test -Dtest="ContaTest#construtor*"
```

Ou pelo Test Explorer, expanda **ContaTest** e clique ▶️ nos testes de `construtor`.

✅ Todos os testes do construtor devem passar (verde).

### 1.4 Pontos a observar

Analise atentamente os testes do construtor e observe:

- **Padrão AAA:** cada teste segue a estrutura Arrange → Act → Assert.
- `@Test` é usado para testes com valores fixos (sem parâmetros).
- `@ParameterizedTest` + `@CsvSource` permite executar o mesmo teste com valores diferentes.
- `assertThrows(Tipo.class, () -> ...)` verifica que uma exceção específica é lançada.
- **Nomenclatura:** os nomes dos testes seguem `metodo_Cenario_ResultadoEsperado`.
- **Cobertura:** há testes para o caminho feliz, cenários de exceção e casos de borda.

### 1.5 O que este exemplo demonstra (e o que não demonstra)

O construtor e seus testes já estão implementados quando você recebe o repositório. Eles ajudam a reconhecer JUnit, AAA e as regras de validação, mas o estado atual dos arquivos, sozinho, **não comprova a ordem histórica** em que teste e implementação foram escritos. Portanto, não trate o construtor pronto como uma demonstração executável da etapa Red. A Parte 2 apresenta um ciclo pequeno que você executará de fato, começando por `depositar`.

---

## 🏦 Parte 2 — Exercício: Crie os Demais Testes

> **Objetivo:** Praticar ciclos pequenos de TDD para os métodos restantes da classe `Conta`. O código inicial é um esqueleto didático, não uma implementação bancária pronta para uso real.

Agora é a sua vez! Faça um ciclo completo por vez. **Não escreva primeiro todos os testes:** cada pequeno teste deve orientar a próxima mudança de produção.

### Requisitos

Abra `src/main/java/contabancaria/Conta.java` e use o Javadoc de cada método como contrato. A sequência abaixo respeita as dependências entre cenários; não testa comportamento sem regra definida:

| Ordem | Método / cenário | Preparação e ação | Resultado esperado |
|---|---|---|---|
| 1 | `depositar` válido | Conta com saldo 100; depositar 50 | Saldo 150 |
| 1 | `depositar` zero ou negativo | Conta ativa; depositar 0 ou -10 | `IllegalArgumentException`; saldo preservado |
| 2 | `sacar` válido | Saldo 100; sacar 40 | Saldo 60 |
| 2 | `sacar` zero/negativo | Conta ativa; sacar 0 ou -10 | `IllegalArgumentException`; saldo preservado |
| 2 | `sacar` acima do saldo | Saldo 100; sacar 101 | `IllegalStateException`; saldo preservado |
| 3 | `encerrar` com saldo zero | Conta nova; encerrar | `isAtiva()` é `false` |
| 3 | `encerrar` com saldo positivo | Saldo 1; encerrar | `IllegalStateException`; conta continua ativa e saldo preservado |
| 3 | `encerrar` conta inativa | Encerrar duas vezes | Segunda chamada lança `IllegalStateException`; conta permanece inativa |
| 4 | Operação após encerramento | Encerrar conta antes de depositar/sacar | `IllegalStateException`; estado preservado |
| 5 | `transferir` válido | Origem 200, destino 100; transferir 50 | Origem 150 e destino 150 |
| 5 | `transferir` zero/negativo | Duas contas ativas | `IllegalArgumentException`; os dois saldos preservados |
| 5 | `transferir` acima do saldo | Origem 200, destino 100; transferir 201 | `IllegalStateException`; os dois saldos preservados |
| 5 | `transferir` conta inativa | Encerrar origem ou destino antes | `IllegalStateException`; os dois saldos preservados |

Quando uma linha lista alternativas (por exemplo, zero e negativo, ou origem e destino inativos), teste cada caso separadamente ou use `@ParameterizedTest` com uma invocação por entrada. Para toda transferência rejeitada, verifique os saldos de **origem e destino**.

### Instruções

1. Abra `src/test/java/contabancaria/ContaTest.java`. Insira cada novo método dentro de `class ContaTest`, na seção do método correspondente. Os imports de `assertEquals`, `assertThrows` e `assertTrue` já existem. Se usar `assertFalse` para verificar uma conta encerrada, acrescente `import static org.junit.jupiter.api.Assertions.assertFalse;`.
2. Escreva **um comportamento por vez**, execute somente o teste novo e confirme que ele compila e falha pela causa esperada.
3. Em `Conta.java`, substitua apenas o corpo do método sob teste; mantenha a assinatura e não implemente regras futuras antes que um teste as exija.
4. Rode o teste direcionado até obter **Green**. Então rode a suíte completa antes de considerar a etapa concluída.
5. Refatore apenas quando já houver comportamento coberto e uma melhoria estrutural concreta. Rode toda a suíte antes e depois; os resultados devem continuar verdes.
6. Siga a ordem: `depositar` → `sacar` → `encerrar` → testar operações em conta encerrada → `transferir`. Transferência depende de contas ativas/inativas testáveis; prepare uma conta encerrada pelo método público `encerrar()`.

> **Sobre dinheiro:** o exercício usa `double` para manter o foco em testes e contratos. `double` não representa todas as frações decimais exatamente; use a tolerância já adotada nos testes (`assertEquals(esperado, atual, 0.001)`) para saldos fracionários. Em sistemas financeiros reais, prefira uma representação decimal apropriada, como `BigDecimal`; essa migração não faz parte deste exercício.

### Exemplo de como começar — Teste do depositar

Adicione este teste dentro da classe `ContaTest`:

```java
@Test
void depositar_ValorValido_AtualizaSaldo() {
    // Arrange
    var conta = new Conta("Maria", 100);

    // Act
    conta.depositar(50);

    // Assert
    assertEquals(150, conta.getSaldo());
}
```

Execute somente esse cenário:

```bash
./mvnw -Dtest="ContaTest#depositar_ValorValido_AtualizaSaldo" test
```

**🔴 Red esperado:** o teste compila e é executado, mas falha porque a implementação atual de `depositar` lança `UnsupportedOperationException`. Essa falha é intencional: o método é um ponto de partida ainda não implementado. Se o comando não inicia, o teste não compila ou o Java não suporta a versão 21, isso é um problema de ambiente/código e não um Red válido.

#### 🟢 Green — implemente somente o necessário

Substitua o corpo de `depositar` em `Conta.java` por esta implementação mínima para o cenário atual:

```java
public void depositar(double valor) {
    saldo += valor;
}
```

Rode o mesmo comando novamente. O teste deve passar. Ainda não adicione regras que não foram dirigidas por um teste: para o próximo ciclo, escreva primeiro um teste para depósito zero (e depois para valor negativo), confirme que ele falha pelo comportamento, implemente a validação e rode os testes outra vez.

### Segundo ciclo — valor zero (Red por comportamento)

Depois que o teste de depósito válido estiver verde, adicione outro teste na seção `depositar` de `ContaTest`. O teste abaixo falha por uma razão diferente do stub: agora o método executa normalmente, mas o depósito zero ainda não lança a exceção exigida.

```java
@Test
void depositar_ValorZero_LancaIllegalArgumentException() {
    var conta = new Conta("Maria", 100);

    assertThrows(IllegalArgumentException.class, () -> conta.depositar(0));
    assertEquals(100, conta.getSaldo(), 0.001);
}
```

Execute somente esse teste:

```bash
./mvnw -Dtest="ContaTest#depositar_ValorZero_LancaIllegalArgumentException" test
```

**🔴 Red esperado:** o teste é executado e falha porque nenhuma `IllegalArgumentException` é lançada. Não confunda isso com “nenhum teste encontrado”, erro de compilação ou problema de Java/Wrapper: nesses casos, o comportamento sequer foi exercitado.

Para obter **Green**, acrescente ao corpo de `depositar` a validação necessária para este contrato e mantenha a atualização do saldo apenas após ela:

```java
if (valor <= 0) {
    throw new IllegalArgumentException("O valor do depósito deve ser maior que zero.");
}
saldo += valor;
```

Rode o teste de valor zero e o teste de depósito válido. Ambos devem passar; então execute `./mvnw test`. No próximo ciclo, escreva primeiro o teste para valor negativo e só então confirme/implemente esse comportamento. A regra de conta ativa também deve ter seu próprio teste antes de ser adicionada.

#### 🔵 Refactor — preserve o verde

Depois que os testes de valores positivos e não positivos para depósito e saque estiverem verdes, compare as duas validações `valor <= 0`. Se a mesma condição ficou duplicada, extraia-a para um método privado e chame-o nos dois métodos.

Antes da refatoração, cada método pode ter sua própria validação:

```java
if (valor <= 0) {
    throw new IllegalArgumentException("O valor deve ser maior que zero.");
}
```

Depois, mantenha a mesma validação em um único lugar:

```java
private void validarValorPositivo(double valor) {
    if (valor <= 0) {
        throw new IllegalArgumentException("O valor deve ser maior que zero.");
    }
}
```

Chame `validarValorPositivo(valor)` em `depositar` e `sacar`, sem alterar as assinaturas nem o restante dos contratos. Rode `./mvnw test` imediatamente antes de extrair e novamente depois; todas as verificações devem continuar verdes. Se não houver duplicação real a eliminar, não force uma refatoração.

### Dicas

Para testar exceções, use `assertThrows`:

```java
@Test
void depositar_ValorNegativo_LancaIllegalArgumentException() {
    var conta = new Conta("Maria", 100);
    assertThrows(IllegalArgumentException.class, () -> conta.depositar(-10));
}
```

Para verificar uma operação rejeitada, confira também o estado depois da exceção. Por exemplo, ao tentar sacar ou transferir um valor inválido/insuficiente, confirme que o saldo não mudou; numa transferência rejeitada, confira **os dois saldos**. O contrato não especifica regras adicionais para destino `null` ou transferência para a própria conta; não invente esses cenários como requisitos desta atividade.

Para testar `transferir`, crie duas contas ativas e verifique os saldos de ambas:

```java
@Test
void transferir_ValorValido_AtualizaSaldoDeAmbasContas() {
    var origem = new Conta("Maria", 200);
    var destino = new Conta("João", 100);

    origem.transferir(destino, 50);

    assertEquals(150, origem.getSaldo());
    assertEquals(150, destino.getSaldo());
}
```

### Executar testes

Os filtros por método só funcionam depois que existe pelo menos um teste com aquele prefixo. Antes disso, o Surefire informa que não encontrou testes; nenhum teste foi executado e esse resultado não é Red.

```bash
# Todos os testes
./mvnw test

# Use cada filtro depois de criar testes daquele método
./mvnw test -Dtest="ContaTest#depositar*"
./mvnw test -Dtest="ContaTest#sacar*"
./mvnw test -Dtest="ContaTest#encerrar*"
./mvnw test -Dtest="ContaTest#transferir*"
```

> ⚠️ **Mínimo exigido:** o relatório do Maven deve mostrar pelo menos **15 casos executados** no total. Os 8 casos iniciais do construtor já contam; os casos de `@ParameterizedTest` contam por cada valor executado, não apenas como um método Java. Use a matriz para priorizar todos os comportamentos e estados preservados; não crie testes repetidos apenas para atingir a contagem.

---

## 📘 Referência Rápida — JUnit 5

### Anotações de teste

| Anotação | Descrição |
|---|---|
| `@Test` | Teste com valores fixos (sem parâmetros) |
| `@ParameterizedTest` | Teste parametrizado (executado N vezes) |
| `@CsvSource({...})` | Fornece dados inline para `@ParameterizedTest` |
| `@ValueSource(ints = {...})` | Fornece valores simples de um tipo |
| `@DisplayName("...")` | Define nome legível para o teste no relatório |
| `@BeforeEach` | Método executado antes de cada teste |
| `@AfterEach` | Método executado depois de cada teste |

### Assertions comuns

```java
// Igualdade
assertEquals(esperado, resultado);

// Igualdade com tolerância (para doubles)
assertEquals(esperado, resultado, 0.001);

// Booleanos
assertTrue(condicao);
assertFalse(condicao);

// Nulos
assertNull(objeto);
assertNotNull(objeto);

// Exceções
assertThrows(TipoExcecao.class, () -> metodoQueLanca());

// Strings
assertTrue(resultado.contains("texto"));
assertTrue(resultado.startsWith("prefixo"));

// Coleções
assertTrue(lista.isEmpty());
assertTrue(lista.contains(item));
assertEquals(tamanhoEsperado, lista.size());
```

### Executando testes no terminal

```bash
# Todos os testes
./mvnw test

# Filtrar por nome de teste
./mvnw test -Dtest="ContaTest#construtor_DadosValidos_CriaContaCorretamente"

# Filtrar por classe
./mvnw test -Dtest="ContaTest"

# Com detalhes
./mvnw test -Dsurefire.printSummary=true

```

> Este projeto não configura JaCoCo; cobertura não faz parte dos comandos validados neste roteiro.

---

## 📦 Entregáveis

Para comprovar a realização da atividade, você deve entregar as seguintes evidências no seu fork do repositório:

### ✅ Checklist obrigatório

| # | Item | Critério | Local |
|---|---|---|---|
| 1 | Testes da Conta Bancária | Pelo menos 15 casos executados no total, incluindo os 8 iniciais e cobrindo os comportamentos da matriz | `src/test/java/contabancaria/ContaTest.java` |
| 2 | Código da Conta Bancária | Implementação dos contratos exercitados, sem `UnsupportedOperationException` nos métodos da atividade | `src/main/java/contabancaria/Conta.java` |
| 3 | Suíte verde e evidência | Saída ou captura de tela de `./mvnw test` após implementar os comportamentos | Entregar no ambiente virtual da disciplina |
| 4 | Histórico de commits (recomendado) | Commits incrementais mostrando o ciclo TDD (ex.: "red: teste depositar", "green: implementa depositar") | Histórico do Git |

### 📸 Evidência de execução

Após concluir, execute os testes e guarde a saída ou uma captura de tela para enviar junto com a atividade no ambiente virtual:

```bash
./mvnw test
```

Não versione um arquivo de log ou screenshot no repositório. O commit contém código e testes; a evidência é entregue no ambiente virtual, evitando conflito entre os dois destinos.

### 🔀 Padrão de commits (recomendado)

Use prefixos para documentar o ciclo TDD nos commits:

```
red:      teste para depositar - valor válido
green:    implementa depositar
refactor: simplifica validação do depositar

red:      teste para sacar - saldo insuficiente
green:    implementa sacar com validação
refactor: extrai validação para método privado
```

### 📤 Como entregar

1. Confirme que `origin` aponta para o seu fork:
   ```bash
   git remote -v
   ```
2. Na branch da atividade, faça commit e envie-a ao fork:
   ```bash
   git add .
   git commit -m "Atividade TDD completa"
   git push -u origin HEAD
   ```
   `HEAD` envia a branch atual; não faça push direto para `main` se estiver trabalhando em uma branch. Se `origin` não for o seu fork, corrija o remoto antes de enviar.
3. Envie o link do fork e a evidência de testes no ambiente virtual da disciplina.

O workflow do GitHub Actions executa a suíte com Java 21 em Linux a cada push e pull request. No repositório inicial, são 8 casos; conforme você acrescenta os testes, a mesma automação os executa também. Assim, ela confirma o build e os comportamentos cobertos, mas não implementa nem substitui testes que ainda não foram escritos.

---

## 📚 Referências

- [JUnit 5 — Guia do Usuário (Oficial)](https://junit.org/junit5/docs/current/user-guide/)
- [Maven Surefire Plugin](https://maven.apache.org/surefire/maven-surefire-plugin/)
- [TDD — Martin Fowler](https://martinfowler.com/bliki/TestDrivenDevelopment.html)
- [Padrão AAA — Arrange, Act, Assert](https://automationpanda.com/2020/07/07/arrange-act-assert-a-pattern-for-writing-good-tests/)

---

> Bom trabalho! Lembre-se: no TDD, o teste sempre vem primeiro. 🧪🔴🟢🔵
