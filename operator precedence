#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_SIZE 50

// Define operator precedence and associativity
int precedence(char op) {
    if (op == '+' || op == '-')
        return 1;
    if (op == '*' || op == '/')
        return 2;
    return 0;
}

typedef struct {
    char stack[MAX_SIZE];
    int top;
} Stack;

void initialize(Stack *s) {
    s->top = -1;
}

void push(Stack *s, char c) {
    s->stack[++s->top] = c;
}

char pop(Stack *s) {
    return s->stack[s->top--];
}

int isOperator(char c) {
    return (c == '+' || c == '-' || c == '*' || c == '/');
}

void printParsingTable() {
    printf("Operator Precedence Parsing Table:\n");
    printf("|   | + | - | * | / | ( | ) | $\n");
    printf("|---|---|---|---|---|---|---|---|\n");
    printf("| + | > | > | < | < | < | > | > |\n");
    printf("| - | > | > | < | < | < | > | > |\n");
    printf("| * | > | > | > | > | < | > | > |\n");
    printf("| / | > | > | > | > | < | > | > |\n");
    printf("| ( | < | < | < | < | < | = |   |\n");
    printf("| ) | > | > | > | > |   | > | > |\n");
    printf("| $ | < | < | < | < | < |   | = |\n");
    printf("|---|---|---|---|---|---|---|---|\n");
}

void operatorPrecedenceParser(char *expression) {
    Stack operatorStack;
    initialize(&operatorStack);

    printf("Parsing Steps:\n");
    printf("|   Stack   |   Input   |  Action  |\n");
    printf("|-----------|-----------|----------|\n");

    int i = 0;
    while (expression[i] != '\0') {
        // Print current state of stack and input
        printf("| %-9s | %-9s |", operatorStack.stack, expression + i);

        if (expression[i] == '(') {
            push(&operatorStack, expression[i]);
            printf(" Shift    |\n");
        } else if (expression[i] == ')') {
            while (operatorStack.stack[operatorStack.top] != '(') {
                printf(" Reduce   |\n");
                pop(&operatorStack);
            }
            pop(&operatorStack); // Pop '(' from stack
            printf(" Reduce   |\n");
        } else if (isOperator(expression[i])) {
            while (operatorStack.top >= 0 && precedence(expression[i]) <= precedence(operatorStack.stack[operatorStack.top])) {
                printf(" Reduce   |\n");
                pop(&operatorStack);
            }
            push(&operatorStack, expression[i]);
            printf(" Shift    |\n");
        } else {
            printf("          |\n");
        }
        i++;
    }

    while (operatorStack.top >= 0) {
        printf("| %-9s | %-9s | Reduce   |\n", operatorStack.stack, "");
        pop(&operatorStack);
    }
    printf("|-----------|-----------|----------|\n");
}

int main() {
    char expression[MAX_SIZE];
    printf("Enter an infix expression: ");
    scanf("%s", expression);

    printf("\n");
    printParsingTable();
    printf("\n");
    operatorPrecedenceParser(expression);

    return 0;
}
