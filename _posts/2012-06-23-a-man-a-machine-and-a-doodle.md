  ----------------------------------------------------------------------------------
  layout: post
  title: A Man, A Machine and A Doodle
  ...
  permalink: http://217.manyu.in/index.php/a-man-a-machine-and-a-doodle/index.html
  ...
  post\_id: 7
  categories: ---
  - Uncategorized
  ----------------------------------------------------------------------------------

 

None of you would have missed the "Google Doodle" today, it
celebrates the 100th birthday of
<a title="Alan Turing Wikipedia" href="http://en.wikipedia.org/wiki/Alan_Turing" target="_blank">Alan
Turing</a> one of the greatest minds ever in the field of
Mathematics, Computer Science and strangely Biology.

<a href="http://217.manyu.in/wp-content/uploads/2012/06/Screenshot-from-2012-06-23-180122.png"><img class="wp-image-8 alignleft" title="The Google Doodle" src="http://217.manyu.in/wp-content/uploads/2012/06/Screenshot-from-2012-06-23-180122-300x184.png" alt="Google Doodle" width="300" height="184" /></a>The
doodle celebrates on of Turing's most important contribution to
Mathematics and Computing - The turing machine.

This blog tries to explain "Turing Machine" to you, and most likely
will fail at it, but still let me try.

The first thing about Turing Machines is that it is NOT actually a
machine. It is a model, a model of a simple machine.

See, as computing scientists , being the loners they are , like
asking philosophical questions about computing machines, about what
machines can do, what machines can't do. Such questions just like
almost all philosophical questions are
<ol>
    <li>
Simple to ask
</li>
    <li>
Simple to understand
</li>
    <li>
Bloody hard to to actually answer.
</li>
</ol>
The turing machine as I told is a mathematical model, it has an
important property. bq. Think of any program (C,C++,Java,Physically
changing the inputs to a processor) that you can write for your
computer, you can write a program for Turing machine which would do
the EXACT same thing. Well actually not the exact same thing but
almost same thing, For e.g : A turing maching even if you build it
cannot play Crysis.

The only way a you can interact with the turing machine is through
is through a tape, the tape is like the one you see on the Google
Doodle,basically whatever is on it when the turing machine starts
is the "Input" whatever is on it when the turing machine stops is
"Output". On top of it, the turing maching also "says" whether you
input is accepted or not.Computer theoreticians don't actually
bother with what is finally on the tape, all they need to know is
whether the input is accepted or not (Weird I know but then again
or else they won't be hardcore)

The only thing missing is how do you program it, as you may know a
program is nothing but a set of rules,  And we will see how Turing
machine does that.

Look at that picture, see the circles, those are what are called
states and that is the program in itself, On each state the
following is done
<ol>
    <li>
A symbol is read of the tape, it can be either (Blank, 0 or 1)
</li>
    <li>
Based on it, the tape head moves to the left or to the right.
</li>
    <li>
The head can also write a symbol on the tape.
</li>
</ol>
For e.g a rule may read the following

*State 1 :*If you read a 0 move left, after writing 1, and move to
*State 2.*If you read 1 , move right after erasing what is written
and move to State 2, If there is nothing on the tape stay there but
move to *State 3.*

Remember me telling about few inputs getting accepted or not , how
that happens is few States are identified Good, and few bad, now
when the program stops depending on which state you end up with,
the input is accepted or not (Think of it like playing the nursery
game of "Bombing the city")

People who have done something to do with computers, can see that
this is instructing the computers to do some action, and this is
called programs.

That is it, the idea of turing machine is encompassed in as simple
as that. For all those with mathematical interests, let me explain
it a bit more mathematically.

Imagine you a string S of infinite length, each of the characters
in the string can be *1* , *0*, or [] (Empty). You start with a
string, and a set of rules and also which character you are looking
at , which initially is the first character *0*. Let us call this
the index *i. * So initially it is looking at S0  and among the
rules you will be looking at a specific one let me call it the Rule
Counter *C*. If R is the set of rules *R0 *will be the first rule
looked at. Now each step is a function which will do the following
\*\*
<pre>Rule_c(i=x)     { 
Si = 0,   i=i+1 , c=p   if Si = [] 
Si = 1,   i=i   , c=q   if Si = 0 
Si = [] , i=i+1 , c=r   if Si = 1 }</pre>
And as said there is a set *Good* of good states, which if is the
final state, your input is said to be accepted, or else it is
rejected.

<span style="text-decoration: underline;">*Solving the Google Doodle*</span>

Our dear Google has split it into multiple states, but essentially
they encompass the same idea.
<ol>
    <li>
Whenever Google says '0' '1' or '[]' they mean they will write that
symbol on the tape.
</li>
    <li>
Whenever Google gives an arrow, they say they will move the tape
(or the tape head depending on relativity)
</li>
    <li>
Whenever you see something like a number and an arrow it says it
reads the symbol and if the symbol matches it will move to a state
shown below or else to the state pointed by the arrow.
</li>
    <li>
The rotation thing is not there in Turing machine, it is just
Google's way of editing the rules. basically determining which
state to move to.
</li>
</ol>
So if you take the first doodle, what it says is

[caption id="attachment\_13" align="aligncenter"
width="300"]<a href="http://217.manyu.in/wp-content/uploads/2012/06/google.png"><img class="size-medium wp-image-13" title="Google Doodle Level 1" src="http://217.manyu.in/wp-content/uploads/2012/06/google-300x187.png" alt="Google Doodle Level 1" width="300" height="187" /></a>
Google Doodle Level 1[/caption]

1.  Move Left 2.Write symbol on the second state (first button) 3.
    Move Right thrice 4. Write symbol on last state (Second button)

Google for some reason doesn't allow you write [] (meaning erase
the tape memory). So solving it also becomes easy. You can see that
once you move left, you have to write a 1, to match the expected
output, the same can be said for the last Write operation, hence it
is easily solved.

The second doodle has the following rules

 

[caption id="attachment\_15" align="aligncenter"
width="300"]<a href="http://217.manyu.in/wp-content/uploads/2012/06/google1.png"><img class="size-medium wp-image-15" title="Google Doodle Level 2" src="http://217.manyu.in/wp-content/uploads/2012/06/google1-300x187.png" alt="Google Doodle Level 2" width="300" height="187" /></a>
Google Doodle Level 2[/caption]

1.  Move left, if the symbol on the tape is the symbol on the
    button write 0 else write 1.

To solve this again is very simple since we want to write 0 we will
need the symbol on the button and that on the tape to be the same,
so we will keep it to the blank symbol [].

From third level the states keep looping but it should be easy for
you to solve. :) Happy solving.



