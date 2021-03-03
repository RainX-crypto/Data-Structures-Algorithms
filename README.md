#include<stdio.h>
#include<stdlib.h>
#include<stdbool.h>



/*------------------------------ARRAY---------------------------------*/

typedef struct myArray{  
    int size;
    int used_size;
    int * ptr;
}Array;

void createArray(Array* a, int org_size, int used_size){
    a->size= org_size;
    a->used_size= used_size;
    a->ptr= (int*)malloc(org_size * sizeof(int));
}

void valueEntry(Array* a){
    int value;
    for(int i=0; i< a->used_size; i++ )
    {
        printf("Enter Element %d - ",i+1);
        scanf("%d",&value);
        (a->ptr)[i]=value;
    }
}

void PrintArray(Array* a){
    for(int i=0; i< a->used_size; i++ ){
        printf("%d ",(a->ptr)[i]);
    }
}

void Insertion(Array* a, int org_size,int used_size,int data,int index ){
    if(used_size>=org_size){ 
        printf("NO space\n");
    }
    for(int i=used_size-1; i>=index; i--){
        (a->ptr)[i+1] = (a->ptr)[i];
    }
    (a->ptr)[index]=data;
}

void Deletion(Array* a, int org_size, int used_size, int index ){
    if(used_size<=0){ 
        printf("NO ELEMENT TO DELETE\n");
    }
    for(int i=index; i<=used_size-1; i++){
        (a->ptr)[i] = (a->ptr)[i+1];
    }
}

bool linearSearch(Array* a, int used_size, int data){
     if(used_size<=0){ 
        printf("NO ELEMENTS IN ARRAY. LINEAR SEARCH STOPPED.exe\n");
    }
    for(int i=0; i<=used_size-1; i++){
        if((a->ptr)[i] == data){
            printf("Linear Search Done! Element Found at Index %d is data - %d\n",i,data);
            return true;
        }
    }
    printf("ELEMENT %d NOT FOUND!\n",data);
    return false;
}

bool binarySearch(Array* a, int used_size, int data){
     if(used_size<=0){ 
        printf("NO ELEMENTS IN ARRAY. BINARY SEARCH STOPPED.exe\n");
    }
    int low,mid,high;
    low= 0; //Array starting index
    high= used_size-1; //Last index of Array
    mid= (low+high)/2;
    while(low<=high){
        if((a->ptr)[mid]==data){
             printf("Binary Search Done! Element Found at Index %d is data - %d\n",mid,data);
             return true;
        }
        if((a->ptr)[mid]<data){  //mid element value less than data
            low=mid+1;
        }
        else{
            high=mid-1;
        }
    }
    printf("ELEMENT %d NOT FOUND!\n",data);
    return false;
}

void Counter(Array* a){
    int count=0;
     for(int i=0; i< a->used_size; i++ ){
         count++;
    }
    printf("The numbers of elements in Array is %d",count);
}

/*----------------------SINGLY LINKED LISTS---------------------------*/

typedef struct Node{   
    int data;
    struct Node* next;
}Node;

Node* head;

void LinkedListTraversal(){
    int i=0;
    Node* ptr= head;
    while(ptr!=NULL){
        printf("Element %d - %d\n",i+1,ptr->data);
        ptr=ptr->next;
        i++;
    }
}

void Insertion_As_Head(int data){
    Node* new_head= (Node*)malloc(sizeof(Node));
    new_head->data= data;
    new_head->next= head;
    head=new_head;
}

void Insertion_At_Index(int data, int index){
    Node* new_node= (Node*)malloc(sizeof(Node));
    Node* ptr=head;
    int i=0;
    while(i!=index-1){
        ptr=ptr->next;
        i++;
    }
    new_node->data=data;
    new_node->next=ptr->next;
    ptr->next=new_node;
}    

void Insertion_At_End(int data){
    Node* new_node= (Node*)malloc(sizeof(Node));
    Node* ptr= head;
    while(ptr->next!=NULL){
        ptr=ptr->next;
    }
    new_node->data= data;
    ptr->next=new_node;
    new_node->next=NULL;
}

void Insertion_After_Node(int data, Node* PrevNode){
    Node* new_node= (Node*)malloc(sizeof(Node));
    Node* ptr= PrevNode;
    new_node->data=data;
    new_node->next=PrevNode->next;
    PrevNode->next=new_node;
}



/*----------------------STACKS(USING ARRAYS)--------------------------*/

typedef struct stack{
    int size;
    int top;
    int* arr;
}stackARR;

void ARRStackTraversal(stackARR* p){
   printf("Displaying Elements\n");
   for(int i=0; i<p->size; i++){
       if(p->arr[i]!='\0'){
           printf("%d ",p->arr[i]);
       }
   }
   printf("\n");
}

bool UnderFlow_Verifier(stackARR* p){
    if(p->top==-1){
        return true;
    }
    else{
        return false;
    }
}

bool OverFlow_Verifier(stackARR* p){
    if(p->top==(p->size)-1){
        return true;
    }
    else{
        return false;
    }
}

void StackTop(stackARR* p){
    printf("THE TOPMOST ELEMENT IN STACK---> %d", p->arr[p->top]);
}

void StackBottom(stackARR* p){
     printf("THE BOTTOMMOST ELEMENT IN STACK---> %d", p->arr[0]);
}

void Peek(stackARR* p, int index){
    int Ind= (p->top)-index;
    if(Ind<0){
        printf("Not Valid Index!\n");
    }
    else{
        printf("The Element at Index %d --->  %d",index,p->arr[Ind+1]);
    }
}

void Push(stackARR* p, int val){
    if(OverFlow_Verifier(p)){
        printf("Error 101: Stack Overflow!\n");
    }
    else{
        p->top++;
        p->arr[p->top]=val;
        printf("Injected Successfully! Data - %d\n",val);
    }
}

void Pop(stackARR* p){
    if(UnderFlow_Verifier(p)){
        printf("Error 101: Stack Underflow!\n");
    }
    else{
        int val=p->arr[p->top];
        p->top--;
        printf("Drained Successfully! Data - %d\n", val);
    }
}

void Store(stackARR* p){
    int count=0;
    for(int i=0; i<p->size; i++){
       if(p->arr[i]!='\0'){
           count++;
       }
}
       printf("The number of Elements in Stack is %d\n",count);
}

/*-------------------------STACKS(LINKED LISTS)-----------------------*/

typedef struct junction{   
    int data;
    struct junction* next;
}stackLL;

stackLL* peak;

void LLStackTraversal(){
    int i=0;
    stackLL* ptr=peak;
    printf("Displaying Elements\n");
    while(ptr!=NULL){
        printf("Element %d --> %d\n",i+1,ptr->data);
        ptr= ptr->next;
        i++;
    }
}


bool Empty_Verifier(){
    if(peak == NULL){
        return true;
    }
    else{
        return false;
    }
}

bool Full_Verifier(){
    stackLL* new_peak=(stackLL*)malloc(sizeof(stackLL));
    if(new_peak == NULL){
        return true;
    }
    else{
        return false;
    }
}

void Inject(int val){
    stackLL* new_peak= (stackLL*)malloc(sizeof(stackLL));
    if(Full_Verifier()==true){
        printf("Error 101: Stack Overflow!\n");
    }
    else{
        new_peak->data=val;
        new_peak->next=peak;
        peak=new_peak;
        printf("Injected Successfully! Data - %d\n",val);
    }
}

void Drain(){
    stackLL* ptr= peak;
    if(Empty_Verifier()==true){
        printf("Error 101: Stack Underflow!\n");
    }
    else{
        ptr= ptr->next;
        int x=peak->data;
        free(peak);
        peak= ptr;
        printf("Drained Successfully! Data - %d\n", x);
    }
}

void Find_Element(int index){
    stackLL* p= peak;
    for(int i=0; (i<index-1 && p!=NULL); i++){
        p= p->next;
    }
    if(p!=NULL){
        printf("The Element at Index %d --->  %d\n",index,p->data);
    }
    else{
        printf("Element not Found!\n");
    }
}

void Stackpeak(){
    printf("THE TOPMOST ELEMENT IN STACK--> %d\n",peak->data);
}

void StackEnd(){
    stackLL* p= peak;
    while(p->next!=NULL){
        p= p->next;
    }
     printf("THE BOTTOMMOST ELEMENT IN STACK---> %d\n",p->data);
}

/*--------------------------PARENTHESIS-------------------------------*/










/*--------------------------------------------------------------------*/

int main() {                           
                             
    int max_size,used_sise,element,position;
    char choice[10];

/*------------------------------ARRAY---------------------------------*/
                                                                
// printf("---ARRAY OPERATIONS---\n\n");
// Array* A= (Array*)malloc(sizeof(Array));
//     printf("Enter Max. size of Array-->  ");
//     scanf("%d",&max_size);
//     printf("Enter size of Array-->  ");
//     scanf("%d",&used_sise);
//     printf("\n\n");
//     createArray(A, max_size, used_sise);  //Creation of Array
//     printf("---INPUT OPERATOR IS RUNNING---\n\n");
//     valueEntry(A);  //Value Entry
//     printf("Showing Array--> ");
//     PrintArray(A);
//     printf("\n\n"); 
//     printf("---INSERTION ALGORITHM IS RUNNING---\n\n");
//     printf("Enter index at which data is to be inserted-->  \n");
//     scanf("%d",&position);
//     printf("Enter Data to be inserted at index %d-->  ",position);
//     scanf("%d",&element);
//     Insertion(A,max_size,used_sise,element,position); //Insertion At Index
//     A->used_size+=1;
//     printf("Showing Array After Insertion--> ");
//     PrintArray(A);
//     printf("\n\n");
//     printf("---DELETION ALGORITHM IS RUNNING---\n\n");
//     printf("Enter index at which data is to be deleted-->   ");
//     scanf("%d",&position);
//     Deletion(A,max_size,used_sise,position);  //Deletion at Index
//     A->used_size-=1;
//     printf("Showing Array After Deletion--> ");
//     PrintArray(A);
//     printf("\n\n"); 
//     printf("---LINEAR SEARCH ALGORITHM RUNNING---\n\n");
//     printf("Enter Data to be Searched-->  ");
//     scanf("%d",&element);
//     linearSearch(A,used_sise,element);  //Linear Search for unsorted array
//     printf("---BINARY SEARCH ALGORITHM RUNNING(FOR SORTED ARRAY STRICTLY---\n\n");
//     printf("Enter Data to be Searched-->  ");
//     scanf("%d",&element);
//     binarySearch(A,used_sise,element);   //Array should be sorted
//     Counter(A);

/*----------------------SINGLY LINKED LISTS---------------------------*/

//  void create(){
//       Node* head= NULL;
//   }
//   Node* second;
//   Node* third;
//   Node* fourth;
   
//   head= (Node*)malloc(sizeof(Node));
//   second= (Node*)malloc(sizeof(Node));    
//   third= (Node*)malloc(sizeof(Node));  
//   fourth= (Node*)malloc(sizeof(Node));   
   
//   head->data=7;
//   head->next=second;
//   second->data=12;
//   second->next=third;
//   third->data=19;
//   third->next=fourth;
//   fourth->data=56;
//   fourth->next=NULL;
//   LinkedListTraversal();   
//   Insertion_As_Head(5);
//   printf("After Insertion at head\n");
//  LinkedListTraversal();
//  Insertion_At_Index(100,3);
//  printf("After Insertion at index (3+1)=4\n");
//  LinkedListTraversal();\
//  Insertion_At_End(55);
//  printf("After Insertion at end\n");
//  LinkedListTraversal();
//  Insertion_After_Node(122,third);
//  printf("Insertion After third node\n");
//  LinkedListTraversal();
 
 
   

/*---------------------STACKS USING ARRAYS---------------------------*/


//   printf("---STACKS USING ARRAYS---\n\n");
//   stackARR* s=(stackARR*)malloc(sizeof(stackARR));
//   printf("Enter size of Array-->  ");
//   scanf("%d",&used_sise);
//   printf("\n\n");
//   s->size=used_sise;
//   s->top=-1;
//   s->arr= (int*)malloc(s->size * sizeof(int));
//   for(int i=0; i<used_sise; i++){
//   printf("Enter Data to Push in Stack--->  ");
//   scanf("%d",&element);
//   Push(s,element);
//   printf("\nWant to enter more data? Y/N   ");
//   scanf("%s",choice);
//   if(strcmp(choice,"N")==0){
//       break;
//   }
//   }
//  for(int i=0; i<used_sise; i++){
//   printf("Popping top element from Stack \n\n");
//   Pop(s);
//   printf("\nWant to pop more data? Y/N   ");
//   scanf("%s",choice);
//   if(strcmp(choice,"N")==0){
//       break;
//   }
//   }
//   ARRStackTraversal(s);
//   StackTop(s);
//   StackBottom(s);
//   printf("Enter index at which data is to be deleted-->   ");
//   scanf("%d",&position);
//   Peek(s,position);


/*-------------------STACKS USING LINKED LISTS------------------------*/
  
//   void create(){
//       stackLL* peak =NULL;
//   }
//   Inject(5);
//   Inject(12);
//   Drain();
//   LLStackTraversal();
//   Stackpeak();
//   StackEnd();

/*----------------------PARANTHESIS-----------------------------------*/

   
   
   
    return 0;
}
