#include <iostream>
#include <fstream>
#include <string>
#include <sstream>
using namespace std;

class student {
public:
    ifstream inputFile;
    string full_name, student_id, course, birthday, address, gender, degree_program, year_level, file_number;
    char record;
    string filename;
    string* fileNames; // Dynamic array to store filenames
    int fileCount = 0; // Counter for the number of filenames stored

    student() {
        fileNames = new string[1]; // Initialize with a single element
    }

    ~student() {
        delete[] fileNames; // Deallocate memory in the destructor
    }

    void menu();
    void AddNewRecord();
    void DisplayAllRecords();
    void DisplaySpecificRecord();
    void DeleteRecord();
    void SearchRecord();
};

void student::menu() {
menustart:
    int choice;
    char x;
    string end;
    system("cls");
    cout<< "------------------------------------"<<endl;
    cout<< "----------STUDENT MANAGEMENT--------"<<endl;
    cout<< "------------------------------------"<<endl;
    cout<<endl;
    cout << "1. Enter a New Record" << endl;
    cout << "2. Search for a Specific Record" << endl;
    cout << "3. Display all Records" << endl;
    cout << "4. Display a Specific Record" << endl;
    cout << "5. Delete a Record" << endl;
    cout << "6. Exit" << endl<<endl;
    cout << "Choose Options:[1/2/3/4/5/6]" << endl;
    cout << "What do you want to do?: ";
    cin >> choice;
    switch (choice) {
    case 1:
        do {
            AddNewRecord();
            cout << "Add Another Student Record? (Y, N): ";
            cin >> x;
        } while (x == 'y' || x == 'Y');
        
        break;
        
    case 2:
        SearchRecord();
        
        break;
       
    case 3:
        DisplayAllRecords();
        
        break;
        
    case 4:
    	DisplaySpecificRecord();
    	
    	break;
    	
    case 5:
    	DeleteRecord();
    	
    	break;
    	
    case 6:
    	cout << endl;
    	cout << "Group 4:" << endl;
    	cout << "Magbag, Coleen        " << endl;
    	cout << "Opulencia Kaiser      " << endl;
    	cout << "Reyes, Jan Andrei     " << endl;
    	cout << "Tee, Xyril Dvonne     " << endl;
    	cout << "Uy, Aislinn           " << endl;
    	
    	cout<<endl<<endl;
    	cout<<"type end to close program : ";
    	cin>>end;
    	exit(0);    	
    default:
        cout << "Only choose options in the menu.";
    }
    cout<<endl<<" type next\n";
    cin>>end;
    goto menustart;
}

void student::AddNewRecord() {
    system("cls");
    fstream inputFile;
    cout << "Add Student Information (use underscore instead of space)" << endl;

    string input;
    bool validInput;

    // File number validation
    do {
        cout << "Enter File Number: ";
        cin >> file_number;
        string dummy;
        getline(cin, dummy); // Dummy getline to consume newline character
        validInput = true;
        for (char c : file_number) {
            if (!isdigit(c)) {
                validInput = false;
                break;
            }
        }
        if (!validInput) {
            cout << "Invalid input. Only Numbers are allowed for File Number." << endl;
        }
    } while (!validInput);

    // Full name validation
    do {
        cout << "Enter Full Name: ";
        cin >> full_name;
        string dummy;
        getline(cin, dummy); // Dummy getline to consume newline character
        validInput = true;
        for (char c : full_name) {
            if (isdigit(c)) {
                validInput = false;
                break;
            }
        }
        if (!validInput) {
            cout << "Invalid input. Numbers are not allowed in Full Name." << endl;
        }
    } while (!validInput);

    // Student ID validation
    do {
        cout << "Enter Student ID.: ";
        cin >> student_id;
        string dummy;
        getline(cin, dummy); // Dummy getline to consume newline character
        validInput = true;
        for (char c : student_id) {
            if (!isdigit(c)) {
                validInput = false;
                break;
            }
        }
        if (!validInput) {
            cout << "Invalid input. Only numbers are allowed for Student ID." << endl;
        }
    } while (!validInput);

	
    // Birthday, Address, Gender, Degree Program, and File name have no restrictions
    cout << "Enter Course: ";
    cin >> course;
    string dummy;
    getline(cin, dummy); // Dummy getline to consume newline character
    cout << "Enter Birthday: ";
    cin >> birthday;
    getline(cin, dummy); // Dummy getline to consume newline character
    cout << "Enter Address: ";
    cin >> address;
    getline(cin, dummy); // Dummy getline to consume newline character
    do {
        cout << "Enter Gender: ";
        cin >> gender;
        string dummy;
        getline(cin, dummy); // Dummy getline to consume newline character
        validInput = true;
        for (char c : gender) {
            if (!isalpha(c)) {
                validInput = false;
                break;
            }
        }
        if (!validInput) {
            cout << "Invalid input. Only alphabetical characters are allowed for Gender." << endl;
        }
    } while (!validInput);
    do {
        cout << "Enter Degree Program: ";
        cin >> degree_program;
        string dummy;
        getline(cin, dummy); // Dummy getline to consume newline character
        validInput = true;
        for (char c : degree_program) {
            if (!isalpha(c)) {
                validInput = false;
                break;
            }
        }
        if (!validInput) {
            cout << "Invalid input. Only alphabetical characters are allowed for Degree Program." << endl;
        }
    } while (!validInput);
    cout << "Year Level: ";
    cin >> year_level;
    getline(cin, dummy); // Dummy getline to consume newline character
    cout << "Filename: ";
    cin >> filename;
    getline(cin, dummy); // Dummy getline to consume newline character
    filename += ".txt";

    inputFile.open(filename, ios::app | ios::out);
    inputFile << " " << file_number << " " << full_name << " " << student_id << " " << course << " " << birthday << " " << address << " " << gender << " " << degree_program << " " << year_level;
    inputFile.close();

    string* temp = new string[fileCount + 1];
    for (int i = 0; i < fileCount; i++) {
        temp[i] = fileNames[i];
    }
    temp[fileCount] = filename;
    delete[] fileNames;
    fileNames = temp; 
    fileCount++; 
}


void student::DisplayAllRecords() {
    system("cls");
    fstream inputFile;
    cout << "All Student Records" << "\n" "\n";

    for (int i = 0; i < fileCount; i++) {
        inputFile.open(fileNames[i], ios::in);
        if (inputFile.is_open()) {
            while (inputFile >> file_number >> full_name >> student_id >> course >> birthday >> address >> gender >> degree_program >> year_level) {
            	cout <<"---------------------------------------"<<endl;
                cout << "File Number: " << file_number << "\n";
                cout << "Name: " << full_name << "\n";
                cout << "Student ID: " << student_id << "\n";
                cout << "Course: " << course << "\n";
                cout << "Birthday: " << birthday << "\n";
                cout << "Address: " << address << "\n";
                cout << "Gender: " << gender << "\n";
                cout << "Degree Program: " << degree_program << "\n";
                cout << "Year Level: " << year_level << "\n" "\n" "\n";
            }
        }
        inputFile.close();
    }
}

void student::DisplaySpecificRecord() {
    system("cls");
    int choice;
    cout << "Select a file to display its contents:" << endl;
    cout <<"----------------------------------------"<<endl;

    for (int i = 0; i < fileCount; i++) {
        cout << i + 1 << ". " << fileNames[i] << endl;
    }

    cout << "Enter the number of the file you want to display: ";
    cin >> choice;

    if (choice < 1 || choice > fileCount) {
        cout << "Invalid selection. Please try again." << endl;
        return;
    }

    fstream inputFile;
    string selectedFileName = fileNames[choice - 1]; 
    inputFile.open(selectedFileName, ios::in);
    if (inputFile.is_open()) {
        while (inputFile >> file_number >> full_name >> student_id >> course >> birthday >> address >> gender >> degree_program >> year_level) {
           	cout <<"---------------------------------------"<<endl;
		    cout << "File Number: " << file_number << "\n";
            cout << "Name: " << full_name << "\n";
            cout << "Student ID: " << student_id << "\n";
            cout << "Course: " << course << "\n";
            cout << "Birthday: " << birthday << "\n";
            cout << "Address: " << address << "\n";
            cout << "Gender: " << gender << "\n";
            cout << "Degree Program: " << degree_program << "\n";
            cout << "Year Level: " << year_level << "\n";
        }
    } else {
        cout << "Failed to open the file." << endl;
    }
    inputFile.close();
}

void student::SearchRecord() {
    system("cls");
    string searchTerm;
    cout << "Enter a student ID or full name to search: ";
    cin >> searchTerm;

    bool matchFound = false;

    for (int i = 0; i < fileCount; i++) {
        fstream inputFile;
        inputFile.open(fileNames[i], ios::in);
        if (inputFile.is_open()) {
            string line;
            while (getline(inputFile, line)) {
                if (line.find(searchTerm) != string::npos) {
                    stringstream ss(line);
                    string file_number, full_name, student_id, course, birthday, address, gender, degree_program, year_level;
                    ss >> file_number >> full_name >> student_id >> course >> birthday >> address >> gender >> degree_program >> year_level;
					cout <<"-------------------------------------------------"<<endl;
                    cout << "File Number: " << file_number << "\n";
                    cout << "Name: " << full_name << "\n";
                    cout << "Student ID: " << student_id << "\n";
                    cout << "Course: " << course << "\n";
                    cout << "Birthday: " << birthday << "\n";
                    cout << "Address: " << address << "\n";
                    cout << "Gender: " << gender << "\n";
                    cout << "Degree Program: " << degree_program << "\n";
                    cout << "Year Level: " << year_level << "\n";
                    matchFound = true;
                    break; 
                }
            }
            inputFile.close();
        } else {
            cout << "Failed to open the file." << endl;
        }
    }

    if (!matchFound) {
        cout << "No student found with the given ID or name." << endl;
    }
}

void student::DeleteRecord() {
    system("cls");
    int choice;
    cout << "Select a file to delete:" << endl;
	cout <<"-----------------------------------------------"<<endl;
	
    for (int i = 0; i < fileCount; i++) {
        cout << i + 1 << ". " << fileNames[i] << endl;
    }

    cout << "Enter the number of the file you want to delete: ";
    cin >> choice;

    if (choice < 1 || choice > fileCount) {
        cout << "Invalid selection. Please try again." << endl;
        return;
    }

    string selectedFileName = fileNames[choice - 1];
    if (remove(selectedFileName.c_str()) == 0) {
        cout << "File deleted successfully." << endl;

        // Remove the filename from the fileNames array and adjust the fileCount
        for (int i = choice - 1; i < fileCount - 1; i++) {
            fileNames[i] = fileNames[i + 1];
        }
        fileCount--;
    } else {
        cout << "Failed to delete the file." << endl;
    }
}



int main() {
    student project; 
    project.menu();
    return 0;
}
