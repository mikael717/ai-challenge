# CASE TÉCNICO: Business Partner de IA Sênior
**Material do Candidato | Seguradora Horizonte**  
*Classificado como Informação Geral*

---

## Informações Gerais do Processo

| Item | Descrição |
| :--- | :--- |
| **Formato** | Case para casa + apresentação de 30 min + 30 min de arguição com a banca |
| **Prazo** | 5 dias corridos a partir do recebimento |
| **Entregável Principal** | **Apresentação de até 12 slides** <br>**E** escolha de um dos problemas para apresentar **apenas uma** das opções técnicas abaixo:<br>• Notebook, ou aplicação, Python;<br>• Pipeline de preparação de dados;<br>• Arquivo README;<br>• Testes de uma regra crítica;<br>• Breve descrição de como a solução seria implantada em AWS, Azure ou Google Cloud. |
| **Anexos Técnicos** | Demais anexos técnicos (arquitetura, diagramas, cálculos) são opcionais, não precisam constar na lista anterior e não contam no limite de slides. |
| **Uso de IA** | Permitido para apoiar a elaboração. Na arguição você deverá defender e aprofundar qualquer ponto apresentado. |
| **Observação** | Empresa, números e relatos são fictícios, mas inspirados em situações reais do mercado segurador. |

---

## 1. Contexto

A **Seguradora Horizonte** é uma seguradora multilinha (*Auto, Residencial, Empresarial, Condomínio e Vida*) com operação nacional. A Diretoria de Operações, Tecnologia e Sinistros tem uma área interna de IA e Inovação que já colocou em produção dezenas de assistentes conversacionais por produto, alguns modelos preditivos e vem acelerando projetos de IA generativa com agentes, em nuvem e com integrações a sistemas internos.

Apesar disso, a percepção da diretoria é que **muitos projetos ficam presos em piloto**: a companhia precisa sair de *"provas de conceito interessantes"* para **ganhos mensuráveis em eficiência, prazo de pagamento e controle de risco em Sinistros**.

Você acabou de assumir como **Business Partner de IA para a área de Sinistros**. Na primeira semana, conversou com quatro gestores. Os relatos estão abaixo como foram ditos – *podem conter imprecisões, vieses ou pedidos que não são necessariamente a melhor solução*.

---

## 2. O que você ouviu das áreas

### Gerente de Sinistros Auto – Análise D0
> *"A minha equipe montou sozinha um prompt no Copilot que faz a pré-análise do sinistro: o analista cola o aviso, o boletim de ocorrência e os dados da apólice, e o prompt diz se está OK ou NÃO OK e dá um score de 0 a 100 de risco de sindicância. Funciona bem, mas cada analista usa de um jeito, copiando e colando de vários sistemas. Quero que isso vire um sistema oficial e que, nos casos OK, o sinistro já siga sem passar pelo analista. Ah, e algumas regras não podem ser flexibilizadas de jeito nenhum: pagamento do prêmio, condutor principal, perfil e CNH."*

### Coordenador de Sindicância / Prevenção a Fraudes Auto
> *"Temos um modelo de ML antigo que indica sinistros para sindicância, mas o time não confia muito. Fizemos várias reuniões e levantamos novas variáveis que achamos importantes: perfil do condutor, histórico de cotações e cancelamentos, registros em bases restritivas do mercado, uso de assistência/guincho antes do evento e avarias na vistoria prévia. Muitas fraudes só a perícia humana pega. Agora também tem o score do prompt. Quero saber qual dos dois usar."*

### Gerente de Sinistros Não-Auto (Ramos Elementares)
> *"No Auto houve muita evolução tecnológica; no Não-Auto, quase nada. Recebemos cerca de 1.500 avisos por mês. Hoje encerramos uns 30% ainda na análise preliminar, mas tudo é manual, por e-mail e caixa departamental. No Empresarial, quebra de vidro é cerca de 12% dos sinistros, tem preço bem conhecido e baixo valor. Quero um agente no WhatsApp que receba o aviso, as fotos e pague o cliente em minutos. Depois a gente expande para Condomínio e Residencial."*

### Gerente de Sinistros Vida
> *"Nós já temos um assistente que ajuda na análise de cobertura de Vida e funciona bem. Agora o Auto e o Não-Auto querem fazer o deles. Cada área está criando seus próprios prompts e ninguém sabe quem pode alterar o quê, nem se uma mudança melhorou ou piorou o resultado. Também temos regras de distribuição de sinistros por região e por analista que mudam com férias e desligamentos – disseram que dava para fazer com IA."*

---

## 3. Informações Disponíveis

### Fontes de Dados e Sistemas

| Fonte | Conteúdo | Observações |
| :--- | :--- | :--- |
| **Base de sinistros (5 anos)** | Apólice, ramo, natureza, datas de ocorrência e aviso, estimativa, pagamento, status, analista, decisão. | Rótulo de fraude só existe para casos enviados à sindicância. |
| **Documentos do sinistro** | Aviso com descrição, boletim de ocorrência, fotos, orçamentos, notas fiscais, laudos. | PDFs nativos e digitalizados; qualidade variável. |
| **Fontes externas consultadas** | Listas restritivas por CPF e chassi, gravame financeiro, registros de sinistros no mercado, leilão. | Consultas pagas por chamada; retorno vazio não garante ausência de restrição. |
| **Emissão e cotação** | Histórico de cotações, endossos, cancelamentos, vistoria prévia. | Em sistemas diferentes; chaves nem sempre consistentes. |
| **Assistência 24h** | Acionamentos de guincho e pane. | Base de outro sistema. |
| **Condições gerais** | Documentos por produto e versão. | Versão aplicável depende da data de contratação. |
| **Atendimento** | Conversas de WhatsApp e chat. | Contém dados pessoais. |
| **Execução do prompt atual**| Não há log centralizado. | Cada analista usa sua cópia. |

### Números de Referência (Fictícios):
* **Sinistros Auto avisados:** ~20 mil/mês. Tempo médio de pré-análise manual: **25 minutos**.
* **Sindicância:** Capacidade de **~600 casos/mês**; taxa de confirmação de irregularidade de **~15%** nos casos enviados.
* **Não-Auto:** **~1.500 avisos/mês**; ~30% encerrados na análise preliminar.
* **Empresarial:** **~10 mil sinistros/ano**, dos quais ~1.150 são de quebra de vidro. Custo operacional estimado de regulação: **R$ 125 por sinistro**.

---

## 4. Sua Missão

Responda às questões abaixo. Quando faltar informação, **declare premissas** – a qualidade delas também será avaliada.  
*Preferimos profundidade e julgamento a amplitude.*

### Bloco 1 – Entendimento das áreas e priorização
1. Reformule o problema real de cada uma das quatro áreas. Que pedidos você contestaria ou ajustaria, e como conduziria essa conversa com o gestor?
2. Que perguntas e dados você pediria antes de propor qualquer solução?
3. Monte um portfólio de iniciativas e priorize com critérios explícitos. Indique o que não deveria ser resolvido com IA.
4. Estime o valor da iniciativa prioritária (ordem de grandeza, com premissas) e o que precisaria ser verdade para ela gerar retorno.

### Bloco 2 – IA Generativa
1. Como transformar o prompt da pré-análise Auto em uma solução corporativa? Detalhe arquitetura (agente único vs. multiagente), integração com sistemas e fontes externas, leitura de documentos (incluindo digitalizados), papel do analista e rastreabilidade da recomendação.
2. Como garantir que as regras inegociáveis nunca sejam flexibilizadas pelo modelo?
3. Proponha um modelo de governança para prompts e agentes compartilhados entre Auto, Não-Auto e Vida: base comum vs. ramificações por produto, versionamento, quem aprova mudanças e como medir se uma alteração melhorou ou piorou o resultado.
4. Desenhe a jornada e os controles do agente de quebra de vidro no WhatsApp. Quais riscos (fraude, imagens manipuladas, prompt injection, LGPD, pagamento indevido, reputação) e mitigações?

### Bloco 3 – Machine Learning e score de risco
1. Score do prompt vs. modelo de ML de sindicância: quais as diferenças, vantagens e limitações de cada um? Proponha como combiná-los ou escolher entre eles e como comparar de forma justa.
2. Desenhe a evolução do modelo de sindicância: definição do alvo, uso das novas variáveis, tratamento do desbalanceamento e do viés de rótulo, prevenção de vazamento de informação.
3. Como definir o ponto de corte considerando a capacidade de 600 casos/mês? Como monitorar o modelo e o agente em produção?

### Bloco 4 – Dados e mensuração
1. Que análises você faria primeiro para dimensionar as oportunidades (por exemplo, perfil dos sinistros encerrados na preliminar ou de vidros)?
2. Quais KPIs (negócio, operação, qualidade e modelo) e como provar que o ganho veio da solução (grupo de controle, piloto escalonado etc.)?

### Bloco 5 – Execução e governança
1. Roadmap de 90 dias e de 12 meses com marcos de decisão (seguir, ajustar, encerrar).
2. Quem precisa estar envolvido (negócio, TI, dados, segurança, jurídico, privacidade, governança de IA) e como você evita que o projeto fique preso em piloto?

---

## 5. Como você será avaliado

* **Capacidade de entender o problema por trás do pedido e priorizar.**
* **Profundidade técnica em IA generativa, machine learning e análise de dados.**
* **Visão de risco, governança e uso responsável de IA.**
* **Mensuração de valor e plano de execução realista.**
* **Clareza e comunicação para públicos executivo e técnico.**