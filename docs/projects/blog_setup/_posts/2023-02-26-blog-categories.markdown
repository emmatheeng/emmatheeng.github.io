---
layout: post
title: "Adding Categories to my Jekyll Blog"
tags: github_pages jekyll minima liquid
image: /assets/img/projects/blog_setup/blog_setup_tags_categories_title.png
comments: true
summary: "Post tags and categories make it easier to navigate through your blog and find relevant posts! In this post I'm explaining how to structure Jekyll blog posts using post categories."
---
I recently set up this blog using Jekyll, GithubPages and Minima (*if you want to learn more about why and how, check out the first parts of this series [here](/projects/blog_setup.html)!*). Once I had a couple of posts on my blog, I realised I wanted to **organise** my posts better - into different series and technology groups. I wanted to make it _as easy as possible_ for someone reading my post about [customising the minima Jekyll template](/projects/blog_setup/blog-styling.html) to find other posts about working with Jekyll, or using HTML/CSS to customise web frontend.

After doing some research, I discovered two ways of doing this:
1. **Tags**: [Jekyll Tags](https://jekyllrb.com/docs/posts/#tags) are one or more attributes set for a given post. Tags can be added to Jekyll posts using the frontmatter keys `tag` or `tags`.
2. **Categories**: [Jekyll Categories](https://jekyllrb.com/docs/posts/#categories) are similar to tags and can be set in frontmatter using keys `category` or `categories`. Other than tags however they work "more hierarchical" - if a post is in a directory other than `_posts`, every directory will be treated as another post category.

This is part (2) of two posts, focusing on organising blog posts using categories. Check out the [part (1)](/projects/blog_setup/blog-tags.html) if you want to learn more about tags! 

## What are Post Categories?
[Jekyll Categories](https://jekyllrb.com/docs/posts/#categories) are a way of structuring blog posts in a hierarchical way. Blog posts within one category are grouped together and relevant for one main project or goal.

On my blog for example, I am writing about different projects - this series about [setting up my blog with Jekyll, Minima & Co](/projects/blog_setup/) is one of them. I want each project to have its own little overview page and description, and I want blog posts to be accessible through their category.

## Implementation
To implement categories on my blog posts, and add overview pages for each category, I need to implement the following things:
- **adding categories to the post** itself and showing them on the post page
- adding the **overview page per category** that shows general information about the given category

I'm additionally going to use [Jekyll Collections](https://jekyllrb.com/docs/collections/) to store information such as a category description for each category.

### Setting up Category Collections
As said, I'm using  [Jekyll Collections](https://jekyllrb.com/docs/collections/) to store general information about each post category. I'll call the categories I'm focusing on in this example "project" categories, you can change that name to anything you like.

First, I need to tell Jekyll that there's a collection called "projects" in this blog. Collections can be configured in `_config.yml` like so:
```
collections:
  projects:
    output: true
    permalink: /:collection/:categories:output_ext
```

This also tells Jekyll that the link to the category overview page is `<my_blog_url>/<collection_name>/<category_name>.html` - in my case, if I have a project called "blog_project", the URL is going to be `<my_blog_url>/projects/blog_project.html`.

To set up the "blog_project" category, I need to create a new directory in my blog root called `_projects`. In this directory, I'm creating a file called `blog_project.markdown` which sets up the blog_project category. 

```
---
title: "Blog Project"
categories: blog_project
layout: project
---
In this series I'm writing about setting up this block with the help of GitHub Pages, Jekyll, Minima & Co.
```

The project layout is defined in the next step.

### Category Overview Page
Now that I have created a new category, I need to tell Jekyll how to render project category overview pages. In the `_layouts` directory, I'm creating a new file called `project.html` which defines the structure of every project overview page. 

This is what my `project.html` looks like:
```
{% raw %}
---
layout: page
---

{{ content }}

<h2>{{ page.list_title | default: "Posts" }}</h2>
<div>
  <ul>
    {% assign page_category = page.categories | first %}
    {% for post in site.posts %}
      {% if post.categories contains page_category %}
      <li>
        {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
        <b>
          <a href="{{ post.url | relative_url }}">
            {{ post.title | escape }}
          </a>
        </b> - <i>{{ post.date | date: date_format }}</i>
      </li>
      {% endif %}
    {% endfor %}
  </ul>
</div>
{% endraw %}
```

This code snippet does the following:
- It first prints the `content` of the project category - eg the description for `blog_project` I implemented in the first step
- It then iterates through all posts of that category, and prints the post title that links to the respective blog post

### Adding Category to Posts
The last step is now to actually add blog posts for the new blog category. There are two ways of doing this:
- **Jekyll Frontmatter**: one can add categories to posts using the `category` frontmatter keys on a post itself, like this

```
---
layout: post
title: "Hello World!"
category: blog_project 
---
Hello World!

This post has a Category :-)
```

- **Post Directory**: Alternatively, one can structure the raw post files in separate directories, which automatically adds respective categories to each post. In my case, my directory structure looks like below - the `hello_world.markdown` post will automatically be in the `blog_project` category.
```
|─ my_blog/
   ├─ _includes/
   ├─ _layouts/
   ├─ _posts/
   ├─ _projects/
   |  └─ blog_project.markdown
   ├─ projects/
   |  └─ blog_project/
   |     └─ _posts/
   |        └─ hello_world.markdown
   └─ _config.yml
```

Here's what the final `blog_project` overview page looks like
<figure>
  <div>
  <img src="{{site.url}}/assets/img/projects/blog_setup/emmatheeng_category_overview.png" alt="Screenshot of Minima blog showing a blog category overview page"/>
  </div>
  <figcaption>{{"Here's the overview page for the `blog_project` category"| markdownify}}</figcaption>
</figure>


## Conclusion
Categories are really helpful for bringing more structure into blog posts and grouping posts based on projects and overarching topics. 

Check out the [first part](/projects/blog_setup/blog-tags.html) on this topic that's using tags for connecting blog posts by topic!

How are you organising your Jekyll blog? Are you using tags? Categories? Something else? **Let me know in the comments :-)**