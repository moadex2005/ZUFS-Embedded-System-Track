Access Strings

Since strings are actually arrays in C, you can access a string by referring to its index number inside square brackets [].
This example prints the first character (0) in greetings:

Example

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    char str[] = "24 degrees";
    int amount = atoi(str);
    printf("%d", amount);  // Output: 24
    return 0;
}
```
Modify Strings

To change the value of a specific character in a string, refer to the index number, and use single quotes:

Example
```c
#include <stdio.h>

int main() {
    char greetings[] = "Hello World!";
    greetings[0] = 'J';
    printf("%s", greetings);  // Outputs: Jello World!
    return 0;
}
```

Loop Through a String

You can also loop through the characters of a string, using a for loop:

Example


```c
#include <stdio.h>

int main() {
    char carName[] = "Volvo";
    int i;

    for (i = 0; i < 5; ++i) {
        printf("%c\n", carName[i]);
    }

    return 0;
}
```


C stdlib atoi() Function


Example

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    char str[] = "24 degrees";
    int amount = atoi(str);
    printf("%d", amount);  // Output: 24
    return 0;
}
```

String Functions 


<table class="ws-table-all notranslate">
  <tbody><tr>
    <th style="width:20%">Function</th>
    <th style="width:80%">Description</th>
  </tr>
  <tr>
    <td><a href="ref_string_memchr.php">memchr()</a></td>
    <td>Returns a pointer to the first occurrence of a value in a block of memory</td>
  </tr>
  <tr>
    <td><a href="ref_string_memcmp.php">memcmp()</a></td>
    <td>Compares two blocks of memory to determine which one represents a larger numeric value</td>
  </tr>
  <tr>
    <td>memcpy()</td>
    <td>Copies data from one block of memory to another</td>
  </tr>
  <tr>
    <td>memmove()</td>
    <td>Copies data from one block of memory to another accounting for the possibility that the blocks of memory overlap</td>
  </tr>
  <tr>
    <td>memset()</td>
    <td>Sets all of the bytes in a block of memory to the same value</td>
  </tr>
  <tr>
    <td><a href="ref_string_strcat.php">strcat()</a></td>
    <td>Appends one string to the end of another</td>
  </tr>
  <tr>
    <td><a href="ref_string_strchr.php">strchr()</a></td>
    <td>Returns a pointer to the first occurrence of a character in a string</td>
  </tr>
  <tr>
    <td><a href="ref_string_strcmp.php">strcmp()</a></td>
    <td>Compares the ASCII values of characters in two strings to determine which string has a higher value</td>
  </tr>
  <tr>
    <td>strcoll()</td>
    <td>Compares the locale-based values of characters in two strings to determine which string has a higher value</td>
  </tr>
  <tr>
    <td><a href="ref_string_strcpy.php">strcpy()</a></td>
    <td>Copies the characters of a string into the memory of another string</td>
  </tr>
  <tr>
    <td><a href="ref_string_strcspn.php">strcspn()</a></td>
    <td>Returns the length of a string up to the first occurrence of one of the specified characters</td>
  </tr>
  <tr>
    <td><a href="ref_string_strerror.php">strerror()</a></td>
    <td>Returns a string describing the meaning of an error code</td>
  </tr>
  <tr>
    <td><a href="ref_string_strlen.php">strlen()</a></td>
    <td>Return the length of a string</td>
  </tr>
  <tr>
    <td><a href="ref_string_strncat.php">strncat()</a></td>
    <td>Appends a number of characters from a string to the end of another string</td>
  </tr>
  <tr>
    <td><a href="ref_string_strncmp.php">strncmp()</a></td>
    <td>Compares the ASCII values of a specified number of characters in two strings to determine which string has a higher value</td>
  </tr>
  <tr>
    <td><a href="ref_string_strncpy.php">strncpy()</a></td>
    <td>Copies a number of characters from one string into the memory of another string</td>
  </tr>
  <tr>
    <td><a href="ref_string_strpbrk.php">strpbrk()</a></td>
    <td>Returns a pointer to the first position in a string which contains one of the specified characters</td>
  </tr>
  <tr>
    <td><a href="ref_string_strrchr.php">strrchr()</a></td>
    <td>Returns a pointer to the last occurrence of a character in a string</td>
  </tr>
  <tr>
    <td><a href="ref_string_strspn.php">strspn()</a></td>
    <td>Returns the length of a string up to the first character which is not one of the specified characters</td>
  </tr>
  <tr>
    <td><a href="ref_string_strstr.php">strstr()</a></td>
    <td>Returns a pointer to the first occurrence of a string in another string</td>
  </tr>
  <tr>
    <td><a href="ref_string_strtok.php">strtok()</a></td>
    <td>Splits a string into pieces using delimiters</td>
  </tr>
  <tr>
    <td>strxfrm()</td>
    <td>Convert characters in a string from ASCII encoding to the encoding of the current locale</td>
  </tr>
</tbody></table>
