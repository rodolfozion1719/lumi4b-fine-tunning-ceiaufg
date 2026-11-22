# 🚀 Lumi 4B: Fine-tuning (equipe AJCAT)

Repositório da equipe para a competição de fine-tuning do **CEIA-BR Lumi 4B**, promovida pela UFG.

> **Status:** em preparação. A tarefa, o dataset e a fórmula do F1 ainda não foram divulgados. O que depende disso está marcado como *a definir*.

## 👥 Equipe

| Integrante | GitHub |
| :--- | :--- |
| Rodolfo Zion Ruthes Brito | [@rodolfozion1719](https://github.com/rodolfozion1719) |
| Mouhamed Jamal Jomaa | [@mouhamedjj2008-oss](https://github.com/mouhamedjj2008-oss) |
| José Daniel Rodrigues de Melo | [@jdrmprofissional08-hue](https://github.com/jdrmprofissional08-hue) |


## 📌 O que já sabemos

| Item | Situação |
| :--- | :--- |
| Modelo base | Lumi 4B (`ceia-research/lumi-4b`), obrigatório e imutável. O ID oficial está a confirmar. |
| Arquitetura | Nemotron 3 Nano 4B, 4 bilhões de parâmetros, bilíngue PT-BR/EN |
| Técnicas permitidas | LoRA, QLoRA e outras de fine-tuning |
| Dados | Dataset bruto fornecido pela organização. Dados sintéticos e públicos são permitidos, com licença adequada. |
| Métrica | F1-Score personalizado (fórmula *a definir*) |
| Avaliação | Leaderboard público no Kaggle (indicativo) e avaliação final privada (define o resultado) |
| Tarefa e formato da resposta | *A definir* |
| Inscrições | Até 24/11 |
| Entrega | Modelo público no Hugging Face e repositório público no GitHub com instruções de reprodução |

## ⚖️ Regras que seguimos

| Regra | O que significa |
| :--- | :--- |
| Modelo base fixo | Partimos sempre do Lumi 4B. Não substituímos por outro. |
| Thinking desligado | `enable_thinking=False` no treino e na inferência. |
| Chat template nativo | Usamos o template do tokenizer (`apply_chat_template`). |
| Teste privado | Não usamos nem tentamos reconstruir o conjunto de teste oculto. |
| Dados externos e sintéticos | Registramos a fonte e confirmamos que a licença permite uso e redistribuição. |
| Entrega pública | Repositório no GitHub e modelo final no Hugging Face, ambos públicos e carregáveis pela organização. |

## 🧭 Como vamos trabalhar

Princípios que valem desde o início. Os arquivos que os sustentam serão criados quando o dataset sair.

| Princípio | Na prática |
| :--- | :--- |
| Uma mudança por vez | Em cada experimento alteramos um único fator (por exemplo, só o learning rate). |
| Comparação justa | Mesma validação, mesma métrica e mesmo prompt em todas as tentativas. |
| Tudo anotado | Cada experimento registra quem rodou, o que mudou e o F1 obtido. |
| Parâmetros em arquivo | Configurações em arquivo YAML, não espalhadas pelo código, para reproduzir o resultado. |
| Segredos fora do Git | Nunca commitamos dados, pesos de modelo, tokens ou arquivos `.env`. |
| Kaggle com critério | Só enviamos ao leaderboard o que já foi bem na validação local. |

## 🗺️ Etapas previstas

| Etapa | Descrição | Situação |
| :--- | :--- | :--- |
| 1 | Entender a tarefa e a métrica com a organização | Aguardando dataset |
| 2 | Explorar e limpar os dados | Não iniciada |
| 3 | Medir o Lumi sem treino (baseline) | Não iniciada |
| 4 | Treino curto com LoRA para validar o pipeline | Não iniciada |
| 5 | Primeira submissão no Kaggle | Não iniciada |
| 6 | Melhorias: dados sintéticos, hiperparâmetros, pós-processamento | Não iniciada |
| 7 | Publicar modelo e código, e testar o carregamento | Não iniciada |

## ❓ Perguntas para a organização

- Qual é a tarefa e em que formato o modelo deve responder?
- Como é calculado o F1 personalizado (macro ou micro, tratamento de saídas mal formatadas)?
- Qual é o ID oficial do modelo: `ceia-research/lumi-4b` ou `ceia-br/lumi-4b`? E qual versão (v1 ou v0.2)?
- Qual é o limite de envios diários no Kaggle e o formato do arquivo de submissão?
- Podemos usar outro modelo de linguagem para gerar dados sintéticos?
- Basta publicar o adaptador LoRA ou é preciso o modelo mesclado?

## 🔗 Links

| Recurso | Link |
| :--- | :--- |
| Competição no Kaggle | [LINK] |
| Regulamento | [LINK] |
| Modelo base | [ceia-research/lumi-4b](https://huggingface.co/ceia-research/lumi-4b) |
| Documentação do SFTTrainer (TRL) | [huggingface.co/docs/trl/sft_trainer](https://huggingface.co/docs/trl/sft_trainer) |
| Modelo final no Hugging Face | *Em breve* |

## 🛠️ Instalação

Em preparação. Quando o código existir, a ordem será instalar o `torch` com a versão de CUDA da máquina e depois rodar `pip install -r requirements.txt`.

## 📄 Licença

Código sob licença MIT. Os datasets usados têm licença própria, registrada neste repositório.
