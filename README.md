# Smart-Data-Logger
A beginner-level Python project that logs and manages simple data entries.

"""
Smart Data Logger
-----------------
A beginner-friendly Python program that helps users store, view, and search for
data records (like daily expenses, study logs, or task notes).

It was designed to help new programmers understand file handling,
basic data structures, and input/output operations.
"""

import os
import datetime

DATA_FILE = "data_log.txt"

def log_entry():
    """Add a new record to the data log."""
    entry = input("Enter your log entry (e.g., Study: 2 hours, Topic: Python): ")
    timestamp = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    with open(DATA_FILE, "a") as file:
        file.write(f"{timestamp} - {entry}\n")
    print("✅ Entry added successfully!\n")

def view_logs():
    """View all logged entries."""
    if not os.path.exists(DATA_FILE):
        print("⚠️ No data log found yet.\n")
        return
    print("\n📘 Logged Entries:")
    with open(DATA_FILE, "r") as file:
        print(file.read())

def search_logs():
    """Search for specific keywords in logs."""
    keyword = input("Enter a keyword to search: ").lower()
    if not os.path.exists(DATA_FILE):
        print("⚠️ No data log found yet.\n")
        return
    print(f"\n🔍 Search results for '{keyword}':")
    with open(DATA_FILE, "r") as file:
        found = False
        for line in file:
            if keyword in line.lower():
                print(line.strip())
                found = True
        if not found:
            print("No matching entries found.")

def main():
    """Main menu loop."""
    while True:
        print("\n=== SMART DATA LOGGER ===")
        print("1. Add new entry")
        print("2. View all entries")
        print("3. Search entries")
        print("4. Exit")

        choice = input("Select an option (1-4): ").strip()
        if choice == "1":
            log_entry()
        elif choice == "2":
            view_logs()
        elif choice == "3":
            search_logs()
        elif choice == "4":
            print("👋 Exiting Smart Data Logger. Goodbye!")
            break
        else:
            print("❌ Invalid choice. Please try again.\n")

if __name__ == "__main__":
    main()
