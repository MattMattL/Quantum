# Qumulator V2

## About This Repository
This is the second version of my original quantum computer simulator, Qumulator (2019).


I'm currently adding more libraries to implement a working quantum computer simulator:

_Complex numbers -> Matrices -> Qubit -> Set of Qubits -> Quantum Logic Gates -> Quantum Algorithm_


## Code

### Initialisation

```C++
#include "Qumulator.hpp"

Qubits<double> qubits(3); // 3 qubits of type double
Qubits<float> qubit(1); // 1 qubit of type float	
```

### Quantum Logic Gates

```C++
qubits.H(0);

qubits.X(0);
qubits.Y(0);
qubits.Z(0);

qubits.T(0); // phase
qubits.S(0);

qubits.U(0); // arbitrary unitary matrix

qubits.CNOT(0, 1);
qubits.CY(0, 1);
qubits.CZ(0, 1);
qubits.Toffoli(0, 1, 2);

qubits.Swap(0, 1);

qubits.Measure(0);
qubits.Measure(1);
qubits.Measure(2);
```

### Visualisation Library

```C++
Qubits<double> qubits(2);

qubits.enableGraphics = true;

// ADD CODE HERE

qubits.margin();
qubits.barrier();

// draw the diagram
qubits.graphics.draw();

// print on screen / save as file
qubits.graphics.print();
qubits.graphics.save("./name.txt");
```

### Matrices and Complex Numbers

```C++
// Initialise a 2 x 2 matrix and set the first entry to 1 - i
Matrix<double> m1(2, 2);
m1.set(0, 0, 1, -1);

// Set c1 = 1 + 2i and copy to the last entry of m1
Complex<double> c1(1, 2);
m1.set(1, 1, c);

// arithmetic operations (+, -, *, /)
Matrix<double> m2(2, 2);
m2 = m1 * m2; 
m2 *= m2
c = 2 * c;
c *= c

// tensor product
m2 = m1.tensor(m2)

// matrix manipulations
m.transpose(); 
m.conjugate();
m.dagger();
```

### Example Code
```C++
/*
 *	Implementing super dense coding using Qumulator library:
 *	transfering two classical bit worth of information with one qubit.
 */
#include "Qumulator.hpp"

int main()
{
	Qubits<double> qubits(2);
	Matrix<double> m_I(2, 2), m_X(2, 2), m_Z(2, 2), m_iY(2, 2);
	QuantumGates<double> gate;

	m_I = gate.Identity();
	m_X = gate.Pauli_X();
	m_Z = gate.Pauli_Z();
	m_iY = m_X * m_Z;

	qubits.H(0);
	qubits.CNOT(0, 1);

	qubits.U(m_X, 0); // any of I, X, Z, iY

	qubits.CNOT(0, 1);
	qubits.H(0);

	qubits.Measure(0);
	qubits.Measure(1);

	qubits.print();
	qubits.graphics.draw();
	qubits.graphics.print();

	return 0;
}
```

Result:
```
|00⟩ =  0               (0.000)
|01⟩ =  0               (0.000)
|10⟩ =  1.000 + 0.000i  (1.000)
|11⟩ =  0               (0.000)

──H──*──U──*──H──M═══
     │     │         
─────@─────@─────M═══
```

Circuit Diagram:
```
──H──*──U──*──H──M═══
     │     │         
─────@─────@─────M═══
```

### Level 3 Text
text text text
text text text

#### Level 4 Text
text text text
text text text

##### Level 5 Text
text text text
text text text

###### Level 6 Text
text text text
text text text
