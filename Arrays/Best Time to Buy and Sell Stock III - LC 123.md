Total allowed transactions is 2
1.  There should be **at most** two transactions, it means possibilities are 0,1,2
2.  You cannot buy 2 stocks at same time, you have to sell one stock before buying a new.
![[Pasted image 20220910235246.png]]
The reason for 5 states is that ther
The state equation for each node:  
**x\[i]=x\[i-1];  
y\[i]=max(x\[i-1]-prices\[i], y\[i-1]);  
z\[i]=max(y\[i-1]+prices\[i],z\[i-1]);  
a\[i]=max(a\[i-1],z\[i-1]-prices\[i]);  
b\[i]=max(a\[i-1]+prices\[i],b\[i-1]);**
