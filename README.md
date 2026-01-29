## EX. NO:2 IMPLEMENTATION OF PLAYFAIR CIPHER

 

## AIM:
 

 

To write a C program to implement the Playfair Substitution technique.

## DESCRIPTION:

The Playfair cipher starts with creating a key table. The key table is a 5×5 grid of letters that will act as the key for encrypting your plaintext. Each of the 25 letters must be unique and one letter of the alphabet is omitted from the table (as there are 25 spots and 26 letters in the alphabet).

To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. The two letters of the diagram are considered as the opposite corners of a rectangle in the key table. Note the relative position of the corners of this rectangle. Then apply the following 4 rules, in order, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of corners of the rectangle defined by the original pair.
## EXAMPLE:
![image](https://github.com/Hemamanigandan/EX-NO-2-/assets/149653568/e6858d4f-b122-42ba-acdb-db18ec2e9675)

 

## ALGORITHM:

STEP-1: Read the plain text from the user.
STEP-2: Read the keyword from the user.
STEP-3: Arrange the keyword without duplicates in a 5*5 matrix in the row order and fill the remaining cells with missed out letters in alphabetical order. Note that ‘i’ and ‘j’ takes the same cell.
STEP-4: Group the plain text in pairs and match the corresponding corner letters by forming a rectangular grid.
STEP-5: Display the obtained cipher text.




## Program:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

char m[5][5];
void keyMatrix(char key[])
{
    int used[26]={0}, k=0;
    for(int i=0; key[i]; i++)
    {
        if(key[i]=='J') key[i]='I';
        if(!used[key[i]-'A'])
            m[k/5][k%5]=key[i], used[key[i]-'A']=1, k++;
    }
    for(int i=0;i<26;i++)
        if(i+'A'!='J' && !used[i])
            m[k/5][k%5]=i+'A', k++;
}
void find(char c,int *r,int *c1)
{
    for(int i=0;i<5;i++)
        for(int j=0;j<5;j++)
            if(m[i][j]==c){*r=i;*c1=j;}
}

void encrypt(char t[])
{
    int r1,c1,r2,c2;
    printf("Encrypted Text: ");
    for(int i=0;i<strlen(t);i+=2)
    {
        find(t[i],&r1,&c1);
        find(t[i+1],&r2,&c2);

        if(r1==r2)
            printf("%c%c",m[r1][(c1+1)%5],m[r2][(c2+1)%5]);
        else if(c1==c2)
            printf("%c%c",m[(r1+1)%5][c1],m[(r2+1)%5][c2]);
        else
            printf("%c%c",m[r1][c2],m[r2][c1]);
    }
}

int main()
{
    char key[20], text[50];

    printf("Enter Key: ");
    scanf("%s",key);
    printf("Enter Plain Text: ");
    scanf("%s",text);

    for(int i=0;key[i];i++) key[i]=toupper(key[i]);
    for(int i=0;text[i];i++){
        text[i]=toupper(text[i]);
        if(text[i]=='J') text[i]='I';
    }

    if(strlen(text)%2!=0) strcat(text,"X");

    keyMatrix(key);
    encrypt(text);
    return 0;
}
```
## Output:
<img width="1918" height="946" alt="Screenshot 2026-01-29 144621" src="https://github.com/user-attachments/assets/48723edb-cab2-4657-8465-b5ec48adf2d8" />
<img width="1920" height="998" alt="Screenshot 2026-01-29 at 14-46-38 Online C Compiler - Programiz" src="https://github.com/user-attachments/assets/3320bd3e-47ca-4c17-8262-91703db02e7b" />

## Result:
Thus the program executed successfully.


