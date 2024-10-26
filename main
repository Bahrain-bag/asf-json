import os
import json
import tkinter as tk
from tkinter import filedialog


def create_json_files(input_folder, output_folder):
    if not os.path.exists(output_folder):
        os.makedirs(output_folder)

    count = 0

    for filename in os.listdir(input_folder):
        if filename.endswith('.txt'):
            with open(os.path.join(input_folder, filename), 'r') as file:
                lines = file.readlines()

                if not lines:
                    log_text.insert(tk.END, f"File {filename} is empty. Skipping.\n")
                    continue

                for line in lines:
                    content = line.strip().split(':')
                    if len(content) < 2:
                        log_text.insert(tk.END, f"Invalid line in {filename}: {line}\n")
                        continue

                    login = content[0]
                    password = content[1]

                    json_data = {
                        "AcceptGifts": True,
                        "Enabled": True,
                        "FarmingPreferences": 128,
                        "SteamLogin": login,
                        "SteamPassword": password
                    }
                    output_file_path = os.path.join(output_folder, f'{login}.json')
                    with open(output_file_path, 'w') as json_file:
                        json.dump(json_data, json_file, indent=4)

                    count += 1

                    log_text.insert(tk.END, f'Successfully created JSON file: {output_file_path}\n')

    log_text.insert(tk.END, f'Готово! JSON файлы в количестве {count} были созданы в папке {output_folder}.\n')


def browse_input_folder():
    folder_path = filedialog.askdirectory()
    input_folder_entry.delete(0, tk.END)
    input_folder_entry.insert(0, folder_path)


def browse_output_folder():
    folder_path = filedialog.askdirectory()
    output_folder_entry.delete(0, tk.END)
    output_folder_entry.insert(0, folder_path)


def start_processing():
    input_folder = input_folder_entry.get()
    output_folder = output_folder_entry.get()

    log_text.delete(1.0, tk.END)  # Clear previous log

    if not input_folder or not output_folder:
        log_text.insert(tk.END, "Выберите входную и выходную папки.\n")
    else:
        create_json_files(input_folder, output_folder)


# Создаем основное окно
root = tk.Tk()
root.title("Конвертер TXT в JSON")

# Применяем темную цветовую схему
root.configure(bg='#333333')
root.option_add('*background', '#333333')
root.option_add('*foreground', '#ffffff')

# Растягиваемость окна
root.columnconfigure(0, weight=1)
root.rowconfigure(4, weight=1)

# Создаем и размещаем виджеты на окне
input_folder_label = tk.Label(root, text="Входная папка:", bg='#333333', fg='#ffffff')
input_folder_label.grid(row=0, column=0, padx=10, pady=5, sticky="e")

input_folder_entry = tk.Entry(root, width=40)
input_folder_entry.grid(row=0, column=1, padx=5, pady=5)

input_folder_button = tk.Button(root, text="Обзор", command=browse_input_folder, bg='#666666', fg='#ffffff',
                                relief=tk.RAISED, borderwidth=3)
input_folder_button.grid(row=0, column=2, padx=5, pady=5)

output_folder_label = tk.Label(root, text="Выходная папка:", bg='#333333', fg='#ffffff')
output_folder_label.grid(row=1, column=0, padx=10, pady=5, sticky="e")

output_folder_entry = tk.Entry(root, width=40)
output_folder_entry.grid(row=1, column=1, padx=5, pady=5)

output_folder_button = tk.Button(root, text="Обзор", command=browse_output_folder, bg='#666666', fg='#ffffff',
                                 relief=tk.RAISED, borderwidth=3)
output_folder_button.grid(row=1, column=2, padx=5, pady=5)

start_button = tk.Button(root, text="START", command=start_processing, bg='#4CAF50', fg='#ffffff', relief=tk.RAISED,
                         borderwidth=3)
start_button.grid(row=2, column=1, pady=10)

log_label = tk.Label(root, text="Лог действий:", bg='#333333', fg='#ffffff')
log_label.grid(row=3, column=0, columnspan=3, pady=(10, 5))

log_text = tk.Text(root, height=10, width=50, bg='#666666', fg='#ffffff')
log_text.grid(row=4, column=0, columnspan=3, padx=10, pady=5, sticky="nsew")

# Запускаем цикл обработки событий
root.mainloop()
