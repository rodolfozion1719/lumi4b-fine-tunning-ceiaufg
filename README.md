# 🚀 Lumi 4B: Fine-tuning (equipe AJCAT)

Repositório da equipe para a competição de fine-tuning do **CEIA-BR Lumi 4B**, promovida pela UFG.

> **Status:** em preparação. A tarefa, o dataset e a métrica oficial ainda não foram divulgados.

## 👥 Equipe

| Integrante | GitHub |
| :--- | :--- |
| Rodolfo Zion Ruthes Brito | [@rodolfozion1719](https://github.com/rodolfozion1719) |
| Mouhamed Jamal Jomaa | [@mouhamedjj2008-oss](https://github.com/mouhamedjj2008-oss) |
| José Daniel Rodrigues de Melo | [@jdrmprofissional08-hue](https://github.com/jdrmprofissional08-hue) |

## 📌 Visão geral

| Item | Detalhe |
| :--- | :--- |
| Modelo base | Lumi 4B (`ceia-research/lumi-4b`) |
| Arquitetura | Nemotron 3 Nano 4B, 4 bilhões de parâmetros, bilíngue PT-BR/EN |
| Técnica | LoRA / QLoRA (PEFT) |
| Métrica | F1-Score personalizado |
| Avaliação | Leaderboard público no Kaggle e avaliação final privada |
| Checkpoint no Hugging Face | *Em breve* |

## ⚖️ Regras que seguimos

| Regra | O que significa |
| :--- | :--- |
| Modelo base fixo | Partimos sempre do Lumi 4B. Não substituímos por outro. |
| Thinking desligado | `enable_thinking=False` no treino e na inferência. |
| Chat template nativo | Usamos o template do tokenizer (`apply_chat_template`). |
| Teste privado | Não usamos nem tentamos reconstruir o conjunto de teste oculto. |
| Dados externos e sintéticos | Registramos a fonte e confirmamos que a licença permite uso e redistribuição. |
| Entrega pública | Repositório no GitHub e modelo final no Hugging Face, ambos públicos. |

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
