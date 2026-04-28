# get_next_line

[English](#english) · [Español](#español)

---

## English

### Overview

`get_next_line` is a C function that reads from a file descriptor **line by line**, returning one line per call (including the trailing `\n` when present). This project is commonly associated with the **42 School** curriculum.

### Features

- Reads from any valid **file descriptor**
- Returns **one line per call**
- Handles lines of arbitrary length using an internal buffer (`BUFFER_SIZE`)
- Keeps leftover data between calls (static storage)

### Bonus

This repository includes the **bonus** implementation (multiple file descriptors), using:

- `get_next_line_bonus.c`
- `get_next_line_utils_bonus.c`
- `get_next_line_bonus.h`

The bonus version stores leftover data per file descriptor (e.g. `static char *data[1024];`).

### Files

Mandatory:

- `get_next_line.c`
- `get_next_line_utils.c`
- `get_next_line.h`

Bonus:

- `get_next_line_bonus.c`
- `get_next_line_utils_bonus.c`
- `get_next_line_bonus.h`

### Build / Usage

#### Mandatory

```bash
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 \
  get_next_line.c get_next_line_utils.c your_program.c -o gnl
```

#### Bonus

```bash
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 \
  get_next_line_bonus.c get_next_line_utils_bonus.c your_program.c -o gnl_bonus
```

### Example

```c
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>
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
- The function returns `NULL` when there is nothing left to read or on error.
- The caller is responsible for `free()`-ing the returned line.

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

### Bonus

Este repositorio incluye la implementación **bonus** (múltiples file descriptors), usando:

- `get_next_line_bonus.c`
- `get_next_line_utils_bonus.c`
- `get_next_line_bonus.h`

La versión bonus guarda el contenido sobrante por file descriptor (por ejemplo `static char *data[1024];`).

### Archivos

Obligatorio:

- `get_next_line.c`
- `get_next_line_utils.c`
- `get_next_line.h`

Bonus:

- `get_next_line_bonus.c`
- `get_next_line_utils_bonus.c`
- `get_next_line_bonus.h`

### Compilación / Uso

#### Mandatory

```bash
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 \
  get_next_line.c get_next_line_utils.c tu_programa.c -o gnl
```

#### Bonus

```bash
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 \
  get_next_line_bonus.c get_next_line_utils_bonus.c tu_programa.c -o gnl_bonus
```

### Ejemplo

```c
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>
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

### Autor

- GitHub: [@brturcio](https://github.com/brturcio)
