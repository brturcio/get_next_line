# get_next_line

[English](#english) · [Español](#español)

---

## English

### Overview

`get_next_line` is a C function that reads a file descriptor **line by line**, returning one line per call (including the trailing `\n` when present). This project is commonly associated with the **42 School** curriculum.

### Features

- Reads from any valid **file descriptor**
- Returns **one line per call**
- Handles lines of arbitrary length using an internal buffer (`BUFFER_SIZE`)
- Manages leftover data between calls (static storage)

> Bonus (if implemented): support for **multiple file descriptors** at the same time.

### Files

Typical project structure:

- `get_next_line.c`
- `get_next_line_utils.c`
- `get_next_line.h`

### Build / Usage

1) Include the header:

```c
#include "get_next_line.h"
```

2) Compile your program with the project files:

```bash
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 \
  get_next_line.c get_next_line_utils.c your_program.c -o a.out
```

3) Example:

```c
#include <fcntl.h>
#include <stdio.h>
#include "get_next_line.h"

int main(void)
{
    int   fd = open("file.txt", O_RDONLY);
    char *line;

    if (fd < 0)
        return (1);

    while ((line = get_next_line(fd)) != NULL)
    {
        printf("%s", line);
        free(line);
    }
    close(fd);
    return (0);
}
```

### Notes

- `BUFFER_SIZE` controls how many bytes are read per `read()` call.
- Return value is `NULL` when there is nothing left to read or on error.
- The caller is responsible for `free()`-ing the returned line.

### Testing

You can quickly test with:

```bash
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=1 \
  get_next_line.c get_next_line_utils.c main.c -o gnl
./gnl
```

Try multiple `BUFFER_SIZE` values (e.g. 1, 42, 1024) and different inputs.

### Author

- GitHub: [@brturcio](https://github.com/brturcio)

---

## Español

### Descripción

`get_next_line` es una función en C que lee desde un **file descriptor** **línea por línea**, devolviendo una línea por llamada (incluyendo el `\n` final cuando existe). Este proyecto suele formar parte del currículo de **42 School**.

### Características

- Lee desde cualquier **descriptor de archivo** válido
- Devuelve **una línea por llamada**
- Soporta líneas de longitud arbitraria usando un buffer interno (`BUFFER_SIZE`)
- Conserva datos sobrantes entre llamadas (almacenamiento estático)

> Bonus (si lo implementaste): soporte para **múltiples file descriptors** al mismo tiempo.

### Archivos

Estructura típica del proyecto:

- `get_next_line.c`
- `get_next_line_utils.c`
- `get_next_line.h`

### Compilación / Uso

1) Incluye el header:

```c
#include "get_next_line.h"
```

2) Compila tu programa junto con los archivos del proyecto:

```bash
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 \
  get_next_line.c get_next_line_utils.c tu_programa.c -o a.out
```

3) Ejemplo:

```c
#include <fcntl.h>
#include <stdio.h>
#include "get_next_line.h"

int main(void)
{
    int   fd = open("file.txt", O_RDONLY);
    char *line;

    if (fd < 0)
        return (1);

    while ((line = get_next_line(fd)) != NULL)
    {
        printf("%s", line);
        free(line);
    }
    close(fd);
    return (0);
}
```

### Notas

- `BUFFER_SIZE` define cuántos bytes se leen por llamada a `read()`.
- La función devuelve `NULL` cuando no queda nada por leer o ante un error.
- El usuario debe hacer `free()` de la línea devuelta.

### Pruebas

Puedes probar rápido con:

```bash
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=1 \
  get_next_line.c get_next_line_utils.c main.c -o gnl
./gnl
```

Prueba distintos valores de `BUFFER_SIZE` (por ejemplo 1, 42, 1024) y diferentes archivos.

### Autor

- GitHub: [@brturcio](https://github.com/brturcio)
