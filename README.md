# tarefa-de-automato

class AutomatoFinitoDeterministico:
    def __init__(self):
        self.estado_atual = 'q0'
        self.estados_finais = {'q0', 'q2'}

    def processar_entrada(self, entrada):
        for simbolo in entrada:
            if simbolo not in {'a', 'b', '&'}:
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


class AutomatoFinitoNaoDeterministico:
    def __init__(self):
        self.estados = {'q0', 'q1', 'q2'}
        self.alphabet = {'a', 'b','&'}
        self.transitions = {
            'q0': {'a': {'q0', 'q1'}, 'b': {'q0'},'&': {'q1'}},
            'q1': {'a': {'q2'}, 'b': {'q0'},'&': {'q1'}},
            'q2': {'a': {'q1', 'q2'}, 'b': {'q2'}, '&': set()},
        }
        self.start_state = 'q0'
        self.accept_states = {'q0', 'q2'}

    def processar_entrada(self, entrada):
        current_states = {self.start_state}
        for simbolo in entrada:
            if simbolo not in self.alphabet:
                return False
            next_states = set()
            for state in current_states:
                if simbolo in self.transitions[state]:
                    next_states.update(self.transitions[state][simbolo])
            current_states = next_states
        return any(state in self.accept_states for state in current_states)

    @staticmethod
  
    def converter_nfa_em_dfa(nfa):
        
        pass



automato_dfa = AutomatoFinitoDeterministico()


entradas = ['bab', 'bba', 'ababab', 'bbbb', 'baaa']
for entrada in entradas:
    if automato_dfa.processar_entrada(entrada):
        print(f'A entrada "{entrada}" foi aceita pelo autômato DFA.')
    else:
        print(f'A entrada "{entrada}" foi rejeitada pelo autômato DFA.')


automato_nfa = AutomatoFinitoNaoDeterministico()


entradas_nfa = ['bab', 'bba', 'ababab', 'bbbb', 'baaa']
for entrada in entradas_nfa:
    if automato_nfa.processar_entrada(entrada):
        print(f'A entrada "{entrada}" foi aceita pelo autômato NFA.')
    else:
        print(f'A entrada "{entrada}" foi rejeitada pelo autômato NFA.')
