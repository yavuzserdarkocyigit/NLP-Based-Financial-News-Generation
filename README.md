# 📈 NLP-Based News Generation from Turkish Financial Reports 🇹🇷

This project aims to automate the generation of news-style summaries from official Turkish financial disclosures, such as KAP (Public Disclosure Platform) reports. By leveraging state-of-the-art transformer-based models, we convert regulatory financial documents into accessible, journalistic summaries for retail investors.

## Project Overview

- **Goal**: Transform formal Turkish financial statements into concise and readable news articles.
- **Domain**: Turkish Capital Markets (Borsa İstanbul - KAP Reports)
- **Techniques Used**: Abstractive summarization, style transfer, sentiment injection
- **Language**: Turkish

## Models Fine-Tuned

We experimented with the following transformer architectures:

| Model Variant               | Description                                                                 |
|----------------------------|-----------------------------------------------------------------------------|
| `ozcangundes/mt5-small`     | Turkish-specialized mT5 for news summarization                             |
| `csebuetnlp/mT5-multilingual-XLSum` | Multilingual model trained on BBC XLSum dataset                          |
| `facebook/mbart-large-cc25` | Pretrained multilingual model across 25 languages                         |
| Custom Transformer          | Encoder-decoder trained from scratch (used for comparison)                |

## Dataset

- **Size**: 400 KAP report-summary pairs
- **Structure**:
  - Column 1: Full KAP disclosure (in Turkish)
  - Column 2: Human-written journalistic summary

All data samples include both factual content and interpretive commentary.

## Methodology

- Tokenizer: Model-specific (MT5Tokenizer / MBartTokenizer)
- Summarization Prompt: `"haberleştir: <KAP report text>"`
- Sequence Lengths: 
  - Input max: 512 tokens  
  - Output max: 128–256 tokens
- Training Techniques:
  - Beam Search (`num_beams=4`)
  - Repetition and length penalties
  - Early stopping and gradient clipping
  - Epochs: 40–50
  - Batch size: 4–8
  - Optimizer: AdamW

## Key Findings

- All models successfully adapted to financial tone and style.
- `mT5-small` yielded the most fluent summaries.
- `mbart-large-cc25` showed strong stylistic alignment.
- **Challenge**: Models hallucinate numerical values — a known limitation in low-resource numeric domains.

