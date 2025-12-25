# Task: Extract Knowledge from PR Reviews and Generate knowledge.json

Execute the following steps immediately:

## Step 1: Fetch PR Review Data

Run this command to get PR review threads (only resolved ones):

```bash
gh api graphql -f query='
  {
    repository(owner: "'$REPO_OWNER'", name: "'$REPO_NAME'") {
      pullRequest(number: '$PR_NUMBER') {
        reviewThreads(first: 100) {
          nodes {
            isResolved
            comments(first: 10) {
              nodes {
                body
                path
                diffHunk
              }
            }
          }
        }
        files(first: 100) {
          nodes {
            path
          }
        }
      }
    }
  }
'
```

## Step 2: Analyze and Extract Knowledge

From the resolved review threads (`isResolved: true`), extract valuable insights based on these criteria:

**Include comments about:**
- Security risks (SQL injection, XSS, etc.)
- Performance issues (N+1 queries, memory leaks)
- Design/architecture improvements
- Error handling gaps
- Testing issues
- Best practices violations

**Exclude comments about:**
- Typos/spelling
- Formatting/style only
- Simple approvals ("LGTM")
- Personal preferences

## Step 3: Generate knowledge.json

Create a `knowledge.json` file with this structure:

```json
{
  "knowledge_items": [
    {
      "category": "security|performance|readability|design|testing|error-handling|other",
      "language": "java|nodejs|python|php|etc",
      "severity": "critical|warning|info",
      "title": "Short title",
      "summary": "Problem description",
      "recommendation": "How to fix",
      "code_example": {
        "bad": "Problematic code",
        "good": "Corrected code"
      },
      "file_path": "path/to/file",
      "pr_url": "'$PR_URL'",
      "original_comment": "Original review comment"
    }
  ],
  "skipped_comments": [
    {
      "reason": "Why skipped",
      "comment_preview": "Comment preview"
    }
  ]
}
```

**IMPORTANT:**
- Write the `knowledge.json` file to the current directory using `cat > knowledge.json`
- Include only resolved review threads
- If no valuable insights found, create an empty JSON: `{"knowledge_items": [], "skipped_comments": []}`

Now execute these steps and generate the knowledge.json file.
