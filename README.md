# Quantum-TSP-Solver
TSP solver using QAOA. Finds approximate solution to Traveling Salesman Problem. Written in python(qiskit), efficient and quantum-inspired approach. Finds optimal route with minimum distance.
 here's an explanation of the code line by line:

1-import numpy as np: This line imports the NumPy library, which is used for numerical operations such as creating arrays and matrices.

2-import matplotlib.pyplot as plt: This line imports the Matplotlib library, which is used for creating plots and visualizations.

3-from qiskit.tools.visualization import plot_histogram: This line imports the plot_histogram function from the Qiskit library, which is used to display the results of a quantum circuit as a histogram.

4-from qiskit import QuantumCircuit, QuantumRegister, ClassicalRegister: These lines import the QuantumCircuit, QuantumRegister, and ClassicalRegister classes from the Qiskit library, which are used to create and manipulate quantum circuits.

5-from qiskit import execute, Aer: These lines import the execute function and Aer class from the Qiskit library, which are used to execute quantum circuits on a simulator or real quantum device.

def create_cost_Hamiltonian(distances):: This line starts the definition of a function named create_cost_Hamiltonian which takes a matrix of distances between the cities as input.

n_cities = len(distances): This line finds the number of cities by finding the length of the input distance matrix.

H = np.zeros((n_cities, n_cities)): This line creates a matrix of size n_cities * n_cities filled with zeroes. This matrix will be used to store the cost Hamiltonian.

for i in range(n_cities):: This line starts a for loop that iterates over the rows of the matrix.

for j in range(n_cities):: This line starts a nested for loop that iterates over the columns of the matrix.

if i != j:: This line checks if the current row and column indices are different. If they are different,

H[i][j] = distances[i][j]: This line assigns the value of the distance between the cities as the value in the cost Hamiltonian matrix.

return H: This line returns the cost Hamiltonian matrix.

def create_mixer_Hamiltonian(n_cities):: This line starts the definition of a function named create_mixer_Hamiltonian which takes the number of cities as input.

H = np.ones((n_cities, n_cities)) - np.eye(n_cities): This line creates a matrix of size n_cities * n_cities filled with ones and then subtracts the identity matrix of size n_cities * n_cities from it. This matrix will be used to store the mixer Hamiltonian.
