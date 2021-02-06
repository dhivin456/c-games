//dhivinrithik
#include <stdio.h>
#include <time.h>

#define BOARD_SIZE 10
#define TRUE 1
#define FALSE 0

void display_welcome();
void player_name();
void start_game();
void build_minesboard();
void build_userboard();
void print_userboard();
int nearbymines();
int num_of_mines();
int win_check();
void you_won();
void you_lost();
void print_minesboard();
void play_again();
void exit();
//dhivinrithik
struct player_info
{
    char name[15];
}p;

char uboard[BOARD_SIZE][BOARD_SIZE];	//2-dimensional board visible to user
char mboard[BOARD_SIZE][BOARD_SIZE];	//2-dimensional board which contains mines

void play_again()
{
    char choice;
 
    printf("\n\nWould you like to play again? (Y/N) --> ");
    getchar();
    scanf("%c", &choice);
 
    if(toupper(choice) == 'Y')
    {
        system("cls");
        start_game();
    }
 
    else
    {
        printf("\n\nThanks for playing! Bye %s.",p.name);
        exit(0);
    }
}

void you_won()
{
 	printf("Congratulations %s, you have won!",p.name);
 	play_again();
}

void you_lost()
{
    printf("Sorry %s, You have lost!, Better luck next time",p.name);
    play_again();
}

int win_check()
{
    int column, row;
	for(column = 0; column < BOARD_SIZE; column++)
        for(row = 0; row < BOARD_SIZE; row++) 
		{
            if(uboard[column][row] == '-' && mboard[column][row] != 'M')
            {
            	return FALSE;
			}
        }
    return TRUE;
}

int num_of_mines(int column, int row)	//Finds mines in adjacent locations to user selection
{
	int mines = 0;
     
	// Check up, down, left, right
    if(mboard[column][row - 1] == 'M')  //up
    {
    	mines++;
	}
    if(mboard[column][row + 1] == 'M')  //down
    {
    	mines++;
	}
    if(mboard[column - 1][row] == 'M')  //left
    {
    	mines++;
	}
    if(mboard[column + 1][row] == 'M')  //right
    {
    	mines++;
	}
 
	// Check all diagonal directions
    if(mboard[column + 1][row - 1] == 'M')  //upright
    {
    	mines++;
	}
    if(mboard[column - 1][row - 1] == 'M')  //upleft
    {
    	mines++;
	}    
    if(mboard[column + 1][row + 1] == 'M')  //downright
    {
    	mines++;
	}    
    if(mboard[column - 1][row + 1] == 'M')  //downleft
    {
    	mines++;
	}    

    return mines;
}

int nearbymines(int column, int row)
{
	int nearbyminess = 0;
	
	if( row < 0 || row >= BOARD_SIZE || column < 0 || column >= BOARD_SIZE || uboard[column][row] != '-')
	{
        return 0;
    }
	
	nearbyminess = num_of_mines(column, row);
	uboard[column][row] = (char)nearbyminess + '0';		//int to char conversion to store integer in 2-dimensional character array
    
    if (nearbyminess == 0)		//if nearbyminess is 0 then check each space around it
	{
        nearbymines(column, row-1); //up
        nearbymines(column, row+1); //down
        nearbymines(column-1, row); //left
        nearbymines(column+1, row); //right
        nearbymines(column+1, row-1); //upright
        nearbymines(column-1, row-1); //upleft
        nearbymines(column+1, row+1); //downright
        nearbymines(column-1, row+1); //downleft
    }
    return 1;
}

void print_minesboard()
{
	int column, row;
	
    for(column = 0; column < BOARD_SIZE ; column++)		//print the top row of numbers
    {
    	printf(" %d ", column);
	}    
    printf("\n");

    for(row = 0; row < BOARD_SIZE; row++)
    {
        for(column = 0; column < BOARD_SIZE; column++)
        {
            printf(" %c ", mboard[column][row]);
        }
        if(row >= 0 && row <= BOARD_SIZE)
        {
        	printf("   %d", row);
		}
        printf("\n");
    }
}

void print_userboard()
{
    int column, row;
	system("cls");
    
    for(column = 0; column < BOARD_SIZE ; column++)		//print the top row of numbers
    {
    	printf(" %d ", column);
	}    
    printf("\n");

    for(row = 0; row < BOARD_SIZE; row++)
    {
        for(column = 0; column < BOARD_SIZE; column++)
        {
            printf(" %c ", uboard[column][row]);
        }
        if(row >= 0 && row <= BOARD_SIZE)
        {
        	printf("   %d", row);
		}
        printf("\n");
    }
}

void build_userboard()
{
    int column, row;
 	
    for(column = 0; column < BOARD_SIZE; column++)
    {
    	for(row = 0; row < BOARD_SIZE; row++)
    	{
    		uboard[column][row] = '-';		//set all elements in the user board to '-'
		}
	}
}

void build_minesboard()
{
	int column, row;
	
	for(column = 0; column < BOARD_SIZE ; column++)
	{
        for (row = 0; row < BOARD_SIZE ; row++)
        {
        	mboard[column][row] = '-';		//set all elements in the mines board to '-'
		}
    }
	
    srand(time(0));
    
    for(row = 0; row < BOARD_SIZE ; row++)
	{
        int random = rand() % (BOARD_SIZE);		//set mines 'M' in random column of the mines board
        mboard[random][row] = 'M';
    }    
}

void start_game()
{	
	int column, row;
	
	build_minesboard();
	build_userboard();
	
	print_userboard();
	//print_minesboard();
	
	for(;;)
	{
	    do
		{	
	        printf("Enter the column: ");
	        scanf("%d",&column);
			printf("Enter the row: ");
	        scanf("%d",&row);
	        printf("\n");
	    }while(row < 0 || row > BOARD_SIZE -1 || column < 0 || column > BOARD_SIZE -1);
	 
	 
	    if (mboard[column][row] == 'M')
		{
	        printf("You have hit a mine!\n\n");
	        print_minesboard();
	        you_lost();
	    }
	    else
	    {
	    	nearbymines(column, row);
	    	if(win_check())
    		{
    			print_minesboard();
    			you_won();
			}
	    }
		print_userboard();
    }
}

void player_name()
{
    printf("Please enter your name: ");
    scanf("%s", p.name);
}


void display_welcome()
{
    puts("-----------------------Welcome to Minesweeper---------------------------");
    puts("\n");
}
//dhivinrithik
int main()
{
	display_welcome();
	player_name();
	start_game();
}
//dhivinrithik
