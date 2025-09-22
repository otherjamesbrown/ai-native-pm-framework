# Test Data for Customer Insights Processing

This folder contains realistic test data for validating the customer insights processing system.

## Test Scenarios

### 1. TechCorp Solutions - Interview Transcript
**File**: `techcorp-solutions-interview.txt`
**Format**: Raw interview transcript
**Persona**: Marcus Rodriguez (VP of Product) at mid-size tech company
**Key Themes**: Manual process pain, need for automation, reliability requirements

### 2. DataFlow Inc - Transcript + Notes
**Folder**: `dataflow-inc-interview/`
**Files**: 
- `transcript.txt` - Raw interview transcript
- `notes.md` - Structured notes with feature mapping
**Persona**: Jennifer Walsh (Head of Strategy) at data analytics startup
**Key Themes**: Startup constraints, team collaboration, multi-channel tracking

### 3. CloudScale Systems - Interview Notes
**File**: `cloudscale-systems-notes.md`
**Format**: Structured interview notes
**Persona**: David Park (CTO) at enterprise cloud company
**Key Themes**: Enterprise requirements, scale challenges, compliance needs

## Testing the Processing System

### How to Test
1. **Copy files to inbound folder**: Move test files to `customer-insights/inbound/interviews/`
2. **Run AI processing**: Use the prompt in `prompt-interview-processing.md`
3. **Verify output**: Check `processed/interviews/` for structured insights
4. **Review processing log**: Check `processing-log.csv` for status tracking

### Expected Outputs
Each test file should produce a token-optimized markdown file with:
- Customer summary
- Pain points identified
- Feature requests
- Competitive insights
- Key quotes
- Action items

### Test Validation
- **Duplicate detection**: Try processing the same file twice
- **Different formats**: Test transcript vs notes vs folder structure
- **Customer name extraction**: Verify correct company names
- **Token optimization**: Check for concise, abbreviated output

## Company Backgrounds

### TechCorp Solutions
- Mid-size technology company
- Struggling with manual competitive intelligence
- Needs reliable automation
- Budget: $500-1000/month

### DataFlow Inc
- Data analytics startup
- One-person competitive intelligence
- Needs team collaboration features
- Budget: $200-500/month

### CloudScale Systems
- Enterprise cloud infrastructure provider
- Complex compliance requirements
- Needs enterprise-grade features
- Budget: $50K-100K/year

## Use Cases for Testing

1. **Basic Processing**: Test single file processing
2. **Batch Processing**: Test multiple files at once
3. **Error Handling**: Test with corrupted/missing data
4. **Format Variations**: Test different input formats
5. **Token Optimization**: Verify concise output format
