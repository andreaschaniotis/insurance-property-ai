# Insurance Property Location Risk Classification System v7.7

**Production-Grade Prompt System for Property Intelligence**  
*By Andreas Chaniotis — CC BY 4.0 License*

## TL;DR
Transform messy property data into insurance-ready intelligence using only free sources. 
**Input:** "Cheesegrater, I2Z Leadenhall St London 4O storeys, completion 2104"  
**Output:** Corrected address, ISIC codes, coordinates, construction details with confidence scores.  
Zero training required. Works with any LLM.

---

## 🔍 Overview
A next-generation AI-driven classification engine that transforms minimal property input—business name, loose address, or coordinates—into fully structured, audit-ready property risk intelligence. Powered by free, open-licensed data sources and advanced prompt engineering logic.

Built entirely in free time and tested across 14 LLMs, delivering 21 enriched fields with robust fallback logic and conflict-aware outputs for commercial and industrial property profiling.

## Why This Matters
✅ **Instant data cleanup**: Fix OCR errors, typos, standardize formats, validate addresses  
✅ **Free enrichment**: Add missing occupancy, coordinates, construction details using only open sources  
✅ **Enterprise ready**: Confidence scores, source attribution, full audit trails  
✅ **Zero setup**: No training, APIs, or subscriptions required  
✅ **Modular design**: Use standalone or integrate with existing workflows

---

## 🚀 Quick Start
1. Copy the full v7.7 prompt from this repository
2. Input your property data in any format: `Business Name | Address | Occupancy`
3. Run on GPT-4o, Claude, or DeepSeek with markdown output
4. Review the markdown table—each field has confidence scoring
5. Filter flagged/conflict entries for manual review

## Example Input/Output

**Input:** `"Cheesegrater, I2Z Leadenhall St London 4O storeys, completion 2104"`

**Output:**
| Property Name | Address | Occupancy (ISIC) | Lat, Lon | Stories | Year | Construction | Confidence |
|---|---|---|---|---|---|---|---|
| The Leadenhall Building | 122 Leadenhall Street, London EC3V 4AB | 7010 - Head offices | 51.5138, -0.0821 | 48 | 2014 | Steel megaframe & glass | [Medium] |

**Auto-corrections made:**
- ❌ "I2Z" → ✅ "122" (OCR fix)
- ❌ "4O storeys" → ✅ "48 storeys" (OCR fix)  
- ❌ "2104" → ✅ "2014" (year correction)
- ✅ Added full postal address, coordinates, detailed construction specs
- ⚠️ Story count conflict flagged (CTBUH: 47 vs Wikipedia: 48)

*Full output includes 21 fields with source attribution*

---

## 📊 Tested Performance
- **14 LLMs tested** on 50 challenging properties with known validation points
- **Top performers**: 
  - 🥇 Gemini-2.5 Pro (via Perplexity): 87%
  - 🥈 ChatGPT-o3: 83% 
  - 🥉 DeepSeek-DeepThink: 80%
- **Address correction**: 6/6 errors caught by best models (IKEA, Best Buy ZIP, Wegmans OCR, etc.)
- **OCR cleanup**: Handles I→1, O→8, merged ZIP codes, typos
- **Geographic coverage**: Strongest in Europe/NA (80-90% [High] fields), moderate elsewhere

## 🧠 Key Capabilities

| Feature | Description |
|---------|-------------|
| 🏠 **Multi-source Address Validation** | Dual geocoder logic with conflict flags, typo repair, confidence scoring |
| 🏢 **ISIC Occupancy Classification** | OSM, OpenCorporates, Wikidata-based mapping with dual-class fallback |
| 📍 **Coordinate Precision** | Verified coordinates with geographic delta checks and bounds |
| 🧱 **Construction Intelligence** | Stories, materials, construction year with fallback inference |
| 🌍 **Hazard Score Integration** | FEMA, USGS, UNISDR exposure enrichment (when available) |
| 📊 **Confidence Calibration** | Per-field scoring: [High], [Medium], [Low], or blank |
| 🚩 **Quality Flags** | Auto-generated: CONFLICT, INFERRED, CORRECTED, VERIFICATION_REQUIRED |
| ⚙️ **Slim-Mode Auto-Switch** | Reduces output fields if LLM token limits detected |

---

## 🤖 LLM Compatibility

**✅ Recommended**: GPT-4o, Claude Sonnet 4, DeepSeek V3, Gemini-2.5 Pro  
**⚠️ Budget options**: Use Slim Mode for smaller models  
**📊 Performance varies**: See full testing matrix in `/docs/model-performance.md`

**Requirements**: 8k-32k tokens, markdown formatting support

---

## 🧩 Business Integration Scenarios

- **🔍 Pre-screening**: Bulk SOV enrichment before commercial rating
- **🏛️ Compliance**: Full source traceability, free data licensing
- **⚙️ API Layer**: Modular pipeline with slim-mode fallback  
- **🧮 Portfolio Insights**: Risk modeling + hazard exposure tags
- **💼 Manual Triage**: Flag [Low] or CONFLICT entries for review
- **📊 Legacy Enhancement**: Enrich historical submissions for better modeling

---

## 📋 Confidence & Quality System

### Confidence Levels
| Level | Criteria |
|-------|----------|
| **[High]** | 2+ reliable external sources agree |
| **[Medium]** | 1 trusted source or multiple secondary |
| **[Low]** | Single source, inference, or partial agreement |
| **Blank** | No reliable match or conflict detected |

### Quality Flags
- `VERIFIED` – Multi-source confirmation
- `INPUT_CORRECTED` – Fixed OCR errors, typos, formatting
- `CONFLICT` – Source disagreement detected
- `INFERRED` – Fallback logic or era-based estimation
- `DUAL_OCCUPANCY` – Multiple valid ISIC codes
- `VERIFICATION_REQUIRED` – Manual review recommended

---

## 🔧 Technical Architecture

```
1. INPUT: Business Name, Address, or Coordinates
2. CLEAN: OCR cleanup, typo fixes, format parsing
3. VALIDATE: Dual geocoders + confidence rules
4. CLASSIFY: ISIC mapping from OSM + registries  
5. ENRICH: Add coordinates, construction, hazard data
6. SCORE: Per-field confidence + quality flags
7. OUTPUT: Markdown table, 21 fields, silent execution
```

**Data Sources**: OSM, Wikidata, OpenCorporates, GeoNames, FEMA, USGS (all free/open)

---

## ⚠️ Known Limitations

- **Geographic coverage**: Strongest in Europe/North America, weaker in rural/developing regions
- **Language support**: Optimized for English, limited non-Latin script support  
- **Industrial facilities**: May lack detailed construction data for specialized facilities
- **Real-time data**: No live business status updates (closures, relocations)
- **LLM dependency**: Results quality varies significantly by model choice

---

## 📚 License & Attribution

**Creative Commons Attribution 4.0 International (CC BY 4.0)**

You are free to:
- ✅ **Share** — copy and redistribute in any medium or format
- ✅ **Adapt** — remix, transform, build upon for any purpose, including commercial

**Required attribution:**  
*"Insurance Property Location Risk Classification System v7.7 by Andreas Chaniotis — CC BY 4.0"*

---

## 🤝 Contributing & Feedback

Built entirely in **free time** using personal API costs. Community feedback drives improvements:

- **Issues**: Report bugs, edge cases, or regional data gaps
- **Enhancements**: Suggest new fields, data sources, or validation rules  
- **Testing**: Share results from your region or use case
- **Integration**: Document your workflow integrations

**Contact**: LinkedIn [@AndreasChanniotis] | **System Version**: v7.7

---

## ⚠️ Disclaimer

This is a proof-of-concept system built for education and prototyping. Results require human review for high-value or regulatory use. Not affiliated with any insurer, reinsurer, or commercial provider. Use at your own risk—results may vary by LLM and input format.

---

*"GenAI is powerful—but like Python or SQL, its real value lies in what you build with it."*  
— Andreas Chaniotis