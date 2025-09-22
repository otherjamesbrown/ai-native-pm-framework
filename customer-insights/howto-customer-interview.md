# How to Import Customer Interviews: A Junior PM Guide

## 🎯 What This System Does

This system helps you turn messy interview notes into structured, searchable insights that actually inform your product decisions. Instead of losing interview insights in random documents, everything gets organized and processed automatically.

## 🚀 Quick Start (5 Minutes)

### Step 1: Drop Your Interview Files
1. **Find your interview files** (notes, transcripts, recordings)
2. **Copy them** into the `inbound/interviews/` folder
3. **That's it!** The system will handle the rest

### Step 2: Run the Processing
1. **Open the AI prompt** (`prompt-interview-processing.md`)
2. **Copy the prompt** into your AI assistant (ChatGPT, Claude, etc.)
3. **Let it run** - it will process all your files automatically

### Step 3: Review Your Insights
1. **Check `processed/interviews/`** for your structured insights
2. **Review the output** - each interview becomes a clean, searchable document
3. **Use the insights** in your PRDs and decision-making

## 📁 What Goes Where

```
customer-insights/
├── inbound/interviews/          ← Drop your raw files here
├── processed/interviews/        ← Clean, structured insights appear here
├── failed/interviews/          ← Files that need manual review
└── archive/                    ← Original files (permanent record)
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
1. **Duplicate detection**: Won't process the same interview twice
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

## 🚨 Common Issues & Solutions

### "My file didn't process"
**Check**: Is it already in `processed/interviews/`?
**Solution**: The system tracks what's been processed - check the processing-log.csv file

### "Processing failed"
**Check**: Look in `failed/interviews/` folder
**Solution**: The file might be corrupted or unreadable - try converting to plain text

### "Wrong customer name"
**Check**: The system extracts names automatically
**Solution**: Edit the processed file to correct the name

### "Missing insights"
**Check**: Was the original content detailed enough?
**Solution**: The system can only extract what's in the source material

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
1. Check if it's already processed (look in `processed/interviews/`)
2. Check the processing-log.csv file
3. Try renaming the file and processing again

### Processing Failed
1. Check the `failed/interviews/` folder
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
