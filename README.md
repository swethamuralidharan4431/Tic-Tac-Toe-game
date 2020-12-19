\* Tic-Tac-Toe-game *\
#include <stdio.h>
#include <stdlib.h>

char matrix[3][3];  /* no of column and rows */
char matrix1[3][3];

char check(void);     /* to check the winner */
char check1(void);

void create_matrix(void);    /*matrix*/
void create_matrix1(void);

void get_player_move(void);     /* get player move */
void get_player1_move(void);
void get_player2_move(void);
void get_computer_move(void);

void disp_matrix(void);          /* display matrix */
void disp_matrix1(void);

char History();

int main(void)
{
    char value;
    char value1;

    printf(" -------------  -------------     ----------     ------------- -------------    ------------     --------------   ------------   ------------  \n");
    printf("       |              |           |                    |       |           |    |                      |          |          |   |              \n");
    printf("       |              |           |                    |       |           |    |                      |          |          |   |              \n");
    printf("       |              |           |                    |       | --------- |    |                      |          |          |   |--------       \n");
    printf("       |              |           |                    |       |           |    |                      |          |          |   |                 \n");
    printf("       |              |           |                    |       |           |    |                      |          |          |   |                  \n");
    printf("       |        -------------     ----------           |       |           |    -----------            |          ------------   ------------        \n");
    printf("                                                                                                                                                      \n");
    printf("\n");
    printf("                                                                                                                                By SWETHA MURALIDHARAN\n");
    printf("                                                                                                                                                20PW35\n");

    while(2){
    int choice,c,c1;
    char p[50],p1[50],p2[50];
    printf("******************************************\n");
    printf("*         1. Play against computer       *\n");
    printf("*         2. Play against a player       *\n");
    printf("*         3. How to play this game       *\n");
    printf("******************************************\n");
    scanf("%d",&choice);

    switch(choice)
    {
    case 1:
        printf("Enter your name (in caps)");
        scanf("%s",p);
        printf("%s will play as X\nComputer will play as O\n",p);
        create_matrix();
        value = ' ';
        do{
                disp_matrix();
                get_player_move();
                value = check();
                if(value!= ' ') break;
                get_computer_move();
                value = check();
        }
        while(value== ' ');
        disp_matrix();
        if(value=='X')
            printf("YOU WON THE GAME.\nCONGRAJULATIONS!!!\n");
        else
            printf("YOU LOST THE GAME.\n BAD LUCK !\n");
        break;
    case 2:
        printf("Enter player 1 name (in caps)");
        scanf("%s",p1);
        printf("Enter player 2 name (in caps)");
        scanf("%s",p2);
        printf("%s will play as X\n%s will play as O \n",p1,p2);
        create_matrix1();
        value1 = ' ';
        do{
                disp_matrix1();
                get_player1_move();
                value1 = check1();
                if(value1!= ' ') break;
                get_player2_move();
                value1 = check1();
        }
        while(value1== ' ');/* show final positions */
        if(value1=='X')
            printf(" %s WON THE GAME.\nCONGRAJULATIONS!!!\n" , p1);
        else
            printf(" %s WON THE GAME.\nCONGRAJULATIONS!!!\n\n",p2);
        break;

    case 3:
        History();
        break;
    }

    printf("Do u want to Play ( Yes ==1 and any other number for Exit)\n");
    scanf("%d",&c1);
    if(c1==1)
        continue;
    else
        printf("Thank you for playing\n");
        break;
}
}

/* Initialize the matrix. */

void create_matrix(void)
{
    int i, j;
    for(i=0; i<3; i++)
    for(j=0; j<3; j++)
        matrix[i][j] = ' ';
}

/* Display the matrix on the screen. */
void disp_matrix(void)
{
    int i;
    for(i=0; i<3; i++){
    printf(" %c | %c | %c ",matrix[i][0],matrix[i][1], matrix [i][2]);
    if(i!=2)
        printf("\n---|---|---\n");
    }
    printf("\n");
}
void create_matrix1(void)
{
    int i, j;
    for(i=0; i<3; i++)
    for(j=0; j<3; j++)
        matrix1[i][j] = ' ';
}

/* Display the matrix on the screen. */
void disp_matrix1(void)
{
    int i;
    for(i=0; i<3; i++){
    printf(" %c | %c | %c ",matrix1[i][0],matrix1[i][1], matrix1[i][2]);
    if(i!=2) printf("\n---|---|---\n");
    }
    printf("\n");
}
/* Get a player's move. */

void get_player_move(void)
{
    int x, y;
    printf("Enter X coordinate: ");
    scanf("%d", &x);
    printf("Enter Y coordinate: ");
    scanf("%d",&y);
    x--; y--;
    if(matrix[x][y]!= ' '){
        printf("Invalid move, try again.\n");
        get_player_move();
    }
    else
        matrix[x][y] = 'X';
}

/* Get a move from the computer. */

void get_computer_move(void)
{
    int i, j;
    for(i=0; i<3; i++){
    for(j=0; j<3; j++)if(matrix[i][j]==' ')break;
    if(matrix[i][j]==' ') break;
    }
    if(i*j==9) {
    printf("draw\n");
    exit(0);
    }
    else
    matrix[i][j] = 'O';
}


void get_player1_move(void)
{
    int x, y;
    printf("Enter X coordinate for player 1 move: ");
    scanf("%d", &x);
    printf("Enter Y coordinate for player 1 move: ");
    scanf("%d",&y);
    x--; y--;
    if(matrix1[x][y]!= ' '){
        printf("Invalid move, try again.\n");
        get_player1_move();
    }
    else
        matrix1[x][y] = 'X';
        disp_matrix1();

}

/* player 2 move */
void get_player2_move(void)
{
    int x, y;
    printf("Enter X coordinate for player 2 move: ");
    scanf("%d", &x);
    printf("Enter Y coordinate for player 2 move: ");
    scanf("%d",&y);
    x--; y--;
    if(matrix1[x][y]!=' '){
        printf("Invalid move, try again.\n");
        get_player2_move();
    }
    else
        matrix1[x][y] = 'O';

}

char check(void)
{
    int i;
    for(i=0; i<3; i++)                                                 /* check rows */
    if(matrix[i][0]==matrix[i][1] && matrix[i][0]==matrix[i][2])
        return matrix[i][0];
    for(i=0; i<3; i++)    /* check columns */
    if(matrix[0][i]==matrix[1][i] && matrix[0][i]==matrix[2][i])
        return matrix[0][i];
                                                                      /* test diagonals */
    if(matrix[0][0]==matrix[1][1] && matrix[1][1]==matrix[2][2])
        return matrix[0][0];
    if(matrix[0][2]==matrix[1][1] && matrix[1][1]==matrix[2][0])
        return matrix[0][2];
    return ' ';
}

char check1(void)
{
    int i;
    for(i=0; i<3; i++)                                                 /* check rows */
    if(matrix1[i][0]==matrix1[i][1] && matrix1[i][0]==matrix1[i][2])
        return matrix1[i][0];
    for(i=0; i<3; i++)    /* check columns */
    if(matrix1[0][i]==matrix1[1][i] && matrix1[0][i]==matrix1[2][i])
        return matrix1[0][i];
    if(matrix1[0][0]==matrix1[1][1] && matrix1[1][1]==matrix1[2][2])  /* check diagonals */
        return matrix1[0][0];
    if(matrix1[0][2]==matrix1[1][1] && matrix1[1][1]==matrix1[2][0])
        return matrix1[0][2];
    return ' ';
}

char History()
{
    printf(" INSTRUCTIONS \n");
    printf("In order to win the game, a player must place three of their marks in a horizontal, vertical, or diagonal row\n");
    printf("1.Win: If the player has two in a row, they can place a third to get three in a row.\n");
    printf("2.Block: If the opponent has two in a row, the player must play the third themselves to block the opponent.\n");
    printf("3.Fork: Create an opportunity where the player has two ways to win (two non-blocked lines of 2\n");
    printf("4.Opposite corner: If the opponent is in the corner, the player plays the opposite corner.\n");
    printf("5.Empty corner: The player plays in a corner square.\n");
    printf("6.Empty side: The player plays in a middle square on any of the 4 sides\n");
}

