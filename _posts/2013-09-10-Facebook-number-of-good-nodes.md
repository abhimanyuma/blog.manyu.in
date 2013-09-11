---
layout: post
title: "[Facebook] Number of Good Nodes in a Graph"
tagline: "Facebook Placement Test, IIT Kanpur, Dec. 2012"
category: tech
modified: 2013-09-10
tags: [facebook,placement,recruitment,puzzle,graph-theory,algorithm]
---

The following question was asked in the placement test of Facebook in 2012, at IIT Kanpur, this is a question from a secondary source, and hence may be erroneous. Since I asked this question 3 days ago (in a private group).

## Fancy Question

_Extremely Paraphrased_

Jayan is a very curious student and gets easily bored, he has his house at one end of the city, and the school at another end. His school ends in the afternoon, but his parents come home only during the evening. Not wanting to waste this time, getting bored at home, he decides while returing from school to home, he will visit some place. There are many interesting places in the city, and there is a good bidirectional road network connecting many pairs (but not all) of places. Given that he gets extremely bored, he will visit only those places in the city, if he can go from the school to the place, and then to his house, without going through any other place more than once. He does not mind if he visits the same place on different days, but he will not visit the same place on the same day twice. 

Given the list of places, and the list of roads between the places help Jayan find the total number of places he can visit in the least possible amount of time. 

## Algorithmic Question   

The first step of any problem is to convert it into formal terms, so that we can look at what we can do, so stripping off all the mumbo-jumbo we arrive at 

So essentially we see the following

- We are given a graph of places-vertices and roads-edges, 
- The graph is undirected (bidirectional)
- We are not bothered about time or weights of edges
- What we want to find are paths, which by definition does not contain cycles. 
- We need to find it there is a path from school to home through a node.
- We finally need to cound the number of nodes, which has a path through them. 

Once we add all this up we arrive at the following formal deifinition of the problem.

Given a **undirected** graph \\\(G(V,E)\\\) where \\\(V\\\) is the set of \\\(vertices\\\) and \\\(E\\\) is the set of edges \\\(E\\\) , and \\\( \|V\|=n\\\) , \\\( \|E\|=m\\\) , and let \\\(s\\\) be the source(school) and \\\(t\\\) be the destination)home). A node \\\(v\\\) is called \\\(good\\\) if and only if there is a \\\(path\\\) \\\(p\\\) (i.e no nodes, or edges are repeated) from \\\(s\\\) to \\\(t\\\) that passes through \\\(v\\\) . Count the number of \\\(good\\\) vertices in \\\(V\\\) .

## A brute force approach

The brute force approach in this case is simple find all paths between the *source* and the *destination*. Since this approach is trivial the following are the steps, this is in some ways a modification of DFS, here instead of setting a node to visited permanently we will unvisit it on the way back.   

{% highlight ruby %}
G = V,E 
s = start
t = destination

def search (node)
	if node == t
		return true
	end
	node.visited = true
	good = false
	node.neighbours each do |neighbour|
		if neighbour.visited == false
			good = good || search(neighbour)
		end
	end
	node.visited = false
	return good
end

def main
	V.each do |v| 
		v.good = false
		v.visited = false
	end
	good=[]
	search(s)
	V.each do |v|
		if v.good
			good << v
		end
	end
	puts good.size
end
{% endhighlight %}

This clearly is not a polynomial time algorithm and the time complexity is equal to the number of paths in a graph, which is \\\( O((n-2)!) \\\) and even for moderate \\\( n \geq 15 \\\) it takes a lot of time. 

## A better non-optimal solution

We see that the major problem with the last algorithm was that we were wasting too much time on already computed paths and vertices, so we see if we can do better. This was a solution I got from Ravi Teja

_Since this is a non-optimal solution, I will only discuss the idea_

Essentially we find one of the possible paths using DFS or BFS, and then mark all the nodes in that path as good. If there aren't any paths, then there are no good nodes in the graph. Now for each non-good node we see if there is a path that starts at a good node, and goes through this and ends at another good node. And then we mark all these nodes also as good. Essentially this is equivalent to doing multiple rounds of BFS starting from a good node, and then going to a blank node. 

The advantage here is that we mark each node as good only once, avoid a lot of wastage in the previous response. 

To look at the complexity, note that each iteration will do 

- Find atleast one good node
- Find atleast one bad node
- Find that there are no more good nodes neighbouring that vertex

This gives us that the algorithm will run a BFS/DFS \\\(O(n)\\\) times giving a total complexity of \\\(O(mn)\\\)

## Optimal solution using a single DFS

We will now consider a bit more complex but optimal solution that uses a single DFS to get to the solution. 

The way I got to this is that generally connectivity problems like this involve DFS, hence I drew a simple DFS tree, and once I defined what it means for a node to be good on the tree, it was straight forward from there.

Consider a **DFS Tree** rooted at the source vertex. We can make the following two observations easily 

1. Any node that is an ancestor of \\\(t\\\) in the DFS Tree rooted at \\\(s\\\)is a good node. 
2. Any node that is NOT an ancestor of \\\(t\\\) in the DFS Tree rooted at \\\(s\\\) has to use back edges in some form. 

Now the first case is easy to check, so consider this DFS Tree. 

<figure>
	<a href="/images/51.png">
	<img src="/images/51.png" /></a>
	<figcaption>The DFS Tree without backedges</figcaption>
</figure>


Here \\\(b\\\) is the common ancestor of the destination and the vertex we need to find if it is a good node. As it is it can easily be seen it cannot be, but we are yet to add the back edges. 

**Lemma 1**: _Using tree edges alone it is not possible to find a path from_ \\\(s\\\) _to_ \\\(t\\\) _through_ \\\(v\\\) _if_ \\\(v\\\) _is not an ancestor of_ \\\(t\\\)

Now we look at the backedges, and we see something 

**Theorem 2**: \\\(v\\\) _is a good node iff there is a backedge from_ \\\(v\\\) _or one of it's successors to a node higher than the common ancestor of_ \\\(t\\\) _and_ \\\(v\\\)

We shall prove this both ways. 

1. Let there be \\\(y\\\) a successor of \\\(v\\\), and let it have a backedge to \\\(b\\\) . Then there definitely is a \\\(s \rightarrow ... \rightarrow b \rightarrow ... \rightarrow y \rightarrow ... \rightarrow v \rightarrow ... \rightarrow c \rightarrow ... \rightarrow t \\\) . Hence in this case it is quite easy to see the path. The image below will make it clear. 
<figure>
	<a href="/images/66.png">
	<img src="/images/66.png" /></a>
	<figcaption>The DFS Tree with added backedge and path</figcaption>
</figure>
2. If there is no back edge to a higher node than the common ancestor then we can see that we have to use at least one of the tree edges to get back to the common ancestor, since DFS,by design does not contain cross edges, and hence it is not possible to get to \\\(t\\\) without using a vertex twice.
<figure>
    <a href="/images/be.png">
	<img src="/images/be.png" /></a>
	<figcaption>The DFS Tree with a bad node after adding backedges</figcaption>
</figure>
Now that the proof is done we will see how to implement this practically. We see that 

+ We need level information
+ Common ancestor information can be represented using level numbers
+ We also maintain a highest_vertex variable to get to know the highest vertex that can be reached without using the tree edges above. 

So essentially algorithm is this. 

1. Do a DFS from \\\(s\\\) and get the DFS tree rooted at \\\(s\\\). 
2. During this step if we find a back edge we update the highest\_vertex (which is the vertex with the **lowest** level number) variable. Essentially it can be defined recursively as 
{% highlight ruby %}
V.Highest-Ancestor = V.Lowest-Ancestor-Level
                   = min(Level of all backedges of V,
                   Highest-ancestors of it's children)
{% endhighlight%}
This recursive definition takes care of all successors of the children.The confusing part is with level numbers since the highest ancestor has the lowest level number. Once we get to terms with that it is easy.    
3. We also need to set the common ancestor levels, this is what we do, we start at \\\(t\\\) and do the following

    + For all the children of t , t itself is the lowest common ancestor. 
    + Now if we go up from t to s, for all other nodes, it is the first node they meet on this path. So we will go up the path till root, and for each node n we see set all the successors of that node except the one we came from to  have common ancestor as the node n.

<figure>
	<a href="/images/73.png">
	<img src="/images/73.png" /></a>
	<figcaption>Setting common ancestor levels</figcaption>
</figure>
 
{% highlight ruby %}
G = V,E 
s = start
t = destination
good = []
def dfs (node,level)
	node.visited = true
	node.level=level
	#We can atleast reach this level
	high=level 
	node.neighbours each do |neighbour|
		if neighbour.visited == false
			node.children << neighbour
			neighbour.parent = node
			dfs(neighbour,level+1)
			high=min(high,neighbour.highest_vertex)
		elsif
			#This is a back-edge
			high=min(high,neighbour.level)
		end
	end
	node.highest_vertex=high
end

def set_ancestor (node,level,specialchild = nil)
	#One of the nodes on the path
	#Set all it's children and their children 
	#to have the level as node's
	node.children.each do |child|
		if child != specialchild
			child.ancestor_level = level
			#We don't want to change level 
			#since it is of common ancestor
			set_ancestor(child,level)
		end
	end
end

def main
	V.each do |v| 
		v.good = false
		v.visited = false
		v.level=nil
		v.highest_vertex=nil
		v.ancestor_level=nil
		v.children=[]
	end
	dfs(s,0)
	current = t
	child = nil
	while current != nil
		set_ancestor(current,current.level,child)
		child = current
		current = current.parent
	end
	V.each do |v|
		if v.highest_vertex < v.ancestor_level
			v.good = true
			good << v
		end
	end
	puts good.size
end
{% endhighlight %}

## Next Set of Questions

Faster simpler questions

1. We have a matrix of size \\\( 2n \times 2n \\\) , which is filled with elements from \\\(1\\\) to \\\( 4n^2 \\\) continously in row major format (i.e first row has from \\\(1\\\) to \\\(2n\\\), the next row the next set of numbers and so on). **Prove that** the sum of each row and column is divisible by \\\(n\\\).   
Tower Research, December 2012,IIT Kanpur, First Round Interview

2. Given a unit square (a square with each side having unit length) **prove that** given any nine points inside the square the smallest triangle that can be constructed using three of the points as 3 vertices, has an area that is smaller than or equal to \\\(\frac{1}{8}^{th}\\\) of the size of the square. Ignore boundary cases of three points in a line, or more than one dot at the same place.   
Goldman Sachs, November 2012, All India Test 

Answers next week. 