# <center>ASSIGNMENT NO - 6 Unit_1 </center>

## Title  
In Computer Engg. Dept. of VIT there are S.Y., T.Y., and B.Tech. students. Assume that all these students are on ground for a function. We need to identify a student of S.Y. div. (X) whose name is `"Neha"` and roll no. is `"17"`. Apply appropriate Searching method to identify the required student.

---

### Theory: Linear Search

Linear Search (also called Sequential Search) is the simplest searching algorithm.  
It works by checking each element of a list, one by one, until the desired element is found or the list ends.

---

### Algorithm (Step-by-Step)

1. Define `Student` struct with: `roll`, `name`, `city`, `className`, `branch`, `div`, `age`.  
2. Read `n` (number of student records).  
3. Allocate an array of `n` Students using `malloc`; if it fails → exit program.  
4. Prepare small sample arrays for: `name`, `city`, `className`, `branch`, `div`.  
5. For each student `i` from `0` to `n-1`:  
   - 5a. Set `roll = i + 1`.  
   - 5b. Pick random `name` from sample names array.  
   - 5c. Pick random `city` from sample cities array.  
   - 5d. Pick random `className` from sample classNames array.  
   - 5e. Pick random `branch` from sample branches array.  
   - 5f. Pick random `div` from sample divs array.  
   - 5g. Set random `age` between `18` and `22`.  
6. Print all student records so the user can see the dataset.  
7. Perform a **linear search** to identify a specific student whose:  
   - `className = "SE"` (S.Y.),  
   - `div = "B"`,  
   - `name = "Neha"`,  
   - `roll = 17`.  
   If match found → print the record; else → print `"RECORD NOT FOUND"`.  
8. Free the allocated memory using `free()` and end program.  

---

### Code

```cpp
#include <iostream>
#include <cstdlib>
#include <cstring>
#include <ctime>

using namespace std;

#define NAME_LEN    32
#define CITY_LEN    32
#define CLASS_LEN   8
#define BRANCH_LEN  12
#define DIV_LEN     4

struct Student
{
    int  roll;
    char name[NAME_LEN];
    char city[CITY_LEN];
    char className[CLASS_LEN];
    char branch[BRANCH_LEN];
    char div[DIV_LEN];
    int  age;
};

int main()
{
    srand(time(0)); // seed for randomness

    Student* st = nullptr;
    int n;

    cout << "Enter the Number of Student Records to create: ";
    cin >> n;

    st = (Student*)malloc(sizeof(Student) * n);
    if (!st)
    {
        cout << "Memory allocation failed." << endl;
        return -1;
    }

    const char* names[] = { "Abir","Aarav","Isha","Rohan","Priya","Vikas","Neha","Sahil","Anaya","Dev","Kriti",
        "Mira","Kabir","Tanvi","Yash","Riya","Arjun","Asha","Nikhil","Pooja","Kunal", "Vishal","Amir","Sharukh","Salman","Mrunal","Kirti" };
    const int N_NAMES = sizeof(names) / sizeof(names[0]);

    const char* cities[] = { "Amravati","Akola","Nagar","Pune","Mumbai","Nashik","Nagpur","Aurangabad","Thane","Satara","Solapur","Kolhapur","Nanded" };
    const int N_CITIES = sizeof(cities) / sizeof(cities[0]);

    const char* classes[] = { "FE","SE","TE","BE" };
    const int N_CLASSES = sizeof(classes) / sizeof(classes[0]);

    const char* branches[] = { "COMP","IT","AIDS","ENTC","MECH","CIVIL", "AIML", "IOT" };
    const int N_BRANCHES = sizeof(branches) / sizeof(branches[0]);

    const char* divs[] = { "A","B","C","D" };
    const int N_DIVS = sizeof(divs) / sizeof(divs[0]);

    // Fill student records randomly
    for (int i = 0; i < n; i++)
    {
        st[i].roll = i + 1;
        strcpy(st[i].name, names[rand() % N_NAMES]);
        strcpy(st[i].city, cities[rand() % N_CITIES]);
        strcpy(st[i].className, classes[rand() % N_CLASSES]);
        strcpy(st[i].branch, branches[rand() % N_BRANCHES]);
        strcpy(st[i].div, divs[rand() % N_DIVS]);
        st[i].age = 18 + (rand() % 5);
    }

    // Print all student records
    cout << "\n================ All Student Records ================\n";
    for (int i = 0; i < n; i++)
    {
        cout << "Roll: " << st[i].roll
             << " | Name: " << st[i].name
             << " | Class: " << st[i].className
             << " | Branch: " << st[i].branch
             << " | Div: " << st[i].div
             << " | Age: " << st[i].age << endl;
    }

    // Searching for a specific student of S.Y. div B with name "Neha" and roll no 17
    cout << "\nSearching for S.Y. student in Div B with Name='Neha' and Roll No=17...\n";
    bool found = false;

    for (int i = 0; i < n; i++)
    {
        if (strcmp(st[i].className, "SE") == 0 &&
            strcmp(st[i].div, "B") == 0 &&
            strcmp(st[i].name, "Neha") == 0 &&
            st[i].roll == 17)
        {
            cout << "\nRECORD FOUND:\n";
            cout << "Roll: " << st[i].roll
                 << " | Name: " << st[i].name
                 << " | Class: " << st[i].className
                 << " | Branch: " << st[i].branch
                 << " | Div: " << st[i].div
                 << " | Age: " << st[i].age << endl;
            found = true;
            break;
        }
    }

    if (!found)
        cout << "RECORD NOT FOUND." << endl;

    free(st); // free allocated memory
    return 0;
}

### Output
```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Linear_assign.cpp -o Linear_assign } ; if ($?) { .\Linear_assign }
Enter the Number of Student Records to create: 5

================ All Student Records ================
Roll: 1 | Name: Tanvi | Class: TE | Branch: COMP | Div: C | Age: 18
Roll: 2 | Name: Rohan | Class: SE | Branch: IOT | Div: C | Age: 18
Roll: 3 | Name: Rohan | Class: FE | Branch: MECH | Div: B | Age: 19
Roll: 4 | Name: Dev | Class: TE | Branch: AIML | Div: D | Age: 18
Roll: 5 | Name: Arjun | Class: BE | Branch: COMP | Div: B | Age: 18

Searching for S.Y. student in Div B with Name='Neha' and Roll No=17...
RECORD NOT FOUND.
```