  ---------------------------------------------
  layout: post
  title: Add Code Bits in your Wordpress Blog
  ...
  permalink: http://blog.manyu.in/?p=293
  ...
  post\_id: 293
  categories: ---
  - C++ Code
  - Code
  - Computer Code
  - Displaying
  - General
  - Pre Tag
  - Programming
  - Source Code
  - Wordpress
  ---------------------------------------------

If you have your own tech blog and use wordpress, generally all the
newbies will face this same problem, how to add code bits to your
own blog when you try to add them generally what happens is that
they will appear with paragraph line spacing, this looks good when
you write normal paragraphs but with computer code it looks weird
like this

ConnectionConfiguration connConfig = \*\*

*new*ConnectionConfiguration(“talk.google.com”,5222, “gmail.com”);

XMPPConnection connection = *new* XMPPConnection(connConfig);

connection.connect();

connection.login(“blahblah@gmail.com”, “password”);

Chat chat =
connection.getChatManager().createChat(“friend@gmail.com”, *null*);

chat.sendMessage(“Hi Tom!”);

}

<!--more-->
The first method would be to use space and not to use enter at all
but that would not give you consistent results, for with a
different theme it would look even worse than what is give above
because of your spaces

The other method I would suggest is use the pre tag, which involves
the following steps
<ul>
    <li>
Complete your blog post except for the computer code parts
</li>
    <li>
Take HTML editor of the same, look for where you want to place your
code, place the cursor there
</li>
    <li>
Now type
<pre style="overflow:auto;"> </li>
    <li>Paste your code</li>
    <li>Close the tag by typing </pre></li>
    <li>
Publish
</li>
</ul>
Now your code will look like this
<pre style="overflow:auto;">ConnectionConfiguration connConfig =
newConnectionConfiguration(“talk.google.com”,5222, “gmail.com”);
XMPPConnection connection =
new XMPPConnection(connConfig); connection.connect();
connection.login(“blahblah@gmail.com”, “password”);
Chat chat = connection.getChatManager().createChat(“friend@gmail.com”, null);
chat.sendMessage(“Hi Tom!”);</pre>
The pre tag tells your browser that the text is PREformatted and
has already been given the needed spacing so they need not
interfere.



