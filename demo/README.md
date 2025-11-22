# Data Processor Demo Examples

This directory contains demo examples to test and showcase the data-processor chatmode.

## Demo 1: GitHub Repository Info Fetcher (Recommended)

**Purpose**: Fetch repository information from GitHub's public API.

**Files**:
- `repos_list.txt` - List of GitHub repositories in `owner/repo` format
- `github_rules.md` - Processing rules for GitHub API

**Usage**:
```
Process the repositories in repos_list.txt using the rules in github_rules.md
```

**What it demonstrates**:
- JSON API parsing
- Error handling (includes an invalid repo)
- Multiple field extraction
- Default values for missing fields
- Special conditions (archived, fork detection)

---

## Demo 2: JSONPlaceholder User Info (Simplest)

**Purpose**: Fetch user data from JSONPlaceholder test API (guaranteed to work).

**Files**:
- `users_list.txt` - List of user IDs
- `jsonplaceholder_rules.md` - Processing rules for JSONPlaceholder API

**Usage**:
```
Process the users in users_list.txt using the rules in jsonplaceholder_rules.md
```

**What it demonstrates**:
- Simple API calls
- Nested JSON field extraction
- Error handling (user 999 doesn't exist)
- Fast processing (short delays)

---

## Expected Output Structure

After processing, you'll get:
- `processing_todo.md` - TODO list showing progress
- `processed_output.md` - Final results with all processed items

---

## Testing Tips

1. Start with **Demo 2 (JSONPlaceholder)** if you want guaranteed success
2. Use **Demo 1 (GitHub)** for a more real-world example
3. Check `processing_todo.md` during execution to see progress
4. Review `processed_output.md` for final results

---

## Customization

You can create your own demos by:
1. Creating an input list file (one item per line)
2. Creating a processing rules file following the format in the examples
3. Invoking the data-processor chatmode with your files
