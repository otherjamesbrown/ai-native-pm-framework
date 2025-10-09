# Customer Insights Processing System

## 📁 Folder Structure

```
customer-insights/
├── interviews/              # Interview workflow module
│   ├── workflow/            # Core processing workflow
│   │   ├── inbound/         # Drop raw interview files/folders here
│   │   ├── processed/       # Structured output files
│   │   ├── failed/          # Files that failed processing
│   │   └── archive/         # Original source files after processing
│   ├── system/              # System files and logs
│   │   └── logs/
│   │       └── processing-log.csv  # Processing status tracking
│   └── docs/                # Documentation and guides
│       ├── howto-customer-interview.md  # Step-by-step guide
│       ├── interview-template.md   # Structured 45-minute interview format
│       ├── interview-best-practices.md  # Advanced techniques and tips
│       └── question-bank.md        # 200+ organized questions for different scenarios
├── prompt-interview-processing.md  # AI processing instructions
└── README.md               # This documentation
```

## 🔄 Processing Workflow

### 1. Input Files
- **Individual files**: Drop `.md`, `.txt`, `.docx` files directly in `interviews/workflow/inbound/`
- **Interview folders**: Create a folder with transcript + notes + other materials
- **Multiple formats**: Supported formats include transcripts, notes, recordings (transcribed)

### 2. Processing Logic
1. **Check interviews/system/logs/processing-log.csv**: Look for `filename + customer_name` match with status = `completed`
2. **If found with status = completed**: Skip processing, move to next file
3. **If not found OR status = reprocessed/failed**: Process the file using AI prompt
4. **After processing**:
   - Add entry to `interviews/system/logs/processing-log.csv` with `completed` status and appropriate reason
   - Move original files to `interviews/workflow/archive/yyyy-mm-dd-customername-01/`
   - Create structured output in `interviews/workflow/processed/`
5. **If processing fails**:
   - Add entry to `interviews/system/logs/processing-log.csv` with `failed` status and reason
   - Move files to `interviews/workflow/failed/` for manual review

### 3. Processing Log Format
```csv
filename, customer_name, processed_date, status, processed_file_path, reason
customer-a-interview.md, "acme corp", 2024-01-15, completed, processed/2024-01-15-acme-corp.md, initial
customer-b-folder, "beta inc", 2024-01-16, failed, null, initial
customer-a-interview.md, "acme corp", 2024-01-16, reprocessed, processed/2024-01-15-acme-corp-v2.md, prompt_update
```

#### Processing Reason Codes
- **initial**: First time processing this file
- **prompt_update**: Processing prompt was improved/updated
- **manual_retry**: Manual reprocessing after failure
- **content_update**: Source content was modified
- **format_fix**: Output format corrections needed

**Customer Name Normalization**:
- Convert to lowercase
- Remove extra spaces and punctuation
- Standardize abbreviations (Corp/Corporation → corporation, Inc → incorporated, LLC → llc, Ltd → limited, Co → company, & → and)
- Remove business suffixes (Solutions, Systems, Services, Group, Technologies)
- Extract from email domains (@techcorp.com → techcorp)
- Handle multi-word variations ("Tech Corp" → "techcorp")

## 🚨 Manual Override Process

### When to Use Manual Override
- File renamed but same content
- Customer name variation (typos, different formats)
- Processing failed and needs retry
- Duplicate detection false positive

### How to Override
1. **Edit interviews/system/logs/processing-log.csv** directly
2. **Change status** from `failed` to `completed` (if manually processed)
3. **Add missing entries** for files that should be skipped
4. **Update customer names** for consistency
5. **Update reason** to reflect why reprocessing occurred

## 📋 Output Template

Processed files follow this structure (optimized for token efficiency):
```markdown
# [Customer] - [Date]

## Summary
- **Customer**: [Name/Role/Company]
- **Date**: [Date]
- **Interviewer**: [Name]
- **Themes**: [3-5 bullet points]

## Primary Pain Point / Other Pain Points
- **Primary**: [Single biggest problem] (🔥 Critical/⚠️ High/📋 Medium) OR "No primary pain point identified"
- **Other**: [Pain point 1] (🔥 Critical/⚠️ High/📋 Medium)
- **Other**: [Pain point 2] (🔥 Critical/⚠️ High/📋 Medium)

## Biggest Feature Ask / Other Feature Asks
- **Biggest**: [Single most important request] OR "No biggest feature ask identified"
- **Other**: [Request 1]
- **Other**: [Request 2]

## Competitive
- [Competitor insights]

## Quotes
> "[Quote 1]"
> "[Quote 2]"

## Actions
- [ ] [Follow-up]
- [ ] [Investigate]

## Source
- Files: `archive/yyyy-mm-dd-customername-01/`
```

### Token Optimization Features
- **Abbreviated headers**: "Pain Points" not "Pain Points Identified"
- **Short phrases**: Concise bullet points, minimal prose
- **Consistent format**: Same structure across all files
- **Essential info only**: Skip filler words and explanations
- **Severity indicators**: Use emoji shortcuts (🔥⚠️📋) for efficient categorization

### Severity Classification Guide
- **🔥 Critical**: Deal-breaker, blocks adoption, causes customer churn, immediate action required
- **⚠️ High**: Major frustration, significant workaround needed, impacts daily workflow
- **📋 Medium**: Inconvenience, minor issue, nice-to-have improvement

## 🔧 Troubleshooting

### Common Issues
1. **File not processing**: Check if already in interviews/system/logs/processing-log.csv with status = `completed`
2. **Processing fails**: Check interviews/workflow/failed/ folder
3. **Need to reprocess**: Change status from `completed` to `reprocessed` and add appropriate reason
4. **Duplicate detection**: Edit interviews/system/logs/processing-log.csv to add/remove entries
5. **Customer name mismatch**: Update interviews/system/logs/processing-log.csv with normalized name
6. **Customer name variations**: "TechCorp" vs "Tech Corp" vs "TechCorp Solutions" should normalize to same value
7. **Missing customer name**: AI will prioritize file headers/titles, then try email domains, context clues, or filename fallback
8. **Header detection**: First line headers like "CompanyX Meeting Notes" take priority over content-based detection

### Getting Help
- Check the AI prompt in `prompt-interview-processing.md`
- Review failed files in `interviews/workflow/failed/`
- Edit interviews/system/logs/processing-log.csv for manual overrides
