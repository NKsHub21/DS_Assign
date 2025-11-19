## ASSIGNMENT NO - 2 Unit_1

\<p align="center"\>Implementation of Doubly Circular Linked List to Manage ‘Galaxy Multiplex’ Seat Reservations\</p\>

-----

## Concept: The Doubly Circular Linked List

A **Doubly Circular Linked List (DCLL)** is a complex linear data structure where elements (nodes) are sequentially linked in a **circular** fashion, and each node has pointers to both the **next** and **previous** nodes.

In the 'Galaxy Multiplex' structure:

  * Each row of seats is managed by its own DCLL.
  * The array of head pointers (`head_pointers_npk`) stores the starting node for each row.
  * Each node represents a seat and holds:
    1.  **Data Field:** Seat number and booking status (`is_booked_npk`).
    2.  **Pointer Field** (`next_npk`): Stores the memory address of the next seat.
    3.  **Pointer Field** (`prev_npk`): Stores the memory address of the previous seat.
  * **Circular Property:** For any row's DCLL, the `next_npk` pointer of the last seat points back to the first seat (`head_npk`), and the `prev_npk` pointer of the first seat points to the last seat.

-----

## Algorithms

### 1\. `get_node_npk()`

Allocate memory for a new seat node using `new DCLL_npk`.

Initialize `seat_number_npk` and `is_booked_npk`.

Set `prev_npk = NULL` and `next_npk = NULL`.

Return the new node.

### 2\. `create_multiplex_npk()`

Loop through all 8 rows.

For each row, loop through all 8 seats (1 to 8).

Create a new node (`new_node_npk`) for each seat and assign a random booking status.

If the list is empty, set `head_npk = last_npk = new_node_npk`.

Otherwise, link the new node to `last_npk`.

After creating all 8 nodes, establish the circular links: `last_npk->next_npk = head_npk` and `head_npk->prev_npk = last_npk`.

Store `head_npk` in the `head_pointers_npk` array for the current row.

### 3\. `display_available_seats_npk()`

Loop through the `head_pointers_npk` array (Rows 1 to 8).

For each row, start traversal from `head_npk`.

Use a `do-while` loop to print the seat number and booking status until the pointer returns to `head_npk`, which ensures all seats in the circular list are covered.

### 4\. `book_seats_npk()` (A Key Operation)

Accept the target row, starting seat number, and number of seats (`num_seats_npk`).

Locate the starting seat node (`current_npk`) in the DCLL for the target row.

Traverse `num_seats_npk` consecutive nodes starting from `current_npk` to **check** if they are all available (`is_booked_npk == false`).

If all are available, traverse the same range again and set `is_booked_npk = true` for each seat.

### 5\. `cancel_booking_npk()` (A Key Operation)

Accept the target row and seat number.

Locate the seat node (`current_npk`) in the DCLL for the target row.

If the node's `seat_number_npk` matches and `is_booked_npk` is true, set `current_npk->is_booked_npk = false`.

-----

## C++ Code Implementation

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
#include <cstring>

using namespace std;

// --------------------- Node Structure ---------------------
typedef struct seat_npk {
    int seat_number_npk;
    bool is_booked_npk;
    struct seat_npk* prev_npk;
    struct seat_npk* next_npk;
} DCLL_npk;

// --------------------- Constants and Global Array ---------------------
const int NUM_ROWS_npk = 8;
const int SEATS_PER_ROW_npk = 8;
DCLL_npk* head_pointers_npk[NUM_ROWS_npk];

// --------------------- Function Prototypes ---------------------
DCLL_npk* get_node_npk(int seat_num_npk, bool booked_npk);
void create_multiplex_npk();
void display_available_seats_npk();
void book_seats_npk();
void cancel_booking_npk();
DCLL_npk* destroy_list_npk(DCLL_npk* head_npk);
void destroy_multiplex_npk();
int menu_npk();

// --------------------- Menu Function ---------------------
int menu_npk() {
    int choice_npk;
    cout << "\n========== Galaxy Multiplex Reservation System ==========\n";
    cout << "1. Display Available Seats\n";
    cout << "2. Book Seats\n";
    cout << "3. Cancel Booking\n";
    cout << "4. Exit\n";
    cout << "Enter your choice: ";
    cin >> choice_npk;
    return choice_npk;
}

// --------------------- Main Function ---------------------
int main() {
    srand(time(0));
    create_multiplex_npk();

    int choice_npk;
    while (1) {
        choice_npk = menu_npk();
        switch (choice_npk) {
        case 1:
            display_available_seats_npk();
            break;
        case 2:
            book_seats_npk();
            break;
        case 3:
            cancel_booking_npk();
            break;
        case 4:
            destroy_multiplex_npk();
            cout << "Exiting program...\n";
            exit(0);
        default:
            cout << "Invalid choice.\n";
        }
    }
    return 0;
}

/* Function 1: get_node_npk()
Purpose: Allocates memory and initializes DCLL node
*/
DCLL_npk* get_node_npk(int seat_num_npk, bool booked_npk) {
    DCLL_npk* new_node_npk = new DCLL_npk;
    if (!new_node_npk) {
        cout << "Memory allocation failed.\n";
        exit(1);
    }
    new_node_npk->seat_number_npk = seat_num_npk;
    new_node_npk->is_booked_npk = booked_npk;
    new_node_npk->prev_npk = NULL;
    new_node_npk->next_npk = NULL;
    return new_node_npk;
}

/* Function 2: create_multiplex_npk()
Purpose: Initializes the DCLL for all rows with random bookings
*/
void create_multiplex_npk() {
    for (int i_npk = 0; i_npk < NUM_ROWS_npk; ++i_npk) {
        DCLL_npk* head_npk = NULL;
        DCLL_npk* last_npk = NULL;
        for (int j_npk = 1; j_npk <= SEATS_PER_ROW_npk; ++j_npk) {
            bool booked_npk = (rand() % 4 == 0); // Approx 25% randomly booked
            DCLL_npk* new_node_npk = get_node_npk(j_npk, booked_npk);

            if (!head_npk) {
                head_npk = new_node_npk;
                last_npk = new_node_npk;
            } else {
                last_npk->next_npk = new_node_npk;
                new_node_npk->prev_npk = last_npk;
                last_npk = new_node_npk;
            }
        }
        // Make it circular
        if (head_npk) {
            last_npk->next_npk = head_npk;
            head_npk->prev_npk = last_npk;
        }
        head_pointers_npk[i_npk] = head_npk;
    }
    cout << "Multiplex setup complete with random initial bookings.\n";
}

/* Function 3: display_available_seats_npk()
Purpose: Display the current list of available seats
*/
void display_available_seats_npk() {
    cout << "\n========== Current Seat Availability (Row: [Seat - Status]) ==========\n";
    for (int i_npk = 0; i_npk < NUM_ROWS_npk; ++i_npk) {
        cout << "Row " << (i_npk + 1) << ": ";
        DCLL_npk* head_npk = head_pointers_npk[i_npk];
        if (!head_npk) {
            cout << "Empty Row.\n";
            continue;
        }

        DCLL_npk* temp_npk = head_npk;
        do {
            cout << "[" << temp_npk->seat_number_npk << " - " << (temp_npk->is_booked_npk ? "Booked" : "Available") << "] ";
            temp_npk = temp_npk->next_npk;
        } while (temp_npk != head_npk);
        cout << "\n";
    }
}

/* Function 4: book_seats_npk()
Purpose: Book one or more seats
*/
void book_seats_npk() {
    int row_npk, num_seats_npk;
    cout << "Enter row number (1-" << NUM_ROWS_npk << "): ";
    cin >> row_npk;
    if (row_npk < 1 || row_npk > NUM_ROWS_npk) {
        cout << "Invalid row number.\n";
        return;
    }

    int row_index_npk = row_npk - 1;
    DCLL_npk* head_npk = head_pointers_npk[row_index_npk];
    if (!head_npk) {
        cout << "Row is empty/not initialized.\n";
        return;
    }

    cout << "Enter number of seats to book (1-" << SEATS_PER_ROW_npk << "): ";
    cin >> num_seats_npk;
    if (num_seats_npk < 1 || num_seats_npk > SEATS_PER_ROW_npk) {
        cout << "Invalid number of seats.\n";
        return;
    }

    cout << "Enter starting seat number to book (1-" << SEATS_PER_ROW_npk - num_seats_npk + 1 << "): ";
    int start_seat_npk;
    cin >> start_seat_npk;

    if (start_seat_npk < 1 || start_seat_npk > SEATS_PER_ROW_npk - num_seats_npk + 1) {
        cout << "Invalid starting seat number or range.\n";
        return;
    }

    DCLL_npk* current_npk = head_npk;
    int seats_checked_npk = 0;
    
    // Find the starting seat
    while (current_npk->seat_number_npk != start_seat_npk && seats_checked_npk < SEATS_PER_ROW_npk) {
        current_npk = current_npk->next_npk;
        seats_checked_npk++;
    }

    // Check availability of consecutive seats
    DCLL_npk* check_npk = current_npk;
    bool can_book_npk = true;
    for (int i_npk = 0; i_npk < num_seats_npk; ++i_npk) {
        if (check_npk->is_booked_npk) {
            can_book_npk = false;
            break;
        }
        check_npk = check_npk->next_npk;
    }

    if (!can_book_npk) {
        cout << "Booking failed: One or more selected seats are already booked.\n";
        return;
    }

    // Book the seats
    for (int i_npk = 0; i_npk < num_seats_npk; ++i_npk) {
        current_npk->is_booked_npk = true;
        current_npk = current_npk->next_npk;
    }

    cout << "Successfully booked " << num_seats_npk << " seats in Row " << row_npk << " starting from Seat " << start_seat_npk << ".\n";
}

/* Function 5: cancel_booking_npk()
Purpose: Cancel an existing booking
*/
void cancel_booking_npk() {
    int row_npk, seat_npk;
    cout << "Enter row number (1-" << NUM_ROWS_npk << ") for cancellation: ";
    cin >> row_npk;
    if (row_npk < 1 || row_npk > NUM_ROWS_npk) {
        cout << "Invalid row number.\n";
        return;
    }

    cout << "Enter seat number (1-" << SEATS_PER_ROW_npk << ") to cancel: ";
    cin >> seat_npk;
    if (seat_npk < 1 || seat_npk > SEATS_PER_ROW_npk) {
        cout << "Invalid seat number.\n";
        return;
    }

    int row_index_npk = row_npk - 1;
    DCLL_npk* head_npk = head_pointers_npk[row_index_npk];
    if (!head_npk) {
        cout << "Row is empty/not initialized.\n";
        return;
    }

    DCLL_npk* current_npk = head_npk;
    int seats_checked_npk = 0;

    // Find the seat
    while (current_npk->seat_number_npk != seat_npk && seats_checked_npk < SEATS_PER_ROW_npk) {
        current_npk = current_npk->next_npk;
        seats_checked_npk++;
    }

    if (current_npk->seat_number_npk == seat_npk) {
        if (current_npk->is_booked_npk) {
            current_npk->is_booked_npk = false;
            cout << "Booking for Row " << row_npk << ", Seat " << seat_npk << " cancelled successfully.\n";
        } else {
            cout << "Seat is not currently booked.\n";
        }
    } else {
        cout << "Seat not found.\n";
    }
}

/* Function 6: destroy_list_npk()
Purpose: Free all allocated nodes in a single row's list
*/
DCLL_npk* destroy_list_npk(DCLL_npk* head_npk) {
    if (!head_npk) return NULL;

    DCLL_npk* current_npk = head_npk->next_npk;
    DCLL_npk* temp_npk;
    
    // Break the circle
    head_npk->prev_npk->next_npk = NULL;
    head_npk->prev_npk = NULL;

    while (current_npk) {
        temp_npk = current_npk;
        current_npk = current_npk->next_npk;
        delete temp_npk;
    }
    delete head_npk;
    return NULL;
}

/* Function 7: destroy_multiplex_npk()
Purpose: Destroy all DCLLs
*/
void destroy_multiplex_npk() {
    for (int i_npk = 0; i_npk < NUM_ROWS_npk; ++i_npk) {
        head_pointers_npk[i_npk] = destroy_list_npk(head_pointers_npk[i_npk]);
    }
    cout << "All seat lists destroyed.\n";
}

```

-----

## Output

PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Assign_12.cpp -o Assign_12 } ; if ($?) { .\Assign_12 }
Multiplex setup complete with random initial bookings.

========== Galaxy Multiplex Reservation System ==========
1. Display Available Seats
2. Book Seats
3. Cancel Booking
4. Exit
Enter your choice: 1

========== Current Seat Availability (Row: [Seat - Status]) ==========
Row 1: [1 - Booked] [2 - Available] [3 - Available] [4 - Available] [5 - Available] [6 - Available] [7 - Available] [8 - Booked]
Row 2: [1 - Available] [2 - Booked] [3 - Available] [4 - Available] [5 - Available] [6 - Available] [7 - Available] [8 - Available]
Row 3: [1 - Available] [2 - Booked] [3 - Available] [4 - Available] [5 - Available] [6 - Booked] [7 - Available] [8 - Booked]
Row 4: [1 - Booked] [2 - Available] [3 - Available] [4 - Available] [5 - Available] [6 - Available] [7 - Available] [8 - Available]
Row 5: [1 - Available] [2 - Booked] [3 - Booked] [4 - Available] [5 - Available] [6 - Available] [7 - Available] [8 - Available]
Row 6: [1 - Booked] [2 - Available] [3 - Available] [4 - Booked] [5 - Available] [6 - Booked] [7 - Available] [8 - Available]
Row 7: [1 - Available] [2 - Available] [3 - Booked] [4 - Available] [5 - Booked] [6 - Available] [7 - Booked] [8 - Available]
Row 8: [1 - Available] [2 - Available] [3 - Booked] [4 - Available] [5 - Booked] [6 - Available] [7 - Available] [8 - Available]

========== Galaxy Multiplex Reservation System ==========
1. Display Available Seats
2. Book Seats
3. Cancel Booking
4. Exit
Enter your choice: 2
Enter row number (1-8): 4
Enter number of seats to book (1-8): 2
Enter starting seat number to book (1-7): 2
Successfully booked 2 seats in Row 4 starting from Seat 2.

========== Galaxy Multiplex Reservation System ==========
1. Display Available Seats
2. Book Seats
3. Cancel Booking
4. Exit
Enter your choice: