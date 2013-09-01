  ---------------------------------------------------------------------------------------------------------------
  layout: post
  title: Using Matrix Exponentiation to solve Recurrence Relations
  ...
  permalink: http://217.manyu.in/index.php/using-matrix-exponentiation-to-solve-recurrence-relations/index.html
  ...
  post\_id: 24
  categories: ---
  - Uncategorized
  ---------------------------------------------------------------------------------------------------------------

In this blog post I am attempting to show you how to solve
recurrence relations fast *for algorithmic contests.*

Imagine you have a equation of the form [latex] f*n=f*{n-1}
+f\_{n-2}[/latex]

Well if I give you $latex f_0=1$  $latex f_1=1$ then you would
recognize it as the
<a title="Fibonacci Sequence (Wikipedia)" href="http://en.wikipedia.org/wiki/Fibonacci_Sequence" target="_blank">fibonacci
sequence</a>.

If you want to list out each element of the sequence one by one you
would compute each element after another, but imagine if you were
asked for the 1,234,567,890th Fibonacci element, well you would be
in bit of trouble.

Usually algorithmic contest people understand the numbers can be
large and hence don't ask for the exact number but only the
remainder when the number is divided by a relatively small(usually
of the order of $latex 10^9 - 10^7$)number.

This would mean that you have to actually do everything required
for computing the number, but stay within the limits of INT or LONG
LONG INT. This is helped by the following modulo (remainder
operation) identities.

$latex A mod C = ( A mod C ) mod C$ - This one is obvious
$latex (A + C) mod C = A mod C$ This helps wrapping around and can
mean larger numbers can give smaller modulo values
$latex (A+B) mod C = ( A mod C + B mod C) mod C$

$latex AB mod C = ((A mod C)(B mod C))mod C$

So in short your formula becomes something like
$latex F_n = (F_{n-1} + F_{n-2}) mod M$ where M is the relatively
small number. bq. Easy error warning : The numbers
$latex A mod C + B mod C$ will initially be larger than C, and
might not fit within INT. If you have multiplication you would have
to use LONG LONG INT when C is INT. So coming back to our original
problem. The solution could be as simple as the following loop
<pre>int a=1,b=1;
int n=1234567890;
int m=1000000007;
for (int i=3;i<=n;i++)
{
     a=(a+b) mod m;  // Fn  = Fn-1 + Fn-2
     b=(a-b) mod m;  // Fn-1= Fn   - Fn-2
}</pre>
This suffers from the above problem it will take about few minutes
before you get an answer, that is this is of order $latex O(n)$ so
I will talk a bit of mathematics, as you may have noticed, the
equation is linear.Consider a simple matrix

$latex [F_n,F_{n-1}]$

Just transposing we get
<pre>[ Fn  Fn-1 ] =  [ Fn-1 Fn-2 ] [ 1 1 ] 
                              [ 1 0 ]</pre>
So basically if we have a matrix of [1 1] to start with, and we
multiply it with the matrix associated with our equation our we get
the next elements. bq. Mathematically this is called  2-dimensional
system of linear difference equations that describes the Fibonacci
sequence [Wikipedia] So now if we multiply it again we get the next
two terms it is important to preserve one term from the previous
since it is required for the next level. So if we go on we can see
<pre>[ Fn+1 Fn ] = [ 1 1 ]  [ 1 1 ] [ 1 1 ] ... [1 1]
                       [ 1 0 ] [ 1 0 ] ... [1 0 ] n times

[ Fn+1 Fn ] = [ 1 1 ]  [ 1 1 ] ^ n
                       [ 1 0 ]</pre>
Right now you would be wondering whether this gives you any
advantage, so before we go into that we will go into h3. Fast
Exponentiation

Suppose you want to find $latex 2\^{123} $. You could do it in 123
steps by multiplying each time, or else to suggest a faster method
you could do $latex 2 . 2\^2 . 2\^8. 2\^{16} . 2\^{32} . 2\^{64} $

But then again you would ask me how I obtain each of these without
multiplying completely the answer is simple

$latex 2\^{2n} = 2\^n . s\^n ==\> 2\^{16} = 2^8.2^8 $

This is called
<a href="http://en.wikipedia.org/wiki/Exponentiation_by_squaring" target="_blank">Exponentiation
by squaring</a>. As you can see to get $latex a^x$ it takes only
$latex log x$ steps. If you would see it is also applicable to
matrices. Since the only property required for this is
associativity which is satisfied.

So in short we have the following algorithm

To find the nth fibonacci number break it down into powers of 2,
and for each multiply it with the corresponding matrix obtained by
fast exponentitation
<pre>Result = [ 1 1 ] //Base Case;
PowMat = [ 1 1 ]
         [ 1 0 ]
N // Number we want to find
while (N>0) :
    if 2 doesn't divide N :
        Result = Result * PowMat
    N=N/2;
    PowMat = PowMat * PowMat

Here we assume that multiplication is modular.</pre>
This would give you the $latex n^{th}$ fibonacci number in about
$latex log$ $latex n$ time. which is really fast. Now generalizing
it. h3. Fast method for General Recursive solution

Imagine that now our equation is

$latex G_n = a.G_{n-1} + b. G_{n-2}$

Again solving this is not that hard, a careful analysis will say
that what we want is
<pre>[ Gn Gn-1 ] = [ Gn-1 Gn-2 ] [ Some Matrix ]</pre>
Replacing $latex G_n$ by $latex a.G_{n-1} + b. G_{n-2}$ we get
<pre>[ Gn Gn-1 ] = [ Gn-1 Gn-2 ] [ a 1 ]
                            [ b 0 ]</pre>
So all you need to do is replace the matrix is the above equation.
h3. Some more different cases and the matrices

h4. Deeper Recursion

Imagine your solution now is

$latex G_n = a.G_{n-1} + b. G_{n-2} + c.G_{n-3} + d.G_{n-4}$

The solution just changes to
<pre>[ Gn Gn-1 Gn-2 Gn-3 ] = [ Gn-1 Gn-2 Gn-3 Gn-4 ] [ a 1 0 0 ]
                                                [ b 0 1 0 ]
                                                [ c 0 0 1 ]
                                                [ d 0 0 0 ]</pre>
 

A point to note here would be we would need the first four terms
hand coded, and also that from here and beyond this the matrix
multiplication complexity is also to be taken into consideration.

  h4. Multiple Equations

Consider you have a pair of equation like this.

$latex G_n = a.F_{n-1} + b. G_{n-2}$

$latex F_n = c.G_{n-1} + d. F_{n-2}$

Again if we think what we need is
<pre>[ Gn Fn Gn-1 Fn-1]  = [ Gn-1 Fn-1 Gn-2 Fn-2]  [Some Matrix]
[ Gn Fn Gn-1 Fn-1]  = [ Gn-1 Fn-1 Gn-2 Fn-2]  [ 0 c 1 0 ]
                                              [ a 0 0 1 ]
                                              [ 0 d 0 0 ]
                                              [ b 0 0 0 ]</pre>
Now you may think what if $latex G_n$ is dependent on $latex F_n$
(or the other way round, but never both since then recursion would
be cyclic) as well, then our equation won't work, but the solution
is as simple as replacing $latex F_n$ by it's equation and removing
$latex F_n$. h4. Odd and Even

Consider an equation like

$latex G_2n = a.G_{2n-1} + b. G_{2n-3}$

$latex G_2n-1 = c.G_{2n-2} + d. G_{2n-3}$

This is nothing but a different way of writing the equation in the
case above (with the small modification)

 

*[Here ends the tutorial Please leave feedback]*



