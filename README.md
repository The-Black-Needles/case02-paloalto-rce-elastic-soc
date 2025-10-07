# case02 – PaloAlto RCE (ELK | SOC | DFIR-lite)

Este repositório implementa um pipeline defensivo para um incidente simulado de **RCE em firewalls Palo Alto** (CVE-like), usando **Elasticsearch + Kibana** para caça, detecção e narrativa executiva.

## Objetivos
- Montar ambiente local (ELK) e ingerir **logs brutos** do lab.
- Criar **detecções** (KQL/DSL) e **hunting** para responder:
  - Q1: IP do primeiro agente de ameaça.
  - Q2: Data/hora (UTC) da primeira interação.
  - Q3: Comando usado para **persistência**.
  - Q4: Primeira **porta** de shell reverso.
  - Q5: Nome do **arquivo** tentado para exfiltração.
  - Q6: **URL** completo de exfil realizada com sucesso.
- Produzir **artefatos reprodutíveis** (CSVs) e **relatório executivo**.

## Estrutura  

```case02-paloalto-rce-elastic-soc/
├─ README.md
├─ data/
│ └─ raw/ # logs do lab (NDJSON/CSV) — NÃO versionar
├─ detections/ # consultas KQL/DSL por regra (R1..R6)
├─ scripts/ # ingestão, hunting, enriquecimento
├─ reports/
│ ├─ alerts/ # CSVs por regra + consolidado
│ └─ IR_PaloAltoRCE.md # relatório final
└─ tests/ # amostras mínimas p/ validar regras```

## Como rodar (visão geral)
1) Subir ELK (docker compose).  
2) Ingerir `data/raw/*.ndjson` em `paloalto-lab`.  
3) Explorar campos no Kibana (Discover).  
4) Rodar detecções (KQL) + `scripts/hunt.py` → CSVs em `reports/alerts/`.  
5) Correlacionar timeline e preencher `reports/IR_PaloAltoRCE.md`.

> **Aviso**: `data/raw/*` está no `.gitignore` para evitar subir dados reais.
