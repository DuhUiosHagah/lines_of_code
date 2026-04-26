# lines_of_code

import sys
import tkinter as tk
from tkinter import filedialog, messagebox


def count_lines(filepath):
    try:
        with open(filepath) as f:
            count = 0
            for line in f:
                if line.strip() == "" or line.lstrip().startswith("#"):
                    continue
                count += 1
        return count
    except FileNotFoundError:
        messagebox.showerror("Erro", "File does not exist")
        return None


def browse_file():
    filepath = filedialog.askopenfilename(
        filetypes=[("Python files", "*.py")]
    )
    if filepath:
        entry.delete(0, tk.END)
        entry.insert(0, filepath)
        result = count_lines(filepath)
        if result is not None:
            result_label.config(text=f"Total number of valid lines: {result}")


# Janela principal
root = tk.Tk()
root.title("Lines of Code")
root.configure(bg="black")
root.geometry("500x200")
root.resizable(False, False)

# Título
title_label = tk.Label(
    root,
    text="Lines of Code",
    bg="black",
    fg="white",
    font=("Arial", 16, "bold")
)
title_label.pack(pady=(20, 10))

# Frame para o campo + botão
frame = tk.Frame(root, bg="black")
frame.pack(pady=5)

entry = tk.Entry(frame, width=40, font=("Arial", 11))
entry.pack(side=tk.LEFT, padx=(0, 5))

browse_btn = tk.Button(
    frame,
    text="Buscar",
    font=("Arial", 11),
    command=browse_file
)
browse_btn.pack(side=tk.LEFT)

# Resultado
result_label = tk.Label(
    root,
    text="",
    bg="black",
    fg="white",
    font=("Arial", 13)
)
result_label.pack(pady=10)

# Símbolo decorativo
symbol_label = tk.Label(
    root,
    text="۞",
    bg="black",
    fg="white",
    font=("Arial", 13)
)
symbol_label.pack(side=tk.BOTTOM, pady=10)

root.mainloop()
