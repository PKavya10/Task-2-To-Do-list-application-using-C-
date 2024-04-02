#include <iostream>
#include <vector>
#include <string>
#include <algorithm> // For std::find

using namespace std;

class ToDoList {
private:
    vector<string> tasks;

public:
    void addTask(const string& task) {
        tasks.push_back(task);
        cout << "Task added: " << task << endl;
    }

    void viewTasks() {
        if (tasks.empty()) {
            cout << "No tasks in the list." << endl;
        } else {
            cout << "Tasks:" << endl;
            for (size_t i = 0; i < tasks.size(); ++i) {
                cout << i+1 << ". " << tasks[i] << endl;
            }
        }
    }

    void searchTask(const string& keyword) {
        vector<string> matchingTasks;
        for (const string& task : tasks) {
            if (task.find(keyword) != string::npos) {
                matchingTasks.push_back(task);
            }
        }

        if (matchingTasks.empty()) {
            cout << "No matching tasks found." << endl;
        } else {
            cout << "Matching Tasks:" << endl;
            for (const string& task : matchingTasks) {
                cout << "- " << task << endl;
            }
        }
    }

    void removeTask(const string& task) {
        auto it = find(tasks.begin(), tasks.end(), task);
        if (it != tasks.end()) {
            tasks.erase(it);
            cout << "Task removed: " << task << endl;
        } else {
            cout << "Task not found." << endl;
        }
    }
};

int main() {
    ToDoList myList;
    int choice;
    string task;
    string keyword;

    do {
        cout << "\nTo-Do List Menu:" << endl;
        cout << "1. Add Task" << endl;
        cout << "2. View Tasks" << endl;
        cout << "3. Search Task" << endl;
        cout << "4. Remove Task" << endl;
        cout << "5. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Enter task: ";
                cin.ignore();
                getline(cin, task);
                myList.addTask(task);
                break;
            case 2:
                myList.viewTasks();
                break;
            case 3:
                cout << "Enter keyword to search: ";
                cin.ignore();
                getline(cin, keyword);
                myList.searchTask(keyword);
                break;
            case 4:
                cout << "Enter task to remove: ";
                cin.ignore();
                getline(cin, task);
                myList.removeTask(task);
                break;
            case 5:
                cout << "Exiting program." << endl;
                break;
            default:
                cout << "Invalid choice. Please enter a number between 1 and 5." << endl;
        }
    } while (choice != 5);

    return 0;
}
