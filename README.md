
Question::::https://codeforces.com/problemset/problem/1872/G            
                  
                  
                  # Import the sys module for reading input and set a constant for infinity.
                  import sys
                  INFINITY = int(1e9)
                  
                  # Define a function to read integers from standard input and return them as a list.
                  def read_integer(T=int):
                      return [T(i) for i in sys.stdin.readline().split()]
                  
                  # Define a function to solve a single test case.
                  def solve_case():
                      # Read the number of elements (n) and the list of integers (array) from input.
                      n, array = read_integer()[0], read_integer()
                      # Initialize an empty list to store the starting positions of intervals and a product variable.
                      interval_indices, product = [], 1
                  
                      # Iterate through the list of integers.
                      for i in range(n):
                          # Calculate the product of elements, ensuring it doesn't exceed INFINITY.
                          product = min(INFINITY, product * array[i])
                          # If the element is not equal to 1, append its position to the interval_indices list.
                          if array[i] - 1:
                              interval_indices.append(i)
                  
                      # Check if the product is equal to INFINITY, and if so, print the first and last interval positions and return.
                      if product == INFINITY:
                          print(interval_indices[0] + 1, interval_indices[-1] + 1)
                          return
                  
                      # Calculate the number of intervals, initialize variables for tracking the best interval, and the maximum difference.
                      num_intervals, left, right, max_difference = len(interval_indices), 0, 0, 0
                  
                      # Iterate through all possible pairs of intervals.
                      for i in range(num_intervals):
                          for j in range(i + 1, num_intervals):
                              # Initialize variables for calculating the product of elements in the current interval.
                              old_product, new_product = 0, 1
                              # Iterate through the elements in the current interval and calculate the old and new product.
                              for x in range(i, j + 1):
                                  new_product *= array[interval_indices[x]]
                                  old_product += array[interval_indices[x]]
                  
                              # Calculate the current difference between new and old products, adjusting for interval length.
                              current_difference = new_product - old_product - ((interval_indices[j] - interval_indices[i] + 1) - (j - i + 1))
                              
                              # Update the maximum difference and interval positions if the current difference is larger.
                              if current_difference > max_difference:
                                  max_difference, left, right = current_difference, interval_indices[i], interval_indices[j]
                  
                      # Print the starting positions of the best interval, adding 1 to convert from 0-based indexing to 1-based indexing.
                      print(left + 1, right + 1)
                  
                  # Define the main function.
                  def main():
                      # Read the number of test cases from input.
                      num_test_cases = read_integer(int)[0]
                      # Iterate through each test case and solve it.
                      for _ in range(num_test_cases):
                          solve_case()
                  
                  # Call the main function to start the program.
                  main()
