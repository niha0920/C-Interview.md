## 1. Storage classes
| Keyword    | Meaning                        | Lifetime | Scope        | Example                 |
| ---------- | ------------------------------ | -------- | ------------ | ----------------------- |
| `auto`     | Default for local vars         | Block    | Local        | `auto int a = 5;`       |
| `static`   | Persists across function calls | Program  | Local/Global | `static int count = 0;` |
| `extern`   | Declared in another file       | Program  | Global       | `extern int x;`         |
| `register` | Suggests CPU register use      | Block    | Local        | `register int i;`       |
