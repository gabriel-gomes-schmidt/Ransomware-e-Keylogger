# Ransomware-e-Keylogger
# Malware Lab — Projeto Educacional (Ransomware & Keylogger — Simulados)

**Descrição curta:**  
Repositório educacional que demonstra, de forma segura e controlada, como funcionam dois vetores de ameaça comuns — *ransomware* e *keylogger* — usando **simulações** em Python sobre arquivos gerados localmente. O objetivo é aprender comportamento, técnicas de detecção e medidas de defesa, sem riscos para dados reais.

---

## ⚠️ Aviso de Ética e Segurança (LEIA ANTES)
- Este projeto é **estritamente educacional** e **NÃO** deve ser executado em máquinas de produção, em sistemas com dados reais, ou em redes públicas.  
- **Não há** neste repositório código para capturar teclas do sistema real, para exfiltrar dados por rede, ou para propagar malware. Todas as ações são executadas somente sobre arquivos gerados localmente na pasta `sandbox_test_files/`.  
- Ao utilizar este repositório você se compromete a executar os testes apenas em ambientes isolados (VMs, containers ou máquinas de laboratório).

---

## Objetivos do projeto
- Simular o comportamento de criptografia em massa (ransomware) sobre arquivos de teste.
- Simular a captura e registro de entradas (keylogger) usando um arquivo de entrada simulado.
- Implementar medidas de segurança e detecção: snapshot de integridade (hashes), regra YARA exemplificativa e documentação de defesa.
- Documentar procedimentos, evidências e recomendações de defesa para um relatório de segurança.

---

## Estrutura do repositório (sugerida)
draconic-malware-lab/
├─ README.md # (este arquivo)
├─ requirements.txt
├─ .gitignore
├─ /sandbox_test_files/ # arquivos gerados pelos scripts (sandbox)
├─ /scripts/
│ ├─ util_helpers.py
│ ├─ gerar_arquivos_teste.py
│ ├─ simulador_ransom_safe.py
│ ├─ simulador_keylogger_safe.py
│ └─ scanner_deteccao.py
├─ /docs/
│ ├─ defensas.md
│ └─ yara_exemplo.yar
└─ /images/ # (opcional) prints para evidências

yaml
Copiar código

---

## Dependências
- Python 3.8 ou superior  
Instale dependências:
```bash
python -m venv .venv
# macOS / Linux
source .venv/bin/activate
# Windows (PowerShell)
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
requirements.txt mínimo:

shell
Copiar código
cryptography>=3.4.7
Passo a passo (fluxo de uso recomendado)
Gerar arquivos de teste (sandbox)
Gera textos e um arquivo binário que serão usados nas simulações.

bash
Copiar código
python scripts/gerar_arquivos_teste.py
Criar snapshot de baseline (hashes)
Registra hashes dos arquivos em sandbox_test_files/.hashes para detectar alterações posteriores.

bash
Copiar código
python scripts/scanner_deteccao.py snapshot
Simular keylogger (com entrada simulada)
O script lê simulated_input.txt (gerado no sandbox) e grava captura_log.txt com timestamps. Não lê o teclado do sistema.

bash
Copiar código
python scripts/simulador_keylogger_safe.py
Simular criptografia (ransomware simulado)
Opera apenas sobre sandbox_test_files/. O script salva/usa uma chave local dentro do sandbox e exige confirmação textual (CONFIRMAR) antes de prosseguir.

bash
Copiar código
python scripts/simulador_ransom_safe.py --encrypt
Detectar alterações com o scanner
Compara os hashes atuais com o baseline e reporta arquivos novos/modificados.

bash
Copiar código
python scripts/scanner_deteccao.py
Descriptografar (restaurar)
Reverte a criptografia usando a chave salva no sandbox.

bash
Copiar código
python scripts/simulador_ransom_safe.py --decrypt
O que entregar (para avaliação / portfólio)
No botão "Entregar Projeto" do curso, inclua:

Link do repositório público no GitHub (ex.: https://github.com/seuusuario/draconic-malware-lab)

Breve descrição (2–4 linhas) do que foi feito.

Comandos executados (cole os comandos usados, ex. os listados acima).

Evidências (coloque imagens em /images/):

Saída de gerar_arquivos_teste.py

Conteúdo de sandbox_test_files/ após geração

Saída do simulador_keylogger_safe.py (ex.: trecho do captura_log.txt)

Saída antes/depois do simulador_ransom_safe.py --encrypt e da descriptografia

Saída do scanner_deteccao.py antes e depois da simulação

Checklist de segurança / avaliação (use para autoteste)
 Todos os scripts operam somente em sandbox_test_files/.

 O repositório contém README.md detalhado (este).

 Há instruções claras para instalar dependências.

 Há um snapshot de baseline (hashes) e comandos para detectar alterações.

 Scripts pedem confirmação antes de executar ações destrutivas (ex.: criptografar).

 docs/defensas.md contém medidas de mitigação e resposta.

 Não existem funções de exfiltração (envio por rede) ou captura de hardware real.

Boas práticas e recomendações (resumo)
Execute testes em máquinas isoladas (VMs revertíveis ou containers).

Mantenha backups offline e testados (estratégia 3-2-1).

Use MFA e gerenciadores de senha — não armazene senhas em texto.

Implemente EDR/monitoramento de integridade (hashes) e regras YARA para identificar artefatos.

Treine usuários contra phishing e anexos suspeitos.
