from typing import TYPE_CHECKING
if TYPE_CHECKING:
    from circuit_simulator.Circuit import Circuit

from circuit_simulator import Circuit, Element

class OperationalAmplifier(Element):
    """Class representing an ideal operational amplifier."""
    def __init__(
        self,
        parent_circuit: "Circuit",
        name: str,
        node_plus: int,
        node_minus: int,
        node_output: int,
    ) -> None:
        super().__init__(parent_circuit, name)
        self.node_plus = node_plus
        self.node_minus = node_minus
        self.node_output = node_output
        # Cria linha extra para a corrente da fonte de tensão ideal
        self.extra_line = parent_circuit.nodes + parent_circuit.extra_lines + 1
        self.parent_circuit.extra_lines += 1

    def add_conductance(self, G, I, x_t, deltaT, method):
        if method == 'BE':
            # Coluna da tensão da fonte (saída)
            G[self.node_output, self.extra_line] += +1
            G[0, self.extra_line] += -1  # nó de referência (terra)

            # Linha da equação de restrição: va - vb - vc = 0
            G[self.extra_line, self.node_plus] += +1
            G[self.extra_line, self.node_minus] += -1
            G[self.extra_line, self.node_output] += -1

            return G, I

        elif method == 'FE':
            print("Forward Euler method not implemented for OperationalAmplifier yet.")
            return G, I

        elif method == 'TRAP':
            print("Trapezoidal method not implemented for OperationalAmplifier yet.")
            return G, I

        else:
            raise ValueError("Método de análise desconhecido.")
