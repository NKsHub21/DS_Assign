
# <center> ASSIGNMENT NO -1 Unit _1</center>

## Title :  
Implement basic string operations such as length calculation, copy, reverse, and concatenation using character single dimensional arrays without using built-in string library functions 

---

## What are Basic String Operations ?  

Strings are arrays of characters terminated by a special null character `'\0'`.  
In programming, we often perform operations such as **finding the length of a string, copying one string to another, reversing a string, and concatenating two strings**.  

Here, we will implement these operations **manually using single-dimensional character arrays** instead of relying on built-in string library functions like `strlen()`, `strcpy()`, `strcat()`, etc.  

---

## Algorithm  

### 1. String Length Calculation
```

1. Start
2. Initialize a counter = 0
3. Traverse the string character by character
4. For each character until '\0' is found, increment counter
5. Return counter as the length
6. End

```

### 2. String Copy
```

1. Start
2. Input source string (src)
3. Initialize destination string (dest)
4. Traverse src until '\0'
5. For each character in src → copy it to dest
6. Append '\0' at the end of dest
7. End

```

### 3. String Reverse
```

1. Start
2. Input string str
3. Find its length using length algorithm
4. Initialize two indices: start = 0, end = length - 1
5. Swap str\[start] and str\[end] until start < end
6. End

```

### 4. String Concatenation
```

1. Start
2. Input two strings str1 and str2
3. Find length of str1
4. From the end of str1, append characters of str2 one by one
5. Add '\0' at the end
6. End

```
```

---
```

## Code
```
#include <iostream>
using namespace std;

int strlen_npk(char str[])
{
    int len_npk = 0;
    while (str[len_npk] != '\0')
    {
        len_npk++;
    }
    return len_npk;
}

void strcpy_npk(char dest_npk[], char src_npk[])
{
    int i = 0;
    while (src_npk[i] != '\0')
    {
        dest_npk[i] = src_npk[i];
        i++;
    }
    dest_npk[i] = '\0';
}

void strrev_npk(char dest_npk[], char src_npk[])
{
    int len = strlen_npk(src_npk);
    int i = 0;
    
    while (i < len)
    {
        dest_npk[i] = src_npk[len - 1 - i]; 
        i++;
    }
    dest_npk[i] = '\0';
}

void strconcat_npk(char str1[], char str2[])
{
    int i = strlen_npk(str1);
    int j = 0;
    
    while (str2[j] != '\0')
    {
        str1[i] = str2[j];
        i++;
        j++;
    }
    str1[i] = '\0';
}

int main(void)
{
    char str1_npk[50], str2_npk[50];

    cout << "Enter string 1: ";
    cin.getline(str1_npk, 50);
    cout << "Enter string 2: ";
    cin.getline(str2_npk, 50);

    cout << "Length of string 1 is: " << strlen_npk(str1_npk) << endl;
    cout << "Length of string 2 is: " << strlen_npk(str2_npk) << endl;

    char dest_npk[50];
    strcpy_npk(dest_npk, str1_npk);
    cout << "String 1 copied to dest is: " << dest_npk << endl;

    char rev_dest_npk[50]; 
    strrev_npk(rev_dest_npk, str1_npk); 
    cout << "String 1 reversed is: " << rev_dest_npk << endl;

    strconcat_npk(str1_npk, str2_npk);
    cout << "String 1 and String 2 concatenated is: " << str1_npk << endl;

    return 0;
}

```
## Output
```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Assign_1.cpp -o Assign_1 } ; if ($?) { .\Assign_1 }
Enter string 1: Nandini
Enter string 2: Kurle
Length of string 1 is: 7
Length of string 2 is: 5
String 1 copied to dest is: Nandini
String 1 reversed is: inidnaN
String 1 and String 2 concatenated is: NandiniKurle
PS C:\Users\Nandini\Documents\DS_VIT> 
```