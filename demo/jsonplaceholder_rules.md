# JSONPlaceholder User Info Processing Rules

## URL_TEMPLATE
https://jsonplaceholder.typicode.com/users/{item}
- Simple numeric ID substitution
- Follow redirects: yes

## FIELDS_TO_EXTRACT
1. **name**: JSON path `$.name`
2. **email**: JSON path `$.email`
3. **city**: JSON path `$.address.city`
4. **company**: JSON path `$.company.name`
5. **website**: JSON path `$.website`, default `Not provided`

## OUTPUT_FORMAT
```
User ID: {input_item}
API URL: {constructed_url}
Name: {name}
Email: {email}
City: {city}
Company: {company}
Website: {website}
```

## ERROR_HANDLING
- HTTP 404: Record as `Error: User not found (HTTP 404)`
- HTTP 5xx: Retry once after 1 second, then record error
- Network timeout: Retry once after 2 seconds
- Missing field: Record as `Not found`

## PRE_PROCESSING
- Trim whitespace from input items
- Validate that item is numeric

## POST_PROCESSING
- Trim all field values
- Validate email format (just record, don't fail)

## SPECIAL_CONDITIONS
- None for this simple API

## REQUEST_SETTINGS
- User-Agent: Mozilla/5.0 (compatible; DataProcessor/1.0)
- Delay between requests: 0.5 seconds
- Timeout: 10 seconds
- Follow redirects: yes
