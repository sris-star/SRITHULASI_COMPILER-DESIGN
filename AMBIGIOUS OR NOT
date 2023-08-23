#include <stdio.h>
#include <stdbool.h>
#include <string.h>
const char *productions[] = {
    "S -> S + S",
    "S -> S * S",
    "S -> id"
};

bool isAmbiguous(const char *input, int start, int end) {
    int i;
	if (start == end) {
        return true;  // Single 'id' is ambiguous
    }
    for (i = start + 1; i < end; i++) {
        if ((input[i] == '+' || input[i] == '*') &&
            isAmbiguous(input, start, i - 1) &&
            isAmbiguous(input, i + 1, end)) {
            return true;
        }
    }
    return false;
}

int main() {
    const char *input = "id+id*id";
    printf("Input: %s\n", input);

    if (isAmbiguous(input, 0, strlen(input) - 1)) {
        printf("The grammar is ambiguous for the given input.\n");
    } else {
        printf("The grammar is not ambiguous for the given input.\n");
    }

    return 0;
}
 
