# lab-assignment-5
// Tavon Griffith

#include <stdio.h>
#include <stdlib.h>


typedef struct node 
{
  char letter;
  struct node* next;
} node;


int length(node* head)
{
  //declare variable 
  int size = 0;
  
  
  while (head != NULL) 
  {
    
    size++;
    
    head = head->next;
  }
  
  return size;
}


char* toCstring(node* head) 
{
  
  int size = length(head);
  
  char* str = (char*)malloc(size + 1);
  int i = 0;
  
  while (head != NULL) 
  {
    
    str[i] = head->letter;
    
    head = head->next;
    i++;
  }
  
  str[size] = '\0';
  
  return str;
}

void deleteList(node** pHead) 
{
  //set node as head
  node* currentnode = *pHead;
  
  while (currentnode != NULL)
  {
    
    node* temp = currentnode;
    
    currentnode = currentnode->next;
    
    free(temp);
  }
  
  *pHead = NULL;
}

void insertChar(node** pHead, char c)
{

  node* newNode = (node*)malloc(sizeof(node));

  newNode->letter = c;

  newNode->next = NULL;

  if (*pHead == NULL) 
  {
    *pHead = newNode;
  }

  else 
  {

    node* currentnode = *pHead;

    while (currentnode->next != NULL)
    {

      currentnode = currentnode->next;
    }

    currentnode->next = newNode;
  }
}


int main(void) 
{
  
  int i, strLen, numInputs;
  node* head = NULL;
  
  char* str;
  char c;
  
  FILE* itFile = fopen("input.txt", "r");
  
  fscanf(itFile, "%d\n", &numInputs);
  
  while (numInputs > 0) 
  {
   
    fscanf(itFile, "%d\n", &strLen);
    
    for (i = 0; i < strLen; i++) 
    {
      
      fscanf(itFile, "%c", &c);
      
      insertChar(&head, c);
    }
   
    str = toCstring(head);

    
    printf("String is: (%s)\n", str);
   
    free(str);
   
    deleteList(&head);
    
    if (head != NULL)
    {
      printf("deleteList is not correct!\n");
      break;
    }
    
    numInputs--;
  }
 
  fclose(itFile);
  
  return 0;
}
