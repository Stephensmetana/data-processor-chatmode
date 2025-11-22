# Data Processor Chatmode

> **A rule-based data processing engine powered by GitHub Copilot that autonomously processes lists of items—from web scraping to API calls—with zero data fabrication and built-in fault tolerance.**

## Overview

Have a list of items you need to process? URLs to scrape? API endpoints to query? Data to transform? The Data Processor Chatmode is a generic, autonomous agent that takes any input list and processes each item according to custom rules you define—no coding required.

Simply provide:
- 📝 **An input file** with items to process (one per line)
- 📋 **A rules file** that defines what to do with each item

The chatmode handles everything else: fetching data, parsing responses, extracting fields, handling errors, tracking progress, and saving results—all while running completely autonomously to completion.

**Perfect for:** Web scraping, API data collection, batch validation, data transformation, content aggregation, and any repetitive data processing task.

## What It Does

The data-processor chatmode reads:
1. **An input file** - containing a list of items to process (one per line)
2. **A processing rules file** - defining how each item should be processed

It then automatically:
- Creates a TODO list for tracking progress
- Processes each item row-by-row according to your rules
- Fetches data from APIs or web pages
- Extracts specified fields
- Handles errors and retries
- Writes results incrementally to `processed_output.md`
- Never invents data - only records what's actually found

## Key Features

✅ **Fully Autonomous** - Runs to completion without requiring user interaction  
✅ **Row-by-Row Processing** - Saves progress incrementally (safe from interruptions)  
✅ **Custom Rules** - Define your own processing logic via rules file  
✅ **Error Handling** - Built-in retry logic and error recording  
✅ **Progress Tracking** - TODO list updates after each item  
✅ **Flexible** - Works with APIs, web scraping, data transformation, etc.  
✅ **Verification** - Ensures all items are processed before completion  

## How to Use

### Step 1: Create Your Input File

Create a text file with one item per line:

**`items_list.txt`**
```
item1
item2
item3
```

### Step 2: Create Your Processing Rules File

Create a markdown file defining how to process each item:

**`processing_rules.md`**
```markdown
# Processing Rules

## URL_TEMPLATE
https://api.example.com/{item}

## FIELDS_TO_EXTRACT
1. **field1**: JSON path `$.data.field1`
2. **field2**: JSON path `$.data.field2`

## OUTPUT_FORMAT
Name: {input_item}
Field 1: {field1}
Field 2: {field2}

## ERROR_HANDLING
- HTTP 404: Record as `Error: Not found (HTTP 404)`
- Missing field: Record as `Not found`
```

See `data-processor.chatmode.md` for complete rules file format documentation.

### Step 3: Run the Processor

Use this prompt format in GitHub Copilot:

```
process #file:items_list.txt based on #file:processing_rules.md
```

### Step 4: Monitor Progress

The chatmode will automatically:
1. Create `processing_todo.md` with a checklist
2. Process each item and update the TODO list
3. Write results to `processed_output.md`
4. Report completion when all items are processed

## Use Cases

- **Web Scraping** - Extract data from websites for a list of items
- **API Data Collection** - Fetch information from REST APIs
- **Batch Validation** - Verify items against a data source
- **Data Transformation** - Convert and enrich data from various sources
- **Content Aggregation** - Collect information into a unified format

## Processing Rules Format

Your rules file should include these sections:

- **URL_TEMPLATE** - How to construct URLs from input items
- **FIELDS_TO_EXTRACT** - What data to extract and how
- **OUTPUT_FORMAT** - How to format the results
- **ERROR_HANDLING** - How to handle errors
- **REQUEST_SETTINGS** - Delays, timeouts, headers, etc.

See the full chatmode documentation in `data-processor.chatmode.md` for complete details.

## File Structure

```
data-processor.chatmode.md     # Main chatmode definition
demo/
  jsonplaceholder_example/     # Complete working example
    inputs/
      users_list.txt           # Sample input list
      jsonplaceholder_rules.md # Sample rules file
    outputs/
      processed_output.md      # Generated results
      processing_todo.md       # Progress tracking
```

---

## Example: JSONPlaceholder API

A complete working example is included in `demo/jsonplaceholder_example/`.

### Input File (`users_list.txt`)
```
1
2
3
5
999
```

### Rules File (`jsonplaceholder_rules.md`)
```markdown
# JSONPlaceholder User Info Processing Rules

## URL_TEMPLATE
https://jsonplaceholder.typicode.com/users/{item}

## FIELDS_TO_EXTRACT
1. **name**: JSON path `$.name`
2. **email**: JSON path `$.email`
3. **city**: JSON path `$.address.city`
4. **company**: JSON path `$.company.name`
5. **website**: JSON path `$.website`, default `Not provided`

## OUTPUT_FORMAT
User ID: {input_item}
API URL: {constructed_url}
Name: {name}
Email: {email}
City: {city}
Company: {company}
Website: {website}

## ERROR_HANDLING
- HTTP 404: Record as `Error: User not found (HTTP 404)`
- Missing field: Record as `Not found`

## REQUEST_SETTINGS
- Delay between requests: 0.5 seconds
- Timeout: 10 seconds
```

### Prompt Used
```bash
process #file:users_list.txt based on #file:jsonplaceholder_rules.md 
```

### Output Generated (`processed_output.md`)
```
User ID: 1
API URL: https://jsonplaceholder.typicode.com/users/1
Name: Leanne Graham
Email: Sincere@april.biz
City: Gwenborough
Company: Romaguera-Crona
Website: hildegard.org

User ID: 2
API URL: https://jsonplaceholder.typicode.com/users/2
Name: Ervin Howell
Email: Shanna@melissa.tv
City: Wisokyburgh
Company: Deckow-Crist
Website: anastasia.net

User ID: 3
API URL: https://jsonplaceholder.typicode.com/users/3
Name: Clementine Bauch
Email: Nathan@yesenia.net
City: McKenziehaven
Company: Romaguera-Jacobson
Website: ramiro.info

User ID: 5
API URL: https://jsonplaceholder.typicode.com/users/5
Name: Chelsey Dietrich
Email: Lucio_Hettinger@annie.ca
City: Roscoeview
Company: Keebler LLC
Website: demarco.info

User ID: 999
API URL: https://jsonplaceholder.typicode.com/users/999
Error: User not found (HTTP 404)
```

Notice how user ID 999 was handled gracefully with an error message instead of invented data.

---

## Notes

- The processor runs completely autonomously after the TODO list is created
- Progress is saved incrementally - safe to interrupt and resume
- Never fabricates data - only records what's actually found
- Respects rate limits and delays specified in rules
- Works with JSON APIs, HTML scraping, or any other data source
