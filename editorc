#include <stdio.h>
#include <string.h>
#include <ctype.h>

#define MAX_LINES 100
#define MAX_LENGTH 256

char lines[MAX_LINES][MAX_LENGTH];
int lineCount = 0;

/* Read a complete line of input */
void readText(char text[]) {
    if (fgets(text, MAX_LENGTH, stdin) != NULL) {
        text[strcspn(text, "\n")] = '\0';
    }
}

/* Insert a new line */
void insertLine(void) {
    int position;
    char text[MAX_LENGTH];

    if (lineCount >= MAX_LINES) {
        printf("Document is full.\n");
        return;
    }

    printf("Enter line number (1-%d): ", lineCount + 1);

    if (scanf("%d", &position) != 1) {
        printf("Invalid line number.\n");
        while (getchar() != '\n');
        return;
    }

    getchar();

    if (position < 1 || position > lineCount + 1) {
        printf("Invalid line number.\n");
        return;
    }

    printf("Enter text: ");
    readText(text);

    for (int i = lineCount; i >= position; i--) {
        strcpy(lines[i], lines[i - 1]);
    }

    strcpy(lines[position - 1], text);
    lineCount++;

    printf("Line inserted successfully.\n");
}

/* Delete a line */
void deleteLine(void) {
    int position;

    if (lineCount == 0) {
        printf("Document is empty.\n");
        return;
    }

    printf("Enter line number to delete: ");

    if (scanf("%d", &position) != 1) {
        printf("Invalid line number.\n");
        while (getchar() != '\n');
        return;
    }

    getchar();

    if (position < 1 || position > lineCount) {
        printf("Invalid line number.\n");
        return;
    }

    for (int i = position - 1; i < lineCount - 1; i++) {
        strcpy(lines[i], lines[i + 1]);
    }

    lineCount--;

    printf("Line deleted successfully.\n");
}

/* Display all lines */
void displayDocument(void) {
    if (lineCount == 0) {
        printf("Document is empty.\n");
        return;
    }

    printf("\n--- Document ---\n");

    for (int i = 0; i < lineCount; i++) {
        printf("%d: %s\n", i + 1, lines[i]);
    }
}

/* Save document to a text file */
void saveFile(void) {
    char filename[100];

    printf("Enter filename: ");
    readText(filename);

    FILE *file = fopen(filename, "w");

    if (file == NULL) {
        printf("Unable to save file.\n");
        return;
    }

    for (int i = 0; i < lineCount; i++) {
        fprintf(file, "%s\n", lines[i]);
    }

    fclose(file);
    printf("File saved successfully.\n");
}

/* Load document from a text file */
void loadFile(void) {
    char filename[100];
    char text[MAX_LENGTH];

    printf("Enter filename: ");
    readText(filename);

    FILE *file = fopen(filename, "r");

    if (file == NULL) {
        printf("Unable to open file.\n");
        return;
    }

    lineCount = 0;

    while (lineCount < MAX_LINES &&
           fgets(text, MAX_LENGTH, file) != NULL) {

        text[strcspn(text, "\n")] = '\0';
        strcpy(lines[lineCount], text);
        lineCount++;
    }

    fclose(file);
    printf("File loaded successfully.\n");
}

/* Search for a word */
void searchWord(void) {
    char word[MAX_LENGTH];
    int found = 0;

    printf("Enter word to search: ");
    readText(word);

    for (int i = 0; i < lineCount; i++) {
        if (strstr(lines[i], word) != NULL) {
            printf("Found on line %d\n", i + 1);
            found = 1;
        }
    }

    if (!found) {
        printf("Word not found.\n");
    }
}

/* Count words in the document */
void countWords(void) {
    int count = 0;
    int inWord = 0;

    for (int i = 0; i < lineCount; i++) {
        for (int j = 0; lines[i][j] != '\0'; j++) {
            if (isspace((unsigned char)lines[i][j])) {
                inWord = 0;
            } else if (!inWord) {
                count++;
                inWord = 1;
            }
        }

        inWord = 0;
    }

    printf("Total words: %d\n", count);
}

/* Display available commands */
void help(void) {
    printf("\n--- Line Editor Commands ---\n");
    printf("i - Insert a line\n");
    printf("d - Delete a line\n");
    printf("p - Display document\n");
    printf("s - Save document\n");
    printf("l - Load document\n");
    printf("f - Search for a word\n");
    printf("w - Count words\n");
    printf("h - Help\n");
    printf("q - Quit\n");
}

/* Main function */
int main(void) {
    char command;

    printf("Simple Line Editor in C\n");
    help();

    while (1) {
        printf("\nEnter command: ");

        if (scanf(" %c", &command) != 1) {
            break;
        }

        getchar();

        switch (command) {
            case 'i':
                insertLine();
                break;

            case 'd':
                deleteLine();
                break;

            case 'p':
                displayDocument();
                break;

            case 's':
                saveFile();
                break;

            case 'l':
                loadFile();
                break;

            case 'f':
                searchWord();
                break;

            case 'w':
                countWords();
                break;

            case 'h':
                help();
                break;

            case 'q':
                printf("Exiting editor.\n");
                return 0;

            default:
                printf("Invalid command. Enter h for help.\n");
        }
    }

    return 0;
}