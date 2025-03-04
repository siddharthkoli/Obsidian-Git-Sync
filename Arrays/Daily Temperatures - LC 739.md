Similar idea to that of [[Sliding Window Maximum - LC 239]]. Maintain a ***monotonic*** `deque`. 
The only difference is in the previous problem, we were looking for the entire max in the window.
Here, we're only looking for the next maximum.
So when were maintaining the monotonic property of the `deque`, i.e. removing smaller elements when a bigger ele