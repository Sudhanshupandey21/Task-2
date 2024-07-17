# Task-2


#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void playGame();
char getComputerChoice();
char getUserChoice();
void determineWinner(char userChoice, char computerChoice);

int main() {
    char playAgain;

    printf("Welcome to Rock, Paper, Scissors!\n");

    do {
        playGame();
        printf("Do you want to play again? (y/n): ");
        scanf(" %c", &playAgain);
    } while (playAgain == 'y' || playAgain == 'Y');

    printf("Thanks for playing!\n");
    return 0;
}

void playGame() {
    char userChoice, computerChoice;

    userChoice = getUserChoice();
    computerChoice = getComputerChoice();

    printf("You chose: %c\n", userChoice);
    printf("Computer chose: %c\n", computerChoice);

    determineWinner(userChoice, computerChoice);
}

char getComputerChoice() {
    srand(time(0)); // Seed the random number generator
    int randomNum = rand() % 3; // Generate a random number between 0 and 2

    switch (randomNum) {
        case 0:
            return 'R';
        case 1:
            return 'P';
        case 2:
            return 'S';
    }
    return 'R'; // Default return value
}

char getUserChoice() {
    char choice;

    printf("Enter your choice (R for Rock, P for Paper, S for Scissors): ");
    scanf(" %c", &choice);
    
    while (choice != 'R' && choice != 'P' && choice != 'S' &&
           choice != 'r' && choice != 'p' && choice != 's') {
        printf("Invalid choice. Please enter R, P, or S: ");
        scanf(" %c", &choice);
    }

    // Convert to uppercase if the user entered a lowercase letter
    if (choice >= 'a' && choice <= 'z') {
        choice = choice - 'a' + 'A';
    }

    return choice;
}

void determineWinner(char userChoice, char computerChoice) {
    if (userChoice == computerChoice) {
        printf("It's a tie!\n");
    } else if ((userChoice == 'R' && computerChoice == 'S') ||
               (userChoice == 'P' && computerChoice == 'R') ||
               (userChoice == 'S' && computerChoice == 'P')) {
        printf("You win!\n");
    } else {
        printf("You lose!\n");
    }
}
