# Data Processor Demo Example

## Demo: JSONPlaceholder User Info 

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
