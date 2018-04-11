#include <stdio.h>
#include <stdlib.h>
#include <iostream>

using namespace std;

void push(int arr[],int *f,int *r,int item)
{
   arr[*r]=item;
   *r=*r+1;			
}
int pop(int arr[],int *f,int *r)
{
	int item;
    item=arr[*f];
	*f=*f+1;
	return item;
}

main()
{
	int n,i,e;
	printf("Enter the total number of process you want to entered:-\n");
	scanf("%d",&n);
	int id[n],at[n],bt[n],w[n];
	
	for(i=0;i<n;i++)                                  //the complexity of these loop is n
	{
		printf("Enter the PROCESS ID:-  \n ");
		scanf("%d",&id[i]);
		printf("Enter the ARRIVAL TIME of given process=> %d\n ",id[i]);
		scanf("%d",&at[i]);
		printf("Enter the BURST TIME of process=> %d\n ",id[i]);
		scanf("%d",&bt[i]);
		e=e+bt[i];
	}
	int ind,min,k,j,m;
	
	for(i=0;i<n;i++)                                  //the complexity of these loop is n
	{
		m=at[i];
	    ind=i;
		for(int j=i+1;j<n;j++)                         //the complexity of these loop is n^2
		{
			if(at[j]<m)
			{
				ind=j;
				m=at[j];
			}	
		}
		min=at[i];
		at[i]=at[ind];
		at[ind]=min;
		min=id[i];
		id[i]=id[ind];
		id[ind]=min;
		min=bt[i];
		bt[i]=bt[ind];
		bt[ind]=min;
}
	
	int a[n],b[n],c[n];
	for(i=0;i<n;i++)                                      //the complexity of these loop is n
	{
       printf("    %d    \t     %d     \t     %d\n",id[i],at[i],bt[i]);
       a[i]=id[i];
       b[i]=at[i];
       c[i]=bt[i];
	}
	printf("[PROCESS ID]\t[ARRIVAL TIME]\t[BURST TIME]\n");
    for(i=0;i<n;i++)                                           //the complexity of these loop is n
	{                                                         //to display the result of the sorting 
       printf("    %d    \t     %d     \t     %d\n",id[i],at[i],bt[i]);	      //the complexity of the loop is n
    }
    int f=0,r=0,ar[e],t=0,t1,p,quantum=3;
    push(ar,&f,&r,0);	
 
while(f!=r)                                               //the complexity of these loop is e
{
  t1=t;
  p=pop(ar,&f,&r);

  if(bt[p]==quantum)
  {
	bt[p]=0;
	t=t+quantum;
	w[p]=t;
	printf("%d --> ",(p+1));
  }
  
  else if(bt[p]<quantum)
  {
	t=t+bt[p];
	bt[p]=0;
	w[p]=t;
   printf("%d -->  ",(p+1));
  }
 
  else
  {
	bt[p]=bt[p]-quantum;
	t=t+quantum;

	for(int j=0;j<n;j++)
	{
			if(j==p)
			{
				continue;
			}
		    if(at[j]>t1 && at[j]<=t)
			{
				push(ar,&f,&r,j);
			}
	}
	push(ar,&f,&r,p);
	w[p]=t;

	printf("%d --> ",(p+1));
	}

   if(p==3)
   {
		quantum=6;
   }
}
int tt[n],wt[n];
float avw=0.0,avt=0.0;

for(i=0;i<n;i++)                                       //the complexity of these loop is n
{
	tt[i]=w[i]-at[i];
	wt[i]=tt[i]-c[i];
	avw=avw+wt[i];
}
	
	printf("\n");
	printf("{PROCESS ID}\t{ARRIVAL TIME}\t{BURST TIME}\t{TURNAROUND TIME}\t{WAITING TIME}\n");
    for(i=0;i<n;i++)                                     //the complexity of these loop is n
	{                                                         //to display the result of the sorting 
      printf("    %d    \t     %d     \t    %d     \t      %d    \t           %d  \n",id[i],at[i],c[i],tt[i],wt[i]);	      //the complexity of the loop is n
      avt=avt+tt[i];
    }	

    printf("\n\n");
    printf("%f %f \n\n",avt,avw);
    printf("Average TURNAROUND TIME is -: %f\n",avt/n);
    printf("Average WAITING TIME is -: %f\n",avw/n);

}

	
	
