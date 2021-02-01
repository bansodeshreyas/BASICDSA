
***Name:Shreyas Prabhakar Bansode***



***Roll no:6***


# Assignment 3: Sorting Algorithms –Counting Sort, Merge Sort, Quick Sort

# Set A


***a) Sort a random array of n integers (accept the value of n from user) in ascending order by 
using recursive Counting sort algorithm.***

```c
#include<stdio.h>
#include<stdlib.h>


int * accept(int n)
{
    int *arr=(int *)malloc(sizeof(int)*n);
    int i;
    
    printf("Enter n elements\n");
    for(i=0;i<n;i++)
        scanf("%d",arr+i);
    return arr;
}


void print_arr(int *arr,int n)
{
    printf("\n");
    int i;
    for( i=0;i<n;i++)
        printf(" %d ",arr[i]);
    printf("\n");
}
int *c_sort(int *arr,int range,int n)
{
    int output[n];
    int count[range+1];
    int i;
    
   
    for(i=0;i<range+1;i++)
       count[i]=0;
    
    for(i=0;i<n;i++)
     ++count[arr[i]];
    
    for(i=1;i<=range;i++)
      count[i]+=count[i-1];
    
    for(i=n-1;i>=0;i--)
    {
        output[count[arr[i]]-1]=arr[i];
        --count[arr[i]];
    }
    
    for(i=0;i<n;i++)
    arr[i]=output[i];
    
    return arr;
}
int main()
{
    int *arr;
    int range,n;
    
    printf("\n Enter range:");
    scanf("%d",&range);
    printf("\nEnter n value:");
    scanf("%d",&n);
    arr=accept(n);
    print_arr(arr,n);
    printf("\nSorted array :");
    print_arr(c_sort(arr,range,n),n);
    free(arr);
}
```


***b) Sort a random array of n integers (create a random array of n integers) in ascending order 
by using recursive Quick sort algorithm.***

```c
#include<stdio.h>
#include<stdlib.h>

int * accept(int n)
{
    int *arr=(int *)malloc(sizeof(int)*n);
    int i;
    
    printf("Enter n elements\n");
    for(i=0;i<n;i++)
        scanf("%d",arr+i);
    return arr;
}


void printarr(int *arr,int n)
{
    printf("\n");
    int i;
    for( i=0;i<n;i++)
        printf(" %d ",arr[i]);
    printf("\n");
}

void merge(int *arr,int low,int high,int mid)
{
    int i=low,j=mid+1,k=0;
    int b[30];
    
    while(i<=mid && j<=high)
    {
        if(arr[i]<=arr[j])
          b[k++]=arr[i++];
        else
          b[k++]=arr[j++];
    }
    
    while(i<=mid)
       b[k++]=arr[i++];
    
    while(j<=high)
      b[k++]=arr[j++];
    
    
    for(j=low,k=0;j<=high;j++,k++)
      arr[j]=b[k];
    
}

int *  m_sort(int *arr,int low,int high)
{
    int mid=(low+high-1)/2;
    
    if(low<high)
    {
        m_sort(arr,low,mid);
        m_sort(arr,mid+1,high);
        merge(arr,low,high,mid);
    }
    return arr;
}
int main()
{
    int *arr;
    int n;
    
    printf("\nEnter n value:");
    scanf("%d",&n);
    arr=accept(n);
    printarr(arr,n);
    printf("\nSorted array :");
    printarr(m_sort(arr,0,n-1),n);
    free(arr);

   
}

```

***c)Sort a random array of n integers (accept the value of n from user) in ascending order by 
using a recursive Merge sort algorithm.***

```c
#include<stdio.h>
#include<stdlib.h>

int * accept(int n)
{
    int *arr=(int *)malloc(sizeof(int)*n);
    int i;
    
    printf("Enter n elements\n");
    for(i=0;i<n;i++)
        scanf("%d",arr+i);
 
    return arr;
}


void printarr(int *arr,int n)
{
    printf("\n");
    int i;
    for( i=0;i<n;i++)
        printf(" %d ",arr[i]);
    printf("\n");
    
}

int partition(int *arr,int lb,int ub)
{
    int down=lb+1,up=ub,temp;
    int pivot=arr[lb];
    
    do
    {
        while((arr[down]<pivot )&& down<=up)
          down++;
        while(arr[up]>pivot&& up>=down)
          up--;
        
        if(down<up)
        {
            temp=arr[up];
            arr[up]=arr[down];
            arr[down]=temp;
        }
        
     }while(down<up);
    
    
     arr[lb]=arr[up];
     arr[up]=pivot;
    
   
    return up;
    
}

int*  q_sort(int *arr,int lb,int ub,int n)
{
    int j;
    if(lb<ub)
    {
        j=partition(arr,lb,ub);
        q_sort(arr,lb,j-1,n);
        q_sort(arr,j+1,ub,n);
        
    }
    return arr;
}

int main()
{
    int *arr;
    int n;
    
    printf("\nEnter n value:");
    scanf("%d",&n);
    arr=accept(n);
    printarr(arr,n);
    printf("\nSorted array :");
    printarr(q_sort(arr,0,n-1,n),n);
    free(arr);
}

```

# Set B

***a)Read the data from the ‘employee.txt’ file and sort on age using Counting sort, Merge sort, 
Quick sort and write the sorted data to another file 'sortedemponage.txt'.***


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

void writeFile(Employee *emp,int size)
{
	int i;
	FILE *fp;
	fp = fopen("sortedemponage.txt","w+");
	if(fp!= NULL)
	{
		for (i = 0; i < size; i++)
			fprintf(fp, "%s\t%d\t%d\n", emp[i].name, emp[i].age, emp[i].salary);
			
		printf("\nrecords saved succesfull in sortedemponage.txt\n");
		fclose(fp);
	}
}

void print_emp(Employee *emp,int size)
{
	int i=0;
	printf("\nEmployees Details:\n");
	while(i<size)
	printf("\nname: %s || age: %d || salary: %d\n",emp[i].name,emp[i].age,emp[i++].salary);
}


Employee * c_sort(Employee *emp,int size,int range)
{
	int count[range+1];
	Employee output[size];
	int i;

	for(i=0;i<range+1;i++)
		count[i]=0;

	for(i=0;i<size;i++)
		count[emp[i].age]++;

	for(i=1;i<range+1;i++)
		count[i]+=count[i-1];

	for(i=size-1;i>=0;i--)
	{
		output[count[emp[i].age]-1]=emp[i];
			count[emp[i].age]--;
	}
	for(i=0;i<size;i++)
		emp[i]=output[i];

	return emp;
}

void merge(Employee *emp,int low,int high,int mid)
{
	int i=low,j=mid+1,k=0;
	Employee b[30];

	while(i<=mid && j<=high)
	{
		if(emp[i].age<=emp[j].age)
			b[k++]=emp[i++];
		else
			b[k++]=emp[j++];
	}

	while(i<=mid)
		b[k++]=emp[i++];

	while(j<=high)
		b[k++]=emp[j++];

	for(j=low,k=0;j<=high;j++,k++)
		emp[j]=b[k];

}
Employee *m_sort(Employee *emp,int low,int high)
{
	int mid=(low+high-1)/2;

	if(low<high)
	{
		m_sort(emp,low,mid);
		m_sort(emp,mid+1,high);
		merge(emp,low,high,mid);
	}

	return emp;

}
int partition(Employee *emp,int lb,int ub)
{
	int down=lb+1,up=ub;
	Employee pivot=emp[lb];

	do
	{
		while(emp[down].age<pivot.age && down<=up)
			down++;

		while(emp[up].age>pivot.age && up>=down)
			up--;

		if(down<up)
		{
		  Employee temp=emp[down];
		  emp[down]=emp[up];
		  emp[up]=temp;
		}
	}while(down<up);

	emp[lb]=emp[up];
	emp[up]=pivot;

	return up;
}

Employee * q_sort(Employee *emp,int lb,int ub)
{
	int j;

	if(lb<ub)
	{
		j=partition(emp,lb,ub);
		q_sort(emp,lb,j-1);
		q_sort(emp,j+1,ub);
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
			puts("1-COUNTING SORT");
			puts("2-MERGE SORT");
			puts("3-QUICK SORT");
			printf("\nEnter choice:");
			scanf("%d",&choice);
      puts("---------------------------order by age--------------------------");
			switch(choice)
			{
			  
			  case 1:
			  print_emp(c_sort(emp,size,50),size);
			  break;
			  
				case 2:
			  print_emp(m_sort(emp,0,size-1),size);
				break;
				
				case 3:
				print_emp(q_sort(emp,0,size-1),size);
			  break;
			  
				default:
				puts("Enter valid choice please");
				break;
			}
			writeFile(emp,size);
		}
		else
			printf("File not found");
	}
}


```

***b)Read the data from the file and sort on names in alphabetical order (use strcmp) using 
Counting sort, Merge sort, Quick sort and write the sorted data to another file 
'sortedemponname.txt'.***

```c



#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#define RANGE 255
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

void writeFile(Employee *emp,int size)
{
	int i;
	FILE *fp;
	fp = fopen("sortedemponname.txt","w+");
	if(fp!= NULL)
	{
		for (i = 0; i < size; i++)
			fprintf(fp, "%s\t%d\t%d\n", emp[i].name, emp[i].age, emp[i].salary);
			
		printf("\nrecords saved succesfull in sortedemponname.txt\n");
		fclose(fp);
	}
}
void swap(Employee *emp,int i,int j)
{
        Employee temp=emp[i];
        emp[i]=emp[j];
        emp[j]=temp;
}


void print_emp(Employee *emp,int size)
{
	int i=0;
	printf("\nEmployees Details:\n");
	while(i<size)
	printf("\nname: %s || age: %d || salary: %d\n",emp[i].name,emp[i].age,emp[i++].salary);
}

int get_max(Employee *emp,int size)
{
	int max=0,i;

	for(i=1;i<size;i++)
	{
		if(strlen(emp[max].name)<strlen(emp[i].name))
			max=i;
	}
	return strlen(emp[max].name);
}

int c_sort(Employee *emp,int size,int max,int c)
{
	int count[RANGE+1];
	Employee output[size];
	int i;

	for(i=0;i<RANGE+1;i++)
		count[i]=0;

	for(i=0;i<size;i++)
			count[emp[i].name[c]]++;

	for(i=1;i<RANGE+1;i++)
		count[i]+=count[i-1];

	for(i=0;i<size;i++)
	{
		
			output[count[emp[i].name[c]]-1]=emp[i];
			count[emp[i].name[c]]--;
	}
	for(i=0;i<size;i++)
		emp[i]=output[i];
		
	return -1;
}
Employee* r_sort(Employee *emp,int size)
{
	int i, max=get_max(emp,size);

	printf("\n%d",max);
	for(i=max-1;i>=0;i--)
		c_sort(emp,size,max,i);

	return emp;
}
void merge(Employee *emp,int low,int high,int mid)
{
	int i=low,j=mid+1,k=0;
	Employee b[30];
	
	while(i<=mid && j<=high)
	{
		if(strcmp(emp[i].name,emp[j].name)<=0)
			b[k++]=emp[i++];
		else
			b[k++]=emp[j++];
	}

	while(i<=mid)
		b[k++]=emp[i++];

	while(j<=high)
		b[k++]=emp[j++];

	for(j=low,k=0;j<=high;j++,k++)
		emp[j]=b[k];
}
Employee* m_sort(Employee *emp,int low,int high)
{
	int mid=(low+high-1)/2;

	if(low<high)
	{
		m_sort(emp,low,mid);
		m_sort(emp,mid+1,high);
		merge(emp,low,high,mid);
	}
	return emp;
}
int partition(Employee *emp,int lb,int ub)
{
	int down=lb+1,up=ub;
	Employee pivot=emp[lb];

	do
	{
		while(strcmp(emp[down].name,pivot.name)<0 && down<=up)
			down++;

		while(strcmp(emp[up].name,pivot.name)>0 && up>=down)
			up--;

		if(down<up)
		{
		  Employee temp=emp[down];
		  emp[down]=emp[up];
		  emp[up]=temp;
		}
	}while(down<up);
	emp[lb]=emp[up];
	emp[up]=pivot;

	return up;
}

Employee* q_sort(Employee *emp,int lb,int ub)
{
	int j;
	
	if(lb<ub)
	{
		j=partition(emp,lb,ub);
		q_sort(emp,lb,j-1);
		q_sort(emp,j+1,ub);
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
			puts("1-COUNTING SORT");
			puts("2-MERGE SORT");
			puts("3-QUICK SORT");
			printf("\nEnter choice:");
			scanf("%d",&choice);
          puts("---------------------------order by name--------------------------");
			switch(choice)
			{
			  
			  case 1:
			  print_emp(r_sort(emp,size),size);
			  break;
			  
				case 2:
			  print_emp(m_sort(emp,0,size-1),size);
				break;
				
				case 3:
				print_emp(q_sort(emp,0,size-1),size);
			  break;
			  
				default:
				puts("Enter valid choice please");
				break;
			}
			writeFile(emp,size);
		}
		else
			printf("File not found");
	}
}





```
