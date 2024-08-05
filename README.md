def print_grid(grid):
    """Prints the Sudoku grid."""
    for row in grid:
        print(" ".join(str(num) if num != 0 else '.' for num in row))
    print()

def is_safe(grid, row, col, num):
    """Checks if it's safe to place a number in a given position."""
    # Check if the number is not in the current row and column
    for x in range(9):
        if grid[row][x] == num or grid[x][col] == num:
            return False
    
    # Check if the number is not in the current 3x3 subgrid
    start_row = row - row % 3
    start_col = col - col % 3
    for i in range(3):
        for j in range(3):
            if grid[i + start_row][j + start_col] == num:
                return False
                
    return True

def solve_sudoku(grid):
    """Solves the Sudoku puzzle using backtracking."""
    for row in range(9):
        for col in range(9):
            if grid[row][col] == 0:
                for num in range(1, 10):
                    if is_safe(grid, row, col, num):
                        grid[row][col] = num
                        if solve_sudoku(grid):
                            return True
                        grid[row][col] = 0
                return False
    return True

# Sample Sudoku puzzle
sudoku_grid = [
    [5, 3, 0, 0, 7, 0, 0, 0, 0],
    [6, 0, 0, 1, 9, 5, 0, 0, 0],
    [0, 9, 8, 0, 0, 0, 0, 6, 0],
    [8, 0, 0, 0, 6, 0, 0, 0, 3],
    [4, 0, 0, 8, 0, 3, 0, 0, 1],
    [7, 0, 0, 0, 2, 0, 0, 0, 6],
    [0, 6, 0, 0, 0, 0, 2, 8, 0],
    [0, 0, 0, 4, 1, 9, 0, 0, 5],
    [0, 0, 0, 0, 8, 0, 0, 7, 9]
]

print("Unsolved Sudoku:")
print_grid(sudoku_grid)

if solve_sudoku(sudoku_grid):
    print("Solved Sudoku:")
    print_grid(sudoku_grid)
else:
    print("No solution exists.")
