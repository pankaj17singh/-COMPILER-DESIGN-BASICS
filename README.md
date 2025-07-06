# -COMPILER-DESIGN-BASICS

*COMPANY NAME* : CODETECH IS SOLUTIONS

*NAME* : PANKAJ SINGH

*INTRERN NO* : CT04DF19

*DOMAIN* : C PROGRAMING

*DURATION*  : 4 WEEKS

*MENTOR* : NEELAM SANTOSH KUMAR

* I USE VS CODE*

* *THE CODE IS :: *


  #include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

#define MAX 100

// List of keywords
const char* keywords[] = {
    "int", "float", "if", "else", "while", "return", "char", "for", "double", "do", "void", "break"
};
int num_keywords = sizeof(keywords) / sizeof(keywords[0]);

// Function to check if a string is a keyword
int isKeyword(char* str) {
    for (int i = 0; i < num_keywords; i++) {
        if (strcmp(str, keywords[i]) == 0)
            return 1;
    }
    return 0;
}

// Function to check if a character is an operator
int isOperator(char ch) {
    return ch == '+' || ch == '-' || ch == '*' || ch == '/' || ch == '=' || ch == '<' || ch == '>';
}

// Function to check if a string is a valid identifier
int isIdentifier(char* str) {
    if (!isalpha(str[0]) && str[0] != '_') return 0;
    for (int i = 1; str[i]; i++) {
        if (!isalnum(str[i]) && str[i] != '_') return 0;
    }
    return 1;
}

int main() {
    char ch, buffer[MAX];
    FILE *fp = fopen("input.c", "r");
    int i = 0;

    if (!fp) {
        printf("Cannot open file.\n");
        return 1;
    }

    while ((ch = fgetc(fp)) != EOF) {
        // If separator or operator, handle previous buffer
        if (isalnum(ch) || ch == '_') {
            buffer[i++] = ch;
        } else {
            if (i > 0) {
                buffer[i] = '\0';
                if (isKeyword(buffer))
                    printf("Keyword: %s\n", buffer);
                else if (isIdentifier(buffer))
                    printf("Identifier: %s\n", buffer);
                else
                    printf("Invalid Token: %s\n", buffer);
                i = 0;
            }

            if (isOperator(ch)) {
                printf("Operator: %c\n", ch);
            }
        }
    }

    // If buffer not empty at end
    if (i > 0) {
        buffer[i] = '\0';
        if (isKeyword(buffer))
            printf("Keyword: %s\n", buffer);
        else if (isIdentifier(buffer))
            printf("Identifier: %s\n", buffer);
        else
            printf("Invalid Token: %s\n", buffer);
    }

    fclose(fp);
    return 0;
}
