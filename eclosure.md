```
#include <stdio.h>
#include <string.h>

char result[20][20], copy[3], states[20][20];

// Adds a state to the result array for epsilon closure
void add_state(char a[3], int i) {
    strcpy(result[i], a);
}

// Displays the epsilon closure for a particular state
void display(int n) {
    int k = 0;
    printf("Epsilon closure of %s = { ", copy);
    while (k < n) {
        printf(" %s", result[k]);
        k++;
    }
    printf(" }\n");
}

int main() {
    FILE *INPUT;
    INPUT = fopen("input1.txt", "r");
    
    char state[3];
    int end, i = 0, n, k = 0;
    char state1[3], input[3], state2[3];
    
    printf("Enter the number of states: ");
    scanf("%d", &n);
    
    printf("Enter the states\n");
    for (k = 0; k < n; k++) {
        scanf("%s", states[k]);
    }

    for (k = 0; k < n; k++) {
        i = 0;
        strcpy(state, states[k]);
        strcpy(copy, state);
        add_state(state, i++);

        while (1) {
            end = fscanf(INPUT, "%s %s %s", state1, input, state2);
            if (end == EOF) {
                break;
            }
            if (strcmp(state, state1) == 0) {
                if (strcmp(input, "e") == 0) {  // Checks for epsilon transition
                    add_state(state2, i++);
                    strcpy(state, state2);
                }
            }
        }

        display(i);
        rewind(INPUT);  // Reset the file pointer for the next state
    }

    return 0;
}

```
