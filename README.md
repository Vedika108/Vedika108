#include <stdio.h>
#include <string.h>

// Function declarations
void explore_room(char *room);
void question_suspect(char *suspect);
int make_accusation(int *wrong_attempts);

int main() {
    char choice[20];
    int case_solved = 0;
    int wrong_attempts = 0;

    printf("Welcome to **The Last Clue**!\n");
    printf("You are a detective investigating a murder in a grand estate.\n");
    printf("Explore rooms, question suspects, and gather clues to solve the case!\n\n");

    while (!case_solved && wrong_attempts < 3) {
        printf("\nWhat would you like to do?\n");
        printf("1. Explore a Room\n");
        printf("2. Question a Suspect\n");
        printf("3. Make an Accusation\n");
        printf("Enter your choice: ");
        scanf("%s", choice);

        if (strcmp(choice, "1") == 0) {
            printf("\nChoose a room to explore:\n");
            printf("a. Dining Room\nb. Library\nc. Bedroom\n");
            printf("Enter your choice: ");
            scanf("%s", choice);

            if (strcmp(choice, "a") == 0) {
                explore_room("Dining Room");
            } else if (strcmp(choice, "b") == 0) {
                explore_room("Library");
            } else if (strcmp(choice, "c") == 0) {
                explore_room("Bedroom");
            } else {
                printf("Invalid room choice. Try again.\n");
            }
        } else if (strcmp(choice, "2") == 0) {
            printf("\nChoose a suspect to question:\n");
            printf("a. Butler\nb. Maid\nc. Gardener\n");
            printf("Enter your choice: ");
            scanf("%s", choice);

            if (strcmp(choice, "a") == 0) {
                question_suspect("Butler");
            } else if (strcmp(choice, "b") == 0) {
                question_suspect("Maid");
            } else if (strcmp(choice, "c") == 0) {
                question_suspect("Gardener");
            } else {
                printf("Invalid suspect choice. Try again.\n");
            }
        } else if (strcmp(choice, "3") == 0) {
            case_solved = make_accusation(&wrong_attempts);
        } else {
            printf("Invalid choice. Try again.\n");
        }
    }

    if (wrong_attempts >= 3) {
        printf("\nToo many incorrect accusations. The case has gone cold.\n");
    }

    return 0;
}

void explore_room(char *room) {
    printf("\nExploring the %s...\n", room);

    if (strcmp(room, "Dining Room") == 0) {
        printf("You find a broken glass with fingerprints on it. Could it belong to the killer?\n");
    } else if (strcmp(room, "Library") == 0) {
        printf("A note is hidden in a book that reads: 'Meet me here at midnight.'\n");
    } else if (strcmp(room, "Bedroom") == 0) {
        printf("You discover a torn piece of fabric on the bed that matches the victim's clothing.\n");
    } else {
        printf("Nothing significant found in the %s.\n", room);
    }
}

void question_suspect(char *suspect) {
    printf("\nQuestioning the %s...\n", suspect);

    if (strcmp(suspect, "Butler") == 0) {
        printf("Butler: \"I was cleaning the silverware in the kitchen when the incident happened.\"\n");
    } else if (strcmp(suspect, "Maid") == 0) {
        printf("Maid: \"I saw the Gardener sneaking out of the house late last night.\"\n");
    } else if (strcmp(suspect, "Gardener") == 0) {
        printf("Gardener: \"I was tending to the greenhouse all evening. I heard nothing.\"\n");
    } else {
        printf("No useful information from %s.\n", suspect);
    }
}

int make_accusation(int *wrong_attempts) {
    char accused[20];
    printf("\nWho do you accuse of the crime? (Butler, Maid, Gardener): ");
    scanf("%s", accused);

    if (strcmp(accused, "Maid") == 0) {
        printf("\nCongratulations! You've solved the case! The Maid was indeed the culprit.\n");
        return 1;
    } else {
        (*wrong_attempts)++;
        if (strcmp(accused, "Butler") == 0) {
            printf("\nThe Butler seems innocent. He was occupied with cleaning during the incident.\n");
        } else if (strcmp(accused, "Gardener") == 0) {
            printf("\nThe Gardener insists he was in the greenhouse. No evidence points to him.\n");
        } else {
            printf("\n%s is not a valid suspect. Try focusing on the main suspects.\n", accused);
        }

        printf("Incorrect accusation count: %d/3\n", *wrong_attempts);
        return 0;
    }
}
