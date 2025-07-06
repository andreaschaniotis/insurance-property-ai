# Model Performance Comparison

## Testing Methodology

The Insurance Property Location Risk Classification System v7.7 was tested across **14 different LLMs** using a standardized dataset of **50 challenging properties** with known validation points.

### Test Dataset Composition
- **Geographic coverage**: 9 countries, 13 business categories
- **Input formats**: Complete data, missing occupancy, coordinates-only, OCR errors
- **Challenge levels**: 8 difficulty levels from standard to extreme minimal data
- **Critical tests**: Address corrections, brand validation, occupancy classification, business status detection

## Performance Rankings

| Rank | Model | Score | Key Strengths | Notable Weaknesses |
|------|-------|-------|---------------|-------------------|
| 🥇 1st | **Gemini-2.5 Pro (via Perplexity)** | **87%** | Perfect address corrections, format handling | Some coordinate validation gaps |
| 🥈 2nd | **ChatGPT-o3** | **83%** | Excellent real estate validation, brand discrepancy detection | Missed some OCR errors |
| 🥉 3rd | **DeepSeek-DeepThink** | **80%** | Strong overall performance, good reasoning | Limited address correction capability |
| 4th | **Claude Opus 4** | **77%** | Conservative approach, good classification | False positive on fabrication test |
| 5th | **Grok-3** | **73%** | Best business closure detection, comprehensive error detection | Missed some specialized classifications |
| 6th | **Claude Sonnet 4** | **70%** | Excellent specialized classification (Starbucks processing) | Poor overall error detection |
| 6th | **Gemini-2.5 Flash** | **70%** | Good speed and basic accuracy | Limited complex reasoning |
| 6th | **Microsoft Copilot Free** | **70%** | Decent general performance | Limited advanced features |
| 9th | **DeepSeek V3** | **53%** | Cost-efficient option | Missed many validation tests |
| 10th | **QWEN-2.5 Max** | **57%** | Good for specific use cases | Inconsistent performance |
| 11th | **QWEN-3-32B** | **50%** | Large context handling | Limited accuracy on key tests |
| 12th | **QWEN-3-32B-Think** | **47%** | Reasoning mode available | Slower with mixed results |
| 13th | **ChatGPT-4.1** | **47%** | Standard GPT performance | Limited error detection |
| 14th | **ChatGPT-4.1 Mini** | **43%** | Lightweight option | Failed most critical tests |

## Key Test Categories

### Address Correction Success Rates
- **IKEA 600→601 correction**: 4/4 top models ✅
- **Best Buy ZIP correction**: 2/4 top models ✅
- **Wegmans OCR correction**: 1/4 top models ⚠️
- **Overall**: Significant variation in error detection capability

### Brand Validation Performance
- **Marriott→Bellevue Hotel test**: Only ChatGPT-o3 achieved perfect validation
- **Missing business names**: Top models successfully inferred 75%+ of cases
- **Occupancy disambiguation**: McDonald's HQ vs restaurant correctly identified by all top models

### Geographic Performance
- **Europe/North America**: 80-90% accuracy for top models
- **Asia-Pacific**: 40-60% accuracy (data coverage limitations)
- **Urban vs Rural**: Urban areas showed consistently better performance

## Recommendations by Use Case

### Production Insurance Workflows
**Recommended**: Gemini-2.5 Pro, ChatGPT-o3
- High accuracy on critical validation tasks
- Good error detection and correction
- Suitable for enterprise deployment

### Cost-Conscious Applications
**Recommended**: DeepSeek V3, QWEN models
- Lower per-token costs
- Acceptable accuracy for bulk processing
- Good for preliminary data cleanup

### Specialized Classification Tasks
**Recommended**: Claude Sonnet 4, Claude Opus 4
- Excellent for complex occupancy determination
- Conservative approach reduces false positives
- Best for high-stakes manual review workflows

### Research and Development
**Recommended**: Any model with access to reasoning modes
- DeepSeek-DeepThink for cost-effective experimentation
- Multiple model comparison for robustness testing

## Testing Infrastructure

All tests conducted using:
- **Consistent prompt**: Insurance Property Location Risk Classification System v7.7
- **Standard input**: 50-location validation dataset
- **Objective scoring**: Binary pass/fail on 30 validation checks
- **Multiple iterations**: Results verified across multiple runs
- **Human validation**: All ground truth points manually verified

## Limitations and Considerations

- **Model availability**: Some models may have limited API access
- **Cost variations**: Significant differences in per-token pricing
- **Geographic bias**: Testing focused on Western markets
- **Temporal factors**: Model performance may change with updates
- **Context limitations**: Some models may trigger slim-mode operation

## Future Testing Plans

- Expand geographic coverage to emerging markets
- Test multilingual capabilities
- Evaluate integration with premium data APIs
- Benchmark against commercial property intelligence services
- Assess performance on industry-specific property types