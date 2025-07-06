# Testing Methodology

## Overview
The Insurance Property Location Risk Classification System v7.7 underwent comprehensive testing across 14 different Large Language Models using a carefully designed validation dataset.

## Test Dataset Design

### 50-Location Validation Set
The test dataset was specifically designed to challenge different aspects of the classification system:

#### Geographic Distribution
- **🇺🇸 United States**: 37 locations (74%) - Primary test market
- **🇪🇺 Europe**: 6 locations (12%) - UK, France, Germany, Netherlands, Sweden, Switzerland
- **🌏 Asia-Pacific**: 2 locations (4%) - Japan, Australia  
- **🇨🇦 North America**: 1 location (2%) - Canada
- **🌍 Coordinates-only**: 4 locations (8%) - Geographic inference testing

#### Business Category Coverage
- **Retail General**: 15 locations (Target, Nordstrom, Gap, etc.)
- **Grocery/Food**: 8 locations (Whole Foods, Trader Joe's, etc.)
- **Industrial Manufacturing**: 4 locations (ExxonMobil, Boeing, Tesla, Nucor)
- **Technology/Electronics**: 3 locations (ASML, RadioShack, Berlin Electronics)
- **Healthcare/Pharmacy**: 2 locations (CVS locations)
- **Financial Services**: 1 location (Chase Bank)
- **Hospitality**: 2 locations (Marriott, Renaissance)
- **Fitness/Recreation**: 2 locations (REI, Planet Fitness)
- **Office/Coworking**: 1 location (WeWork)

#### Input Format Complexity
- **Complete Data**: 20 locations - Full name, address, occupancy
- **Missing Occupancy**: 15 locations - Business name inference required
- **Missing Names**: 3 locations - Reverse business lookup needed
- **Coordinates Only**: 3 locations - Geographic inference testing
- **Minimal Data**: 4 locations - Extreme challenge scenarios
- **Format Errors**: 5 locations - OCR and typo correction testing

## Validation Challenges

### Level 1: Standard Challenges
- **IKEA Renton**: Address correction test (600→601 SW 41st St)
- **Marriott Courtyard**: Brand mismatch validation (real property is The Bellevue Hotel)
- **Westfield Mall**: Multi-occupancy detection
- **Carrefour Hypermarket**: International address parsing

### Level 2: Moderate Challenges  
- **McDonald's Corporate**: Distinguish headquarters vs restaurant
- **Best Buy Store**: ZIP code error correction (94019→94109)
- **Renaissance Seattle**: Coordinate-only input with potential conflicts
- **Starbucks Roastery**: Processing facility vs standard café classification

### Level 3: Geographic & Format Challenges
- **Whole Foods**: Missing comma in address parsing
- **Swiss Shopping Mall**: Missing property name inference
- **CVS Pharmacy**: Missing business name identification
- **Sephora Broadway**: Incomplete address completion

### Level 4: International Challenges
- **Tesco Express**: UK postcode handling
- **Canadian Tire**: Canadian postal code formatting
- **Berlin Electronics**: German address + business inference
- **ASML HQ**: Dutch address + high-tech classification

### Level 5: Asia-Pacific Challenges
- **Uniqlo Ginza**: Japanese address formatting
- **Woolworths Metro**: Australian address handling
- **H&M Stockholm**: Swedish address processing

### Level 6: Industrial & Complex Facilities
- **ExxonMobil Refinery**: Heavy industrial classification
- **Boeing Factory**: Aerospace manufacturing
- **Tesla Gigafactory**: Battery manufacturing + coordinate validation
- **Nucor Steel**: Steel manufacturing

### Level 7: Missing Occupancy & Error Correction
- **RadioShack Denton**: Business closure detection
- **Wegmans**: OCR error correction (1444S→14445)
- **Kroger**: City name typo correction

### Level 8: Extreme Minimal Data
- **Copper Mountain Solar**: Facility name + state only
- **Camping Store**: Coordinates only
- **H-E-B**: City typo + minimal data

## Testing Protocol

### Model Selection
14 LLMs tested representing different:
- **Model families**: GPT, Claude, Gemini, DeepSeek, Grok, QWEN
- **Size categories**: From lightweight (Mini) to largest available
- **Access methods**: Direct API, web interfaces, specialized platforms
- **Cost tiers**: Free, standard, premium pricing models

### Pre-Testing Protocol

#### Memory State Management
Before each model test, a standardized memory cleaning protocol was applied:

1. **Memory Audit**: Custom prompt v2.6 used to assess context state
2. **Context Clearing**: Complete conversation history cleared using specialized memory management commands
3. **Fresh Session**: New session initiated for each model test
4. **Baseline Confirmation**: Verified clean starting state before v7.7 prompt injection

This ensures:
- **No cross-contamination** between model tests
- **Consistent starting conditions** across all 14 LLMs
- **Elimination of context bias** from previous interactions
- **Reproducible testing environment**

#### Memory Cleaning Prompt
A specialized memory management prompt (v2.6) was developed to:
- Audit current context and token usage
- Identify redundant or outdated information  
- Compress or clean memory state as needed
- Provide structured summaries when required
- Execute "CLEAN" commands to reset context before testing

### Standardized Testing Process
1. **Memory Reset**: Applied memory cleaning protocol before each model
2. **Consistent Prompt**: Identical v7.7 prompt across all models
3. **Batch Processing**: Same 50-location dataset for each model
4. **Silent Execution**: No additional prompting or clarification
5. **Raw Output Capture**: Complete unedited responses recorded
6. **Multiple Validation**: Key tests repeated to verify consistency

### Scoring Methodology

#### Binary Validation Checks (30 total)
Each model evaluated on pass/fail basis for:

**Address Corrections (5 checks)**
- IKEA 600→601 correction
- Best Buy ZIP error fix
- Wegmans OCR correction
- City name typo corrections (2 instances)

**Format Handling (3 checks)**
- ZIP code spacing correction
- Address parsing with missing punctuation
- International postal code formatting

**Brand/Property Validation (1 check)**
- Marriott→Bellevue Hotel identification

**Missing Name Inference (4 checks)**
- Swiss shopping center identification
- Chicago pharmacy identification
- NYC department store identification
- Berlin electronics store identification

**Occupancy Classification (2 checks)**
- McDonald's HQ vs restaurant distinction
- Starbucks processing vs café classification

**Business Status Detection (1 check)**
- RadioShack closure identification

**Coordinate Validation (2 checks)**
- Renaissance Seattle coordinate handling
- Tesla Gigafactory coordinate accuracy

### Ground Truth Validation

All test validation points manually verified through:
- **Multiple independent sources**
- **On-site verification** where possible
- **Official business registries**
- **Government databases**
- **Authoritative mapping services**

#### Confirmed Validation Points
- **IKEA Renton**: Confirmed correct address is 601 SW 41st St
- **Marriott Test**: Confirmed 1415 Chancellor St is The Bellevue Hotel (Hyatt)
- **Tesla Gigafactory**: Confirmed coordinates 39.5357, -119.4399
- **RadioShack Denton**: Confirmed permanent closure
- **Wegmans ZIP**: Confirmed correct ZIP is 14445

## Quality Assurance

### Human Review Process
- **Double-checking**: All model outputs reviewed by domain expert
- **Bias Detection**: Systematic review for geographic or business type bias
- **Edge Case Analysis**: Special attention to unusual or borderline cases
- **Consistency Verification**: Cross-model comparison for validation

### Limitations Acknowledged
- **Geographic Bias**: Testing focused on English-speaking markets
- **Temporal Factors**: Business status may change between testing and use
- **Model Updates**: LLM performance may vary with version changes
- **Access Variations**: Some models accessed through different interfaces

### Future Testing Plans
- **Expanded Geographic Coverage**: More developing market properties
- **Industry Specialization**: Sector-specific property challenges  
- **Multilingual Testing**: Non-English address handling
- **Integration Testing**: Performance with premium data APIs
- **Longitudinal Studies**: Performance tracking over time

## Reproducibility

### Open Testing Framework
- **Dataset Available**: 50-location test set included in repository
- **Prompt Standardized**: v7.7 prompt publicly available
- **Methodology Documented**: Complete testing process described
- **Results Transparent**: Full model outputs included
- **Validation Criteria**: Clear pass/fail definitions provided

This testing methodology ensures reliable, reproducible evaluation of the classification system's performance across different AI models and use cases.