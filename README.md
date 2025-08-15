# Game
import tkinter as tk
import random

words = ["raz", "rz", "tavakoli",' py', "hello"]
word = random.choice(words)
guessed = ["_"] * len(word)

def update_word():
    label_word.config(text=" ".join(guessed))

def check_letter(letter, btn):
    btn.config(state="disabled")  
    if letter in word:
        for i, ch in enumerate(word):
            if ch == letter:
                guessed[i] = letter
        update_word()
    else:
        btn.config(bg="red")


root = tk.Tk()
root.title("حدس کلمه")

label_word = tk.Label(root, text=" ".join(guessed), font=("Arial", 24))
label_word.pack(pady=10)

frame_keys = tk.Frame(root)
frame_keys.pack()


alphabet = "abcdefghijklmnopqrstuvwxyz"
row = 0
col = 0
for letter in alphabet:
    btn = tk.Button(frame_keys, text=letter.upper(), width=4, height=2,
                    command=lambda l=letter, b=None: check_letter(l, b))
    btn.grid(row=row, column=col, padx=2, pady=2)
    btn.config(command=lambda l=letter, b=btn: check_letter(l, b))
    col += 1
    if col > 8:
        col = 0
        row += 1

root.mainloop()
