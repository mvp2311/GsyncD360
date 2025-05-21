## 📝 Bug Report: Typo Tolerance Not Working on Article Content

### Summary
During internal testing, it was found that typo tolerance works as expected for article titles, but fails for article content. This issue was consistently reproduced with non-English content using common typographical errors.

### Steps to Reproduce
1. Create a new article in Japanese or Danish with a detailed body.
2. Index the article in Algolia.
3. Perform a search:
   - With correct keywords from the article → ✅ Results appear
   - With keywords having minor typos → ❌ No results appear

### Observation
- ✅ Typo tolerance is functional for titles.
- ❌ Typo tolerance is not applied to article content.

## 🔍 Developer Analysis

### Root Cause
The `searchableAttributes` configuration in the Algolia index includes the `title`, but **excludes** the `content` field. Since typo tolerance only applies to fields that are marked as searchable, this results in missing search results for typos in article content.

### Technical Details
- `title` → `"searchableAttributes"` ✅
- `content` → missing in `"searchableAttributes"` ❌

#### Suggested Fix
Update the Algolia index configuration to include the `content` field under `searchableAttributes`.

## ✅ Preventive Action

### Configuration Checklist
- [ ] Ensure all important text fields are added to `searchableAttributes`
- [ ] Validate typo tolerance in multilingual contexts
- [ ] Automate tests to check typo-tolerant behavior across fields

### QA Coverage
- Extend test scenarios to validate typo tolerance on all configured fields.
- Include language-specific typo variants in regression tests.

