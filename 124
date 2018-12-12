import re
import sys

from utils import print_error, is_const, is_var, check_brackets

input_string = 'b2:=a-c=0; c:=(a-c)*2*a;'

print(input_string, end='\n\n')

keys = {"while": "while", "<>": "Not equals", "do": "do", "begin": "begin",
        ":=": "Assign", "=": "Equals", "-": "Minus", ";": "Semicolon", "+": "Plus",
        "[": "Square left bracket", "]": "Square right bracket", "end": "End", "if": "If",
        "then": "Then", "*": "Multiply", "/": "Division", "(": "Round left bracket",
        ")": "Round right bracket", ">": "More", "<": "Less", ":": "Colon"}

connectors = (':=', '=', '*', '/', '+', '-', '(', ')', '[', ']', ':')


tokens = re.findall(r':=|[\-\=\;\[\]\(\)\{\}\*/\+]|[a-zA-Z][\w\_]*|\d*', input_string)
# print(tokens)

for i, t in enumerate(tokens):
    if re.fullmatch(r'\w{1,100}', t):
        if re.fullmatch(r':=|-|\+|=|>|<|<>|;|\*|:|\)', tokens[i+1]):
            if re.fullmatch(r'=', tokens[i + 1]):
                print('Error. Incorrect ' + tokens[i+1])
                sys.exit()
        else:
            print_error(tokens[i+1], t)
    elif re.fullmatch(r':=', t):
        if re.fullmatch(r'\w{1,100}|\(|\)', tokens[i+1]):
            continue
        else:
            print_error(tokens[i+1], t)
    elif re.fullmatch(r'-|\+|\*|/', t):
        if re.fullmatch(r'\w{1,100}|\(|\)', tokens[i+1]):
            continue
        else:
            print_error(tokens[i+1], t)

check_brackets(input_string, '(', ')')
check_brackets(input_string, '[', ']')

# if all corect
for t in tokens:
    if t in keys:
        print(f'{t.ljust(5)} | KEY WORD {keys[t]}')
    elif is_const(t):
        print(f'{t.ljust(5)} | CONST')
    elif is_var(t):
        print(f'{t.ljust(5)} | VAR')
