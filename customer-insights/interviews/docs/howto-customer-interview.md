# How to Import Customer Interviews: A Junior PM Guide

## 🎯 What This System Does

This system helps you turn messy interview notes into structured, searchable insights that actually inform your product decisions. Instead of losing interview insights in random documents, everything gets organized and processed automatically.

## 🚀 Quick Start (Complete Setup)

### Prerequisites (First Time Only)
1. **Check you have the right file structure**:
   ```
   customer-insights/
   ├── interviews/workflow/inbound/               ← Must exist
   ├── interviews/workflow/processed/             ← Must exist
   ├── interviews/workflow/failed/               ← Must exist
   ├── interviews/workflow/archive/               ← Must exist
   └── interviews/system/logs/processing-log.csv  ← Must exist
   ```
2. **If folders don't exist**: Create them manually or run the test setup
3. **If processing-log.csv doesn't exist**: Create it with header: `filename, customer_name, processed_date, status, processed_file_path, reason`

### Step 1: Prepare Your Interview Files
1. **Collect your raw materials**:
   - Meeting notes (.md, .txt, .docx)
   - Interview transcripts (any text format)
   - Email conversations with customers
   - Survey responses
2. **Clean up the content** (optional but recommended):
   - Add customer company name to the top of the file
   - Include interview date if known
   - Remove any sensitive information
3. **Name your files clearly**: `companyname-interview.txt` or `2024-01-15-meeting-notes.md`

### Step 2: Drop Files for Processing
1. **Navigate to**: `customer-insights/interviews/workflow/inbound/`
2. **Copy your files** into this folder
3. **Verify**: Files should now be visible in the inbound folder
4. **Don't worry about duplicates**: The system checks for already-processed files

### Step 3: Run the AI Processing
1. **Open the processing prompt**:
   - File location: `customer-insights/prompt-interview-processing.md`
   - Open in any text editor
2. **Copy the entire prompt** (Ctrl+A, then Ctrl+C)
3. **Open your AI assistant**:
   - Recommended: Claude Code, ChatGPT, or Claude
   - Paste the prompt into a new conversation
4. **Add your instruction**:
   ```
   Please process all files in the customer-insights/interviews/workflow/inbound/ folder using the above prompt.
   ```
5. **Let it run**: AI will process each file automatically
6. **Monitor progress**: AI will show which files it's processing

### Step 4: Review and Verify Results
1. **Check processed files**: Look in `interviews/workflow/processed/`
2. **Verify file movement**: Original files should now be in `interviews/workflow/archive/`
3. **Check processing log**: Review `interviews/system/logs/processing-log.csv` for status
4. **Review any failures**: Check `interviews/workflow/failed/` for problematic files

### Step 5: Use Your Insights
1. **Read the structured output**: Each file now has standardized sections
2. **Look for patterns**: Common pain points across customers
3. **Extract quotes**: Use direct customer quotes in presentations
4. **Update PRDs**: Incorporate insights into product requirements
5. **Share with team**: Processed files are easy to share and search

## ⏱️ What to Expect on First Run

### Processing Time
- **Small files** (1-2 pages): 30-60 seconds each
- **Large files** (5+ pages): 2-3 minutes each
- **Multiple files**: AI processes one at a time sequentially

### AI Behavior During Processing
1. **File discovery**: AI will list all files it finds
2. **Processing order**: Files processed alphabetically
3. **Status updates**: AI will show progress for each file
4. **Error reporting**: Any failed files will be reported with reasons
5. **Final summary**: Count of successful vs failed processing

### What Success Looks Like
- Files appear in `interviews/workflow/processed/`
- Original files moved to `interviews/workflow/archive/[date-company]/`
- Entry added to `interviews/system/logs/processing-log.csv`
- No files left in `interviews/workflow/inbound/`

### Red Flags (When Something's Wrong)
- Files remain in inbound folder after processing
- No new entries in processing-log.csv
- AI reports it can't find files
- All files end up in failed folder

## 📁 What Goes Where

```
customer-insights/
├── interviews/workflow/inbound/                    ← Drop your raw files here
├── interviews/workflow/processed/                  ← Clean, structured insights appear here
├── interviews/workflow/failed/                    ← Files that need manual review
└── interviews/workflow/archive/                    ← Original files (permanent record)
```

## 📋 Supported File Types

### ✅ What Works
- **Text files**: `.md`, `.txt`, `.docx`
- **Interview transcripts**: Any text-based transcript
- **Meeting notes**: Bullet points, paragraphs, anything readable
- **Folder structures**: Multiple files per interview (transcript + notes)

### ❌ What Doesn't Work (Yet)
- **Audio files**: Need to be transcribed first
- **Video files**: Need to be transcribed first
- **Images**: Need to be converted to text first

## 🔄 The Processing Magic

### What Happens Automatically
1. **Duplicate detection**: Won't process the same interview twice (unless status != 'completed')
2. **Version tracking**: Each reprocessing gets a new version with reason code
3. **Processing history**: Complete audit trail of all processing attempts
2. **Customer name extraction**: Finds company/person names
3. **Insight extraction**: Pulls out pain points, feature requests, quotes
4. **Structuring**: Organizes everything into a consistent format
5. **Archiving**: Keeps original files safe

### What You Get
Each processed interview becomes a structured document with:
- **Summary**: Key themes and context
- **Pain Points**: Specific problems mentioned
- **Feature Requests**: What they want built
- **Competitive Insights**: What they said about competitors
- **Quotes**: Direct quotes for presentations
- **Action Items**: Follow-up tasks

**Note**: Output is optimized for token efficiency, not human readability. Use abbreviations and concise formatting to minimize AI processing costs.

## 🚨 First-Time Setup Issues & Solutions

### "Folders don't exist"
**Problem**: You get errors about missing directories
**Solution**: Create the required folder structure:
```bash
mkdir -p customer-insights/interviews/workflow/inbound
mkdir -p customer-insights/interviews/workflow/processed
mkdir -p customer-insights/interviews/workflow/failed
mkdir -p customer-insights/interviews/workflow/archive
mkdir -p customer-insights/interviews/system/logs
```

### "processing-log.csv not found"
**Problem**: AI can't find the tracking file
**Solution**: Create the file with this header:
```csv
filename, customer_name, processed_date, status, processed_file_path, reason
```

### "AI can't access my files"
**Problem**: AI says it can't read files in the inbound folder
**Solution**:
1. Make sure files are actually in `interviews/workflow/inbound/`
2. Check file permissions (files should be readable)
3. Try using Claude Code or similar AI that can access local files

### "My file didn't process"
**Check**: Is it already in `interviews/workflow/processed/`?
**Solution**:
1. Check the `interviews/system/logs/processing-log.csv` file
2. Look for your filename - if status is 'completed', it won't reprocess
3. To force reprocessing, delete the entry from the CSV

### "Processing failed"
**Check**: Look in `interviews/workflow/failed/` folder
**Solution**:
1. File might be corrupted - try opening it manually
2. Convert to plain text (.txt) format
3. Check if file contains readable text content
4. Remove any special characters or formatting

### "Wrong customer name detected"
**Problem**: System extracted wrong company name
**Solution**:
1. Add clear header to your file: `# CompanyName Interview`
2. Include company name in first few lines
3. Edit the processed file to correct the name
4. For future files, put company name at the very top

### "Missing insights or empty sections"
**Problem**: Processed file has empty sections
**Check**: Was the original content detailed enough?
**Solution**:
1. Original file needs substantial content (not just names/dates)
2. Include actual conversation content, problems mentioned, requests made
3. Add more context to your notes before processing
4. The system can only extract what exists in source material

## 💡 Pro Tips for Better Results

### Before Processing
- **Clean up your notes**: Remove personal info, add context
- **Include customer details**: Company name, role, date
- **Be specific**: "The login is slow" vs "The login takes 30 seconds"
- **Token optimization**: Shorter input = lower processing costs

### After Processing
- **Review the output**: Make sure insights make sense
- **Add context**: Fill in any missing details
- **Connect dots**: Link related insights across interviews
- **Understand format**: Output is token-optimized (abbreviated, concise)

### For Multiple Interviews
- **Process in batches**: Don't overwhelm the system
- **Check for patterns**: Look for common themes across customers
- **Update your PRDs**: Use insights to inform requirements

## 🔧 Troubleshooting

### File Not Processing
1. Check if it's already processed (look in `interviews/workflow/processed/`)
2. Check the interviews/system/logs/processing-log.csv file
3. Try renaming the file and processing again

### Processing Failed
1. Check the `interviews/workflow/failed/` folder
2. Try converting the file to plain text (.txt)
3. Check if the file is corrupted

### Wrong Output
1. Review the original file - was it clear enough?
2. Edit the processed file to correct mistakes
3. Re-process with better source material

## 📚 Next Steps

Once you have processed interviews:
1. **Review patterns**: What do customers keep saying?
2. **Update your PRDs**: Use insights to inform requirements
3. **Share with team**: Use quotes and insights in presentations
4. **Track decisions**: Log how insights influenced product decisions

## 🤔 Questions?

- **Check the README.md** for detailed technical info
- **Look at the prompt file** (`prompt-interview-processing.md`) for AI instructions
- **Review failed files** in the failed folder for error details

---

**Remember**: This system is designed to make your life easier, not harder. Start simple, process a few interviews, and see how it works for you!
