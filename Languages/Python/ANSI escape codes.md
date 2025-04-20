ANSI escape codes are special character sequences that the terminal understands as formatting instructions

Here is a basic format (courtesy of ChatGPT)
```python
"\033[<style>;<fg>;<bg>mYour text here\033[0m"
```

Here is another example
```python
print("\033[31mThis is red text\033[0m")
print("\033[1;32mThis is bold green text\033[0m")
print("\033[33;44mYellow text on blue background\033[0m")
```
- `\033` = Escape character
- `[` Introduces a control sequence
- `m` Ends the sequence
- `0m` Resets formatting
- Always use `\033[0m` after coloring text or everything will have that formatting

Common color codes

| Color              | Foreground | Background |
| ------------------ | ---------- | ---------- |
| Black              | 30         | 40         |
| Red                | 31         | 41         |
| Green              | 32         | 42         |
| Yellow             | 33         | 43         |
| Blue               | 34         | 44         |
| Magenta            | 35         | 45         |
| Cyan               | 36         | 46         |
| White              | 37         | 47         |
| Bright versions(?) | 90-97      | 100-107    |
