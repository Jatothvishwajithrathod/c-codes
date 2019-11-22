#include <stdio.h>
long angryAnimals(int n,vector<int> a, vector<int> b){

vector<priority_queue<int> > e(n+1);

for(int i=0;i<a.size();i++){

// We will only push smaller element as we will be checking from left to right

if(a[i]<=n && b[i]<=n)

if(a[i]<b[i]){

e[b[i]].push(a[i]);

}else{

e[a[i]].push(b[i]);

}

}

long count = 0;

queue<int> q;

for(int i=1;i<=n;i++){

if(e[i].empty()){

count++;

q.push(i);

}else{

while(!q.empty()&& !e[i].empty() && q.front()<=e[i].top() && q.back() >=e[i].top()){

if(q.front() >= e[i].top()){

e[i].pop();

}

q.pop();

count+=q.size();

}

q.push(i);

count++;

}

}

int size = q.size();

//number of ways for remaining elements

count+= size*(size-1)/2;

return count;

}
