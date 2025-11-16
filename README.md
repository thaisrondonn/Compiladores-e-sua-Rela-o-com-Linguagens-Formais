# Compiladores-e-sua-Rela-o-com-Linguagens-Formais
Aula de Linguagens Formais e Autômatos.

# lexer.py
import re

TOKEN_REGEX = [
    ("NUM", r"\d+"),
    ("PLUS", r"\+"),
    ("SPACE", r"[ \t]+"),
]

def lexer(texto):
    tokens = []
    i = 0
    while i < len(texto):
        match = None
        for token_type, pattern in TOKEN_REGEX:
            regex = re.compile(pattern)
            match = regex.match(texto, i)
            if match:
                lexema = match.group(0)
                if token_type != "SPACE":
                    tokens.append((token_type, lexema))
                i = match.end(0)
                break
        if not match:
            raise ValueError(f"Símbolo inválido na posição {i}: {texto[i]}")
    return tokens


# parser.py
def parser(tokens):
    if len(tokens) != 3:
        raise ValueError("Expressão inválida.")

    if tokens[0][0] != "NUM":
        raise ValueError("A expressão deve começar com um número.")

    if tokens[1][0] != "PLUS":
        raise ValueError("Falta o operador '+'.")

    if tokens[2][0] != "NUM":
        raise ValueError("A expressão deve terminar com um número.")

    return "Expressão sintaticamente válida!"


# main.py
from lexer import lexer
from parser import parser

codigo_fonte = "23 + 7"

print("Código fonte:", codigo_fonte)

tokens = lexer(codigo_fonte)
print("Tokens:", tokens)

resultado = parser(tokens)
print("Parser:", resultado)


# README.md
# Mini Compilador — Linguagens Formais e Autômatos

Este projeto demonstra, de forma simples, como funciona um processo básico de compilação utilizando conceitos de **linguagens formais**, **autômatos** e **gramáticas livres de contexto**.

## Arquivos
- **lexer.py** — Implementa o analisador léxico usando expressões regulares (linguagens regulares / AFD)
- **parser.py** — Implementa o analisador sintático usando uma GLC simples
- **main.py** — Executa o processo completo
- **README.md** — Documentação do projeto

## Gramática utilizada (GLC)
```
Expressao → NUM PLUS NUM
```

## Como executar
```bash
python3 main.py
```

## Resultado esperado
```
Código fonte: 23 + 7
Tokens: [('NUM', '23'), ('PLUS', '+'), ('NUM', '7')]
Parser: Expressão sintaticamente válida!
