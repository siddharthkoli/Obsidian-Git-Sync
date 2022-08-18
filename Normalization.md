It is the processes of reducing the redundancy of data in the table and also improving the data integrity. So why is this required? without Normalization in SQL, we may face many issues such as:

1.  _**Insertion anomaly**_: It occurs when we cannot insert data to the table without the presence of another attribute
2.  _**Update anomaly**_:  It is a data inconsistency that results from data redundancy and a partial update of data.
3.  _**Deletion Anomaly**_: It occurs when certain attributes are lost because of the deletion of other attributes.

### **1st Normal Form (1NF)**

In this Normal Form, we tackle the problem of atomicity. Here atomicity means values in the table should not be further divided. In simple terms, a single cell cannot hold multiple values. If a table contains a composite or multi-valued attribute, it violates the First Normal Form.  

![1NF_table - Normalization in SQL -Edureka](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2019/10/tab_1NF_img1-300x119.png)

In the above table, we can clearly see that the `Phone Number` column has two values. Thus it violated the 1st NF. Now if we apply the 1st NF to the above table we get the below table as the result.

![1NF_table_example - Normalization in SQL -Edureka](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2019/10/tab_1NF_img2-300x124.png)

By this, we have achieved atomicity and also each and every column have unique values.
<hr/>

### **2nd Normal Form** **(2NF)**

The first condition in the 2nd NF is that the table has to be in 1st NF. The table also should not contain partial dependency. Here partial dependency means the proper subset of candidate key determines a non-prime attribute. To understand in a better way lets look at the below example.

Consider the table 

![2nf - normalization in sql - Edureka](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2019/10/tab_2NF_img1-1-300x120.png)

This table has a composite primary key `Emplyoee ID, Department ID`. The non-key attribute is **`Office Location`**. In this case, **`Office Location`** only depends on **`Department ID`**, which is only part of the primary key. Therefore, this table does not satisfy the second Normal Form.

To bring this table to Second Normal Form, we need to break the table into two parts. Which will give us the below tables:

![2nf_tab1 - normalization in sql - edureka](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2019/10/tab_2NF_example1-300x229.png)![2nf_tab2 - normalization in sql - edureka](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2019/10/tab_2NF_example2-300x180.png)

 

As you can see we have removed the partial functional dependency that we initially had. Now, in the table, the column **`Office Location`** is fully dependent on the primary key of that table, which is **`Department ID`**.
<hr/>

### **3rd Normal Form** **(3NF)**

The same rule applies as before i.e, the table has to be in 2NF before proceeding to 3NF. The other condition is there should be no transitive dependency for non-prime attributes. That means non-prime attributes (which doesn’t form a candidate key) should not be dependent on other non-prime attributes in a given table. So a transitive dependency is a functional dependency in which X → Z (X determines Z) indirectly, by virtue of X → Y and Y → Z (where it is not the case that Y → X)

Let’s understand this more clearly with the help of an example:

![3nf - normalization in sql - edureka](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2019/10/tab_3NF_img1-300x117.png)

In the above table, **`Student ID`** determines **`Subject ID`**, and **`Subject ID`** determines **`Subject`**. Therefore, **`Student ID`** determines **`Subject`** via **`Subject ID`.** This implies that we have a transitive functional dependency, and this structure does not satisfy the third normal form.

Now in order to achieve third normal form, we need to divide the table as shown below:

![3nf_tab1 - normalization in sql - edureka](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2019/10/tab_3NF_example1-300x101.png) ![3nf_tab2 - normalization in sql - edureka](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2019/10/tab_3NF_example2-300x142.png)

### 

As you can see from the above tables all the non-key attributes are now fully functional dependent only on the primary key. In the first table, columns **`Student Name`, `Subject ID`** and `**Address**` are only dependent on **`Student ID`**. In the second table, **`Subject`** is only dependent on **`Subject ID`**.