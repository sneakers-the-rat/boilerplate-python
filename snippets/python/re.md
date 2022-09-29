[[Regular Expressions]] [[regex]]

## Capturing Groups

Reuse text from capturing group with [[re.sub]]

```python
re.sub(r"(\w)", "\1", "input text")
```