#include <iostream>
#include <vector>
#include <string>

struct Task {
    std::string description;
    bool completed;

    // Constructor to initialize task
    Task(const std::string& desc) : description(desc), completed(false) {}
};

class ToDoList {
private:
    std::vector<Task> tasks;

public:
    // Function to add a task to the list
    void addTask(const std::string& description) {
        tasks.push_back(Task(description));
        std::cout << "Task added: " << description << std::endl;
    }

    // Function to display all tasks
    void viewTasks() const {
        if (tasks.empty()) {
            std::cout << "No tasks in the list." << std::endl;
        } else {
            std::cout << "Tasks:" << std::endl;
            for (size_t i = 0; i < tasks.size(); ++i) {
                std::cout << i + 1 << ". ";
                if (tasks[i].completed) {
                    std::cout << "[Completed] ";
                }
                std::cout << tasks[i].description << std::endl;
            }
        }
    }

    // Function to mark a task as completed
    void markAsCompleted(size_t index) {
        if (index > 0 && index <= tasks.size()) {
            tasks[index - 1].completed = true;
            std::cout << "Task marked as completed: " << tasks[index - 1].description << std::endl;
        } else {
            std::cout << "Invalid task index." << std::endl;
        }
    }

    // Function to remove a task from the list
    void removeTask(size_t index) {
        if (index > 0 && index <= tasks.size()) {
            std::cout << "Task removed: " << tasks[index - 1].description << std::endl;
            tasks.erase(tasks.begin() + index - 1);
        } else {
            std::cout << "Invalid task index." << std::endl;
        }
    }
};

int main() {
    ToDoList todoList;

    char choice;
    do {
        std::cout << "\nTO-DO LIST MANAGER\n";
        std::cout << "1. Add Task\n";
        std::cout << "2. View Tasks\n";
        std::cout << "3. Mark Task as Completed\n";
        std::cout << "4. Remove Task\n";
        std::cout << "5. Quit\n";
        std::cout << "Enter your choice: ";
        std::cin >> choice;

        switch (choice) {
            case '1': {
                std::string taskDescription;
                std::cout << "Enter task description: ";
                std::cin.ignore();  // Ignore any previous newline character
                std::getline(std::cin, taskDescription);
                todoList.addTask(taskDescription);
                break;
            }
            case '2':
                todoList.viewTasks();
                break;
            case '3': {
                size_t taskIndex;
                std::cout << "Enter the index of the task to mark as completed: ";
                std::cin >> taskIndex;
                todoList.markAsCompleted(taskIndex);
                break;
            }
            case '4': {
                size_t taskIndex;
                std::cout << "Enter the index of the task to remove: ";
                std::cin >> taskIndex;
                todoList.removeTask(taskIndex);
                break;
            }
            case '5':
                std::cout << "Exiting the program. Goodbye!\n";
                break;
            default:
                std::cout << "Invalid choice. Please enter a valid option.\n";
        }

    } while (choice != '5');

    return 0;
}
