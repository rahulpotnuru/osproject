# osproject
#include<bits/stdc++.h>
#include<iostream>
using namespace std;
 
struct Process
{
    int pid;  
    int bt;
    int at;   
    int priority; 
}proc[10];
 

bool comparison(Process a, Process b)
{
    return (a.priority > b.priority);
}

int findWaitingTime(Process proc[], int n, int wt[])
{
    
    wt[0] = 0;
 
    for (int  i = 1; i < n ; i++ )
    {
    wt[i] =  proc[i-1].bt + wt[i-1] ;
    return wt[i];
    }
}
 
void findTurnAroundTime( Process proc[], int n,int wt[], int tat[])
{
 
    for (int  i = 0; i < n ; i++)
    tat[i] = proc[i].bt + wt[i];
}
 
void findavgTime(Process proc[], int n)
{
    int wt[n], tat[n], total_wt = 0, total_tat = 0;
 
    findWaitingTime(proc, n, wt);
 
    findTurnAroundTime(proc, n, wt, tat);
 
    cout << "\nProcesses  "<< " Burst time  "
         << " Waiting time  " << " Turn around time\n";
 
    for (int  i=0; i<n; i++)
    {
        total_wt = total_wt + wt[i];
        total_tat = total_tat + tat[i];
        cout << "   " << proc[i].pid << "\t\t"
             << proc[i].bt << "\t    " << wt[i]
             << "\t\t  " << tat[i] <<endl;
    }
 
    cout << "\nAverage waiting time = "
         << (float)total_wt / (float)n;
    cout << "\nAverage turn around time = "
         << (float)total_tat / (float)n;
}
 
void priorityScheduling(Process proc[], int n)
{
 
    sort(proc, proc + n, comparison);
 
    cout<< "Order in which processes gets executed \n";
    for (int  i = 0 ; i <  n; i++)
        cout << proc[i].pid <<" " ;
 
    findavgTime(proc, n);
}
int et[3];
int endtime(Process proc[],int n)
{
   
   for(int i = 0; i < n ; i++ )
   {
    et[i] = proc[i].at + proc[i].bt;
    return et[i];
   }
} 

int main()
{
   for (int i = 0 ; i < 3 ; i++)
   proc[i].priority = 1 + (wt[i]/et[i]);  
   Process proc[] = {{1,10,0,proc[0].priority}, {2, 5,2,proc[1].priority}, {3, 8,3,proc[2].priority}};
   int n = sizeof proc / sizeof proc[0];
   priorityScheduling(proc, n);
   return 0;
}
