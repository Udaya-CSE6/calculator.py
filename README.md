# simple_calculator.py
# A simple command-line calculator

def add(a, b): return a + b
def sub(a, b): return a - b
def mul(a, b): return a * b
def div(a, b):
    if b == 0:
        raise ZeroDivisionError("Cannot divide by zero.")
    return a / b
def power(a, b): return a ** b
def mod(a, b):
    if b == 0:
        raise ZeroDivisionError("Cannot use modulus by zero.")
    return a % b

operations = {
    "1": ("Add", add),
    "2": ("Subtract", sub),
    "3": ("Multiply", mul),
    "4": ("Divide", div),
    "5": ("Power", power),
    "6": ("Modulus", mod),
    "0": ("Exit", None)
}

def print_menu():
    print("\nSimple Calculator")
    for key, (name, _) in operations.items():
        print(f"  {key}. {name}")
    print()

def get_number(prompt):
    while True:
        try:
            return float(input(prompt))
        except ValueError:
            print("  That's not a valid number. Try again.")

def main():
    while True:
        print_menu()
        choice = input("Choose an operation (0 to exit): ").strip()
        if choice not in operations:
            print("  Invalid choice — choose a number from the menu.")
            continue
        if choice == "0":
            print("Goodbye!")
            break

        op_name, op_func = operations[choice]
        a = get_number("  Enter first number: ")
        b = get_number("  Enter second number: ")

        try:
            result = op_func(a, b)
        except ZeroDivisionError as e:
            print(f"  Error: {e}")
            continue
        except Exception as e:
            print(f"  Unexpected error: {e}")
            continue

        # Show integer-like floats without .0
        if result == int(result):
            result = int(result)
        print(f"  Result of {op_name.lower()}ing {a} and {b} => {result}")

if __name__ == "__main__":
    main()

