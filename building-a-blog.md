# Building a Developer Blog

I will be giving a full walkthrough of how I built this developer blog, including the tools I used, the thought process behind my design decisions, and some implementation decisions.

## Design

The first step in building a blog is thinking about the capabilities of it. Blogs have been done a million times, so there are a lot of examples to draw inspiration from. I really like the look of the blog run by my team's architect [Jeff Doolittle](https://jeffdoolittle.com/). His design is very simple and minimalistic, but still conveys all the important aspects of a blog for showcasing his thoughts, services, and accomplishments.

With Jeff's blog in mind, I drafted what I thought the core requirements of my blog would be:

- A page containing some formatted text which functions as a blog post
- A home page with a list of my recent posts and a short description of myself
- An about page that gives more detail about who I am and what I like to do
- A resume page that displays my resume in a nice format and provides a method for downloading it

The core requirement and goal of the entire blog is to showcase who I am, what my skills are, and archive my thoughts and opinions on the software industry.

## Implementing the Design

### Post Content

I started with thinking about where the content for my articles/posts would come from. Did I want to keep the articles contained within the client itself, or fetch them from some outside resource like an API? Wheat kinds of content would be allowed? How would I want to update and publish the content on my blog?

With all this in mind I put together the following design for retrieving content to display.

1. The client makes a request to the API for the content of a particular blog post
2. The API retrieves the external location of the post's text from its database
3. The API retrieves the text from the external location and formats it in the way that the client has requested
4. The API returns the text to the client, which then renders it to the end user

The reason I decided to separate out the content retrieval process into these pieces is that it lets me control the location of the post's text. It also means that I don't need to update my API or client whenever I add a new blog post, I just need to tell the API where the new location is at. It also means that I can modify a post on the fly and even stage new posts without publishing them.