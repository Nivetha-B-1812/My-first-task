import json
import os

FILENAME = "todo_list.json"

def load_tasks():
    if os.path.exists(FILENAME):
        with open(FILENAME, 'r') as file:
            return json.load(file)
    return []

def save_tasks(tasks):
    with open(FILENAME, 'w') as file:
        json.dump(tasks, file)

def display_tasks(tasks):
    if not tasks:
        print("📭 No tasks available.")
    else:
        print("\n📋 To-Do List:")
        for i, task in enumerate(tasks, 1):
            status = "✅" if task['done'] else "❌"
            print(f"{i}. {status} {task['task']}")

def add_task(tasks):
    new_task = input("Enter new task: ")
    tasks.append({'task': new_task, 'done': False})
    print("✅ Task added.")

def mark_done(tasks):
    display_tasks(tasks)
    index = int(input("Enter task number to mark as done: ")) - 1
    if 0 <= index < len(tasks):
        tasks[index]['done'] = True
        print("✅ Task marked as done.")
    else:
        print("❌ Invalid task number.")

def delete_task(tasks):
    display_tasks(tasks)
    index = int(input("Enter task number to delete: ")) - 1
    if 0 <= index < len(tasks):
        tasks.pop(index)
        print("🗑️ Task deleted.")
    else:
        print("❌ Invalid task number.")

def main():
    tasks = load_tasks()

    while True:
        print("\n🔘 MENU:")
        print("1. View Tasks")
        print("2. Add Task")
        print("3. Mark Task as Done")
        print("4. Delete Task")
        print("5. Exit")

        choice = input("Choose an option: ")

        if choice == '1':
            display_tasks(tasks)
        elif choice == '2':
            add_task(tasks)
        elif choice == '3':
            mark_done(tasks)
        elif choice == '4':
            delete_task(tasks)
        elif choice == '5':
            save_tasks(tasks)
            print("🛑 Exiting... Tasks saved.")
            break
        else:
            print("❗ Invalid choice. Try again.")

if __name__ == "__main__":
    main()
