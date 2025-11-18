# Ex-4 Rail-Fence-Program
# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM
```
 #include <stdio.h>
#include <string.h>
#define MAX 100
// FuncƟon to encrypt the plaintext using Rail-Fence Cipher
void encryptRailFence(char plainText[], char cipherText[], int key) {
 char rail[key][MAX];
 int i, j, row = 0, col = 0, dir_down = 0;
 int len = strlen(plainText);
 // IniƟalize rail matrix
 for(i = 0; i < key; i++)
 for(j = 0; j < len; j++)
 rail[i][j] = '\n';
 // Place characters in zig-zag paƩern
 for(i = 0; i < len; i++) {
 if(row == 0) dir_down = 1;
 if(row == key-1) dir_down = 0;
 rail[row][col++] = plainText[i];
 dir_down ? row++ : row--;
 }
 // Read matrix row-wise to get encrypted text
 int index = 0;
 for(i = 0; i < key; i++)
 for(j = 0; j < len; j++)
 if(rail[i][j] != '\n')
 cipherText[index++] = rail[i][j];
 cipherText[index] = '\0';
}
// FuncƟon to decrypt the ciphertext using Rail-Fence Cipher
void decryptRailFence(char cipherText[], char decryptedText[], int key) {
 char rail[key][MAX];
 int i, j, row = 0, col = 0, dir_down = 0;
 int len = strlen(cipherText);
 // IniƟalize rail matrix
 for(i = 0; i < key; i++)
 for(j = 0; j < len; j++)
 rail[i][j] = '\n';
 // Mark the zig-zag posiƟons with '*'
 for(i = 0; i < len; i++) {
 if(row == 0) dir_down = 1;
 if(row == key-1) dir_down = 0;
 rail[row][col++] = '*';
 dir_down ? row++ : row--;
 }
 // Fill the leƩers in marked posiƟons
 int index = 0;
 for(i = 0; i < key; i++)
 for(j = 0; j < len; j++)
 if(rail[i][j] == '*' && index < len)
 rail[i][j] = cipherText[index++];
 // Read zig-zag to get decrypted text
 row = 0; col = 0; dir_down = 0;
 for(i = 0; i < len; i++) {
 if(row == 0) dir_down = 1;
 if(row == key-1) dir_down = 0;
 decryptedText[i] = rail[row][col++];
 dir_down ? row++ : row--;
 }
 decryptedText[len] = '\0';
}
int main() {
 char plainText[MAX], cipherText[MAX], decryptedText[MAX];
 int key;
 prinƞ("Enter the text: ");
 fgets(plainText, MAX, stdin);
 plainText[strcspn(plainText, "\n")] = 0; // Remove newline
 prinƞ("Enter the number of rails: ");
 scanf("%d", &key);
 encryptRailFence(plainText, cipherText, key);
 prinƞ("\nEncrypted Text: %s\n", cipherText);
 decryptRailFence(cipherText, decryptedText, key);
 prinƞ("Decrypted Text: %s\n", decryptedText);
 return 0;
} 
 ```

# OUTPUT
<img width="592" height="398" alt="image" src="https://github.com/user-attachments/assets/cc8c3b40-228e-4611-b529-c460add14826" />



# RESULT

The program executed successfully.
