import re

# Definição dos padrões (linguagens regulares)
TOKEN_REGEX = [
    ("NUM", r"\d+"),
    ("PLUS", r"\+"),
    ("SPACE", r"[ \t]+"),  # ignorar espaços
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
