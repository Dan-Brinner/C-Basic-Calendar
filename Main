#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <stdbool.h>

// Struct to define a month with its name and number of days
typedef struct {
    char name[10]; // Month name (e.g., "January")
    int days;      // Number of days in the month
} Month;

/* 
   Function to determine if a given year is a leap year.
   A year is a leap year if:
   - Divisible by 4 but not by 100, OR
   - Divisible by 400
*/

bool is_leap_year(int year) {
    return (year % 4 == 0 && year % 100 != 0) || (year % 400 == 0);
}

int main() {
    // Get the current time in seconds since the epoch
    time_t now = time(NULL); 
    struct tm *local = localtime(&now); // Convert to local time structure
    
    // Extract current date details
    int current_month = local->tm_mon; // Current month (0-based index: Jan = 0, Dec = 11)
    int current_day = local->tm_mday;  // Current day of the month
    int current_year = local->tm_year + 1900; // Current year (tm_year is years since 1900)
    int sel_month = current_month; // Selected month for display (initially current month)
    char inp; // User input for menu options
    
    // Array of structs defining the months of the year
    Month months[12] = {
        {"January", 31},
        {"February", 28},
        {"March", 31},
        {"April", 30},
        {"May", 31},
        {"June", 30},
        {"July", 31},
        {"August", 31},
        {"September", 30},
        {"October", 31},
        {"November", 30},
        {"December", 31}
    };

    // Adjust February for leap years
    if (is_leap_year(current_year)) {
        months[1].days = 29;
    }

    // Main loop for displaying the calendar and interacting with the user
    while (true) {
        // Display the name of the selected month
        printf("\n\n%s:", months[sel_month].name);

        // Loop to display days of the selected month
        for (int k = 1; k <= months[sel_month].days; k++) {
            // Print a new line after every 7 days (to mimic a calendar week layout)
            if ((k % 7) == 1) {
                printf("\n");
            }

            // Highlight the current day in green
            if (k == current_day && k < 10 && sel_month == current_month) {
                printf("\033[1;32m %d \033[0m", k);
            } else if (k == current_day && sel_month == current_month) {
                printf("\033[1;32m%d \033[0m", k);
            } else if (k < 10) { // Add extra space for single-digit days for alignment
                printf(" %d ", k);
            } else {
                printf("%d ", k);
            }
        }
        
        // Prompt user for menu options
        printf("\nM for menu\n");
        scanf(" %c", &inp);
        while (getchar() != '\n'); // Clear input buffer to avoid issues in the next iteration

        // Handle menu interaction
        if (inp == 'm' || inp == 'M') {
            inp = '\0'; // Reset input variable
            printf("\nSelect Action: \nE) Exit \nC) Change Month\n"); // Display menu options
            scanf(" %c", &inp);

            switch (inp) {
                case 'e': // Exit the program
                    exit(0);
                    break;
                case 'c': // Change the displayed month
                    printf("Enter new month (1-12): ");
                    scanf("%d", &sel_month);
                    sel_month = sel_month - 1; // Convert user input (1-12) to 0-based index
                    break;
                default: // Handle invalid inputs (ignored)
                    break;
            }
        }
    }

    return 0;
}
