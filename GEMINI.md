# Diretrizes do Projeto: Fine-Tuning Lumi 4B (Equipe AJCAT)

---

## 1. Arquiteto de Treinamento PEFT / QLoRA & VRAM Optimizer

### Papel
Engenheiro focado em eficiência computacional, prevenção de estouro de memória (CUDA OOM) e estabilidade de perda para o modelo CEIA-BR Lumi 4B (`ceia-research/lumi-4b`).

### Restrições
- Modelo base fixo: `ceia-research/lumi-4b`.
- Modo thinking desativado: `enable_thinking=False` no treino e na inferência.
- Chat template nativo via `tokenizer.apply_chat_template`.
- Hardware limitado: priorizar QLoRA (quantização em 4 bits via `bitsandbytes` NF4/FP4) ou LoRA leve; evitar full fine-tuning.

### Diretrizes
- Usar `transformers`, `accelerate`, `peft` (`LoraConfig`) e `trl` (`SFTTrainer`).
- Aplicar `gradient_accumulation_steps`, `per_device_train_batch_size` reduzido, `bf16`/`fp16` e `gradient_checkpointing`.
- Alterar apenas um hiperparâmetro por vez (`learning_rate`, `r`, `lora_alpha`, `lora_dropout`, `warmup_ratio`).

---

## 2. Engenheiro de Dados de PLN & Chat Template

### Papel
Engenheiro focado em limpeza de dados, formatação compatível com o modelo e maximização do F1-Score.

### Restrições e Regras de Dados
- Formatar exemplos estritamente com `tokenizer.apply_chat_template` e `enable_thinking=False`.
- Proibido usar ou tentar reconstruir o conjunto de teste oculto.
- Dados externos e sintéticos devem possuir licença compatível documentada.
- Não commitar dados brutos ou processados no Git (manter em `data/` ignorado no `.gitignore`).

### Diretrizes
- Criar pipeline modular em `src/preprocess.py` usando `pandas` e `datasets`.
- Tratar nulos, duplicatas, formatação de texto e inconsistências de rótulos.
- Garantir separação limpa entre treino e validação sem vazamento de dados.

---

## 3. Especialista em Avaliação, Pós-Processamento & F1-Score

### Papel
Cientista de dados focado em métricas quantitativas, inferência determinística e pós-processamento de saídas da LLM para submissões válidas.

### Contexto da Avaliação
- Métrica: F1-Score personalizado.
- Modo thinking: `enable_thinking=False` na inferência.

### Diretrizes
- Inferência determinística e reproduzível em `src/inference.py` (`temperature=0` / `do_sample=False`).
- Pós-processamento explícito com regex/parsers para limpar texto extra e padronizar o formato exato esperado pela avaliação.
- Validação local consistente em `src/evaluate.py`.
- Validar formato de colunas, IDs e ausência de `NaN` antes de gerar o arquivo final de submissão.

---

## 4. Engenheiro de Software & Reprodutibilidade (MLOps)

### Papel
Arquiteto de software focado em reprodutibilidade, modularidade do código e publicação de artefatos.

### Requisitos
- Código modular em `src/` (`preprocess.py`, `train.py`, `inference.py`, `evaluate.py`), `notebooks/` e configurações em YAML.
- Usar caminhos relativos via `pathlib.Path` e parâmetros configuráveis via `argparse` ou YAML.
- Manter segredos, credenciais e arquivos pesados fora do versionamento.
- Atualizar o `README.md` com instruções claras de instalação, execução e links para os pesos no Hugging Face.