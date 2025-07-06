# Sample Outputs and Examples

## Real-World Test Cases

### Example 1: OCR Error Correction
**Challenge**: Multiple OCR scanning errors from document processing

**Input:**
```
Cheesegrater, I2Z Leadenhall St London 4O storeys, steel structure; completion 2104
```

**Output (ChatGPT-o3):**
| Property Name | Address | Occupancy (ISIC) | Lat, Lon | Stories AG(BG) | Year Built | Construction Material | Confidence |
|---|---|---|---|---|---|---|---|
| The Leadenhall Building ("Cheesegrater") | 122 Leadenhall Street, London EC3V 4AB | 7010 – Head-office offices [High] | 51.5138, -0.0821 | 48 | 2014 | Steel megaframe & glass curtain wall | [Medium] |

**Auto-corrections made:**
- ❌ "I2Z" → ✅ "122" (OCR character recognition fix)
- ❌ "4O storeys" → ✅ "48 storeys" (OCR number fix)
- ❌ "2104" → ✅ "2014" (logical year correction)
- ✅ Added complete postal address and coordinates
- ⚠️ Story count conflict flagged (CTBUH: 47 vs Wikipedia: 48)

---

### Example 2: Brand Mismatch Detection
**Challenge**: Input contains incorrect brand/business type

**Input:**
```
The Fenchurch Building (The Walkie-Talkie), 20 Fenchurch St, London EC3M 8AF, United Kingdom Hotel
```

**Output (ChatGPT-o3):**
| Property Name | Address | Occupancy (ISIC) | Lat, Lon | Stories AG(BG) | Year Built | Construction Material | Confidence |
|---|---|---|---|---|---|---|---|
| 20 Fenchurch Street (The Fenchurch Building) | 20 Fenchurch Street, London EC3M 8AF | 7010 – Head-office offices [High] | 51.511389, -0.083611 | 36 (2) | 2014 | Concrete-Steel composite | [Medium] |

**Key corrections:**
- ❌ Input claimed "Hotel" → ✅ Correctly identified as "Head-office offices"
- ✅ Completed address formatting
- ✅ Added basement levels, construction details, precise coordinates

---

### Example 3: Missing Business Name Inference
**Challenge**: Anonymous address with only occupancy hint

**Input:**
```
–, 757 N Michigan Ave, Chicago, IL 60611, pharmacy
```

**Output (Grok-3):**
| Property Name | Address | Occupancy (ISIC) | Lat, Lon | Stories AG(BG) | Year Built | Construction Material | Confidence |
|---|---|---|---|---|---|---|---|
| Walgreens | 757 N Michigan Ave, Chicago, IL 60611 | 4772 – Retail sale of pharmaceuticals [High] | 41.8956, -87.6238 | 38(0) | 1964 | Concrete, Steel Frame | [High] |

**Intelligence added:**
- ✅ Inferred business name from location + occupancy
- ✅ Identified mixed-use building (38-story with retail at ground level)
- ✅ Added historical construction data

---

### Example 4: Coordinates-Only Input
**Challenge**: Only latitude/longitude provided with minimal context

**Input:**
```
47.6062, -122.3301
```

**Output (Claude Opus):**
| Property Name | Address | Occupancy (ISIC) | Lat, Lon | Stories AG(BG) | Year Built | Construction Material | Confidence |
|---|---|---|---|---|---|---|---|
| Renaissance Seattle Hotel | 515 Madison St, Seattle, WA 98104 | 5510 – Hotels [High] | 47.6066, -122.3317 | 28(0) | 1983 | Concrete, Steel | [High] |

**Reverse geocoding success:**
- ✅ Identified specific business from coordinates
- ✅ Provided complete address
- ✅ Added comprehensive building details
- ⚠️ Minor coordinate adjustment noted

---

### Example 5: Industrial Facility Classification
**Challenge**: Complex industrial facility requiring specialized classification

**Input:**
```
Tesla Gigafactory, 1 Electric Ave, Sparks NV 89434, battery mfg
```

**Output (Gemini-2.5 Pro):**
| Property Name | Address | Occupancy (ISIC) | Lat, Lon | Stories AG(BG) | Year Built | Construction Material | Confidence |
|---|---|---|---|---|---|---|---|
| Tesla Gigafactory Nevada | 1 Electric Ave, Sparks, NV 89434 | 2720 – Manufacture of batteries [High] | 39.5357, -119.4399 | | 2017 | N/A - Industrial Facility | [High] |

**Industrial handling:**
- ✅ Correct ISIC manufacturing classification
- ✅ Precise coordinates for large facility
- ✅ Appropriate "N/A - Industrial Facility" construction classification
- ✅ Accurate completion date

---

### Example 6: International Address Processing
**Challenge**: Non-English address with different formatting conventions

**Input:**
```
ASML HQ, De Run 6501, 5504 DR Veldhoven, NL, semiconductor mfg
```

**Output (DeepSeek-DeepThink):**
| Property Name | Address | Occupancy (ISIC) | Lat, Lon | Stories AG(BG) | Year Built | Construction Material | Confidence |
|---|---|---|---|---|---|---|---|
| ASML Headquarters | De Run 6501, 5504 DR Veldhoven | 2610 – Manufacture of semiconductors [High] | 51.4104, 5.4576 | 4(0) | 2003 | Steel, Concrete | [High] |

**International processing:**
- ✅ Handled Dutch address formatting
- ✅ Correct high-tech manufacturing classification
- ✅ Corporate headquarters identification
- ✅ European construction standards applied

---

## Performance Comparison Summary

| Test Case | ChatGPT-o3 | Claude Opus | Grok-3 | Gemini Pro | DeepSeek |
|-----------|------------|-------------|--------|------------|----------|
| OCR Correction | ✅ Excellent | ❌ Missed errors | ✅ Good | ✅ Very Good | ⚠️ Partial |
| Brand Mismatch | ✅ Perfect | ❌ False positive | ✅ Good | ✅ Good | ✅ Good |
| Name Inference | ✅ Good | ⚠️ Conservative | ✅ Excellent | ✅ Good | ⚠️ Limited |
| Coordinates-Only | ✅ Good | ✅ Excellent | ✅ Good | ✅ Very Good | ✅ Good |
| Industrial Classification | ✅ Good | ✅ Good | ✅ Good | ✅ Excellent | ✅ Good |
| International Addresses | ✅ Good | ✅ Good | ✅ Good | ✅ Good | ✅ Excellent |

## Common Patterns and Insights

### What Works Well Across All Models:
- Standard address validation and formatting
- Basic ISIC occupancy classification
- Corporate vs operational site distinction
- Coordinate validation and precision scoring

### Model-Specific Strengths:
- **ChatGPT-o3**: Complex real estate validation, brand discrepancy detection
- **Claude Opus**: Conservative verification, specialized classifications
- **Grok-3**: Business status detection, comprehensive error correction
- **Gemini Pro**: Format handling, industrial facility classification
- **DeepSeek**: International addresses, cost-effective processing

### Common Limitations:
- Regional data coverage varies significantly
- Business closure detection inconsistent
- Some coordinate conflicts not flagged
- Construction material inference often limited

### Best Practices for Users:
1. **Use multiple models** for critical validations
2. **Review flagged entries** manually
3. **Combine with premium APIs** for enhanced accuracy
4. **Test with your specific geographic region** before deployment
5. **Validate against known ground truth** for quality assurance