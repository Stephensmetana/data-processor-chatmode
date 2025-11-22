# GitHub Repository Info Processing Rules

## URL_TEMPLATE
https://api.github.com/repos/{item}
- No special encoding needed for this API
- Follow redirects: yes

## FIELDS_TO_EXTRACT
1. **name**: JSON path `$.name`
2. **description**: JSON path `$.description`, default `No description provided`
3. **stars**: JSON path `$.stargazers_count`
4. **language**: JSON path `$.language`, default `Not specified`
5. **license**: JSON path `$.license.name`, default `No license`

## OUTPUT_FORMAT
```
Repository: {input_item}
URL: https://github.com/{input_item}
Name: {name}
Description: {description}
Stars: {stars}
Primary Language: {language}
License: {license}
```

## ERROR_HANDLING
- HTTP 404: Record as `Error: Repository not found (HTTP 404)`
- HTTP 403: Record as `Error: API rate limit exceeded (HTTP 403)`
- HTTP 5xx: Retry once after 1 second, then record error
- Network timeout: Retry once after 2 seconds
- Missing field: Record as `Not found`

## PRE_PROCESSING
- Trim whitespace from input items
- No URL encoding needed for GitHub API paths

## POST_PROCESSING
- Trim all field values
- Format star count with commas if needed

## SPECIAL_CONDITIONS
- If repository is archived, add `Note: This repository is archived`
- If repository is a fork, add `Note: This is a fork`

## REQUEST_SETTINGS
- User-Agent: Mozilla/5.0 (compatible; DataProcessor/1.0)
- Delay between requests: 1 second
- Timeout: 10 seconds
- Follow redirects: yes
