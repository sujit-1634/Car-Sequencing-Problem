# Car-Sequencing-Problem
Solving complex car sequencing problems using optimization techniques, linear and Integer Programming by coding in CPLEX,
MOD FILE :
range class=1..6;
range options =1..5;
int check[class][options]= ...;
int demand[class]= ...;
int x=sum(i in class) demand[i];
dvar boolean slots[1..x][class];
dvar boolean slotopt[1..x][options];
int ratio[options][1..2]=...;
subject to{
forall(i in 1..x) sum(j in class) slots[i][j]==1;
forall(c in class) sum(j in 1..x) slots[j][c]==demand[c];
forall(i in 1..x)forall(op in options) slotopt[i][op]==sum(c in class) slots[i]
[c]*check[c][op];

forall(opt in options)
forall(i in 1..x-ratio[opt][2]+1)
sum(j in i..i+ratio[opt][2]-1)
slotopt[j][opt]<=ratio[opt][1];
}

DAT FILE :

demand=[1,1,2,2,2,2];
check=[[1,0,1,1,0],
[0,0,0,1,0],
[0,1,0,0,1],
[0,1,0,1,0],
[1,0,1,0,0],
[1,1,0,0,0]];
ratio=[[1,2],[2,3],[1,3],[2,5],[1,5]];

OUTPUT :

slots = [ [1 0 0 0 0 0]
[0 0 1 0 0 0]
[0 0 0 0 0 1]
[0 1 0 0 0 0]
[0 0 0 0 0 1]
[0 0 0 1 0 0]
[0 0 0 0 1 0]
[0 0 1 0 0 0]

[0 0 0 1 0 0]
[0 0 0 0 1 0] ];
