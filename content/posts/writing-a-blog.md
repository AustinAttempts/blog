---
date: '2025-01-08T14:53:59-08:00'
title: 'Austin Attempts: Writing a Blog'
auhor: ["Austin Guevara"]
type: "post"
---
## Why did I start this?

Honestly, I blame this entire journey on two people: Beau and Chris. As 2024 came to an end, I decided to focus on improving my coding skills. For the first time ever, I participated in [Advent of Code](https://adventofcode.com/) and to make it even more challenging, I completed it entirely in a language that was completely new to me—Zig.[^1] This sparked a series of tangents, including learning RayLib, attempting to create a browser-based game, and eventually diving into Go to build an HTTP server.

<img src="/imgs/writing-a-blog/zig_to_go_v2.png#center" alt="zig to raylib to go to ?">

While going down this rabbit hole of learning, I finally decided to download Letterboxd to start recording my opinions on every movie I watched. Our household had already taken a liking to Goodreads, and as a proud AMC A-List member, I thought it would be fun to carry that habit over to my movie-watching in the new year. That’s when Beau, my roommate, suggested that since I enjoyed sharing my opinions so much, I should just start a blog. When I mentioned this idea to my friend Chris, he pointed out that it would be a perfect project to learn a bit of web development. And so, with all of that in mind... here I am 🤷‍♂️.

The idea for the blog was pretty straightforward:

1) I didn’t want to write a bunch of custom HTML and CSS (it just isn’t enjoyable for me).
2) There should be a simple way for visitors to search for specific posts.
3) Ideally, I could write my posts in Markdown.

## Getting Started... Kinda

The more personal projects I’ve attempted, the more I’ve come to appreciate the truth of the saying, 'You don’t know what you don’t know.' In both school and as a junior engineer, I took for granted how guided my efforts were at the start of a project. In those cases, someone with experience would outline the necessary steps to complete the work. Without those mentors, however, it can be daunting to figure out where to even begin.

Every project I’ve attempted so far could be solved in countless ways, and to avoid being overwhelmed by the choices, I’ve made it a habit to start with whatever tools are immediately available to me. While this often leads to less efficient or outright wrong solutions, it’s a valuable learning experience. Each misstep teaches me why the decision was suboptimal, preparing me for when it’s time to pivot to a better approach.  

As I mentioned earlier, I had just started learning Go when this project idea came to mind, so my first attempt was, naturally, written in... Go. Using the [writing web applications](https://go.dev/doc/articles/wiki/) guide from the Go documentation and a [youtube series](https://www.youtube.com/watch?v=Wx8SMT82aa8&list=PLVEltXlEeWglazv9RrL-ykONIPeWawfT-) focused on building a blog, I was able to get a first version up and running surprisingly quickly.

### ServeMux
First, we create a ```ServeMux``` using Go’s standard ```http``` library. A ```ServeMux``` is an HTTP multiplexer that routes incoming requests to the appropriate handler based on the URL. It acts as a router, matching each request's URL to its corresponding handler function.

```go
mux := http.NewServeMux() // allocates and returns a new [ServeMux].
```

### File Reader
Next, we need to process all the Markdown files containing my posts into a format that is usable. This is accomplished using [GoldMark](https://github.com/yuin/goldmark) and [FrontMatter](https://github.com/adrg/frontmatter) to parse each file in a specified directory. At the time, I didn’t realize how helpful it would be to understand the inner workings of GoldMark and what it was doing behind the scenes.

```go
postReader := goBlog.FileReader{
	Dir: "posts", // local path in which to find files to parse
}
```

### HTML templates
Now that we have our content parsed and organized, we can move it to a template page. This template handles the bulk of the HTML and CSS needed to make the page look presentable. It defines the layout and styling for elements like the post's title, author, and content, determining how and where this information is displayed on the webpage.

```go
postTemplate := template.Must(template.ParseFiles("post.gohtml"))
```

### Associate URL's
We add each post's data to the previously created template and associate a handler to process the GET request for that specific URL.

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
With all the functionality in place, we can now run the server locally on port 8080.
```go
log.Fatal(http.ListenAndServe(":8080", mux))
```

Great, it’s working! Now what? Well, aside from the lack of features, there’s one major issue: I need to host a server somewhere that can handle all the functionality mentioned above. This setup works perfectly for development and testing on my home setup, but how can I make the site accessible to the public?

### WIP... 


[^1]: Advent of Code was an extremely fun experience, and I’ll likely dedicate a series of posts to these puzzles.