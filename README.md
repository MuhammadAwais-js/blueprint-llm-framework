# JSON-Grounded Multimodal LLM Framework for Automated Construction Blueprint Analysis

This repository contains the supplementary materials for the paper:

**"JSON-Grounded Multimodal LLM Framework for Automated Construction Blueprint Analysis with Cost-Optimized Batch Processing"**

Muhammad Awais Arshad and Minsoo Baek
Department of Software Engineering & Department of Construction and Engineering
Kennesaw State University

## Overview

This framework addresses LLM hallucination in construction blueprint analysis by pairing each blueprint image with a structured JSON "digital twin" containing four extraction layers (vector text, raster OCR, geometric paths, structural lines). A four-tier token pruning strategy reduces API costs by 52-61% while maintaining 99.2-100% factual accuracy.

## Repository Structure

```
├── prompts/                    # Full prompt texts for both project types
│   ├── bridge_project_prompt.txt
│   └── interchange_project_prompt.txt
├── code/                       # Pipeline notebooks (Google Colab compatible)
│   ├── Task1_PDF_to_IMG_JSON_Extraction.ipynb
│   ├── Task2_Vector_Validation_Overlay.ipynb
│   ├── Task3_NonOptimized_BatchAnalysis.ipynb
│   ├── Task4_CostOptimized_BatchAnalysis.ipynb
│   └── AccuracyEvaluation.ipynb
├── sample_outputs/             # Complete LLM analysis outputs (.md)
│   ├── bridge_nonoptimized_output.md
│   ├── bridge_optimized_output.md
│   ├── interchange_nonoptimized_output.md
│   └── interchange_optimized_output.md
├── accuracy_results/           # Aggregate evaluation metrics (.csv)
│   ├── bridge_nonoptimized_aggregate_metrics.csv
│   ├── bridge_optimized_aggregate_metrics.csv
│   ├── interchange_nonoptimized_aggregate_metrics.csv
│   └── interchange_optimized_aggregate_metrics.csv
├── sample_json/                # Example Task 1 JSON extractions
│   └── (2-3 sample JSON files showing four-layer structure)
├── figures/                    # Paper figures
│   ├── pipeline_architecture.pdf
│   ├── validation_overlay.png
│   └── pruning_tiers.pdf
└── README.md
```

## Datasets

Two GDOT transportation plan sets were used for evaluation:

| Project | Type | County | P.I. No. | Sheets |
|---------|------|--------|----------|--------|
| CS 1081/Greenville St @ CSX | Bridge Replacement | Troup | 343455 | 15 |
| I-285 at SR 400 | Highway Interchange | Fulton | 0013142 | 29 |

GDOT plan sets are publicly accessible through the Georgia Department of Transportation's plan records.

## Key Results

| Experiment | Sheets | VPR | SAA | Hallucination Rate | Total Cost |
|-----------|--------|-----|-----|--------------------|------------|
| Bridge Non-Optimized | 15 | 100.0% | 100.0% | 0.0% | $1.773 |
| Bridge Cost-Optimized | 15 | 100.0% | 98.5% | 0.0% | $0.731 |
| Interchange Non-Optimized | 28 | 99.2% | 98.3% | 0.8% | $2.991 |
| Interchange Cost-Optimized | 29 | 99.6% | 99.2% | 0.4% | $1.429 |

- **VPR (Value Presence Rate):** Percentage of Vector/OCR-tagged values verifiable in JSON ground truth
- **SAA (Source Attribution Accuracy):** Percentage of values found in the correct claimed source layer
- **Cost Optimization:** 52-61% reduction in input token consumption with equivalent output quality

## Model

All experiments used **Google Gemini 3 Flash Preview** (`gemini-3-flash-preview`) at $0.50 per 1M input tokens and $3.00 per 1M output tokens.

## Requirements

The notebooks are designed for Google Colab. Key dependencies:

- Python 3.10+
- PyMuPDF (fitz)
- EasyOCR
- OpenCV (cv2)
- Google Generative AI SDK (`google-generativeai`)
- fuzzywuzzy (for accuracy evaluation)

A valid Google Generative AI API key is required for Tasks 3 and 4. Set it as an environment variable or Colab secret.

## Citation

If you use this framework or reference these results, please cite:

```bibtex
@article{arshad2026blueprint,
  title={JSON-Grounded Multimodal LLM Framework for Automated Construction Blueprint Analysis with Cost-Optimized Batch Processing},
  author={Arshad, Muhammad Awais and Baek, Minsoo},
  year={2026},
  institution={Kennesaw State University}
}
```

## License

This project is licensed under the MIT License.

## Contact

- Muhammad Awais Arshad: marshad2@students.kennesaw.edu
- Minsoo Baek: mbaek@kennesaw.edu
