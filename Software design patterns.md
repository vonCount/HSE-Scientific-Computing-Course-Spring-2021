Separation of concerns

One of the reasons for abstraction is to separate concerns: any given part of a given program should be written to solve a single problem; if the problem can be broken down conceptually into isolated sub-problems, then these sub-problems should be solved elsewhere.

x = int(input("Tell me the first number: "))
y = int(input("Tell me the second number: "))
op = input("tell me the operation (add, multiply): ")

if op == "add":
  print("result: ", x+y)
elif op == "multiply":
  print("result: ", x*y)

Exercise: In the above program, identify and describe at least two of the sub-problems which are solved multiple times. (I see at least three or four.)

Exercise: Choose one of the sub-problems, write a common solution to that subproblem in the form of a function, and modify the program to use your common solution instead of solving the problem multiple times.
