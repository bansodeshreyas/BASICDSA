

***Name:Shreyas Prabhakar Bansode***



***Roll no:6***


# Assignment 1:Searching Algorithms

# Set A


***a)Create a random array of n integers. Accept a value x from user and use linear search 
algorithm to check whether the number is present in the array or not and output the position if 
the number is present***

```c
#include<stdio.h>
#include<stdlib.h>
#include<time.h>


int * generate_arr(int n)
{
  int i;
  int * arr=(int *)malloc(sizeof(int)*n);
  
  for(i=0;i<n;i++)
  arr[i]=rand()%100;
  return arr;
}

void printarr(int *arr,int n)
{
  int i;
  for(i=0;i<n;i++)
  printf(" %d ",arr[i]);
  printf("\n");
}

int l_search(int *arr,int n,int key)
{
    int i;
    
    for(i=0;i<n;i++)
    {
        if(arr[i]==key)
           return i;
    }
    return -1;
}

int main()
{
        int *arr;
        int key,index,n;
    
        srand(time(0));
        printf("\nEnter n value:");
        scanf("%d",&n);  
        arr=generate_arr(n);
        printarr(arr,n);
        printf("\nEnter number to search:");
        scanf("%d",&key);
        index=l_search(arr,n,key);
        if(index!=-1)
            printf("\nnumber %d found at  index %d\n",key,index);
        else
           printf("\nnumber not found\n");
        free(arr);
        return 0;
}
```

***b)Accept n values in array from user. Accept a value x from user and use sentinel linear 
search algorithm to check whether the number is present in the array or not and output the 
position if the number is present.***


```c
#include<stdio.h>
#include<stdlib.h>

int * acceptarr(int n)
{
    int *arr=(int *)malloc(sizeof(int)*n);
    int i;
    
    printf("Enter n elements\n");
    for(i=0;i<n;i++)
        scanf("%d",arr+i);
    
    return arr;
}

int s_search(int* arr,int n,int key)
{
    int i=0;
    int last=arr[n-1];
    arr[n-1]=key;
    
    while(arr[i]!=key)
     i++;
    arr[n-1]=last;
    
    if(arr[i]==key)
     return i;
    else
     return -1;
}

int main()
{
    int n,index,key;
    int *arr;
    printf("\nEnter n value:");
    scanf("%d",&n);
    arr=acceptarr(n);
    printf("\nEnter number to search:");
    scanf("%d",&key);
    index=s_search(arr,n,key);
    if(index!=-1)
        printf("\n%d found at index %d\n",key,index);
    else
        printf("\n%d not found\n",key);
    free(arr);
    return 0;
}
```


***c) Accept n sorted values in array from user. Accept a value x from user and use binary 
search algorithm to check whether the number is present in sorted array or not and output the 
position if the number is present.***


```c
#include<stdio.h>
#include<stdlib.h>

int search(int *arr,int l,int r,int key)
{
    int mid;
    while(l<=r)
    {
        mid=(l+r)/2;
        
        if(arr[mid]==key)
         return mid;
        
        if(key>arr[mid])
         l=mid+1;
        else
         r=mid-1;
    }
    return -1;
}
int * acceptarr(int n)
{
    int *arr=(int *)malloc(sizeof(int)*n);
    int i;

    printf("Enter n elements\n");
    for(i=0;i<n;i++)
        scanf("%d",arr+i);
    return arr;
}
int main()
{
	int n,index,key;
	int *arr;
	printf("\nEnter n value:");
	scanf("%d",&n);
	arr=acceptarr(n);
	printf("\nEnter number to search:");
	scanf("%d",&key);
	index=search(arr,0,n-1,key);
	if(index!=-1)
		printf("\n%d found at index %d\n",key,index);
	else
		printf("\n%d not found\n",key);
    free(arr);
    return 0;
}
```
# Set B

***a)Read the data from file 'cities.txt' containing names of cities and their STD codes. Accept a 
name of the city from user and use linear search algorithm to check whether the name is 
present in the file and output the STD code, otherwise output “city not in the list”.***


```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>

typedef struct Cities
{
  char name[30];
  int std;

}City;

int store(City *cities)
{
  int i = 0;
  FILE *fp;
  fp = fopen ("cities.txt","r");

  if(fp != NULL)
  {
        while(fscanf(fp,"%s%d",cities[i].name,&cities[i].std) != EOF) //read data and store in arraye
        i++;
        fclose(fp);
        return i;    //returns size of array
  }
  else
        return -1;

}
void display(City *cities,int size)
{
     int i;
     puts("Cities details");
     for(i=0;i<size;i++)
          printf("\nCity name: %s || std code:%d",cities[i].name,cities[i].std);
}

int  l_search(City *cities,int size,char *key)
{
     int i ;
     for(i=0;i<size;i++)
     {
         if(!strcmp(key,cities[i].name))
          return i;
     }
        return -1;
}

int main ()
{
     char key[30];
     City cities[50];
     int index;
     int size;
     size=store(cities);
     
     if(size!=-1) // i.e if file exits
     {
       display(cities,size);
       printf("\nEnter city to search:");
       gets(key);
       index=l_search(cities,size,key);
        
       if(index!=-1)
          printf("\nCity name: %s | std code:%d\n",cities[index].name,cities[index].std);
       else
          printf("\n %s not in list\n",key);
 
      }
      else
          printf("File not found in the directory");
      return 0;
}
```
***b)Read the data from file 'cities.txt' containing names of cities and their STD codes.
 Accept a name of the city from user and use sentinel linear search algorithm to check 
 whether the name is present in the file and output the STD code,
 otherwise output “city not in the list”.***
 
 
```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>

typedef struct Cities
{
  char name[30];
  int std;
}City;

int store(City *cities)
{
     int i = 0;
     FILE *fp;
     fp = fopen ("cities.txt","r");

     if(fp != NULL)
     {
          while(fscanf(fp,"%s%d",cities[i].name,&cities[i].std) != EOF) //read data and store in arraye
          i++;
          fclose(fp);
          return i;    //returns size of array
     }
     else
          return -1;
}
void display(City *cities,int size)
{
     int i;
     puts("Cities details");
     for(i=0;i<size;i++)
        printf("\nCity name: %s || std code:%d",cities[i].name,cities[i].std);
}

int  s_search(City *cities,int size,char *key)
{
        char last[30];
     	int i=0;
    	strcpy(last,cities[size-1].name);
	    strcpy(cities[size-1].name,key);

     	while(strcmp(key,cities[i].name))
        i++;
        
        strcpy(cities[size-1].name,last);
            
        if(!strcmp(cities[i].name,key))
           return i;
        else
           return -1;
}

int main ()
{
     char key[30];
     City cities[50];
     int index;
     int size;
     size=store(cities);
     
     if(size!=-1) // i.e if file exits
    {
        display(cities,size);     
        printf("\nEnter city to search:");
        gets(key);
        index=s_search(cities,size,key);
        
        if(index!=-1)
            printf("\nCity name: %s | std code:%d\n",cities[index].name,cities[index].std);
        else
            printf("\n %s not in the list\n",key);
      
    }
    else
       printf("File not found in the directory");    
    return 0;
}
```

***c)Read the data from file ‘sortedcities.txt’ containing sorted names of cities and their STD codes. 
Accept a name of the city from user and use binary search algorithm to check whetherthe name is 
present in the file and output the STD code, otherwise output “city not in the list”.***

```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>

typedef struct Cities
{
  char name[30];
  int std;

}City;

int store(City *cities)
{
    int i = 0;
    FILE *fp;
    fp = fopen ("sortedcities.txt","r");

   if(fp != NULL)
   {
      while(fscanf(fp,"%s%d",cities[i].name,&cities[i].std) != EOF) //read data and store in array
      i++;
         
      fclose(fp);
      return i;    //returns size of array
    }
    else
      return -1;
}
void display(City *cities,int size)
{
        int i;
        puts("Cities details");
        for(i=0;i<size;i++)
                printf("\nCity name: %s || std code:%d",cities[i].name,cities[i].std);
}
int search(City *cities,int l,int r,char *key)
{
    int mid;                                                      
    while(l<=r)
    {                                                          
	    mid=(l+r)/2;
      if( !strcmp(cities[mid].name,key))                 
		    return mid;
                                                                                      
	    if(strcmp(key,cities[mid].name)>0)
		    l=mid+1;                                                              
	    else                                                   
		    r=mid-1;                                                    
    }
    return -1;
}

int main ()
{
     char key[30];
     City cities[50];
     int index;
     int size;

     size=store(cities);     
     
     if(size!=-1) // i.e if file exits
     {
       display(cities,size);
       printf("\nEnter city to search:");
       gets(key);
       index=search(cities,0,size-1,key);
       
       if(index!=-1)
              printf("\nCity name: %s | std code:%d\n",cities[index].name,cities[index].std);
       else
              printf("\n %s not in list the list\n",key);
     }
     else
        printf("File not found in the directory");
     return 0;
}
```
