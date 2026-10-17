# 🏨 Coworking & Hotel Management System (Sistema de Hotelaria & Coworking)

![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![Neon Serverless Postgres](https://img.shields.io/badge/Neon%20DB-Cloud%20Database-00E599?style=for-the-badge&logo=neon&logoColor=black)
![Paradigma](https://img.shields.io/badge/Paradigma-POO-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Em%20Desenvolvimento-yellow?style=for-the-badge)
![Licença](https://img.shields.io/badge/Licen%C3%A7a-MIT-green?style=for-the-badge)

---

## 📌 Visão Geral do Projeto

O **Sistema de Gestão de Hotelaria & Coworking** é uma aplicação corporativa desenvolvida em **Java** com persistência em banco de dados relacional **PostgreSQL**, hospedado em nuvem serverless via **NeonDB**. O projeto foi concebido para atender à convergência de modelos modernos de hospitalidade: espaços híbridos que combinam hospedagem convencional com locação de estações de trabalho e salas corporativas de coworking.

O projeto foi estruturado no contexto acadêmico a partir da disciplina de **Programação Orientada a Objetos (POO)** do curso de **Análise e Desenvolvimento de Sistemas**, servindo como modelo de engenharia de software aplicada, validação de regras de negócio, modelagem de dados e escalabilidade modular.

> ℹ️ **Decisão Arquitetural de Banco de Dados:**  
> Embora a proposição acadêmica inicial sugerisse o uso de MySQL local, a equipe optou estrategicamente pela migração para o **PostgreSQL** com infraestrutura em nuvem no **NeonDB**. Essa abordagem garante conectividade remota unificada e sincronização de dados multi-ambiente, permitindo que a aplicação seja executada e validada de qualquer dispositivo sem necessidade de replicação de banco de dados local (observando-se apenas eventuais restrições de firewalls de rede corporativas/institucionais quanto à saída para conexões externas de banco).

---

## 🎯 Objetivos

### Objetivo Geral
Desenvolver um ecossistema modular, robusto e escalável para controle de reservas, hospedagens, aluguel de salas/estações de coworking, cadastros e relatórios gerenciais, aplicando boas práticas de Engenharia de Software e Princípios SOLID.

### Objetivos Pedagógicos & Técnicos
- **Modelagem Orientada a Objetos:** Mapeamento de entidades de negócio com responsabilidades atômicas e coesas.
- **Encapsulamento Rigoroso:** Blindagem do estado interno dos objetos com validações consistentes.
- **Herança & Polimorfismo:** Generalização e especialização de fluxos (ex.: `Espaco` $\rightarrow$ `QuartoHotel`, `SalaReuniao`, `EstacaoCoworking`).
- **Persistência de Dados (DAO/JDBC em Nuvem):** Conexão desacoplada via JDBC direcionada ao PostgreSQL gerenciado no NeonDB.
- **Relatórios Analíticos:** Extração de métricas de ocupação, faturamento e taxas de permanência.

---

## 🏛️ Arquitetura e Estrutura de Pacotes

A aplicação adota o padrão em camadas (**Layered Architecture**), separando interface, lógica de negócio e persistência de dados:

```text
SistemaReservaPOO/
├── src/
│   ├── model/                  # Entidades de domínio e regras de encapsulamento
│   │   ├── Espaco.java         # Classe base (abstrata)
│   │   ├── QuartoHotel.java    # Especialização para hotelaria tradicional
│   │   ├── EstacaoCoworking.java # Especialização para postos de trabalho
│   │   ├── SalaReuniao.java    # Especialização para salas de reunião/eventos
│   │   ├── Cliente.java        # Dados cadastrais de hóspedes/membros
│   │   └── Reserva.java        # Vínculo temporal entre Cliente e Espaco
│   ├── dao/                    # Data Access Objects (comunicação JDBC / PostgreSQL NeonDB)
│   │   ├── ConnectionFactory.java
│   │   ├── ClienteDAO.java
│   │   ├── EspacoDAO.java
│   │   └── ReservaDAO.java
│   ├── service/                # Regras de negócio, cálculos tarifários e validações
│   │   ├── ReservaService.java
│   │   └── RelatorioService.java
│   └── ui/                     # Interface de usuário (Console / CLI e futuras UIs)
│       ├── MenuPrincipal.java
│       └── ConsoleUtils.java
└── resources/
    └── database/               # Scripts DDL e DML para criação das tabelas
        ├── schema.sql
        └── seed.sql
```

---

## ⚙️ Funcionalidades do Sistema

### 1. Gestão de Clientes e Membros
- [x] Cadastro completo de clientes (Pessoa Física e Jurídica).
- [x] Histórico de consumos, estadias e reservas por cliente.
- [x] Validação de documentos (CPF/CNPJ) e dados de contato.

### 2. Gestão de Espaços Híbridos
- [x] **Acomodações:** Quartos Standard, Luxo e Suítes Corporativas.
- [x] **Coworking:** Mesas rotativas (*hot desks*), mesas dedicadas e salas de conferência climatizadas.
- [x] Controle de status em tempo real (`DISPONÍVEL`, `OCUPADO`, `MANUTENÇÃO`, `RESERVADO`).

### 3. Motor de Reservas & Locação
- [x] Checagem de disponibilidade sem duplicidade temporal (conflito de horários).
- [x] Precificação dinâmica: cobrança por diária (hotel) e por hora/dia (coworking).
- [x] Check-in e Check-out com fechamento e totalização de valores.

### 4. Inteligência Gerencial e Relatórios
- [x] Relatório de taxa de ocupação diária e mensal.
- [x] Extrato de faturamento por categoria de produto (Hotelaria vs. Coworking).
- [x] Listagem de reservas ativas e pendentes de quitação.

---

## 🛠️ Tecnologias Utilizadas

| Tecnologia | Finalidade |
| :--- | :--- |
| **Java JDK (17+)** | Linguagem base e lógica de domínio orientada a objetos |
| **PostgreSQL (15+)** | Sistema de gerenciamento de banco de dados relacional |
| **NeonDB** | Plataforma Serverless PostgreSQL em nuvem para acesso remoto universal |
| **JDBC (PostgreSQL Driver)** | Driver de conectividade com transações seguras e pool de conexões |
| **Git & GitHub** | Controle de versionamento e colaboração distribuída |

---

## 🚀 Como Executar o Projeto

### Pré-requisitos
- **Java JDK 17** ou superior instalado e configurado nas variáveis de ambiente (`JAVA_HOME` e `PATH`).
- Driver JDBC do PostgreSQL (`postgresql-42.x.x.jar`) no classpath da aplicação.
- Acesso à internet para comunicação com a instância NeonDB (atenção a redes restritas ou com *firewalls* corporativos que bloqueiem a porta de conexão remota `5432`).
- **IDEs recomendadas:** 
  - **NetBeans IDE** (o clássico e excelente ambiente para ecossistemas Java)
  - **IntelliJ IDEA**
  - **VS Code** (com Java Extension Pack)
  - **Eclipse IDE**

### 1. Clonar o Repositório
```bash
git clone https://github.com/MarcoAntonio16AS/Hotelaria-Coworking.git
cd Hotelaria-Coworking
```

### 2. Configurar o Banco de Dados (PostgreSQL / NeonDB)
As tabelas e dados iniciais podem ser executados no console SQL da NeonDB ou em um client SQL (DBeaver, pgAdmin) a partir dos scripts localizados em `resources/database/schema.sql`.

Em seguida, configure sua string de conexão segura em `ConnectionFactory.java` (ou via variáveis de ambiente/arquivo de propriedades):
```java
// Exemplo de formato de conexão NeonDB com SSL obrigatório:
private static final String URL = "jdbc:postgresql://ep-exemplo-pooler.us-east-2.aws.neon.tech/hotelaria_coworking?sslmode=require";
private static final String USER = "seu_usuario_neon";
private static final String PASSWORD = "sua_senha_neon";
```

> ⚠️ *Nota sobre Conectividade:* Caso a aplicação apresente *timeout* de conexão ao rodar em redes acadêmicas ou corporativas, certifique-se de que o firewall da rede autoriza tráfego de saída na porta padrão do PostgreSQL (`5432`).

### 3. Compilar e Executar

#### Via NetBeans / Eclipse / IntelliJ:
1. Abra ou importe a pasta do projeto como projeto Java existente.
2. Certifique-se de que a biblioteca do **PostgreSQL JDBC Driver** está associada em *Libraries / Dependências*.
3. Execute o arquivo `src/ui/MenuPrincipal.java`.

#### Via Terminal / Linha de Comando:
```bash
# Compilar os arquivos fonte direcionando para a pasta bin
javac -d bin -cp "lib/postgresql-42.7.2.jar" -sourcepath src src/ui/MenuPrincipal.java

# Executar a aplicação com o driver no classpath
java -cp "bin:lib/postgresql-42.7.2.jar" ui.MenuPrincipal
```

---

## 🤝 Como Contribuir

> 🎓 **Aviso Acadêmico & Desenvolvimento Ativo:**  
> Este é um projeto desenvolvido no ambiente acadêmico para a disciplina de Análise e Desenvolvimento de Sistemas (POO), mas **encontra-se em constante evolução e desenvolvimento ativo**. Feedbacks, refatorações, novas ideias de design e implementações de regras de negócio são muito bem-vindos!

Para contribuir com o projeto, siga o passo a passo padrão de fluxo Git:

1. **Faça um Fork** do repositório para sua conta no GitHub.
2. **Crie uma Branch** dedicada para a sua funcionalidade ou correção:
   ```bash
   git checkout -b feature/minha-nova-funcionalidade
   ```
3. **Desenvolva e valide suas alterações**, mantendo as boas práticas de POO, separação de camadas e código limpo.
4. **Faça o Commit** das suas alterações com mensagens claras e descritivas:
   ```bash
   git commit -m "feat: implementa validacao de reservas em estacoes de coworking"
   ```
5. **Envie para o seu repositório remoto (Push)**:
   ```bash
   git push origin feature/minha-nova-funcionalidade
   ```
6. **Abra um Pull Request (PR)** detalhando:
   - O que foi implementado ou corrigido.
   - Testes manuais ou unitários executados.
   - Considerações adicionais para revisão da equipe.

Se encontrar algum bug ou tiver sugestões de melhoria arquitetural, fique à vontade para abrir uma **Issue** no repositório!

---

## 🗺️ Roadmap e Próximos Passos

O projeto foi desenhado para evoluir em fases sucessivas até se tornar uma solução corporativa completa:

- [ ] **Fase 1 (Atual - Console Core):** Refinamento das regras POO, validação de transações no PostgreSQL NeonDB e testes unitários (JUnit).
- [ ] **Fase 2 (Interface Gráfica):** Implementação de dashboard desktop em JavaFX ou Swing para os operadores da recepção.
- [ ] **Fase 3 (API RESTful):** Migração das regras de negócio para **Spring Boot** com arquitetura REST e deploy em nuvem.
- [ ] **Fase 4 (Frontend Web/Mobile):** Criação de portal de autoatendimento para clientes realizarem reservas de qualquer local.
- [ ] **Fase 5 (Integração de Pagamento):** Conexão com gateways (Stripe/Mercado Pago) para confirmação automática de reservas via PIX e cartão.

---

## 👥 Autores & Contribuidores

- **Marco Antônio** — *Desenvolvimento & Arquitetura* — [GitHub](https://github.com/MarcoAntonio16AS)
- Equipe de Análise e Desenvolvimento de Sistemas (Turma de POO).

---

## 📄 Licença

Este projeto é distribuído sob a licença **MIT**. Consulte o arquivo `LICENSE` para mais detalhes.
