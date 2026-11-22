# 🚀 Lumi 4B Fine-Tuning — CEIA-BR Competition

Repositório da equipe para a competição de fine-tuning do modelo **CEIA-BR Lumi 4B** (`ceia-research/lumi-4b`).

## 👥 Equipe

- [Rodolfo Zion Ruthes Brito](https://github.com/rodolfozion1719)
- [Mouhamed Jamal Jomaa](https://github.com/mouhamedjj2008-oss)
- [José Daniel Rodrigues de Melo ](https://github.com/jdrmprofissional08-hue)

## ⚖️ Regras que o projeto segue

- Modelo base fixo: Lumi 4B. Não substituir por outro modelo.
- `enable_thinking=False` no treino e na inferência.
- Usar o chat template nativo do tokenizer (`apply_chat_template`).
- Não usar nem tentar reconstruir o conjunto de teste privado.
- Datasets externos e sintéticos: registrar a fonte e confirmar que a licença permite uso e redistribuição.
- Repositório público e modelo final público no Hugging Face.

## 📌 Visão Geral
- **Modelo Base:** `ceia-research/lumi-4b`
- **Técnica:** QLoRA / LoRA (PEFT)
- **Métrica Alvo:** F1-Score
- **Checkpoint Hugging Face:** *[Em treinamento — link será disponibilizado após a submissão final]*

## 🔗 Links

- Modelo base: https://huggingface.co/ceia-research/lumi-4b *(confirmar o ID com a organização)*
- Documentação do SFTTrainer (TRL): https://huggingface.co/docs/trl/sft_trainer
- Competição e leaderboard no Kaggle: [LINK]
- Modelo final no Hugging Face: [em breve]
- Adaptador LoRA no Hugging Face: [em breve]

## ⚙️ Configuração do Ambiente

```bash
python -m venv .venv
source .venv/bin/activate  # ou .venv\Scripts\activate no Windows
pip install -r requirements.txt
