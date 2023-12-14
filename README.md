// Task-3-Tic-Tac-Toe

#include <bits/stdc++.h>
using namespace std;

#define Person_1 1
#define Person_2 2
#define Side 3
// Person_1 will Shift with 'x'  
// Person_2 with 'y'  
#define Person_1Move 'X'
#define Person_2Move 'Y'

void showBoard(char Board[][Side])
{
  printf("\n\n");

  printf("\t\t\t %c | %c | %c \n", Board[0][0],
    Board[0][1], Board[0][2]);
  printf("\t\t\t--------------\n");
  printf("\t\t\t %c | %c | %c \n", Board[1][0],
    Board[1][1], Board[1][2]);
  printf("\t\t\t--------------\n");
  printf("\t\t\t %c | %c | %c \n\n", Board[2][0],
    Board[2][1], Board[2][2]);

  return;
}

void showInstructions()
{
  printf("\t\t\t Tic-Tac-Toe\n\n");
  printf("Choose a cell numbered from 1 to 9 as below"
    " and play\n\n");

  printf("\t\t\t 1 | 2 | 3 \n");
  printf("\t\t\t--------------\n");
  printf("\t\t\t 4 | 5 | 6 \n");
  printf("\t\t\t--------------\n");
  printf("\t\t\t 7 | 8 | 9 \n\n");

  printf("-\t-\t-\t-\t-\t-\t-\t-\t-\t-\n\n");

  return;
}

void initialise(char Board[][Side], int Shifts[])
{
  srand(time(NULL));

  for (int i = 0; i < Side; i++)
  {
    for (int j = 0; j < Side; j++)
      Board[i][j] = ' ';
  }

  for (int i = 0; i < Side * Side; i++)
    Shifts[i] = i;

  random_shuffle(Shifts, Shifts + Side *Side);

  return;
}

void declareWinner(int Turn_For)
{
  if (Turn_For == Person_1)
    printf("Person_1 has won\n");
  else
    printf("Person_2 has won\n");
  return;
}

bool Rows(char Board[][Side])
{
  for (int i = 0; i < Side; i++)
  {	
    if (Board[i][0] == Board[i][1] &&
      Board[i][1] == Board[i][2] &&
      Board[i][0] != ' ')
      return (true);
  }

  return (false);
}

bool Column(char Board[][Side])
{
  for (int i = 0; i < Side; i++)
  {
    if (Board[0][i] == Board[1][i] &&
      Board[1][i] == Board[2][i] &&
      Board[0][i] != ' ')
      return (true);
  }

  return (false);
}

bool Diagonal(char Board[][Side])
{
  if (Board[0][0] == Board[1][1] &&
    Board[1][1] == Board[2][2] &&
    Board[0][0] != ' ')
    return (true);

  if (Board[0][2] == Board[1][1] &&
    Board[1][1] == Board[2][0] &&
    Board[0][2] != ' ')
    return (true);

  return (false);
}

bool It_Over(char Board[][Side])
{
  return (Rows(Board) || Column(Board) || Diagonal(Board));
}

void PlayTTT(int Turn_For)
{
  char Board[Side][Side];

  int Shifts[Side *Side];

  initialise(Board, Shifts);

  showInstructions();

  int Move_Index = 0, x, y;

  while (It_Over(Board) == false &&
    Move_Index != Side *Side)
  {
    if (Turn_For == Person_1)
    {
      x = Shifts[Move_Index] / Side;
      y = Shifts[Move_Index] % Side;
      Board[x][y] = Person_1Move;
      printf("Person_1 has put a %c in cell %d\n",
        Person_1Move, Shifts[Move_Index] + 1);
      showBoard(Board);
      Move_Index++;
      Turn_For = Person_2;
    }
    else if (Turn_For == Person_2)
    {
      x = Shifts[Move_Index] / Side;
      y = Shifts[Move_Index] % Side;
      Board[x][y] = Person_2Move;
      printf("Person_2 has put a %c in cell %d\n",
        Person_2Move, Shifts[Move_Index] + 1);
      showBoard(Board);
      Move_Index++;
      Turn_For = Person_1;
    }
  }

  if (It_Over(Board) == false &&
    Move_Index == Side *Side)
    printf("It's a draw\n");
  else
  {
    if (Turn_For == Person_1)
      Turn_For = Person_2;
    else if (Turn_For == Person_2)
      Turn_For = Person_1;

   	// Declare the winner  
    declareWinner(Turn_For);
  }

  return;
}

int main()
{
 	// Let us play the game with Person_1 starting first  
  PlayTTT(Person_1);

  return (0);
}
