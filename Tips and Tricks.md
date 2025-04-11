1. A good way to optimize space complexity is to modify the existing input. For eg, in a matrix, instead of creating a visited array, the input matrix can be modified to signal visited (1 changed to 0).
2. In graphs, for union find, if the input is a matrix, nodes in the DS can be formed based on index of (i, j) using the formula:
			Index = i * TOTAL_COLS + j