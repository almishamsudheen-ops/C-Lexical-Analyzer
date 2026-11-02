# C Lexical Analyzer

A lexical analyzer (tokenizer) for C source files, written in C. It reads a C file, splits it into tokens, and prints each token with its category and the line number it appears on. This is the first phase of a compiler.

## Features

- Reads any C source file given on the command line
- Classifies each token into a category:
  - Preprocessor directives (`#include <stdio.h>`)
  - Keywords (data types such as `int` and `char`)
  - Non-data keywords (`return`, `for`)
  - Identifiers (`add`, `arr`, `sum`)
  - Numeric constants
  - String literals
  - Operators (`=`, `+`, `<`, `,`, `*`)
  - Symbols (`;`, `[`, `]`)
  - Round braces `( )` and curly braces `{ }`, opening and closing reported separately
- Prints the line number for every token
- Prints "Successfully parsed" when the whole file is read

## Getting Started

### Build

Requires `gcc` or any C compiler.

```bash
gcc main.c lexer.c -o lexer
```

### Usage

```bash
./lexer <path-to-c-file>
```

Example:

```bash
./lexer sample.c
```

## Sample Output

Input (`sample.c`):

```c
#include <stdio.h>
int add(int a, int b) {
    return a + b;
}

int main() {
    int arr[5] = {10, 20, 30, 40, 50};
    int sum = 0;

    for(int i = 0; i < 5; i++) {
        sum += arr[i];
    }

    char *msg = "Total sum:";
    printf("%s %d\n", msg, sum);
    return 0;
}
```

Output (first lines):

```
Line  1 : Preprocessor directive  :  #include <stdio.h>
Line  2 : Keyword                 :   int
Line  2 : identifier              :   add
Line  2 : round braces opening    :  (
Line  2 : Keyword                 :   int
Line  2 : identifier              :   a
Line  2 : operator                :  ,
Line  2 : Keyword                 :   int
Line  2 : identifier              :   b
Line  2 : round braces closing    :  )
Line  2 : curly braces opening    :  {
Line  3 : non-data keyword        :   return
Line  3 : identifier              :   a
Line  3 : operator                :  +
Line  3 : identifier              :   b
Line  3 : symbol                  :  ;
Line  4 : curly braces closing    :  }
...
Line 14 : String literals         :  "Total sum:"
Line 15 : identifier              :   printf
...
Line 17 : curly braces closing    :  }
Successfully parsed
```

## How it works

The program reads the source file one character at a time. It groups characters into a word, number, string, operator or symbol, then checks which category the token belongs to by comparing it against tables of keywords, operators and symbols. Each token is printed with its category and the current line number, and the line counter increases at every newline.

## Known Limitations

- Multi-character operators such as `++` and `+=` are printed as two separate operator tokens
- Floating-point numbers such as `3.14` may be split into separate tokens
- Hex and suffixed numbers such as `0xFF` or `10L` are not fully supported

## Possible Improvements

- Recognize multi-character operators (`==`, `++`, `+=`, `&&`)
- Support floats and hex numbers
- Add a separate token type for character literals
- Write the tokens to a file

## Concepts Covered

Lexical analysis, tokenization, string handling in C, file handling, compiler design (first phase).

## Author

**Almi Shamsudheen**

- GitHub: [@almishamsudheen-ops](https://github.com/almishamsudheen-ops)
- LinkedIn: [Almi Shamsudheen](https://www.linkedin.com/in/almi-shamsudheen-67b4592b2)
