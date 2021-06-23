#include<stdio.h> 
void main() 
{ 
int p,r,i,tp; 
printf("\nEnter no. of processes: "); 
scanf("%d",&p); 
tp=p; 
printf("\nEnter no. of resources: "); 
scanf("%d",&r); 
int maxi[r]; 
printf("\nEnter the maximum resources for each instances: \n"); 
for(i=0;i<r;i++) 
{ 
printf("%c: ",i+97); scanf("%d",&maxi[i]); 
} 
int alloc[p][r],max[p][r],avail[r],need[p][r]; 
int P[p],j; 
printf("\nEnter the allocation matrix:"); 
for(i=0;i<r;i++) 
printf("%c",(i+97)); 
printf("\n"); 
for(i=0;i<p;i++) 
{ 
P[i]=i; 
printf("P[%d]: ",P[i]); 
for(j=0;j<r;j++) 
{ 
scanf("%d",&alloc[i][j]); 
} 
} 
printf("\nEnter the maximum matrix:"); 
for(i=0;i<r;i++) 
printf(" %c",i+97); 
printf("\n"); 
for(i=0;i<p;i++) 
{ 
P[i]=i; 
printf("P[%d]: ",P[i]); 
for(j=0;j<r;j++) 
{ 
scanf("%d",&max[i][j]); 
} 
printf("\n"); 
} 
printf("\nEnter the available resouce:\n"); 
for(i=0;i<r;i++) 
printf(" %c",i+97); 
printf("\n"); 
for(j=0;j<r;j++) 
scanf("%d",&avail[j]); 
printf("Calculating the NEED matrix..."); 
printf("\n\n"); 
for(i=0;i<r;i++) 
printf(" %c",i+97); 
printf("\n"); 
for(i=0;i<tp;i++) 
{ 
P[i]=i; printf("P[%d] ",P[i]); 
for(j=0;j<r;j++) 
{ 
need[i][j]=max[i][j]-alloc[i][j]; 
printf("%d",need[i][j]); 
} 
printf("\n"); 
} 
int count=0,flag=0,safe[tp],k=0,t,finish[tp]; 
for(i=0;i<tp;i++) 
{ 
finish[i]=0; 
} 
int stack[p][r],maxstack[p][r],Ps[p],dup=0; 
for(i=0;i<tp;i++) 
{ 
for(j=0;j<r;j++) 
{ 
if(need[i][j]>avail[j]) 
break; 
} 
if(j!=3) 
{ 
for(k=0;k<r;k++) 
{ 
stack[dup][k]=need[i][k]; 
maxstack[dup][k]=max[i][k]; 
} 
Ps[dup]=i; 
dup++; 
} 
else 
{ 
safe[count++]=i; 
printf("\n"); 
printf("P[%d] is executed successfully!!!",i); 
printf("\n"); 
if(j==3){ 
for(k=0;k<r;k++){ 
avail[k]=avail[k]-need[i][k]; 
avail[k]=avail[k]+max[i][k]; 
} 
} 
} 
}int add[dup],diff[dup]; 
for(i=0;i<dup;i++) 
{ 
add[i]=0; 
for(j=0;j<r;j++) 
{ 
diff[i]=maxi[j]-stack[i][j]; 
add[i]=add[i]+diff[i]; 
} 
} 
int temp=add[0],swap; 
for(i=0;i<dup;i++) 
for(j=i+1;j<dup;j++) 
{ 
if(add[i]<add[j]) 
{ 
temp=j; 
} 
for(k=0;k<r;k++) 
{ 
swap=stack[i][k]; 
stack[i][k]=stack[temp][k]; 
stack[temp][k]=swap; 
swap=maxstack[i][k]; 
maxstack[i][k]=maxstack[temp][k]; 
maxstack[i][k]=swap; 
} 
temp=Ps[i]; 
Ps[i]=Ps[j]; 
Ps[j]=temp; 
} 
for(i=0;i<dup;i++) 
{ 
for(k=0;k<r;k++){ 
avail[k]=avail[k]-stack[i][k]; 
avail[k]=avail[k]+maxstack[i][k]; 
} 
printf("\nP[%d] is executed successfully!!!",Ps[i]); 
}
}
