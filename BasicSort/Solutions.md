
***Name:Shreyas Prabhakar Bansode***



***Roll no:6***


# Assignment 2: Sorting Algorithms – Bubble Sort, Insertion Sort, Selection Sort

# Set A


***a)Sort a random array of n integers (accept the value of n from user) 
in ascending order by using bubble sort algorithm.***

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
    for( i=0;i<n;i++)
        printf(" %d ",arr[i]);
    printf("\n");
}

int *b_sort(int *arr,int n)
{
	int i,j,temp;

	for(i=0;i<n-1;i++)
	{
		for(j=0;j<n-i-1;j++)
		{
			if(arr[j]>arr[j+1])
			{
				temp=arr[j];
				arr[j]=arr[j+1];
				arr[j+1]=temp;
			}
		}
	}

	return arr;
}

int main()
{
    int *arr;
    int n;

    srand(time(0));


    printf("\nEnter n value:");
    scanf("%d",&n);
    arr=generate_arr(n);
    printarr(arr,n);

	  printf("\nSorted array using bubble sort\n");
	  printarr(b_sort(arr,n),n);
    free(arr);
    return 0;
}
```


***b)Sort a random array of n integers (accept the value of n from user) 
in ascending order by using insertion sort algorithm.***

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
    for( i=0;i<n;i++)
        printf(" %d ",arr[i]);
    printf("\n");
}

int *i_sort(int *arr,int n)
{
  int i,j,temp;

  for(i=1;i<n;i++)
  {
    temp=arr[i];
    
    for(j=i-1; (j>=0) && (temp<arr[j]);j--)
	    arr[j+1]=arr[j];
	
	arr[j+1]=temp;
  }
   return arr;
}
int main()
{
    int *arr;
    int n;

    srand(time(0));

    printf("\nEnter n value:");
    scanf("%d",&n);
    arr=generate_arr(n);
    printarr(arr,n);

    printf("\nSorted array using insertion sort\n");
    printarr(i_sort(arr,n),n);
    free(arr);
    
    return 0;
}
```

***c)Sort a random array of n integers (accept the value of n from user) 
in ascending order by using selection sort algorithm.***

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
    for( i=0;i<n;i++)
        printf(" %d ",arr[i]);

    printf("\n");
}

int *s_sort(int *arr,int n)
{
        int i,j,min,temp;

        for(i=0;i<n;i++)
        {
          min=i;
          
          for(j=i+1;j<n;j++)
          {
            if(arr[min]>arr[j])
              min=j;
             
          }
          temp=arr[i];
          arr[i]=arr[min];
         arr[min]=temp;
          
        }
        return arr;
}

int main()
{
    int *arr;
    int n;

    srand(time(0));
    
    printf("\nEnter n value:");
    scanf("%d",&n);
    arr=generate_arr(n);
    printarr(arr,n);

    printf("\nSorted array using selection sort\n");
    printarr(s_sort(arr,n),n);
    free(arr);
    
    return 0;
}
```

# Set B

***a) Read the data from the file “employee.txt” and sort on age using bubble sort,
insertion sort and selection sort.***

```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>

typedef struct Employee
{
	char name[30];
	int age;
	int salary;
}Employee;


int store(Employee *emp)
{
	int i=0;
	FILE *fp;
	
	fp=fopen("Employee.txt","r");

	if(fp!=NULL)
	{
		while(fscanf(fp,"%s %d %d",emp[i].name,&emp[i].age,&emp[i].salary)!=EOF)
		i++;
		
		fclose(fp);
		return i;
	}
		return -1;
}

void print_emp(Employee *emp,int size)
{
	int i=0;
	printf("\nEmployees Details:\n");
	while(i<size)
	printf("\nname: %s || age: %d || salary: %d\n",emp[i].name,emp[i].age,emp[i++].salary);
}

Employee * b_sort(Employee *emp,int size)
{
	int i,j;

	for(i=0;i<size-1;i++)
	{
		for(j=0;j<size-i-1;j++)
		{
			if(emp[j].age>emp[j+1].age)
				swap(emp,j,j+1);
		}
	}
	return emp;
}

Employee * i_sort(Employee *emp,int size)
{
  int i,j;
	Employee temp;
	
  for(i=1;i<size;i++)
  {
    temp=emp[i];
    for(j=i-1;(temp.age<emp[j].age && j>=0);j--)
       emp[j+1]=emp[j];

    emp[j+1]=temp;
  }

  return emp;
}

Employee * s_sort(Employee *emp,int size)
{
  int i,j,min;

  for(i=0;i<size;i++)
  {
    min=i;
    for(j=i+1;j<size;j++)
    {
      if(emp[j].age<emp[i].age)
      min=j;
    }
    Employee temp=emp[i];
    emp[i]=emp[min];
    emp[min]=temp;
  }
  return emp;
}
int main()
{
	
	int choice,size;
	Employee emp[40];

	while(1)
	{
	  size=store(emp);
	  if(size!=-1)
		{
		  puts("-----------------------------------------------------");
		  print_emp(emp,size);
		  puts("1-BUBBLE SORT");
          puts("2-ISERTION SORT");
		  puts("3-SELECTION SORT");
		  printf("\nEnter choice:");
		  scanf("%d",&choice);
		  
          puts("---------------------------order by age--------------------------");
		  switch(choice)
	     {
			  
			  case 1:
			  print_emp(b_sort(emp,size),size);
			  break;
			  
			  case 2:
			  print_emp(i_sort(emp,size),size);
			  break;
				
			  case 3:
			  print_emp(s_sort(emp,size),size);
			  break;
			  
			  default:
			  puts("Enter valid choice please");
			  break;
			}
		}
		else
			printf("File not found");
	}
	return 0;
}
```
***b) Read the data from the file “employee.txt” and sort on names in 
alphabetical order (use strcmp) using bubble sort, insertion sort and selection sort.***

```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>

typedef struct Employee
{
	char name[30];
	int age;
	int salary;
}Employee;


int store(Employee *emp)
{
	int i=0;
	FILE *fp;
	
	fp=fopen("Employee.txt","r");

	if(fp!=NULL)
	{
		while(fscanf(fp,"%s %d %d",emp[i].name,&emp[i].age,&emp[i].salary)!=EOF)
		i++;
		
		fclose(fp);
		return i;
	}
		return -1;
}

void print_emp(Employee *emp,int size)
{
	int i=0;
	printf("\nEmployees Details:\n");
	while(i<size)
	printf("\nname: %s || age: %d || salary: %d\n",emp[i].name,emp[i].age,emp[i++].salary);
}

Employee* b_sort(Employee *emp,int size)
{
	int i,j;

	for(i=0;i<size-1;i++)
	{
		for(j=0;j<size-i-1;j++)
		{
			if(strcmp(emp[j].name,emp[j+1].name)>0)
				swap(emp,j,j+1);
		}
	}
	return emp;
}

Employee * i_sort(Employee *emp,int size)
{
  int i,j;
  Employee temp;

  for(i=1;i<size;i++)
  {
    temp=emp[i];
    for(j=i-1;(strcmp(temp.name,emp[j].name)<0 && j>=0);j--)
    emp[j+1]=emp[j];

	emp[j+1]=temp;
  }

   return emp;

}

Employee * s_sort(Employee *emp,int size)
{
  int i,j,min;

  for(i=0;i<size;i++)
  {
    min=i;
    for(j=i+1;j<size;j++)
    {
      if(strcmp(emp[min].name,emp[j].name)>0)
         min=j;
    }
    Employee temp=emp[i];
    emp[i]=emp[min];
    emp[min]=temp;
  }

        return emp;

}
int main()
{
	
	int choice,size;
	Employee emp[40];

	while(1)
	{
	  size=store(emp);
	  if(size!=-1)
		{
		    puts("-----------------------------------------------------");
		    print_emp(emp,size);
			puts("1-BUBBLE SORT");
			puts("2-ISERTION SORT");
			puts("3-SELECTION SORT");
			printf("\nEnter choice:");
			scanf("%d",&choice);
			puts("---------------------------order by name--------------------------");
			switch(choice)
			{
			  case 1:
			  print_emp(b_sort(emp,size),size);
			  break;
			  
			  case 2:
			  print_emp(i_sort(emp,size),size);
			  break;
				
			  case 3:
			  print_emp(s_sort(emp,size),size);
			  break;
			  
		      default:
			  puts("Enter valid choice please");
		      break;
			}
		}
		else
			printf("File not found");
	}
	return 0;
}

