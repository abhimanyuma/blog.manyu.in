  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  layout: post
  title: If we use a Non-deterministic algorithm for the traveling salesman problem where
  people go on each route. Why are there 2\^n people in total
  ...
  permalink: http://217.manyu.in/index.php/if-we-use-a-np-algorithm-for-the-traveling-salesman-problem-where-people-go-on-each-route-why-are-there-2n-people-total-is-it-because-a/index.html
  ...
  post\_id: 48
  categories: ---
  - Uncategorized
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

*Cross posting a Quora answer I believe which could belong here.*

It is wrong to think that there are
<img class="math" src="http://qlx.cf.quoracdn.net/main-47118852b4069060.png" alt="2^n" width="19" height="15" />
routes, since in total there are
<img class="math" src="http://qlx.cf.quoracdn.net/main-6b146ee05160a5ab.png" alt="n!" width="16" height="14" />
routes. That is all permutations (assuming complete connectivity)
is possible.

On the other hand there is a 
<img class="math" src="http://qlx.cf.quoracdn.net/main-50bcc2b3abe47343.png" alt="O(n^2 2^n)" width="68" height="23" />
algorithm comes from a different way of looking at the solving the
problem. Instead of trying to enumeratre all routes, we make the
following observation that there are only
<img class="math" src="http://qlx.cf.quoracdn.net/main-47118852b4069060.png" alt="2^n" width="19" height="15" />
ways of selecting a subset from the complete set.

The algorithm used Dynamic Programming and this is how it saves
time, imagine two routes.

a b c d e f a b c d f e

The starting points are the same, and hence there is lot of
recomputation, which can be  brought down by dynamic programming

We will look at the algorithm as follows.
<ol>
    <li>
We shall first assume that the starting point is location(vertex)
<img class="math" src="http://qlx.cf.quoracdn.net/main-1555686c59de4f92.png" alt="s" width="8" height="9" />,
and we will be iterating and assigning each of the vertices as
starting location.
</li>
    <li>
Let
<img class="math" src="http://qlx.cf.quoracdn.net/main-7d006d0cc46acdc2.png" alt="B(S,s,k)" width="79" height="21" />
be the shortest path starting from
<img class="math" src="http://qlx.cf.quoracdn.net/main-1555686c59de4f92.png" alt="s" width="8" height="9" />
containing all elements in
<img class="math" src="http://qlx.cf.quoracdn.net/main-34ac93366809b6cb.png" alt="S" width="12" height="14" />
and ending at
<img class="math" src="http://qlx.cf.quoracdn.net/main-3f5c31a281e6d581.png" alt="k" width="9" height="14" />
</li>
    <li>
This is computed as follows
<img class="math" src="http://qlx.cf.quoracdn.net/main-67a50c477b5eef9a.png" alt="B(S,s,k)=min_{v \in S} B(S-\{v\},s,v)+d(v,k) " width="382" height="21" />
This gives us the TSP solution for a sub case of S locations with s
as starting point and k as ending.
</li>
    <li>
The above computation takes
<img class="math" src="http://qlx.cf.quoracdn.net/main-65077aa42d9ef5b7.png" alt="O(n)" width="42" height="21" />
time but requires no branching since the answer once chosen is
fixed.
</li>
    <li>
*Since this is based on total number of <img class="math" src="http://qlx.cf.quoracdn.net/main-34ac93366809b6cb.png" alt="S" width="12" height="14" /> possible it is upper bounded NOT by the number of routes but by number of power sets and that is why it is <img class="math" src="http://qlx.cf.quoracdn.net/main-47118852b4069060.png" alt="2^n" width="19" height="15" />*
</li>
</ol>
<span class="qlink_container"><a href="http://www.quora.com/Algorithms/If-we-use-a-np-algorithm-for-the-traveling-salesman-problem-where-people-go-on-each-route-Why-are-there-2-n-people-total-Is-it-because-a-person-is-either-traveling-a-route-or-not-traveling-a-route">If
we use a np algorithm for the traveling  salesman problem where
people go on each route. Why are there 2\^n people total? Is it
because a person is either traveling a route or not traveling a
route?</a></span>



