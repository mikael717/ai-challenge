# Case Seguradora Horizonte - IA em Sinistros

### IA como copiloto: ganho mensurável com risco sob controle

Resolução do case técnico para a posição de **Business Partner de IA Sênior - Sinistros**. O projeto propõe como transformar iniciativas de IA em resultados mensuráveis de eficiência, prazo e controle de risco, sem presumir que todo problema deva ser resolvido com IA.

> **Importante:** a Seguradora Horizonte, os números e os cenários são fictícios. O notebook usa dados gerados por um simulador; seus resultados ilustram um método de análise e **não são previsões nem evidências sobre uma seguradora real**.

## Entregáveis

- **[Apresentação executiva (12 slides)](./apresentacao.html):** tese, priorização, arquitetura, controles, indicadores e roadmap. Abra o arquivo no navegador. Use os botões, o seletor de slides ou as setas do teclado para navegar.
- **[Notebook técnico](./notebook/sindicancia_score_vs_ml.ipynb):** simulação reproduzível para discutir valor, comparar scores sob capacidade limitada e demonstrar o viés de rótulos observado em sindicância.
- **[Enunciado do case](./escopo/desafio.md)** e [PDF original](./escopo/Case_BP_IA_Senior_Candidato%20(1).pdf).

## Síntese da proposta

1. **Começar pela mensuração e por uma plataforma comum.** Construir baseline, rastreabilidade e controles reutilizáveis antes de ampliar automações isoladas.
2. **Auto D0: primeiro assistido, depois automatizado por faixa.** No cenário-base simulado, a pré-análise libera cerca de 5 mil horas por mês. Isso só representa retorno financeiro se capacidade for convertida em caixa ou valor operacional; as premissas de custo, elegibilidade e conversão precisam ser validadas.
3. **Manter regras inegociáveis fora do LLM.** Verificações de prêmio, condutor, perfil e CNH são determinísticas, com comportamento conservador quando dados ou fontes não estão disponíveis.
4. **Na sindicância, testar primeiro o valor dos novos dados.** A simulação sugere que as variáveis estruturadas novas podem ser mais relevantes que trocar algoritmo ou usar o score do prompt isoladamente. O prompt só deve ser incorporado se trouxer sinal adicional comprovado.
5. **Tratar capacidade e rótulos como parte do problema.** A capacidade informada é de aproximadamente 600 investigações por mês. Como os rótulos dependem de quais casos foram investigados, uma auditoria aleatória fora da seleção do modelo é importante para avaliar o que o processo atual deixa de encontrar.
6. **Não usar IA onde regras ou otimização são mais apropriadas.** Regras de negócio críticas ficam em código determinístico; distribuição de casos pode ser tratada como otimização com restrições.

## Como reproduzir o notebook

É necessário Python e Jupyter. No Windows, a partir da raiz do repositório, crie e ative um ambiente virtual e instale as dependências:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

Abra `notebook/sindicancia_score_vs_ml.ipynb` no VS Code ou Jupyter, selecione o kernel do ambiente `.venv` e execute **Run All**. O notebook não precisa de arquivos de dados externos: a simulação gera os dados localmente. As bibliotecas e versões estão listadas em [`requirements.txt`](./requirements.txt).

## Executar com Docker

Com o Docker Desktop instalado e em execução, abra um terminal na raiz do repositório e inicie o JupyterLab:

```powershell
docker compose up --build
```

Quando o servidor iniciar, abra `http://localhost:8888` no navegador e use o token exibido no terminal. No JupyterLab, abra `notebook/sindicancia_score_vs_ml.ipynb` e execute **Run All**. O notebook e seus resultados ficam no diretório do projeto, pois ele é montado no container; não é preciso instalar Python ou as dependências na máquina.

Para encerrar, pressione `Ctrl+C` no terminal e execute:

```powershell
docker compose down
```

O JupyterLab só é publicado na interface local (`127.0.0.1`), e a autenticação por token permanece habilitada.

## Limites de interpretação

- Os resultados numéricos dependem das premissas programadas no simulador. Em particular, a relação entre variáveis e irregularidade foi definida artificialmente; diferenças de desempenho entre candidatos não devem ser extrapoladas para produção.
- O notebook separa períodos para treino, validação e teste. Ainda assim, os modelos de ML são treinados com rótulos dos casos investigados pelo processo legado, sem corrigir completamente o viés de seleção. A auditoria simulada ajuda a demonstrar a medição, mas **não torna esses resultados uma avaliação imparcial de um modelo treinado em dados reais**.
- Custos, taxas, perdas evitadas, capacidade e outros valores marcados como premissas precisam ser medidos e validados com dados reais antes de uma decisão de investimento ou automação.
- O material é um exercício de análise e desenho de solução, não uma implementação pronta para produção.

## Estrutura

```text
.
├── apresentacao.html
├── Dockerfile
├── compose.yaml
├── .dockerignore
├── escopo/
│   ├── Case_BP_IA_Senior_Candidato (1).pdf
│   └── desafio.md
├── notebook/
│   └── sindicancia_score_vs_ml.ipynb
├── requirements.txt
└── README.md
```

## Licença

Este repositório está sob a licença [MIT](./LICENSE). O enunciado e o PDF do case são materiais fornecidos para a atividade; a licença do projeto não altera os direitos sobre esses materiais.
