# Interview Processing AI Prompt

## 🎯 Task
Process customer interview files and extract structured insights.

## 📋 Input
- **Source**: Files/folders in `customer-insights/inbound/interviews/`
- **Formats**: `.md`, `.txt`, `.docx`, transcript files, interview notes
- **Check**: `customer-insights/processed/processing-log.csv` for existing processing

## 🔄 Processing Steps

### 1. Check Processing Status
```python
def is_already_processed(filename, customer_name):
    # Read processing-log.csv
    # Look for exact match on filename + normalized customer_name
    # Return True if found, False if not
```

### 2. Normalize Customer Name
```python
def normalize_customer_name(name):
    # Convert to lowercase
    # Remove extra spaces
    # Standardize abbreviations (Corp → Corporation, Inc → Incorporated)
    # Return normalized name
```

### 3. Process Interview Content
Extract and structure the following information:

#### Required Fields
- **Customer Name**: Extract company/person name
- **Interview Date**: Extract date (if available)
- **Interviewer**: Extract interviewer name (if available)
- **Key Themes**: Identify 3-5 main topics discussed
- **Primary Pain Point**: Single biggest problem (extract from phrases like "biggest issue", "main problem", "most frustrating", "deal-breaker") OR "No primary pain point identified" if none found
- **Other Pain Points**: List all other specific problems mentioned
- **Biggest Feature Ask**: Single most important feature/request (extract from phrases like "most important", "top priority", "must-have", "if I could only have one thing") OR "No biggest feature ask identified" if none found
- **Other Feature Requests**: List all other requested features with context
- **Competitive Insights**: What they said about competitors
- **Quotes**: Extract 2-3 most impactful direct quotes
- **Action Items**: Identify follow-up actions needed

#### Output Format
Create a markdown file with the template structure provided in the README.

### 4. Update Tracking
```python
def update_tracking(filename, customer_name, status, processed_file_path=None):
    # Add entry to processing-log.csv
    # Format: filename, customer_name, processed_date, status, processed_file_path
```

### 5. File Management
- **Success**: Move original files to `archive/yyyy-mm-dd-customername-01/`
- **Failure**: Move files to `failed/interviews/`
- **Output**: Create processed file in `processed/interviews/`

## 🚨 Error Handling

### Processing Failures
- **Incomplete content**: Extract what's available, mark as partial
- **Unreadable format**: Move to failed folder, log error
- **Missing customer name**: Use filename as fallback
- **No content**: Move to failed folder, log error

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

### Token Optimization Requirements
- **Concise output**: Prioritize token efficiency over human readability
- **Abbreviated format**: Use short phrases, bullet points, minimal prose
- **Essential info only**: Skip filler words, focus on key insights
- **Structured data**: Use consistent formatting for easy parsing
- **No redundancy**: Don't repeat information across sections

## 🔄 Iteration Process

1. **Process one file at a time**
2. **Check tracking before processing**
3. **Handle errors gracefully**
4. **Update tracking after each file**
5. **Move files to appropriate folders**
6. **Continue to next file**

## 💡 Tips for Better Processing

- **Look for patterns**: Common themes across interviews
- **Extract specifics**: Avoid vague statements
- **Preserve emotion**: Keep the human element in quotes
- **Identify urgency**: Note time-sensitive requests
- **Connect dots**: Link related insights across sections

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
