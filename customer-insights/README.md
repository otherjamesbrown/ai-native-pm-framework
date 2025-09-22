# Customer Insights Processing System

## 📁 Folder Structure

```
customer-insights/
├── inbound/
│   └── interviews/          # Drop raw interview files/folders here
├── processed/
│   └── interviews/          # Structured output files
├── failed/
│   └── interviews/          # Files that failed processing
├── archive/                 # Original source files after processing
├── processing-log.csv       # Processing status tracking
├── README.md               # This documentation
├── howto-customer-interview.md  # Step-by-step guide
└── prompt-interview-processing.md  # AI processing instructions
```

## 🔄 Processing Workflow

### 1. Input Files
- **Individual files**: Drop `.md`, `.txt`, `.docx` files directly in `inbound/interviews/`
- **Interview folders**: Create a folder with transcript + notes + other materials
- **Multiple formats**: Supported formats include transcripts, notes, recordings (transcribed)

### 2. Processing Logic
1. **Check processing-log.csv**: Look for `filename + customer_name` match
2. **If found**: Skip processing, move to next file
3. **If not found**: Process the file using AI prompt
4. **After processing**: 
   - Add entry to `processing-log.csv` with `completed` status
   - Move original files to `archive/yyyy-mm-dd-customername-01/`
   - Create structured output in `processed/interviews/`
5. **If processing fails**: 
   - Add entry to `processing-log.csv` with `failed` status
   - Move files to `failed/interviews/` for manual review

### 3. Processing Log Format
```csv
filename, customer_name, processed_date, status, processed_file_path
customer-a-interview.md, "acme corp", 2024-01-15, completed, processed/interviews/2024-01-15-acme-corp.md
customer-b-folder, "beta inc", 2024-01-16, failed, null
```

**Customer Name Normalization**: 
- Convert to lowercase
- Remove extra spaces
- Standardize common abbreviations (Corp → Corporation, Inc → Incorporated)

## 🚨 Manual Override Process

### When to Use Manual Override
- File renamed but same content
- Customer name variation (typos, different formats)
- Processing failed and needs retry
- Duplicate detection false positive

### How to Override
1. **Edit processing-log.csv** directly
2. **Change status** from `failed` to `completed` (if manually processed)
3. **Add missing entries** for files that should be skipped
4. **Update customer names** for consistency

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
- **Primary**: [Single biggest problem] OR "No primary pain point identified"
- **Other**: [Pain point 1]
- **Other**: [Pain point 2]

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

## 🔧 Troubleshooting

### Common Issues
1. **File not processing**: Check if already in processing-log.csv
2. **Processing fails**: Check failed/interviews/ folder
3. **Duplicate detection**: Edit processing-log.csv to add/remove entries
4. **Customer name mismatch**: Update processing-log.csv with normalized name

### Getting Help
- Check the AI prompt in `prompt-interview-processing.md`
- Review failed files in `failed/interviews/`
- Edit processing-log.csv for manual overrides
