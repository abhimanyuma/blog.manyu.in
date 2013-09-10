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
	search(s)
end
{% endhighlight %}

This clearly is not a polynomial time algorithm and the time complexity is equal to the number of paths in a graph, which is \\\( O((n-2)!) \\\) and even for moderate \\\( n \geq 15 \\\) it takes a lot of time. 

## A better non-optimal solution

We see that the major problem with the last algorithm was that we were wasting too much time on already computed paths and vertices, so we see if we can do better. This was a solution I got from ()[] 

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

Now the first case is easy to check, so consider this graph. 


Here \\\(b\\\) is the common ancestor of the destination and the vertex we need to find if it is a good node. As it is it can easily be seen it cannot be, but we are yet to add the back edges. 

**Lemma 1**: Using tree edges alone it is not possible to find a path from \\\(s\\\) to \\\(t\\\) through \\\(v\\\) if \\\(v\\\) is not an ancestor of \\\(t\\\)

Now we look at the backedges, and we see something 

_**Theorem 2**: \\\(v\\\) is a good node iff there is a backedge from \\\(v\\\) or one of it's predecessors to a node higher than the common ancestor of \\\(t\\\) and \\\(v\\\)_

We shall prove this both ways. 

1. Let there be \\\(u\\\) a predecessor of \\\(v\\\), and let it have a backedge to \\\(b\\\) . Then there definitely is a \\\(s \rightarrow ... \rightarrow b \rightarrow ... \rightarrow u \rightarrow ... \rightarrow v \rightarrow ... \rightarrow c \rightarrow ... \rightarrow t \\\) . Hence in this case it is quite easy to see the path. The image below will make it clear. 
2. If there is no back edge to a higher node than the ancestor then we can see that we have to use at least one of the tree edges to get back to the common ancestor, since DFS,by design does not contain cross edges, and hence it is not possible. 

Now that the proof is done we will see how to implement this practically. We see that 

+ We need level information
+ Common ancestor information can be represented using level numbers
+ We also maintain a highest_vertex variable to get to know the highest vertex that can be reached without using the tree edges above. 

So essentially algorithm is this. 

1. Do a DFS from \\\(s\\\) and get the DFS tree rooted at \\\(s\\\). 
2. During this step if we find a back edge we update the highest\_vertex counter, as max of highest\_vertex of children and the backedge of these. 
3. Once done we do a common ancestor assignment by traversing from \\\(t\\\) upwards till \\\(s\\\)

{% highlight ruby %}
G = V,E 
s = start
t = destination

def dfs (node,level)
	node.visited = true
	node.level=level
	high=INF #Infinity
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
	node.highest\_vertex=high
end

def set\_ancestor (node,level,special\_child = nil)
	node.children.each do |child|
		if child != special\_child
			child.ancestor\_level = level
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
		if v.highest\_vertex < v.ancestor\_level
			good << v
		end
	end
	puts good.size
end
{% endhighlight %}
