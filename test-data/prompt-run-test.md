# Test Runner for Customer Insights Processing

## 🎯 Purpose
This prompt automates the testing of the customer insights processing system by copying test files to the inbound directory and running the processing prompt.

## 📋 Test Execution Steps

### Step 1: Copy Test Files to Inbound Directory
```bash
# Copy individual files
cp customer-insights/test-data/techcorp-solutions-interview.txt customer-insights/inbound/interviews/
cp customer-insights/test-data/cloudscale-systems-notes.md customer-insights/inbound/interviews/

# Copy folder structure
cp -r customer-insights/test-data/dataflow-inc-interview customer-insights/inbound/interviews/
```

### Step 2: Verify Files Are in Inbound Directory
```bash
# Check that all test files are in the inbound directory
ls -la customer-insights/inbound/interviews/
```

Expected output should show:
- `techcorp-solutions-interview.txt`
- `cloudscale-systems-notes.md`
- `dataflow-inc-interview/` (folder with transcript.txt and notes.md)

### Step 3: Execute Processing Prompt
Now run the following AI prompt to process all the test files:

---

## 🤖 AI Processing Prompt

**Task**: Process all customer interview files in `customer-insights/inbound/interviews/` and extract structured insights.

**Instructions**: 
1. Read the processing prompt from `customer-insights/prompt-interview-processing.md`
2. Process each file/folder in `customer-insights/inbound/interviews/`
3. Follow the token optimization guidelines (concise, abbreviated output)
4. Update the processing log in `customer-insights/processed/processing-log.csv`
5. Move processed files to appropriate folders (archive, failed, processed)

**Expected Output**: Three processed files in `customer-insights/processed/interviews/`:
- `2024-01-15-techcorp-solutions.md`
- `2024-01-18-dataflow-inc.md`
- `2024-01-22-cloudscale-systems.md`

**Validation Checklist**:
- [ ] All three files processed successfully
- [ ] Processing log updated with entries
- [ ] Original files moved to archive
- [ ] Output follows token-optimized format
- [ ] Customer names extracted correctly
- [ ] Key insights captured (pain points, feature requests, quotes)

---

## 🔍 Test Validation

### After Processing, Verify:

#### 1. Processing Log
Check `customer-insights/processed/processing-log.csv` should contain:
```csv
filename, customer_name, processed_date, status, processed_file_path
techcorp-solutions-interview.txt, "techcorp solutions", 2024-01-15, completed, processed/interviews/2024-01-15-techcorp-solutions.md
cloudscale-systems-notes.md, "cloudscale systems", 2024-01-22, completed, processed/interviews/2024-01-22-cloudscale-systems.md
dataflow-inc-interview, "dataflow inc", 2024-01-18, completed, processed/interviews/2024-01-18-dataflow-inc.md
```

#### 2. Processed Files
Check `customer-insights/processed/interviews/` should contain:
- `2024-01-15-techcorp-solutions.md`
- `2024-01-18-dataflow-inc.md`
- `2024-01-22-cloudscale-systems.md`

#### 3. Archive Files
Check `customer-insights/archive/` should contain:
- `2024-01-15-techcorp-solutions-01/`
- `2024-01-18-dataflow-inc-01/`
- `2024-01-22-cloudscale-systems-01/`

#### 4. Output Quality
Each processed file should contain:
- **Summary**: Customer info, date, themes
- **Pain Points**: Specific problems mentioned
- **Feature Requests**: Requested features
- **Competitive**: Competitor insights
- **Quotes**: Direct quotes (2-3 per file)
- **Actions**: Follow-up items
- **Source**: Archive location

### Token Optimization Validation
- Headers should be abbreviated ("Pain Points" not "Pain Points Identified")
- Content should be concise (bullet points, short phrases)
- No filler words or redundant information
- Consistent format across all files

## 🚨 Troubleshooting

### If Processing Fails
1. **Check inbound directory**: Ensure files are copied correctly
2. **Check processing log**: Look for error entries
3. **Check failed folder**: Files that couldn't be processed
4. **Review AI prompt**: Ensure all instructions are followed

### If Output Quality is Poor
1. **Check token optimization**: Output should be concise
2. **Verify customer names**: Should match test data
3. **Review insights**: Should capture key pain points and requests
4. **Check quotes**: Should include direct quotes from interviews

## 🎯 Success Criteria

**Test passes if**:
- ✅ All three files processed successfully
- ✅ Processing log updated correctly
- ✅ Files moved to appropriate folders
- ✅ Output follows token-optimized format
- ✅ Customer names extracted correctly
- ✅ Key insights captured accurately

**Test fails if**:
- ❌ Any file fails to process
- ❌ Processing log not updated
- ❌ Files not moved to correct folders
- ❌ Output not token-optimized
- ❌ Customer names incorrect
- ❌ Missing key insights

---

## 📝 Test Report Template

After running the test, document results:

**Test Date**: [Date]
**Files Processed**: [Number]
**Success Rate**: [Percentage]
**Issues Found**: [List any problems]
**Token Optimization**: [Pass/Fail]
**Output Quality**: [Pass/Fail]
**Recommendations**: [Any improvements needed]
