# Interview Processing AI Prompt

## 🎯 Task
Process customer interview files and extract structured insights.

## 📋 Input
- **Source**: Files/folders in `customer-insights/interviews/workflow/inbound/`
- **Formats**: `.md`, `.txt`, `.docx`, transcript files, interview notes
- **Check**: `customer-insights/interviews/system/logs/processing-log.csv` for existing processing

## 🔄 Processing Steps

### 1. Check Processing Status
```python
def is_already_processed(filename, customer_name):
    # Read interviews/system/logs/processing-log.csv
    # Look for exact match on filename + normalized customer_name
    # Only check entries with status = 'completed' (not 'reprocessed')
    # Return True if found, False if not
    # Allow reprocessing with explicit reason
```

### 2. Normalize Customer Name
```python
def normalize_customer_name(name):
    # Convert to lowercase
    # Remove extra spaces and punctuation
    # Standardize common abbreviations:
    #   Corp/Corporation → corporation
    #   Inc/Incorporated → incorporated
    #   LLC/Limited Liability Company → llc
    #   Ltd/Limited → limited
    #   Co/Company → company
    #   & → and
    # Remove common business suffixes: Solutions, Systems, Services, Group, Technologies
    # Extract from email domains if present: sarah@techcorp.com → techcorp
    # Handle multi-word variations: "Tech Corp" → "techcorp"
    # Return normalized name for consistent matching
```

### 3. Process Interview Content
Extract and structure the following information:

#### Required Fields
- **Customer Name**: Extract company/person name using hierarchical detection (priority order):
  1. **File headers/titles** (HIGHEST PRIORITY): First line, title, or structured header
  2. **Structured metadata**: Date/Company headers, meeting titles
  3. **Direct mentions**: "I work at TechCorp", "We're from DataFlow Inc"
  4. **Email signatures/domains**: @techcorp.com → TechCorp
  5. **Context clues**: Job titles, company references in conversation
  6. **Filename fallback**: Extract from filename if no other method works
  - Handle variations: "Tech Corp" vs "TechCorp" vs "TechCorp Solutions"
  - Always prioritize explicit headers over inferred names
- **Interview Date**: Extract date (if available)
- **Interviewer**: Extract interviewer name (if available)
- **Key Themes**: Identify 3-5 main topics discussed
- **Primary Pain Point**: Single biggest problem with severity indicator (extract from phrases like "biggest issue", "main problem", "most frustrating", "deal-breaker") OR "No primary pain point identified" if none found
- **Other Pain Points**: List all other specific problems mentioned with severity indicators
- **Biggest Feature Ask**: Single most important feature/request (extract from phrases like "most important", "top priority", "must-have", "if I could only have one thing") OR "No biggest feature ask identified" if none found
- **Other Feature Requests**: List all other requested features with context
- **Competitive Insights**: What they said about competitors
- **Quotes**: Extract 2-3 most impactful direct quotes
- **Action Items**: Identify follow-up actions needed

#### Output Format
Create a markdown file with the template structure provided in the README.

### 4. Update Tracking
```python
def update_tracking(filename, customer_name, status, processed_file_path=None, reason="initial"):
    # Add entry to interviews/system/logs/processing-log.csv
    # Format: filename, customer_name, processed_date, status, processed_file_path, reason
    # Reason codes: initial, prompt_update, manual_retry, content_update, format_fix
```

### 5. File Management
- **Success**: Move original files to `interviews/workflow/archive/yyyy-mm-dd-customername-01/`
- **Failure**: Move files to `interviews/workflow/failed/`
- **Output**: Create processed file in `interviews/workflow/processed/`

## 🚨 Error Handling

### Processing Failures
- **Incomplete content**: Extract what's available, mark as partial
- **Unreadable format**: Move to failed folder, log error
- **Missing customer name**: Try detection methods in priority order:
  1. Check first lines/headers for company names
  2. Look for structured metadata (Date: X, Company: Y)
  3. Check for email domains in content
  4. Look for "from [company]" or "at [company]" patterns
  5. Extract person names from signatures
  6. Use filename as last resort with uncertainty flag
- **No content**: Move to failed folder, log error
- **Ambiguous customer name**: Note multiple possibilities in tracking log

### Quality Checks
- **Minimum content**: Ensure at least customer name and one insight
- **Format validation**: Check markdown syntax
- **Completeness**: Verify all required sections have content

## 📝 Output Requirements

### File Naming
- **Processed files**: `yyyy-mm-dd-customername.md`
- **Archive folders**: `yyyy-mm-dd-customername-01/`

### Content Quality
- **Clear structure**: Follow template exactly
- **Actionable insights**: Focus on specific, actionable information
- **Preserve context**: Maintain original meaning while structuring
- **Complete quotes**: Use full sentences, not fragments
- **Accurate severity**: Assess pain point severity based on customer language and impact

### Token Optimization Requirements
- **Concise output**: Prioritize token efficiency over human readability
- **Abbreviated format**: Use short phrases, bullet points, minimal prose
- **Essential info only**: Skip filler words, focus on key insights
- **Structured data**: Use consistent formatting for easy parsing
- **No redundancy**: Don't repeat information across sections

## 🔄 Iteration Process

1. **Process one file at a time**
2. **Check tracking before processing** (only block if status = 'completed')
3. **Determine processing reason** (initial, prompt_update, manual_retry, etc.)
4. **Handle errors gracefully**
5. **Update tracking after each file** with appropriate reason
6. **Move files to appropriate folders**
7. **Continue to next file**

## 📋 Processing Reason Codes

- **initial**: First time processing this file
- **prompt_update**: Processing prompt was improved/updated
- **manual_retry**: Manual reprocessing after failure
- **content_update**: Source content was modified
- **format_fix**: Output format corrections needed

## 💡 Tips for Better Processing

- **Look for patterns**: Common themes across interviews
- **Extract specifics**: Avoid vague statements
- **Preserve emotion**: Keep the human element in quotes
- **Identify urgency**: Note time-sensitive requests
- **Connect dots**: Link related insights across sections
- **Assess severity accurately**: Use customer language cues to determine pain point severity

## 🎯 Pain Point Severity Assessment

### 🔥 Critical Indicators
- **Language**: "deal-breaker", "can't use without", "blocks us completely", "causes us to churn"
- **Impact**: Prevents adoption, causes customer loss, stops workflow entirely
- **Urgency**: "immediate need", "showstopper", "mission critical"

### ⚠️ High Indicators
- **Language**: "major frustration", "significant problem", "really annoying", "big pain point"
- **Impact**: Requires workarounds, slows down work, affects daily operations
- **Urgency**: "important to fix", "high priority", "affects productivity"

### 📋 Medium Indicators
- **Language**: "minor issue", "would be nice", "small improvement", "not urgent"
- **Impact**: Inconvenience, cosmetic issue, nice-to-have enhancement
- **Urgency**: "eventually", "low priority", "when you get time"

## 🏷️ Customer Name Detection Examples

### ✅ Good Detection Patterns (Priority Order)

#### 🥇 Priority 1: File Headers/Titles (ALWAYS USE FIRST)
- **First line headers**: "CompanyX Meeting Notes", "TechCorp Interview - 2024-01-15"
- **Title formats**: "# DataFlow Inc Customer Interview", "Meeting: CloudScale Systems"
- **Structured headers**: "Company: ACME Corp", "Customer: TechCorp Solutions"

#### 🥈 Priority 2: Structured Metadata
- **Meeting headers**: "Date: 2024-01-15, Company: TechCorp"
- **Document metadata**: "Interview with: DataFlow Inc"
- **Template fields**: "Customer Name: CloudScale Systems"

#### 🥉 Priority 3: Content-Based Detection
- **Direct mention**: "I'm Sarah from TechCorp Solutions"
- **Email signatures**: "Best regards, Marcus Rodriguez, VP Product, DataFlow Inc"
- **Email domains**: "marcus@dataflow-inc.com" → "DataFlow Inc"
- **Context clues**: "Our company, CloudScale Systems, needs..."
- **Job titles**: "As VP at TechCorp, I can tell you..."

### ⚠️ Challenging Cases
- **Header vs content conflict**: "CompanyX Notes" (header) vs "I work at DataFlow" (content) → USE HEADER
- **Person only**: "Hi, I'm John" → Use "John [Unknown Company]" or filename
- **Acronyms**: "I work at ACME" → Could be "ACME Corporation" or "A.C.M.E."
- **Multiple names**: "TechCorp Solutions, formerly DataTech" → Use primary name
- **Informal names**: "We call ourselves the Data Team" → Look for formal name

### 🎯 Header Detection Examples
```
# CompanyX Interview ✅ → Use "CompanyX"
Meeting Notes: DataFlow Inc ✅ → Use "DataFlow Inc"
Customer: TechCorp Solutions ✅ → Use "TechCorp Solutions"
Date: 2024-01-15, Company: ACME ✅ → Use "ACME"
Interview with CloudScale team ✅ → Use "CloudScale"
```

### 🔄 Normalization Examples
- "TechCorp Solutions Inc." → "techcorp"
- "DataFlow, LLC" → "dataflow"
- "CloudScale Systems & Services" → "cloudscale"
- "ACME Corp" → "acme"

## 🎯 Token Optimization Guidelines

### Output Format Priority
1. **Token efficiency** (primary goal)
2. **Structured data** (secondary goal)
3. **Human readability** (tertiary goal)

### Specific Optimization Rules
- **Use abbreviations**: "PM" not "Product Manager", "UI" not "User Interface"
- **Short phrases**: "Login slow" not "The login process is slow"
- **Bullet points**: Avoid full sentences where possible
- **Consistent format**: Same structure across all files
- **Skip articles**: "a", "the", "an" where not essential
- **Minimal prose**: Direct facts, not explanations
