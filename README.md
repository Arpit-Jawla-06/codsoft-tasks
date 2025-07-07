# codsoft-tasks
task 1
              CALCULATOR

Design a simple calculator with basic arithmetic operations.
Prompt the user to input two numbers and an operation choice.
Perform the calculation and display the result.

          code

import tkinter as tk

def on_click(event):
    text = event.widget.cget("text")
    if text == "=":
        try:
            result = str(eval(entry.get()))
            entry.delete(0, tk.END)
            entry.insert(tk.END, result)
        except Exception as e:
            entry.delete(0, tk.END)
            entry.insert(tk.END, "Error")
    elif text == "C":
        entry.delete(0, tk.END)
    else:
        entry.insert(tk.END, text)

root = tk.Tk()
root.title("Simple Calculator")

entry = tk.Entry(root, font="Arial 20", borderwidth=5, relief=tk.RIDGE, justify='right')
entry.pack(fill=tk.BOTH, ipadx=8, pady=10, padx=10)

button_frame = tk.Frame(root)
button_frame.pack()

buttons = [
    ["7", "8", "9", "/"],
    ["4", "5", "6", "*"],
    ["1", "2", "3", "-"],
    ["C", "0", "=", "+"]
]

for row in buttons:
    row_frame = tk.Frame(button_frame)
    row_frame.pack(expand=True, fill="both")
    for btn_text in row:
        button = tk.Button(row_frame, text=btn_text, font="Arial 18", height=2, width=5)
        button.pack(side="left", expand=True, fill="both", padx=2, pady=2)
        button.bind("<Button-1>", on_click)

root.mainloop()

                         TASK 2

Rock-Paper-Scissors Game
User Input: Prompt the user to choose rock, paper, or scissors.
Computer Selection: Generate a random choice (rock, paper, or scissors) for
the computer.

Game Logic: Determine the winner based on the user's choice and the
computer's choice.

Rock beats scissors, scissors beat paper, and paper beats rock.
Display Result: Show the user's choice and the computer's choice.
Display the result, whether the user wins, loses, or it's a tie.
Score Tracking (Optional): Keep track of the user's and computer's scores for
multiple rounds.

Play Again: Ask the user if they want to play another round.

       
User Interface: Design a user-friendly interface with clear instructions and

feedback.

code


import tkinter as tk
import random

# Game logic
def play(user_choice):
    options = ['Rock', 'Paper', 'Scissors']
    computer_choice = random.choice(options)

    result = ''
    if user_choice == computer_choice:
        result = "It's a Tie!"
    elif (user_choice == 'Rock' and computer_choice == 'Scissors') or \
         (user_choice == 'Paper' and computer_choice == 'Rock') or \
         (user_choice == 'Scissors' and computer_choice == 'Paper'):
        result = "You Win!"
    else:
        result = "You Lose!"

    user_label.config(text=f"Your Choice: {user_choice}")
    comp_label.config(text=f"Computer's Choice: {computer_choice}")
    result_label.config(text=result)

# UI setup
root = tk.Tk()
root.title("Rock Paper Scissors")
root.geometry("300x300")
root.resizable(False, False)

title = tk.Label(root, text="Rock Paper Scissors", font=('Helvetica', 16, 'bold'))
title.pack(pady=10)

frame = tk.Frame(root)
frame.pack(pady=10)

rock_btn = tk.Button(frame, text="Rock", width=10, command=lambda: play('Rock'))
paper_btn = tk.Button(frame, text="Paper", width=10, command=lambda: play('Paper'))
scissors_btn = tk.Button(frame, text="Scissors", width=10, command=lambda: play('Scissors'))

rock_btn.grid(row=0, column=0, padx=5)
paper_btn.grid(row=0, column=1, padx=5)
scissors_btn.grid(row=0, column=2, padx=5)

user_label = tk.Label(root, text="Your Choice: ", font=('Helvetica', 12))
user_label.pack(pady=5)

comp_label = tk.Label(root, text="Computer's Choice: ", font=('Helvetica', 12))
comp_label.pack(pady=5)

result_label = tk.Label(root, text="", font=('Helvetica', 14, 'bold'))
result_label.pack(pady=10)

root.mainloop()


                                     task 3 

contact book

Contact Information: Store name, phone number, email, and address for each contact.
Add Contact: Allow users to add new contacts with their details.
View Contact List: Display a list of all saved contacts with names and phone numbers.
Search Contact: Implement a search function to find contacts by name or phone number.
Update Contact: Enable users to update contact details.
Delete Contact: Provide an option to delete a contact.
User Interface: Design a user-friendly interface for easy interaction.

code

import tkinter as tk
from tkinter import messagebox
from tkinter import simpledialog

# Contact list
contacts = []

# Add Contact
def add_contact():
    name = name_entry.get().strip()
    phone = phone_entry.get().strip()
    email = email_entry.get().strip()
    address = address_entry.get().strip()

    if not name or not phone:
        messagebox.showerror("Error", "Name and Phone are required!")
        return

    contact = {"name": name, "phone": phone, "email": email, "address": address}
    contacts.append(contact)
    update_listbox()
    clear_entries()

# Update Contact
def update_contact():
    selected = listbox.curselection()
    if not selected:
        messagebox.showerror("Error", "Select a contact to update.")
        return

    index = selected[0]
    contact = contacts[index]

    contact['name'] = name_entry.get().strip()
    contact['phone'] = phone_entry.get().strip()
    contact['email'] = email_entry.get().strip()
    contact['address'] = address_entry.get().strip()

    update_listbox()
    clear_entries()

# Delete Contact
def delete_contact():
    selected = listbox.curselection()
    if not selected:
        messagebox.showerror("Error", "Select a contact to delete.")
        return

    index = selected[0]
    del contacts[index]
    update_listbox()
    clear_entries()

# View Contact
def view_contact(event):
    selected = listbox.curselection()
    if not selected:
        return

    index = selected[0]
    contact = contacts[index]

    name_entry.delete(0, tk.END)
    name_entry.insert(0, contact['name'])

    phone_entry.delete(0, tk.END)
    phone_entry.insert(0, contact['phone'])

    email_entry.delete(0, tk.END)
    email_entry.insert(0, contact['email'])

    address_entry.delete(0, tk.END)
    address_entry.insert(0, contact['address'])

# Search Contact
def search_contact():
    query = search_entry.get().strip().lower()
    results = []
    for contact in contacts:
        if query in contact['name'].lower() or query in contact['phone']:
            results.append(contact)

    update_listbox(results)

# Refresh list
def update_listbox(display_list=None):
    listbox.delete(0, tk.END)
    display = display_list if display_list is not None else contacts
    for contact in display:
        listbox.insert(tk.END, f"{contact['name']} - {contact['phone']}")

# Clear input fields
def clear_entries():
    name_entry.delete(0, tk.END)
    phone_entry.delete(0, tk.END)
    email_entry.delete(0, tk.END)
    address_entry.delete(0, tk.END)

# Setup GUI
root = tk.Tk()
root.title("Contact Manager")
root.geometry("500x500")
root.resizable(False, False)

# Input Fields
tk.Label(root, text="Name").grid(row=0, column=0, sticky="w", padx=10, pady=5)
name_entry = tk.Entry(root, width=40)
name_entry.grid(row=0, column=1, pady=5)

tk.Label(root, text="Phone").grid(row=1, column=0, sticky="w", padx=10)
phone_entry = tk.Entry(root, width=40)
phone_entry.grid(row=1, column=1)

tk.Label(root, text="Email").grid(row=2, column=0, sticky="w", padx=10)
email_entry = tk.Entry(root, width=40)
email_entry.grid(row=2, column=1)

tk.Label(root, text="Address").grid(row=3, column=0, sticky="w", padx=10)
address_entry = tk.Entry(root, width=40)
address_entry.grid(row=3, column=1)

# Buttons
tk.Button(root, text="Add", width=10, command=add_contact).grid(row=4, column=0, pady=10)
tk.Button(root, text="Update", width=10, command=update_contact).grid(row=4, column=1, sticky="w")
tk.Button(root, text="Delete", width=10, command=delete_contact).grid(row=4, column=1, sticky="e")

# Search Bar
tk.Label(root, text="Search").grid(row=5, column=0, padx=10, sticky="w")
search_entry = tk.Entry(root, width=30)
search_entry.grid(row=5, column=1, sticky="w")
tk.Button(root, text="Go", command=search_contact).grid(row=5, column=1, sticky="e")

# Contact List
listbox = tk.Listbox(root, width=65, height=15)
listbox.grid(row=6, column=0, columnspan=2, padx=10, pady=10)
listbox.bind('<<ListboxSelect>>', view_contact)

# Start App
root.mainloop()
