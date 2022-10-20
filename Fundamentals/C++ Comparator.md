  
A Compare type providing a strict weak ordering.

Note that the Compare parameter is defined such that it returns true if its first argument comes _before_ its second argument in a weak ordering. But because the priority queue outputs largest elements first, the elements that "come before" are actually output last. That is, the front of the queue contains the "last" element according to the weak ordering imposed by Compare.

The return value of the function call operation applied to an object of a type satisfying Compare, when contextually converted to bool, yields true if the first argument of the call appears before the second in the _strict weak ordering relation_ induced by this type, and false otherwise.

Refer: https://en.cppreference.com/w/cpp/container/priority_queue
https://en.cppreference.com/w/cpp/named_req/Compare