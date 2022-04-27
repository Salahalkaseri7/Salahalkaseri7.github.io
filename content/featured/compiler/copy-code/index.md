---
date: '3'
title: 'RANDOM COMPILER'
cover: 'codehs.png'
github: 'https://github.com/Salahalkaseri7/Salahalkaseri7.github.io/tree/gh-pages'
external: 'https://salahalkaseri7.github.io'
tech:
  - c/c++
  - js
  - java
  - Python
showInProjects: true
---
# OS Scheduling Algorithms
---
---
> C program on FCFS(First come first serve) 
```C
#include<stdio.h>
int main()
{
    int AT[10],BT[10],WT[10],TT[10],n;
    int burst=0,cmpl_T;
    float Avg_WT,Avg_TT,Total=0;
    printf("Enter number of the process\n");
    scanf("%d",&n);
    printf("Enter Arrival time and Burst time of the process\n");
    printf("AT\tBT\n");
    for(int i=0;i<n;i++)
    {
        scanf("%d%d",&AT[i],&BT[i]);
    }
    for(int i=0;i<n;i++)
    {
        if(i==0)
            WT[i]=AT[i];
        else
            WT[i]=burst-AT[i];
        burst+=BT[i];
        Total+=WT[i];
    }
    Avg_WT=Total/n;
    cmpl_T=0;
    Total=0;
    for(int i=0;i<n;i++)
    {
        cmpl_T+=BT[i];
        TT[i]=cmpl_T-AT[i];
        Total+=TT[i];
    }
    Avg_TT=Total/n;
    printf("Process ,Waiting_time ,TurnA_time\n");
    for(int i=0;i<n;i++)
    {
        printf("%d\t\t%d\t\t%d\n",i+1,WT[i],TT[i]);
    }
    printf("Average waiting time is : %f\n",Avg_WT);
    printf("Average turn around time is : %f\n",Avg_TT);
    return 0;
} 
```
> Shortest Job First Program in C (Non-preemptive)

```C
#include<stdio.h>
 int main()
{
    int bt[20],p[20],wt[20],tat[20],i,j,n,total=0,pos,temp;
    float avg_wt,avg_tat;
    printf("Enter number of process:");
    scanf("%d",&n);
    printf("\nEnter Burst Time:\n");
    for(i=0;i<n;i++)
    {
        printf("p%d:",i+1);
        scanf("%d",&bt[i]);
        p[i]=i+1;         
    }
    for(i=0;i<n;i++)
    {
        pos=i;
        for(j=i+1;j<n;j++)
        {
            if(bt[j]<bt[pos])
                pos=j;
        }
        temp=bt[i];
        bt[i]=bt[pos];
        bt[pos]=temp;
        temp=p[i];
        p[i]=p[pos];
        p[pos]=temp;
    }
    wt[0]=0;            
    for(i=1;i<n;i++)
    {
        wt[i]=0;
        for(j=0;j<i;j++)
            wt[i]+=bt[j];
        total+=wt[i];
    }
    avg_wt=(float)total/n;      
    total=0;
    printf("\nProcess\t    Burst Time    \tWaiting Time\tTurnaround Time");
    for(i=0;i<n;i++)
    {
        tat[i]=bt[i]+wt[i];   
        total+=tat[i];
        printf("\np%d\t\t  %d\t\t    %d\t\t\t%d",p[i],bt[i],wt[i],tat[i]);
    }
    avg_tat=(float)total/n;    
    printf("\n\nAverage Waiting Time=%f",avg_wt);
    printf("\nAverage Turnaround Time=%f\n",avg_tat);
}
```
>Shortest Job First Program in C (Preemptive)

```C
#include <stdio.h>
int main() 
{
      int arrival_time[10], burst_time[10], temp[10];
      int i, smallest, count = 0, time, limit;
      double wait_time = 0, turnaround_time = 0, end;
      float average_waiting_time, average_turnaround_time;
      printf("\nEnter the Total Number of Processes:\t");
      scanf("%d", &limit); 
      printf("\nEnter Details of %d Processes", limit);
      for(i = 0; i < limit; i++)
      {
            printf("\nEnter Arrival Time:\t");
            scanf("%d", &arrival_time[i]);
            printf("Enter Burst Time:\t");
            scanf("%d", &burst_time[i]); 
            temp[i] = burst_time[i];
      }
      burst_time[9] = 9999;  
      for(time = 0; count != limit; time++)
      {
            smallest = 9;
            for(i = 0; i < limit; i++)
            {
                  if(arrival_time[i] <= time && burst_time[i] < burst_time[smallest] && burst_time[i] > 0)
                  {
                        smallest = i;
                  }
            }
            burst_time[smallest]--;
            if(burst_time[smallest] == 0)
            {
                  count++;
                  end = time + 1;
                  wait_time = wait_time + end - arrival_time[smallest] - temp[smallest];
                  turnaround_time = turnaround_time + end - arrival_time[smallest];
            }
      }
      average_waiting_time = wait_time / limit; 
      average_turnaround_time = turnaround_time / limit;
      printf("\n\nAverage Waiting Time:\t%lf\n", average_waiting_time);
      printf("Average Turnaround Time:\t%lf\n", average_turnaround_time);
      return 0;
}

```
>C program of the priority scheduling (Preemptive)

```C
#include<stdio.h>
struct process
{
    int WT,AT,BT,TAT,PT;
};

struct process a[10];

int main()
{
    int n,temp[10],t,count=0,short_p;
    float total_WT=0,total_TAT=0,Avg_WT,Avg_TAT;
    printf("Enter the number of the process\n");
    scanf("%d",&n);
    printf("Enter the arrival time , burst time and priority of the process\n");
    printf("AT BT PT\n");
    for(int i=0;i<n;i++)
    {
        scanf("%d%d%d",&a[i].AT,&a[i].BT,&a[i].PT);
        temp[i]=a[i].BT;
    }
    a[9].PT=10000;
    
    for(t=0;count!=n;t++)
    {
        short_p=9;
        for(int i=0;i<n;i++)
        {
            if(a[short_p].PT>a[i].PT && a[i].AT<=t && a[i].BT>0)
            {
                short_p=i;
            }
        }
        
        a[short_p].BT=a[short_p].BT-1;
        if(a[short_p].BT==0)
        {
            count++;
            a[short_p].WT=t+1-a[short_p].AT-temp[short_p];
            a[short_p].TAT=t+1-a[short_p].AT;
            total_WT=total_WT+a[short_p].WT;
            total_TAT=total_TAT+a[short_p].TAT;
        }
    }
    Avg_WT=total_WT/n;
    Avg_TAT=total_TAT/n;
    printf("ID WT TAT\n");
    for(int i=0;i<n;i++)
    {
        printf("%d %d\t%d\n",i+1,a[i].WT,a[i].TAT);
    }
    
    printf("Avg waiting time of the process  is %f\n",Avg_WT);
    printf("Avg turn around time of the process is %f\n",Avg_TAT);
    
    return 0;
}


```
>C program on the priority scheduling algorithm (Non preemptive)

```C
#include<stdio.h>
struct process
{
    int id,WT,AT,BT,TAT,PR;
};
struct process a[10];
void swap(int *b,int *c)
{
    int tem;
    tem=*c;
    *c=*b;
    *b=tem;
}
int main()
{
    int n,check_ar=0;
    int Cmp_time=0;
    float Total_WT=0,Total_TAT=0,Avg_WT,Avg_TAT;
    printf("Enter the number of process \n");
    scanf("%d",&n);
    printf("Enter the Arrival time , Burst time and priority of the process\n");
    printf("AT BT PR\n");
    for(int i=0;i<n;i++)
    {
        scanf("%d%d%d",&a[i].AT,&a[i].BT,&a[i].PR);
        a[i].id=i+1;
        if(i==0)
         check_ar=a[i].AT;
         
        if(check_ar!=a[i].AT )
         check_ar=1;
        
    }
    if(check_ar!=0)
    {
        for(int i=0;i<n;i++)
        {
            for(int j=0;j<n-i-1;j++)
            {
                if(a[j].AT>a[j+1].AT)
                {
                      swap(&a[j].id,&a[j+1].id);
                      swap(&a[j].AT,&a[j+1].AT);
                      swap(&a[j].BT,&a[j+1].BT);
                      swap(&a[j].PR,&a[j+1].PR);
                }
            }
        }
    }
    if(check_ar!=0)
    {
        a[0].WT=a[0].AT;
        a[0].TAT=a[0].BT-a[0].AT;
        Cmp_time=a[0].TAT;
        Total_WT=Total_WT+a[0].WT;
        Total_TAT=Total_TAT+a[0].TAT;
        for(int i=1;i<n;i++)
        {
            int min=a[i].PR;
            for(int j=i+1;j<n;j++)
            {
                if(min>a[j].PR && a[j].AT<=Cmp_time)
                {
                      min=a[j].PR;
                      swap(&a[i].id,&a[j].id);
                      swap(&a[i].AT,&a[j].AT);
                      swap(&a[i].BT,&a[j].BT);
                      swap(&a[i].PR,&a[j].PR);
                      
                }
                
            }
            a[i].WT=Cmp_time-a[i].AT;
            Total_WT=Total_WT+a[i].WT;
            Cmp_time=Cmp_time+a[i].BT;
            a[i].TAT=Cmp_time-a[i].AT;
            Total_TAT=Total_TAT+a[i].TAT;
            
        }
    }
    else
    {
        for(int i=0;i<n;i++)
        {
            int min=a[i].PR;
            for(int j=i+1;j<n;j++)
            {
                if(min>a[j].PR && a[j].AT<=Cmp_time)
                {
                    min=a[j].PR;
                      swap(&a[i].id,&a[j].id);
                      swap(&a[i].AT,&a[j].AT);
                      swap(&a[i].BT,&a[j].BT);
                       swap(&a[i].PR,&a[j].PR);
                }
                
            }
            a[i].WT=Cmp_time-a[i].AT;
            Cmp_time=Cmp_time+a[i].BT;
            a[i].TAT=Cmp_time-a[i].AT;
            Total_WT=Total_WT+a[i].WT;
            Total_TAT=Total_TAT+a[i].TAT;
            
        }
        
    }
    
    Avg_WT=Total_WT/n;
    Avg_TAT=Total_TAT/n;
    printf("The process are\n");
    printf("P.NO \t WT\t TAT\n");
    for(int i=0;i<n;i++)
    {
        printf("%d\t%d\t%d\n",a[i].id,a[i].WT,a[i].TAT);
    }
    
    printf("Avg waiting time is: %f\n",Avg_WT);
    printf("Avg turn around time is: %f",Avg_TAT);
    return 0;
}
```
>Round Robin Scheduling Program in C

```C
#include<stdio.h>
 
int main()
{
 
  int count,j,n,time,remain,flag=0,time_quantum;
  int wait_time=0,turnaround_time=0,at[10],bt[10],rt[10];
  printf("Enter Total Process:\t ");
  scanf("%d",&n);
  remain=n;
  for(count=0;count<n;count++)
  {
    printf("Enter Arrival Time and Burst Time for Process Process Number %d :",count+1);
    scanf("%d",&at[count]);
    scanf("%d",&bt[count]);
    rt[count]=bt[count];
  }
  printf("Enter Time Quantum:\t");
  scanf("%d",&time_quantum);
  printf("\n\nProcess\t|Turnaround Time|Waiting Time\n\n");
  for(time=0,count=0;remain!=0;)
  {
    if(rt[count]<=time_quantum && rt[count]>0)
    {
      time+=rt[count];
      rt[count]=0;
      flag=1;
    }
    else if(rt[count]>0)
    {
      rt[count]-=time_quantum;
      time+=time_quantum;
    }
    if(rt[count]==0 && flag==1)
    {
      remain--;
      printf("P[%d]\t|\t%d\t|\t%d\n",count+1,time-at[count],time-at[count]-bt[count]);
      wait_time+=time-at[count]-bt[count];
      turnaround_time+=time-at[count];
      flag=0;
    }
    if(count==n-1)
      count=0;
    else if(at[count+1]<=time)
      count++;
    else
      count=0;
  }
  printf("\nAverage Waiting Time= %f\n",wait_time*1.0/n);
  printf("Avg Turnaround Time = %f",turnaround_time*1.0/n);
  
  return 0;
}
```