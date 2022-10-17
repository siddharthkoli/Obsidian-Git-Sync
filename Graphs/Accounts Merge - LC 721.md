The first step is to find which accounts have an email in common and merge them to form a larger connected component. Any problem that involves merging connected components (accounts) is a natural fit for the Disjoint Set Union (DSU) data structure. Since most implementations of DSU use an array to record the root (representative) of each component, we will use integers to represent each component for ease of operability. Therefore, we will give each account a unique ID, and we will map all the emails in the account to the account's ID. We will use a map, `emailGroup`, to store this information.

We chose the account index to be the identifier for all the emails of an account. We will assign the account index as the group when we get the email for the first time and when we get an email that we have already traversed, we will merge the current account and the group that we have previously stored in `emailGroup` using union operation.

After traversing over all the accounts, we will find the representative of all the emails which will inform us about their group. Emails with the same representative belong to the same person/group and hence will be stored together. Also, we can retrieve the account name for our final answer using `accountList` as we have `group` which is the index in the original accounts list.
![[Pasted image 20221017162421.png]]
![[Pasted image 20221017162429.png]]
![[Pasted image 20221017162433.png]]
![[Pasted image 20221017162437.png]]
![[Pasted image 20221017162440.png]]
![[Pasted image 20221017162445.png]]
![[Pasted image 20221017162450.png]]
![[Pasted image 20221017162454.png]]
![[Pasted image 20221017162500.png]]
![[Pasted image 20221017162504.png]]
![[Pasted image 20221017162508.png]]
