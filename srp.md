#include <stdio.h>
#include <string.h>

struct ProductionRule {
    char left[10];
    char right[10];
};

int main() {
    char input[50], stack[50], temp[50], ch[10], *token1, *token2, *substring;
    int i, j, stack_length, substring_length, stack_top, rule_count = 0;
    struct ProductionRule rules[10];
    
    // Initialize the stack with '$' at the bottom
    stack[0] = '$';
    stack[1] = '\0';

    printf("\nEnter the number of production rules: ");
    scanf("%d", &rule_count);

    // Input production rules in the form 'left->right'
    printf("\nEnter the production rules (in the form 'left->right'): \n");
    for (i = 0; i < rule_count; i++) {
        scanf("%s", temp);
        token1 = strtok(temp, "->");
        token2 = strtok(NULL, "->");
        strcpy(rules[i].left, token1);
        strcpy(rules[i].right, token2);
    }

    // Input the string to be parsed
    printf("\nEnter the input string: ");
    scanf("%s", input);
    strcat(input, "$");  // Append '$' to the end of the input string

    i = 0;
    while (1) {
        // Shift phase: push characters onto the stack until a rule can be applied
        if (i < strlen(input)) {
            if (strncmp(&input[i], "id", 2) == 0) {  // Treat "id" as a single symbol
                strcpy(ch, "id");
                i += 2;
            } else {
                ch[0] = input[i];
                ch[1] = '\0';
                i++;
            }
            strcat(stack, ch);

            // Display the shift action
            printf("%s\t", stack);
            for (int k = i; k < strlen(input); k++) {
                printf("%c", input[k]);
            }
            printf("\tShift %s\n", ch);
        }

        // Reduce phase: apply a production rule if possible
        for (j = 0; j < rule_count; j++) {
            substring = strstr(stack, rules[j].right);
            if (substring != NULL) {
                stack_length = strlen(stack);
                substring_length = strlen(substring);
                stack_top = stack_length - substring_length;
                stack[stack_top] = '\0';
                strcat(stack, rules[j].left);

                // Display the reduction action
                printf("%s\t", stack);
                for (int k = i; k < strlen(input); k++) {
                    printf("%c", input[k]);
                }
                printf("\tReduce %s->%s\n", rules[j].left, rules[j].right);

                // Restart reduction process after applying a rule
                j = -1;
            }
        }

        // Check for acceptance or rejection
        if (input[i] == '$' && stack[0] == '$' && strcmp(stack + 1, rules[0].left) == 0) {
            printf("\nAccepted\n");
            break;
        }
        if (input[i] == '$' && strcmp(stack, "$S") != 0) {
            printf("\nNot Accepted\n");
            break;
        }
    }

    return 0;
}
