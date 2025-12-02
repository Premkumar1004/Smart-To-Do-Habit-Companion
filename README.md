# Smart-To-Do-Habit-Companion
tasks = []
habits = {}
habit_streak = {}

def add_task():
    t = input("Enter task: ")
    tasks.append({"task": t, "done": False})
    print("Task added!\n")

def view_tasks():
    if not tasks:
        print("No tasks yet.\n")
        return
    for i, t in enumerate(tasks):
        status = "✓" if t["done"] else "✗"
        print(f"{i+1}. {t['task']} [{status}]")
    print()

def mark_task_done():
    view_tasks()
    num = int(input("Task number to mark done: "))
    tasks[num-1]["done"] = True
    print("Marked as done!\n")

def add_habit():
    h = input("Enter habit: ")
    habits[h] = False
    habit_streak[h] = 0
    print("Habit added!\n")

def track_habits():
    if not habits:
        print("No habits yet.\n")
        return

    print("\nDid you complete these habits today? (y/n):")
    for h in habits:
        ans = input(f"{h}: ").lower()
        if ans == "y":
            habits[h] = True
            habit_streak[h] += 1
        else:
            habits[h] = False
            habit_streak[h] = 0
    print()

def daily_insight():
    # Task score
    if tasks:
        done = sum(1 for t in tasks if t["done"])
        task_score = int((done / len(tasks)) * 100)
    else:
        task_score = 0

    # Habit score
    if habit_streak:
        max_streak = max(habit_streak.values())
    else:
        max_streak = 0

    print("\DAILY INSIGHT")
    print(f"Task completion: {task_score}%")
    print(f"Best habit streak: {max_streak} days")

    if task_score > 80 and max_streak >= 2:
        print("You're on fire! Keep it going!\n")
    elif task_score > 40:
        print(" Good job, try to finish a bit more tomorrow!\n")
    else:
        print("Slow day… but tomorrow is a new chance!\n")

def menu():
    while True:
        print("==== SMART TO-DO & HABIT COMPANION ====")
        print("1. Add Task")
        print("2. View Tasks")
        print("3. Mark Task Done")
        print("4. Add Habit")
        print("5. Track Today's Habits")
        print("6. Daily Insight")
        print("7. Exit")

        choice = input("Choose: ")

        if choice == "1":
            add_task()
        elif choice == "2":
            view_tasks()
        elif choice == "3":
            mark_task_done()
        elif choice == "4":
            add_habit()
        elif choice == "5":
            track_habits()
        elif choice == "6":
            daily_insight()
        elif choice == "7":
            print("Goodbye!")
            break
        else:
            print("Invalid choice.\n")

menu()
