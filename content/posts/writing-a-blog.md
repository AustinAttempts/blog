---
date: '2025-01-08T14:53:59-08:00'
title: 'Austin Attempts: Writing a Blog'
auhor: ["Austin Guevara"]
type: "post"
---
## Why did I start this?

Honestly, this whole thing can be blamed on two people; Beau and Chris.  For some reason as 2024 came to an end I decided to work on my coding skills.  For the first time ever I attempted [Advent of Code](https://adventofcode.com/) and if that wasn't hard enough I did it all in a langauage completly new to me, Zig.[^1] This led me on a tangent of learning RayLib, trying to make a game for the browser, then finally learning Go to make an HTTP server.

<img src="/imgs/writing-a-blog/zig_to_go_v2.png#center" alt="zig to raylib to go to ?">

While going down this rabit hole of learning I also was finally downloading Letterboxd to begin recording my opinion on every movie I watched.  Our household has taken a liking to GoodReads and now that I was a proud AMC A-List member I was hoping to take that over to my movie watching for the New Years.  This is when Beau, my roomate, suggested that since I enjoyed sharing my oppinions so much I should just start a blog.  Then, when I told my friend Chris of this potential new project, he said it would be an easy project to learn a little web dev... with all that said here I am 🤷‍♂️.

## Getting Started... Kinda
The idea of the blog was pretty straight forward:
1) I do not want to write a bunch of custom HTML and CSS (it just is not fun to me)
2) There should be a simple way for a visitor to search for a specific post
3) Perferably, I can write my posts in MarkDown

The more projects I have attepmted on my own the more I realized the truth of the statement "You don't know what you don't know".  In school and as a junior engineer I took for granted how directed my efforts were at the beginning of projects.  In both cases someone with experience is their to outline the steps needed to complete any project. However, when those mentors aren't there it can be daunting to figure out where to even begin. Every project, at least that I have attempted, can be solved in many many different ways and inorder to not get crushed by the choices I force to myself to start with whatever tools are immediatly available.  Often this is the wrong solution or less effecient but at least I will learn why this was the wrong decision for when I decide to pivot.  

As previously mentioned I had just started learning Go when the project came to mind so my first attempt was obviously written in... Go.  Based on the [writing web applications](https://go.dev/doc/articles/wiki/) book posted in the Go Docs and a [youtube series](https://www.youtube.com/watch?v=Wx8SMT82aa8&list=PLVEltXlEeWglazv9RrL-ykONIPeWawfT-) specifically on creating a Blog I had a first version up and running extremly quickly.

### ServeMux
First, we create a ServeMux using the go standard http library.  This is an HTTP muiltplexer.  It matches the URL of each incoming request and matches it to the associated handler.
```go
mux := http.NewServeMux() // allocates and returns a new [ServeMux].
```

### File Reader
Next we need to process all the MarkDown files that contain my posts into a format that is usable.  This is accomplished using [GoldMark](https://github.com/yuin/goldmark) and [FrontMatter](https://github.com/adrg/frontmatter) to parse each file in a specified directory.  Little did I know at the time how helpful it would be to undesrtand how and what GoldMark was doing.
```go
postReader := goBlog.FileReader{
	Dir: "posts", // local path in which to find files to parse
}
```

### HTML templates
Now that we have our content parsed and seperated we can move it to a template page.  This template handles the majority of the HTML and CSS required to make a page "pretty".  It dictates where and how information like a posts title, author, and content is layed out on the webpage.
```go
postTemplate := template.Must(template.ParseFiles("post.gohtml"))
```

### Associate URL's
We add each post data onto the previously made template and associate a handler for when a get request to that URL is processed. 
```go
mux.HandleFunc("GET /posts/{slug}", goBlog.PostHandler(postReader, postTemplate))
```

### Index all posts
With all posts made and given a URL we now need a landing page.  This landing page has its own template file and can display whatever I want.
```go
indexTemplate := template.Must(template.ParseFiles("index.gohtml"))
mux.HandleFunc("GET /", goBlog.IndexHandler(postReader, indexTemplate))
```

### Run Site
With all functionality added we can now run the server locally on port 8080.
```go
log.Fatal(http.ListenAndServe(":8080", mux))
```

Great its working now what? Well other than the lack of features there is one major issue.  That's right... I have to host a server somewhere that handles all the funciality listed above.  This works great when I am developing and testing on my home setup but how can I have others access my site I need to give access to the public.


[^1]: Advent of Code was an extremly fun experince and I will probably do a series of posts deticated to these puzzles