def print_grid(grid):
    for row in grid:
        print(" ".join(str(num) for num in row))

def find_empty_location(grid):
    for row in range(len(grid)):
        for col in range(len(grid[row])):
            if grid[row][col] == 0:
                return row, col
    return None

def is_safe(grid, row, col, num):
    # Check if num is not in the current row
    if num in grid[row]:
        return False
    
    # Check if num is not in the current column
    if num in [grid[r][col] for r in range(9)]:
        return False
    
    # Check if num is not in the current 3x3 box
    start_row, start_col = 3 * (row // 3), 3 * (col // 3)
    for i in range(3):
        for j in range(3):
            if grid[start_row + i][start_col + j] == num:
                return False

    return True

def solve_sudoku(grid):
    empty_location = find_empty_location(grid)
    if not empty_location:
        return True  # Puzzle solved

    row, col = empty_location

    for num in range(1, 10):
        if is_safe(grid, row, col, num):
            grid[row][col] = num

            if solve_sudoku(grid):
                return True

            grid[row][col] = 0  # Reset and backtrack

    return False

def main():
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

    print("Sudoku Puzzle:")
    print_grid(sudoku_grid)

    if solve_sudoku(sudoku_grid):
        print("\nSolved Sudoku Puzzle:")
        print_grid(sudoku_grid)
    else:
        print("No solution exists.")

if __name__ == "__main__":
    main()
