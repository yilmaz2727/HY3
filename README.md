#include <iostream>
#include <ctime>
#include <iomanip>
#include <conio.h>
#include <clocale>
#include <thread>
#include <chrono>
#include <cstdlib>
using namespace std;
const int CHANCES = 10;
const int MAX = 100;
const int MIN = 1;
void printWON();
void ERROR();
void GAME();
void FINISH();
void clearScreen();
void INPUTANSWERS(int YOUR_GUESS[10] , int TotalChance);
void SHOWİNG_SCORE(int score1);
/////////////////////////////////////////////////////////////////////////////////
 
int main()                
{
    setlocale(LC_ALL, "Turkish");
   
    srand(time(NULL));
        char choice; 
    cout<< setw(75) <<  "WELCOME TO 'Guess the Number'"  << endl
        << setw(77) << "*******************************" << endl<<endl;
        
    cout << setw(90) << "TEST YOUR LUCK AND LOGIC TO UNCOVER THE SECRET NUMBER."<< endl<<endl<<
            setw(95) << " CAN YOU BEAT THE ODDS AND GUESS IT RIGHT? LET THE CHALLENGE BEGIN!" << endl<<endl;
    cout << setw(90) <<"YOU HAVE 10 CHANCES!! LET'S START...... [PRESS A BUTTON]" << endl;
    _getch();   
    do{ 
        clearScreen();
    GAME();
    cout << "DO YOU WANT TO PLAY AGAİN?   YES = 'Y' , 'y'   NO ='N','n' " << endl;
    cin >> choice;
    
    } while (choice == 'y' || choice == 'Y'); 
    FINISH();
  return 0;



}


    /////////////////////////////////////////////////////////////////////////////////

void GAME()           
{ 

    int GUESS;
    int NUMBER = rand()%MAX+MIN;
    int YOUR_GUESS[CHANCES] = {};
    int TotalChance = 0;
    int score = 100;
    bool cntrl = false;
    int count = 0;

    for (int i = 0; i < CHANCES; i++)
    {
        TotalChance += 1;
        
        while (true) {
            
            cout <<  "GUESS THE NUMBER "<< "["<< MIN<< "-"<<MAX<<"]   :   " ;
            cin >> GUESS;
         
            if (cin.fail() || GUESS < MIN || GUESS > MAX) {
                cin.clear();                // Hata durumunu temizle
                cin.ignore(1000, '\n');     // Kalan girdiyi yoksa
                cout <<  "   WRONG CHARACTER!!!! Please try again." << endl;
            }
            else {
                break; 
            } 
           
        } 
         YOUR_GUESS[i] = GUESS;

         if (GUESS == NUMBER)
         { 
           
             clearScreen();
             printWON(); 
             cout << endl << endl << endl;

             break;
         }
      
         else
        {
            cout << "FAIL..  -10 SCORE\t " << endl; 
            score -= 10;
            if (GUESS - NUMBER > 0)
            {
                if (GUESS - NUMBER < 5)
                    cout << "YOU ARE GETTİNG CLOSE!!!\n" << endl;
            }
            else
            {
                if (NUMBER - GUESS < 5)
                    cout << "YOU ARE GETTİNG CLOSE!!!\n" << endl;
            }

            if (GUESS < NUMBER)
            {
                cout << GUESS <<" IS LESS THAN THE SECRET NUMBER\n" << endl;  
            }
            else
            {
                cout << GUESS << " IS GREATER THAN THE SECRET NUMBER\n" << endl;
            }
        }

       

       
    } 
    INPUTANSWERS( YOUR_GUESS, TotalChance);
    SHOWİNG_SCORE(score);
   
}

 
void ERROR()            
{
    cout << "ERRORR!!!";
}

static void FINISH()       
{
    cout << endl <<setw(15)<<"     SEE YOUU....  " << endl;
}



void printWON() {
    cout << setw(52) << "W       W   OOOOO   N     N  " << endl;
    cout << setw(52) << "W       W  O     O  NN    N  " << endl;
    cout << setw(52) << "W   W   W  O     O  N N   N  " << endl;
    cout << setw(52) << "W  W W  W  O     O  N  N  N  " << endl;
    cout << setw(52) << "W W   W W  O     O  N   N N  " << endl;
    cout << setw(52) << "WW     WW  O     O  N    NN  " << endl;
    cout << setw(52) << "W       W   OOOOO   N     N  " << endl;
}



void clearScreen() {
 
    system("CLS");
}

void INPUTANSWERS(int YOUR_GUESS[10], int TotalChance)
{ 
    if (TotalChance == 10)
    {
        cout<< setw(52) << " L       OOO   SSSS  EEEEE\n"
            << setw(52) << " L      O   O  S     E    \n"
            << setw(52) << " L      O   O  SSS   EEEE \n"
            << setw(52) << " L      O   O     S  E    \n"
            << setw(52) << " LLLLL   OOO   SSSS  EEEEE\n";
    }
    cout<<setw(44)  << "   YOUR ANSWERS" << endl;
    cout  <<setw(49)<< "*************************" << endl;
    cout << setw(26) << "- ";
    for (int i = 0; i < TotalChance; i++)
    {
        cout << YOUR_GUESS[i] << "  ";
    }
    cout <<  endl;
    cout << setw(49) << "*************************" << endl;
}


void SHOWİNG_SCORE(int score1)
{
    cout << setw(44) << " YOUR SCORE  " << endl;
    cout << setw(49) << "*************************" << endl;
    cout << setw(50) << "*                        *" << endl;
    cout << setw(37) << score1 << endl;
    cout << setw(50) << "*                        *" << endl;
    cout << setw(49) << "*************************" << endl;
}
