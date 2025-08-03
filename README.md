# 🧠 Keepa Parser Auditor — Campos Faltantes

Este repositório contém a estrutura e scripts para identificar campos ausentes, mal serializados ou com tipagem inválida no JSON unificado da API Keepa. O objetivo é criar um **parser inteligente**, com logs rastreáveis, múltiplas estratégias de fallback e validação de tipo, com apoio do Codex e GPT-4.

---

## 📁 Estrutura do Repositório

| Pasta / Arquivo            | Descrição                                                                 |
|---------------------------|---------------------------------------------------------------------------|
| `data/`                   | Contém o JSON unificado da Keepa e arquivos de entrada da API             |
| `logs/`                   | Logs de execução dos parsers                                              |
| `output/`                 | Arquivos CSV gerados com os campos extraídos                              |
| `scripts/`                | Scripts Python usados para análise dos campos                             |
| `docs/`                   | Documentação adicional (Markdowns, histórico de erros, prompts etc.)      |

---

## 🚧 Problemas Enfrentados

Mesmo com caminhos JSON corretos, os campos aparecem como "ausentes ou inválidos" devido a:

- Tipagem inconsistente (`"nan"` como string)
- Campos presentes como string vazia, null ou estrutura inesperada
- Erros silenciosos em listas/dicionários
- Fusão incorreta no JSON unificado
- Falta de fallback estruturado por bloco

---

## ✅ Status Atual (Exemplo de Campos)

| Campo                  | Status Esperado | Local Correto                                |
|-----------------------|------------------|-----------------------------------------------|
| `csvHeader`           | List OK          | `FULL → products[0] → csv → csvHeader`        |
| `buyBoxPriceHistory`  | List OK          | `BUYBOX_ONLY → products[0] → buyBoxPriceHistory` |
| `salesRankDrops90`    | Float ou nan     | `EXTRAS → products[0] → salesRankDrops90`     |
| `stockCSV`            | String           | `FULL → products[0] → csv → stockCSV`         |

---

## 🧪 Execução Local (PowerShell)

```powershell
# Caminho fixo do interpretador Python
$PythonExe = "C:\Imperio\AiPy\Python\python.exe"

# Script do parser (exemplo)
$ScriptPath = "C:\Imperio\KeepaMaster\Scripts\parser_keepa_MISSING_FIELDS__FINAL.py"

# Executar com log visível
& $PythonExe $ScriptPath
