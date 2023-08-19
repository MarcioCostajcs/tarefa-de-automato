# tarefa-de-automato

class AutomatoFinitoDeterministico:
    def __init__(self):
        self.estado_atual = 'q0'
        self.estados_finais = {'q0', 'q2'}

    def processar_entrada(self, entrada):
        for simbolo in entrada:
            if simbolo not in {'a', 'b'}:
                return False

            if self.estado_atual == 'q0':
                if simbolo == 'a':
                    self.estado_atual = 'q0'
                else:
                    self.estado_atual = 'q1'
            elif self.estado_atual == 'q1':
                if simbolo == 'a':
                    self.estado_atual = 'q2'
                else:
                    self.estado_atual = 'q0'
            elif self.estado_atual == 'q2':
                if simbolo == 'a':
                    self.estado_atual = 'q1'
                else:
                    self.estado_atual = 'q2'

        return self.estado_atual in self.estados_finais


# Criar o autômato
automato = AutomatoFinitoDeterministico()

# Processar algumas entradas
entradas = ['bab', 'bba', 'ababab', 'bbbb', 'baaa']
for entrada in entradas:
    if automato.processar_entrada(entrada):
        print(f'A entrada "{entrada}" foi aceita pelo autômato.')
    else:
        print(f'A entrada "{entrada}" foi rejeitada pelo autômato.')
