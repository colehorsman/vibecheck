# TOON Format

Token-Oriented Object Notation. Save 30-60% on structured data.

## TL;DR

- **TOON** = compact format for sending data to AI
- **Savings** = 30-60% fewer tokens than JSON
- **Use for** = logs, arrays, tabular data
- **Don't use for** = nested objects, config files

---

## The Problem

JSON is verbose. Every key is repeated for every object:

```json
{
  "logs": [
    {"id": 2001, "level": "error", "message": "Auth failed", "timestamp": "2026-01-17T10:00:00Z"},
    {"id": 2002, "level": "warn", "message": "Retry threshold", "timestamp": "2026-01-17T10:01:00Z"},
    {"id": 2003, "level": "error", "message": "Connection lost", "timestamp": "2026-01-17T10:02:00Z"}
  ]
}
```

That's ~400 tokens for 3 log entries. The keys alone account for 40% of tokens.

---

## The Solution: TOON

Define the schema once, then just send values:

```
logs[3]{id,level,message,timestamp}:
  2001,error,Auth failed,2026-01-17T10:00:00Z
  2002,warn,Retry threshold,2026-01-17T10:01:00Z
  2003,error,Connection lost,2026-01-17T10:02:00Z
```

~150 tokens. Same information. 60% savings.

---

## TOON Syntax

### Basic Format

```
arrayName[count]{field1,field2,field3}:
  value1,value2,value3
  value1,value2,value3
```

### Components

| Part | Meaning | Example |
|------|---------|---------|
| `arrayName` | Name of the array | `logs` |
| `[count]` | Number of items | `[3]` |
| `{fields}` | Field names | `{id,level,message}` |
| `:` | Separator | |
| Values | One row per item | `2001,error,Auth failed` |

---

## Examples

### User List

**JSON (320 tokens):**
```json
{
  "users": [
    {"id": 1, "name": "Alice", "email": "alice@example.com", "role": "admin"},
    {"id": 2, "name": "Bob", "email": "bob@example.com", "role": "user"},
    {"id": 3, "name": "Carol", "email": "carol@example.com", "role": "user"}
  ]
}
```

**TOON (120 tokens):**
```
users[3]{id,name,email,role}:
  1,Alice,alice@example.com,admin
  2,Bob,bob@example.com,user
  3,Carol,carol@example.com,user
```

### API Responses

**JSON:**
```json
{
  "endpoints": [
    {"method": "GET", "path": "/users", "status": 200, "latency": 45},
    {"method": "POST", "path": "/users", "status": 201, "latency": 120},
    {"method": "GET", "path": "/users/1", "status": 200, "latency": 32}
  ]
}
```

**TOON:**
```
endpoints[3]{method,path,status,latency}:
  GET,/users,200,45
  POST,/users,201,120
  GET,/users/1,200,32
```

### Error Logs

**JSON:**
```json
{
  "errors": [
    {"code": "AUTH_001", "message": "Invalid token", "count": 15, "lastSeen": "10:30"},
    {"code": "DB_002", "message": "Connection timeout", "count": 3, "lastSeen": "10:45"},
    {"code": "API_003", "message": "Rate limited", "count": 8, "lastSeen": "10:50"}
  ]
}
```

**TOON:**
```
errors[3]{code,message,count,lastSeen}:
  AUTH_001,Invalid token,15,10:30
  DB_002,Connection timeout,3,10:45
  API_003,Rate limited,8,10:50
```

---

## When to Use TOON

### ✅ Good Use Cases

- Log entries
- Database query results
- API response arrays
- CSV-like data
- Metrics and statistics
- User lists
- Event streams

### ❌ Avoid TOON For

- Deeply nested objects
- Config files (use YAML/JSON)
- Single objects
- Data with many optional fields
- Complex relationships

---

## Handling Special Cases

### Values with Commas

Use quotes:

```
products[2]{name,description,price}:
  Widget,"A small, useful tool",9.99
  Gadget,"Large, complex device",49.99
```

### Empty Values

Use empty string or placeholder:

```
users[2]{name,email,phone}:
  Alice,alice@example.com,
  Bob,bob@example.com,555-1234
```

### Nested Data

Flatten or use separate TOON blocks:

```
# Instead of nested orders.items
orders[2]{id,customer,total}:
  1001,Alice,150.00
  1002,Bob,75.50

orderItems[4]{orderId,product,qty,price}:
  1001,Widget,2,20.00
  1001,Gadget,1,110.00
  1002,Widget,3,30.00
  1002,Tool,1,45.50
```

---

## Token Savings Calculator

| Data Type | JSON Tokens | TOON Tokens | Savings |
|-----------|-------------|-------------|---------|
| 10 log entries | ~800 | ~300 | 62% |
| 50 user records | ~4000 | ~1500 | 62% |
| 100 API calls | ~8000 | ~3000 | 62% |
| 1000 events | ~80000 | ~30000 | 62% |

The savings scale linearly with data size.

---

## Converting JSON to TOON

### Manual Process

1. Identify the array
2. Extract field names
3. Count items
4. Write header: `name[count]{fields}:`
5. Write values, one per line

### Quick Script (JavaScript)

```javascript
function jsonToToon(name, array) {
  if (!array.length) return `${name}[0]{}:`;
  
  const fields = Object.keys(array[0]);
  const header = `${name}[${array.length}]{${fields.join(',')}}:`;
  
  const rows = array.map(item => 
    fields.map(f => {
      const val = item[f]?.toString() || '';
      return val.includes(',') ? `"${val}"` : val;
    }).join(',')
  );
  
  return [header, ...rows].join('\n  ');
}

// Usage
const logs = [
  {id: 1, level: 'error', message: 'Failed'},
  {id: 2, level: 'warn', message: 'Retry'}
];

console.log(jsonToToon('logs', logs));
// logs[2]{id,level,message}:
//   1,error,Failed
//   2,warn,Retry
```

---

## Using TOON in Prompts

### Example Prompt

```markdown
Here are the recent error logs in TOON format:

errors[5]{timestamp,level,code,message}:
  10:30:15,error,AUTH_001,Invalid token
  10:30:45,warn,DB_002,Slow query (2.3s)
  10:31:00,error,AUTH_001,Invalid token
  10:31:30,error,API_003,Rate limit exceeded
  10:32:00,warn,DB_002,Slow query (1.8s)

Analyze these logs and identify:
1. The most common error
2. Any patterns
3. Recommended fixes
```

The AI understands TOON format and can parse it correctly.

---

## Best Practices

1. **Include count** - Helps AI validate parsing
2. **Consistent field order** - Same order in header and values
3. **Quote strings with commas** - Prevents parsing errors
4. **Use meaningful field names** - AI uses them for context
5. **Group related data** - Multiple TOON blocks for related arrays

---

## Resources

- [Original TOON Proposal](https://github.com/anthropics/anthropic-cookbook)
- [Token Optimization Guide](token-optimization.md)

---

*Less tokens. Same data. Better results.*
