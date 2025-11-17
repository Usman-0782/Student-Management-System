# Student-Management-System
#include <iostream>
#include <vector>
#include <string>
using namespace std;

class Student {
private:
    int id;
    string name;
    int age;
    string grade;

public:
    Student(int id, string name, int age, string grade) {
        this->id = id;
        this->name = name;
        this->age = age;
        this->grade = grade;
    }

    int getId() { return id; }
    string getName() { return name; }
    int getAge() { return age; }
    string getGrade() { return grade; }

    void setName(string name) { this->name = name; }
    void setAge(int age) { this->age = age; }
    void setGrade(string grade) { this->grade = grade; }

    void display() {
        cout << "ID: " << id << ", Name: " << name
             << ", Age: " << age << ", Grade: " << grade << endl;
    }
};

class StudentManagement {
private:
    vector<Student> students;

public:
    void addStudent(const Student& s) {
        students.push_back(s);
        cout << "Student added successfully.\n";
    }

    void displayAll() {
        if (students.empty()) {
            cout << "No students to display.\n";
            return;
        }
        for (auto& s : students) {
            s.display();
        }
    }

    void updateStudent(int id, string newName, int newAge, string newGrade) {
        for (auto& s : students) {
            if (s.getId() == id) {
                s.setName(newName);
                s.setAge(newAge);
                s.setGrade(newGrade);
                cout << "Student updated successfully.\n";
                return;
            }
        }
        cout << "Student not found.\n";
    }

    void deleteStudent(int id) {
        for (auto it = students.begin(); it != students.end(); ++it) {
            if (it->getId() == id) {
                students.erase(it);
                cout << "Student deleted successfully.\n";
                return;
            }
        }
        cout << "Student not found.\n";
    }
};

int main() {
    StudentManagement sm;
    int choice, id, age;
    string name, grade;

    do {
        cout << "\n====== Student Management System ======\n";
        cout << "1. Add Student\n";
        cout << "2. Display All Students\n";
        cout << "3. Update Student\n";
        cout << "4. Delete Student\n";
        cout << "0. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        cin.ignore(); // input buffer clear

        switch (choice) {
            case 1:
                cout << "Enter ID: ";
                cin >> id;
                cin.ignore();
                cout << "Enter Name: ";
                getline(cin, name);
                cout << "Enter Age: ";
                cin >> age;
                cin.ignore();
                cout << "Enter Grade: ";
                getline(cin, grade);

                sm.addStudent(Student(id, name, age, grade));
                break;

            case 2:
                sm.displayAll();
                break;

            case 3:
                cout << "Enter ID to update: ";
                cin >> id;
                cin.ignore();
                cout << "New Name: ";
                getline(cin, name);
                cout << "New Age: ";
                cin >> age;
                cin.ignore();
                cout << "New Grade: ";
                getline(cin, grade);

                sm.updateStudent(id, name, age, grade);
                break;

            case 4:
                cout << "Enter ID to delete: ";
                cin >> id;
                sm.deleteStudent(id);
                break;

            case 0:
                cout << "\n=========================================\n";
                cout << "   Thanks for using the System! 😊\n";
                cout << "         Have a wonderful day! 🌟\n";
                cout << "               Goodbye! 👋\n";
                cout << "=========================================\n";
                break;

            default:
                cout << "Invalid choice. Try again.\n";
        }
    } while (choice != 0);

    return 0;
}
