Problem statement:

Create a C program to perform various file operations, including reading
from a file, writing to a file, and displaying the contents of a file. The
program should provide options for the user to select the desired operation
from a menu. Upon selecting an operation, the program should execute the
corresponding functionality using appropriate file handling techniques.
Additionally, the program should handle errors such as file not found or
permission issues gracefully and provide informative messages to the user.

Research: 

Links:
 https://www.geeksforgeeks.org/c/basics-file-handling-c/

https://www.geeksforgeeks.org/c/fclose-function-in-c/


File handling  is the process in which we create, open, read, write, and close operations on a file.

Use cases of file handling:

Data Logging:
Recording events, errors, or system activities in log files for debugging, auditing, or performance monitoring.
Example: A web server might log every incoming request to a file.

Data Storage and Retrieval:
Saving and loading data that needs to persist beyond the program's execution, such as user profiles, game states, or database backups.
Example: A word processor saves document content to a .docx file.
Data Processing:
Reading and processing large datasets from files, often in formats like CSV, TSV, or custom binary formats, for analysis or transformation.
Example: A data analysis script reads a large CSV file containing sales data to generate reports

Web Applications and Backend Systems:
Serving static content, storing user-uploaded files, or managing session data in file-based storage.
Example: A social media platform stores user profile pictures as image files on the server.

Analysis:


In file handling in C ,there are various operations:

fopen() -

In C, the fopen() function is used to open a file in the specified mode. The function returns a file pointer (FILE *) which is used to perform further operations on the file, such as reading from or writing to it.

Syntax: FILE*file=fopen("file name","mode");


The file can be opened in 6 modes :

"r" (read mode): Opens an existing text file for reading. Returns NULL if the file does not exist.

"w" (write mode): Opens a text file for writing. If the file exists, its contents 
           are truncated (deleted); otherwise, a new file is created.

"a" (append mode): Opens a text file for appending. Data is written to the end of the file, preserving existing content. If the file does not exist, a new one is created. 

"r+" (read and write mode): Opens an existing text file for both reading and writing. The file must exist. 

"w+" (write and read mode): Opens a text file for both reading and writing. If the file exists, its contents are truncated; otherwise, a new file is created.

"a+" (append and read mode): Opens a text file for both reading and appending. Data is written to the end of the file. If the file does not exist, a new one is created.

fprintf()

fprintf() is used to print information into the file.
Syntax:
fprintf(FILE *file name, “printing lines”);
fprintf(file name,"format specifier”,variable name);

fscanf()

The fscanf() function reads formatted data from a file and writes it into memory locations specified by the arguments, then moves the position indicator to the file position where it stopped reading.

Syntax: 
 fscanf(file name,”format specifier”,address of variable ):
 fscanf(fptr,”%d”,&num):

fclose()

This function is used to close a previously opened file.
Syntax: fclose(file name):

Ideate:
A code 


Built:

#include<stdio.h>
#include<string.h>
int count=0;
 struct list 
    {
        char name[50];
        int ep;
    };
int loadcount()
{
    int c=0;
    char line[100];
    FILE*file=fopen("list.txt","r");
    if (file==NULL)
    {
        return 0;
    }
    while(fgets(line,sizeof(line),file))
    {
        if(strncmp(line,"Sr.No. ",7)==0)
        {
            c++;
        }
    }
    fclose(file);
    return c;
    
}
void add(struct list s[]);
void deletelist(struct list s[]);
void see(struct list s[]);

int main()
{
    struct list s[100];
    int option;
    count=loadcount();
    printf("Welcome to your.anime.list");
    start:
    printf("Enter your choice: \n1)Add new title to your list.\n2)Delete list\n3)See list\n4)Exit\n ");
    scanf("%d",&option);
    switch (option)
    {
        case 1: add(s);
        break;
        case 2: deletelist(s);
        break;
        case 3: see(s);
        break;
        case 4: return 0;
        break;
        default : printf("Invalid input \nEnter valid input\n");
        goto start;
    }
    return 0;
}
void add(struct list s[])
{
    int i,n,ep;
    printf("Enter how many titles to be added\n");
    scanf("%d",&n);
    FILE*file=fopen("list.txt","a");
    if (file == NULL)
    {
        printf("Could not open file!\n");
        return;
    }
    for(i=0;i<n;i++)
    {
        printf("Enter name of title %d ",i+1);
        scanf(" %49[^\n]",s[count].name);
        printf("Enter episodes watched\n");
        scanf("%d",&s[count].ep);
        fprintf(file,"Sr.No. %d\nName: %s\nEpisode: %d\n\n",count+1,s[count].name,s[count].ep);
         count++;
        
    }
    fclose(file);
}

void deletelist(struct list s[])
{
    FILE*file=fopen("list.txt","w");
    fclose(file);
    count=0;
    printf("List content deleted successfull\n");
}

void see(struct list s[])
{
FILE*file=fopen("list.txt","r");
if (file==NULL)
{
    printf("Could not open file!\n");
    return ;
}
char ch;
while((ch=fgetc(file)) != EOF)
{
    putchar(ch);
}
fclose(file);
}
