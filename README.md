# DIO

> [!NOTE]
> **Lógica de Programação e POO. |**
> **Banco de dados Relacionais e Não Relacionais. |**
> **Docker/Docker Compose. |**
> **AWS. |**
> **AZURE.**

## Planejamento MVP - Sistema de Gestão para Oficina Mecânica (99Freelas)

### 1) Escopo da versão 1 (MVP)

**Entra no MVP**
- Login administrativo simples (acesso interno da oficina)
- Cadastro de clientes
- Cadastro de veículos vinculados ao cliente
- Abertura e edição de Ordem de Serviço (OS)
- Itens de orçamento (serviços e peças)
- Controle de status da OS: `aberto`, `em andamento`, `aguardando aprovação`, `aprovado`, `concluído`, `cancelado`
- Geração de orçamento em PDF
- Envio do PDF via WhatsApp
- Painel com visão geral das OS por status

**Fica para depois**
- Multiusuário com permissões avançadas
- Controle de estoque completo
- Integrações financeiras/ERP
- App mobile nativo
- Relatórios avançados com BI

### 2) Entidades principais

- **Cliente**: id, nome, telefoneWhatsApp, email, tipoDocumento (`CPF`/`CNPJ`), numeroDocumento, createdAt
- **Veículo**: id, clienteId, placa, marca, modelo, ano, cor, quilometragem
- **OrdemServico**: id, clienteId, veiculoId, numeroOS, status, problemaRelatado, observacoesInternas, valorTotal, createdAt, updatedAt
- **ItemOrcamento**: id, ordemServicoId, tipo (`serviço`/`peça`), descricao, quantidade, valorUnitario, valorTotal (calculado por item)
- **AprovacaoOrcamento**: id, ordemServicoId, canal (`whatsapp`), status (`pendente`/`aprovado`/`rejeitado`), dataEnvio, dataRetorno

#### Regras de negócio importantes
- `valorTotal` da OS deve ser recalculado automaticamente sempre que os itens mudarem enquanto o status estiver em `aberto`.
- Se a OS estiver em `em andamento` ou `aguardando aprovação`, mudanças de itens devem exigir ação explícita de "recalcular orçamento" antes do novo envio ao cliente.
- Ao alterar o status para `aprovado`, o `valorTotal` deve ser congelado como snapshot do orçamento aceito pelo cliente.

### 3) Fluxo ponta a ponta

1. Cadastrar cliente e veículo.
2. Criar OS com problema relatado.
3. Adicionar itens de orçamento (serviços e peças).
4. Calcular total e alterar status para `aguardando aprovação`.
5. Gerar PDF do orçamento.
6. Enviar orçamento via WhatsApp para o cliente.
7. Registrar retorno de aprovação/reprovação.
8. Se aprovado, mover para `em andamento` e depois `concluído`.
9. Exibir tudo no painel de controle e relatórios básicos.

### 4) Stack e integrações sugeridas

| Camada | Tecnologia | Motivo |
|---|---|---|
| Front-end | React + Vite + TypeScript | Produtividade e manutenção simples |
| Back-end | ASP.NET Core Web API (.NET 8/9) | Alinhado ao foco atual da trilha |
| Banco de dados | MySQL | Familiaridade e boa adoção em sistemas CRUD |
| PDF | QuestPDF ou iText7 | Geração estruturada de orçamento |
| WhatsApp | API oficial Meta (Cloud API) ou provedor (ex.: Z-API/Twilio) | Envio automatizado com rastreabilidade |
| Autenticação | JWT | Controle de sessão para painel administrativo |

> [!WARNING]
> **Licenciamento PDF (atenção):** bibliotecas de PDF podem ter termos comerciais e de distribuição diferentes por versão.
> **Antes de decidir em produção, confirme sempre os termos atuais na documentação oficial (QuestPDF e iText).**

### 5) Planejamento em sprints curtas

- **Sprint 1:** estrutura base, autenticação e CRUD de clientes/veículos
- **Sprint 2:** CRUD de OS + itens + regras de status
- **Sprint 3:** geração de PDF do orçamento
- **Sprint 4:** integração WhatsApp + registro de aprovação
- **Sprint 5:** dashboard, notificações e relatórios básicos

> [!TIP]
> **Conhecimentos em C# (.NET, Versão 9). Python versão 3+ |**
> **Linguagem SQL [DDL, DCL, DML, TCL, DQL]. |**
> **Linguagem NoSQL [MongoDB]. |**
> **Comandos via terminal Docker/Docker Compose. |**
> **Serviços AWS. |**
> **Serviços AZURE.**

> [!IMPORTANT]
> **Versionamento de código GIT | GITHUB (Os desáfios de projetos deste BootCamp, para uma melhor organização estarei sempre alocando em Branchs e aqui na MAIN apontando para a Branch dos projetos).**

## Projetos do Curso (Back-end em C#)

| Projeto | Descrição | Branch |
|--------|-----------|--------|
| Projeto | Criando consultas(Escrevendo) SQL utilizando o Microsof Copilot | [`Ver Projeto`](https://github.com/mauriciocampos1234/databases-e-cards) |
| Projeto | Criando um sistema (Real) de Gestão Escolar - ASPNET Core MVC, Lógica de Programação, POO C#, .NET Versão 8, AZURE | [`Ver Projeto`](https://github.com/mauriciocampos1234/sistema-gerenciamento-escola-completo) |
| Projeto | Criando um sistema de Protótipo de Análise de Extrato Bancário - Lógica de Programação, POO C#, .NET Versão 9  | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/BancoInovaTech) |
| Projeto | Criando um sistema de Gerenciamento de Contas e Suporte Técnico em Telecom - Lógica de Programação, POO C#, .NET Versão 9  | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/SuporteTecnicoTelecom) |
| Projeto | Criando um sistema de Sistema de Gerenciamento de Ordens de Serviço de Oficina Automotiva - Lógica de Programação, POO C#, .NET Versão 9  | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/ServicosDeOficina) |
| Projeto | Criando um sistema de Ordens de Serviço para Manutenção de Máquinas - Lógica de Programação, POO C#, .NET Versão 9  | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/Manufatura) |
| Projeto | Criando um sistema de transformação digital que atua na fabricação quanto na venda de produtos (Indústria e Varejo) - Lógica de Programação, POO C#, .NET Versão 9  | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/IndustriaEVarejo) |
| Projeto | Criando um Gestão de Apólices de Seguro - Lógica de Programação, POO C#, .NET Versão 9  | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/GFTSeguros) |
| Projeto | Criando um sistema para gerenciamento de um estacionamento - Lógica de Programação, C#, .NET Versão 9  | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/Desafio-01) |
| Projeto | Criando um sistema de hospedagem em um hotel - Lógica de Programação, C#, .NET Versão 9  | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/Desafio-02) |
| Projeto | Criando um Sistema e abstraindo um celular com POO. - Lógica de Programação, C#, .NET Versão 9  | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/Desafio-03) |
| Projeto | Criando um Sistema para realizar 12 consultas ao banco de dados, cada uma retornando um tipo de informação. - Banco de dados SQl Server, Management Studio 21, Liguagens SQL usadas [DDL, DML, DQL]  | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/Desafio-04) |
| Projeto | Criando um arquivo YML com as definições de um servidor Apache (httpd). - Docker Compose  | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/Desafio-05) |
| Projeto | Criando um Relatório para um empresa utilizando a infraestrutura da AWS  | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/Desafio-06) |
| Projeto | Criando um Minimal-API (CRUD de ADM's e VEÍCULOS) - Lógica de Programação, C#, .NET Versão 9, MYSQL  | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/Desafio-07) |
| Projeto | Criando um sistema gerenciador de tarefas, onde seja possível cadastrar uma lista de tarefas que permitirá organizar melhor a rotina. - Lógica de Programação, C#, .NET Versão 9, SQLSERVER 2022  | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/Desafio-08) |
| Projeto | Criando um Resumo de aprendizagem durante o desenvolvimento do lab: Computação em Nuvem AZURE  | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/Desafio-09) |
| Projeto | Criando um Resumo de aprendizagem durante o desenvolvimento do lab: Criando máquinas Virtuais na Azure | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/Desafio-10) |
| Projeto | Criando um Resumo e Processo de configuração de uma instância de Banco de Dados na plataforma Microsoft Azure | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/Desafio-11) |
| Projeto | Criando um Projeto completo de cadastro: Front-end: html 5, css 3, JavaScript - Back-end: .net C# versão 8, banco de dados MYSQL  | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/Projeto-Completo-C%23) |

...

## Projetos do Curso (Python)

| Projeto | Descrição | Branch |
|--------|-----------|--------|
| Projeto | projeto-front-back-end - React + Vite + NodeJS | [`Ver Projeto`](https://github.com/mauriciocampos1234/projeto-front-back-end) |
| Projeto | Trabalho Big Data com Pandas (Faculdade) - Este repositório documenta um trabalho prático/microatividades utilizando Python + Pandas para exploração e limpeza de um conjunto de dados. | [`Ver Projeto`](https://github.com/mauriciocampos1234/Trabalho-Big-Data-Pandas-Faculdade) |
| Projeto | KPIs-com-OKRs-estratégicos | [`Ver Projeto`](https://github.com/mauriciocampos1234/KPIs-com-OKRs-estrat-gicos) |
| Projeto | projeto-etl-python-ia-generativa | [`Ver Projeto`](https://github.com/mauriciocampos1234/projeto-etl-python-ia-generativa) |
| Projeto | Educador Financeiro com uso de IA Baseando-se em Dados Mockados | [`Ver Projeto`](https://github.com/mauriciocampos1234/Educador-Financeiro-Bradesco) |
| Projeto | Automacao, Analise de Dados, IA - chatbot-python | [`Ver Projeto`](https://github.com/mauriciocampos1234/automacao-analise-dados-ia-chatbot-python) |
| Projeto | Criando um projeto que Projeto de estudo que implementa uma API REST assíncrona para um “blog”, com autenticação via JWT e CRUD de posts | [`Ver Projeto`](https://github.com/mauriciocampos1234/blog_com_fastapi) |
| Projeto | Criando um projeto que simula um sistema de banco digital - Lógica de Programação, POO em Python, Versão 3+ | [`Ver Projeto`](https://github.com/mauriciocampos1234/sistema-bancario) |
| Projeto | Trilha completa de Aprendizagem da Linguagem Python - Lógica de Programação, POO em Python, Versão 3+ | [`Ver Projeto`](https://github.com/mauriciocampos1234/trilha-python-dio) |
| Projeto | Criando um projeto de academia - POO em Python, Versão 3.10+, FastAPI, Docker | [`Ver Projeto`](https://github.com/mauriciocampos1234/academia-api-main) |
| Projeto | Criando um projeto de rosulução de Códigos em Python com o Github Copilot | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/projeto-resolvendo-codigos-py-copilot) |
| Projeto | Conversando por Voz Com o ChatGPT Utilizando Whisper OpenAI e Python | [`Ver Projeto`](https://github.com/mauriciocampos1234/Conversando-por-Voz-Com-o-ChatGPT-Utilizando-Whisper-OpenAI-e-Python) |

...

## Projetos do Curso (Front-end)

| Projeto | Descrição | Branch |
|--------|-----------|--------|
| Projeto | Landing page para venda de kit de-xicaras-personalizadas - HTML, Tailwindcss, CSS, JS | [`Ver Projeto`](https://github.com/mauriciocampos1234/Landing-page-para-venda-de-kit-de-x-caras-personalizadas) |
| Projeto | Mapeador de Consumo de Cigarros - HTML, Tailwindcss, CSS, JS e Firebase Firestore  | [`Ver Projeto`](https://github.com/mauriciocampos1234/Mapeamento-de-cigarros) |
| Projeto | Calculadora simples com REACT - REACT, HTML, CSS e JS  | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/trilha-react-desafio01-calculadora) |
| Projeto | Projeto simples de estudo de criação de componentes aninhados - REACT + TS + VITE | [`Ver Projeto`](https://github.com/mauriciocampos1234/DIO-BOOT-CAMP/tree/my-app-react-ts) |
| Projeto | Classificador de Nível de Herói - HTML, CSS e JS  | [`Ver Projeto`](https://github.com/mauriciocampos1234/Dio_Hi_Happy/tree/Desafio_03) | 
| Projeto | Criando Game Detona Ralph - HTML, CSS e JS  | [`Ver Projeto`](https://github.com/mauriciocampos1234/Dio_Hi_Happy/tree/Desafio_02) | 
| Projeto | Jemoji-memory-game - HTML, CSS e JS  | [`Ver Projeto`](https://github.com/mauriciocampos1234/Dio_Hi_Happy/tree/Desafio_04) | 
| Projeto | Jyugioh-jo-ken-po - HTML, CSS e JS  | [`Ver Projeto`](https://github.com/mauriciocampos1234/Dio_Hi_Happy/tree/Desafio_06) | 
| Projeto | Landingpage-mundo-invertido - HTML, CSS e JS | [`Ver Projeto`](https://github.com/mauriciocampos1234/Dio_Hi_Happy/tree/Desafio_08) |
| Projeto | Criando uma LandingPage - HTML, CSS e JS  | [`Ver Projeto`](https://github.com/mauriciocampos1234/Dio_Hi_Happy/tree/Desafio_01) | 
| Projeto | Pokedex - HTML, CSS e JS  | [`Ver Projeto`](https://github.com/mauriciocampos1234/Dio_Hi_Happy/tree/Desafio_05) | 
| Projeto | Simulador-de-piano - HTML, CSS e JS  | [`Ver Projeto`](https://github.com/mauriciocampos1234/Dio_Hi_Happy/tree/Desafio_07) | 
| Projeto | Spider-man-multiverses - HTML, CSS e JavaScript  | [`Ver Projeto`](https://github.com/mauriciocampos1234/Dio_Hi_Happy/tree/Desafio_09) | 

...

# Meu site 
🔗 💻 [`meu site pessoal`](https://site-mauricio-campos.vercel.app/)
