# Quantum-TSP-Solver
TSP solver using QAOA. Finds approximate solution to Traveling Salesman Problem. Written in python(qiskit), efficient and quantum-inspired approach. Finds optimal route with minimum distance.
 here's an explanation of the code line by line:
first function 
This code defines the function create_cost_Hamiltonian(distances) which creates the cost Hamiltonian for the TSP.

The first line is the function definition, specifying the input variable distances which is a matrix of distances between the cities.
The second line uses the len() function to determine the number of cities, and assigns it to the variable n_cities.
The third line creates a 2D array of zeros with the shape (n_cities, n_cities) using the np.zeros() function and assigns it to the variable H. This creates a matrix of the same size as the distances matrix, which will later be filled with the elements of the cost Hamiltonian.
The fourth line starts a nested for loop that will iterate over the rows and columns of the distances matrix.
The fifth line checks if the current row and column indices i and j are not equal (i != j), which means that we are not on the diagonal of the matrix.
The sixth line assigns the value of the distances matrix at the current row and column indices to the corresponding element of the H matrix. This means that the H matrix will have the same elements as the distances matrix, but with the diagonal elements set to zero (since we are not assigning any values to the diagonal elements in this loop).
The seventh and eight lines are the end of the nested for loop and function definition respectively.
The last line returns the created matrix H which is the cost Hamiltonian.
So, in summary, this function creates a matrix of the same size as the input distances matrix, and fills this matrix with the elements of the distances matrix, but with the diagonal elements set to zero. This matrix H is the cost Hamiltonian for the TSP problem.
_________________________________
2nd function
This code defines the function create_mixer_Hamiltonian(n_cities) which creates the mixer Hamiltonian for the TSP.

The first line is the function definition, specifying the input variable n_cities which is the number of cities.
The second line creates a 2D array of ones with the shape (n_cities, n_cities) using the np.ones() function, and subtracts from it an identity matrix of the same shape using the np.eye() function, which is an array where the diagonal elements are set to 1 and the off-diagonal elements are set to 0. This subtraction is done element-wise. The result is assigned to the variable H.
The third line is the return statement which returns the created matrix H which is the mixer Hamiltonian.
So, in summary, this function creates a matrix of the same size as the input number of cities, and fills this matrix with all ones, except the diagonal elements which are set to zero. This matrix H is the mixer Hamiltonian for the TSP problem. The mixer Hamiltonian is used to create the mixing operation in QAOA which explores the solution space.
____________________________________________________________________
3rd function 
This code defines the function create_QAOA_circuit(distances, p) which creates the QAOA circuit for the TSP.

The first line is the function definition, specifying the input variables distances which is a matrix of distances between the cities and p which is the number of steps.
The second line uses the len() function to determine the number of cities, and assigns it to the variable n_cities.
The third and fourth lines create quantum registers and classical register with the number of qubits equal to the number of cities.
The fifth line creates a quantum circuit object qc which is associated with the quantum and classical registers.
The sixth and seventh lines creates the cost and mixer Hamiltonians by calling the functions create_cost_Hamiltonian(distances) and create_mixer_Hamiltonian(n_cities) respectively.
The eighth line starts a for loop that will iterate over the number of steps p.
The ninth line starts a nested for loop that will iterate over the rows and columns of the cost_H matrix.
The tenth line applies the cx gate, which is a controlled-NOT gate, on qubits j and k of the quantum register.
The eleventh line applies the rotation p-gate on qubit k of the quantum register with the rotation angle equal to negative of the element of cost_H matrix at indices i and j.
The twelfth line applies the cx gate again on qubits j and k of the quantum register.
The thirteenth line starts another nested for loop that will iterate over the number of cities.
The fourteenth line applies the h gate, which is the Hadamard gate, on qubit j of the quantum register.

The fifteenth line applies the x gate, which is the Pauli-X gate, on qubit j of the quantum register.
The sixteenth line adds barrier to the circuit.
The seventeenth line starts another nested for loop that will iterate over the rows and columns of the mixer_H matrix.
The eighteenth line applies the cx gate on qubits j and k of the quantum register.
The nineteenth line applies the rotation p-gate on qubit k of the quantum register with the rotation angle equal to negative of the element of mixer_H matrix at indices i and j.
The twentieth line applies the cx gate again on qubits j and k of the quantum register.
The twenty-first line starts another nested for loop that will iterate over the number of cities.
The twenty-second line applies the x gate on qubit j of the quantum register.
The twenty-third line applies the h gate on qubit j of the quantum register.
The twenty-fourth line ends the outer for loop that iterated over the number of steps p.
The twenty-fifth line starts another for loop that will iterate over the number of cities.
The twenty-sixth line measures qubit j of the quantum register and stores the result in the classical register.
The twenty-seventh line is the end of the function definition and it returns the quantum circuit object qc.
In summary, this function creates a quantum circuit that implements the QAOA algorithm for the TSP problem. The function creates quantum and classical registers, quantum circuit object, cost and mixer Hamiltonians, then iterates over the number of steps 'p' applying the cost and mixer Hamiltonians using cx, p, h and x gates and also includes measurements on all qubits. This circuit can be executed on a quantum computer or simulator to obtain the optimal solution for the TSP problem.
_________________________________________________________________________________________________________________________-
The Driver code starts here
This code is using the QAOA circuit that was created earlier and executing it on a simulator backend to obtain the results.

The first two lines define two lists. The first list cities is a list of city names, and the second list distances is a 2D array representing the distance between the cities.
The third line creates a variable cv which is the result of calling the function create_QAOA_circuit(distances, 4). This means that the QAOA circuit is created using the given distances matrix and the number of steps is 4.
The fifth line creates a variable backend which is the Aer simulator backend with the qasm_simulator provider.
The sixth line creates a variable result which is the result of executing the circuit with the given backend and number of shots.
The seventh line extracts the counts from the execution object.
The ninth line initializes an empty list called optimal_costs
The eleventh line starts a for loop that iterates over the results in the counts dictionary.
The twelfth line converts the bitstring to a list of integers and assigns it to the variable path.
The thirteenth line starts another for loop that iterates over the path and initializes the cost variable to 0.
The fourteenth line adds the distance between the current city and the next city to the cost variable.
The fifteenth line ends the inner for loop and adds the distance between the last city and the first city to the cost variable.
The sixteenth line appends the cost variable to the optimal_costs list.
The seventeenth line ends the outer for loop
The eighteenth line plots a histogram of the optimal costs using matplotlib library and shows the plot.
In summary, this code uses the results obtained from executing the QAOA circuit and computes the cost of each path obtained from the results. It converts the bitstring results to a list of integers representing the path, computes the cost of each path by adding the distances between the cities visited in the path, and appends the cost to a list. Finally, it plots a histogram of the optimal costs.
