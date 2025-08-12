# new-coding-bot
new repository
# github_project.py
# A simple CLI to-do list application

import json
import os

FILE_NAME = "tasks.json"

def load_tasks():
    """Load tasks from the JSON file."""
    if os.path.exists(FILE_NAME):
        with open(FILE_NAME, "r") as file:
            return json.load(file)
    return []

def save_tasks(tasks):
    """Save tasks to the JSON file."""
    with open(FILE_NAME, "w") as file:
        json.dump(tasks, file, indent=4)

def show_tasks(tasks):
    """Display all tasks."""
    if not tasks:
        print("\n✅ No tasks found. Your to-do list is empty!")
    else:
        print("\n📋 Your To-Do List:")
        for i, task in enumerate(tasks, 1):
            status = "✅" if task["done"] else "❌"
            print(f"{i}. {task['title']} - {status}")

def add_task(tasks):
    """Add a new task."""
    title = input("\nEnter task title: ").strip()
    if title:
        tasks.append({"title": title, "done": False})
        save_tasks(tasks)
        print(f"🆕 Task '{title}' added successfully!")
    else:
        print("⚠️ Task title cannot be empty.")

def mark_done(tasks):
    """Mark a task as done."""
    show_tasks(tasks)
    try:
        task_no = int(input("\nEnter task number to mark as done: "))
        if 1 <= task_no <= len(tasks):
            tasks[task_no - 1]["done"] = True
            save_tasks(tasks)
            print("✅ Task marked as done!")
        else:
            print("⚠️ Invalid task number.")
    except ValueError:
        print("⚠️ Please enter a valid number.")

def delete_task(tasks):
    """Delete a task."""
    show_tasks(tasks)
    try:
        task_no = int(input("\nEnter task number to delete: "))
        if 1 <= task_no <= len(tasks):
            removed_task = tasks.pop(task_no - 1)
            save_tasks(tasks)
            print(f"🗑️ Task '{removed_task['title']}' deleted successfully!")
        else:
            print("⚠️ Invalid task number.")
    except ValueError:
        print("⚠️ Please enter a valid number.")

def menu():
    """Main menu for the application."""
    tasks = load_tasks()
    while True:
        print("\n==== TO-DO LIST MENU ====")
        print("1️⃣ View Tasks")
        print("2️⃣ Add Task")
        print("3️⃣ Mark Task as Done")
        print("4️⃣ Delete Task")
        print("5️⃣ Exit")

        choice = input("Choose an option: ")
        if choice == "1":
            show_tasks(tasks)
        elif choice == "2":
            add_task(tasks)
        elif choice == "3":
            mark_done(tasks)
        elif choice == "4":
            delete_task(tasks)
        elif choice == "5":
            print("👋 Goodbye!")
            break
        else:
            print("⚠️ Invalid choice. Please try again.")

if __name__ == "__main__":
    menu()
