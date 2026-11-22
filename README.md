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

- **Modelo base:** Lumi 4B (`ceia-research/lumi-4b`), obrigatório e imutável. Arquitetura Nemotron 3 Nano 4B, com 4 bilhões de parâmetros, bilíngue PT-BR/EN.
- **Técnicas permitidas:** LoRA, QLoRA e outras de fine-tuning.
- **Dados:** a organização fornece um dataset bruto. Dados sintéticos e públicos são permitidos, desde que a licença permita uso e redistribuição.
- **Métrica:** F1-Score personalizado.
- **Avaliação:** o leaderboard público no Kaggle é indicativo. A avaliação final é privada e define o resultado.
- **Inscrições:** até 24/11.
- **Entrega:** modelo público no Hugging Face e este repositório público, com instruções para reproduzir a execução.

## ⚠️ Limitações e pendências

O que ainda não sabemos e que muda o código quando for respondido. Quando um item for resolvido, ele sai daqui e entra em "O que já sabemos".

- **Tarefa e formato da resposta:** define o prompt, o pós-processamento e o que o modelo deve devolver. *A definir.*
- **Fórmula do F1 personalizado:** define como medimos localmente (macro ou micro, tratamento de saídas mal formatadas). *A definir.*
- **ID oficial do modelo:** este repositório usa `ceia-research/lumi-4b`, mas exemplos do model card usam `ceia-br/lumi-4b`. *A confirmar.*
- **Limite de envios no Kaggle:** define quantas vezes por dia podemos testar. *A definir.*
- **Entrega do adaptador:** se basta o adaptador LoRA ou se é preciso publicar o modelo mesclado. *A confirmar.*
- **Dados sintéticos gerados por outro LLM:** se isso é permitido. *A confirmar.*
- **Recursos de GPU:** modelo, memória e horas disponíveis por grupo. *A definir.*
- **QLoRA no Lumi:** o modelo é híbrido (Mamba + atenção), e a quantização em 4 bits pode não funcionar em todas as camadas. *A testar.*

## ⚖️ Regras que seguimos

- **Modelo base fixo.** Partimos sempre do Lumi 4B e não o substituímos por outro.
- **Thinking desligado.** Usamos `enable_thinking=False` no treino e na inferência.
- **Chat template nativo.** Formatamos tudo com o template do tokenizer (`apply_chat_template`).
- **Teste privado.** Não usamos e nem tentamos reconstruir o conjunto de teste oculto.
- **Dados externos e sintéticos.** Registramos a fonte e confirmamos que a licença permite uso e redistribuição.
- **Entrega pública.** Repositório no GitHub e modelo final no Hugging Face, ambos públicos e carregáveis pela organização.

## 🧭 Como vamos trabalhar

Princípios que valem desde o início. Os arquivos que os sustentam serão criados quando o dataset sair.

| Princípio | Na prática |
| :--- | :--- |
| Um fator por rodada | Mudamos uma coisa de cada vez (por exemplo, só o learning rate), para saber o que causou a diferença no F1. |
| Régua única | Todo resultado é medido na mesma amostra de validação e com a mesma métrica. Se uma delas mudar, refazemos as comparações anteriores. |
| Registro simples | Uma tabela com data, quem rodou, o que mudou e o F1, que qualquer pessoa do time consegue ler. |
| Leaderboard como termômetro | O ranking público é só indicativo, segundo o regulamento. Decidimos pela validação local e usamos os envios para conferir. |
| Parâmetros em arquivo | Configurações em arquivo YAML, para reproduzir o resultado. |
| Segredos fora do Git | Nunca commitamos dados, pesos de modelo, tokens ou arquivos `.env`. |

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

## 🔐 Configuração de segredos

O token do Hugging Face fica num arquivo `.env`, que o Git ignora e nunca vai para o GitHub.

1. Copie o modelo: `cp .env.example .env` (no Windows: `copy .env.example .env`).
2. Abra o `.env` e preencha o valor.
3. Se um token vazar, revogue-o no Hugging Face e crie outro.

O `.env.example` não tem segredo e pode ser versionado:

```text
# Token do Hugging Face (huggingface.co/settings/tokens). Não commitar o .env.
HF_TOKEN=
```

## 🛠️ Instalação e verificação

Em preparação. A ordem prevista é esta:

```bash
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate

# 1. PyTorch primeiro, com a versão de CUDA da máquina (ver pytorch.org)
pip install torch --index-url https://download.pytorch.org/whl/cu121

# 2. Dependências do projeto
pip install -r requirements.txt

# 3. Kernels do Mamba, exigidos pelo Lumi (precisa de GPU NVIDIA com CUDA)
pip install mamba-ssm causal-conv1d --no-build-isolation
```

O `cu121` é só um exemplo. Troque pela versão compatível com a GPU e o driver da máquina.

### Lista de verificação

Rode na ordem. Se um passo falhar, não siga para o próximo.

1. PyTorch enxerga a GPU. Deve imprimir a versão e `True`:
   ```bash
   python -c "import torch; print(torch.__version__, torch.cuda.is_available())"
   ```
2. Transformers na versão exigida pelo modelo (5.8.1 ou superior):
   ```bash
   python -c "import transformers; print(transformers.__version__)"
   ```
3. Kernels do Mamba instalados. Deve imprimir `ok`:
   ```bash
   python -c "import mamba_ssm, causal_conv1d; print('ok')"
   ```
4. Tokenizer do Lumi baixa. Deve imprimir `ok`:
   ```bash
   python -c "from transformers import AutoTokenizer; AutoTokenizer.from_pretrained('ceia-research/lumi-4b', trust_remote_code=True); print('ok')"
   ```
5. Login no Hugging Face (depois de `huggingface-cli login`). Deve mostrar o seu usuário:
   ```bash
   huggingface-cli whoami
   ```

Estes comandos ainda não foram testados numa máquina com GPU. Confirmem na primeira instalação e corrijam a lista se algo diferir.

## 🔗 Links

- **Regulamento:** [LINK]
- **Modelo base:** [ceia-research/lumi-4b](https://huggingface.co/ceia-research/lumi-4b)
- **Documentação do SFTTrainer (TRL):** [huggingface.co/docs/trl/sft_trainer](https://huggingface.co/docs/trl/sft_trainer)
- **Modelo final no Hugging Face:** *em breve*

## 📄 Licença

Código sob licença MIT. Os datasets usados têm licença própria, registrada neste repositório.
