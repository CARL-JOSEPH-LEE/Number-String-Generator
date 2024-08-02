import random
import tkinter as tk
from tkinter import ttk, scrolledtext

def generate_random_string(l, q, x):
    result = []
    current_number = random.randint(0, 9)

    for i in range(l):
        result.append(str(current_number))
        if random.random() < q:
            current_number = random.randint(0, 9)
        if random.random() < x:
            result.append('\n')

    return ''.join(result)

def on_generate():
    try:
        l = int(length_entry.get())
        q = float(chaos_entry.get())
        x = float(newline_entry.get())
        result = generate_random_string(l, q, x)
        output_text.delete(1.0, tk.END)
        output_text.insert(tk.INSERT, result)
    except ValueError:
        output_text.delete(1.0, tk.END)
        output_text.insert(tk.INSERT, "Invalid input. Please enter valid numbers.")

# Create the main window
root = tk.Tk()
root.title("Number String Generator")

# Length input
length_label = ttk.Label(root, text="Length of the string:")
length_label.grid(column=0, row=0, padx=10, pady=5)
length_entry = ttk.Entry(root)
length_entry.grid(column=1, row=0, padx=10, pady=5)

# Chaos degree input
chaos_label = ttk.Label(root, text="Chaos degree (0 to 1):")
chaos_label.grid(column=0, row=1, padx=10, pady=5)
chaos_entry = ttk.Entry(root)
chaos_entry.grid(column=1, row=1, padx=10, pady=5)

# Newline probability input
newline_label = ttk.Label(root, text="Newline probability (0 to 1):")
newline_label.grid(column=0, row=2, padx=10, pady=5)
newline_entry = ttk.Entry(root)
newline_entry.grid(column=1, row=2, padx=10, pady=5)

# Generate button
generate_button = ttk.Button(root, text="Generate", command=on_generate)
generate_button.grid(column=0, row=3, columnspan=2, pady=10)

# Output text area
output_text = scrolledtext.ScrolledText(root, width=40, height=10)
output_text.grid(column=0, row=4, columnspan=2, padx=10, pady=10)

# Run the application
root.mainloop()
