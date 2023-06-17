---
layout: post
title: "Setting up my Blog with GithubPages, Jekyll & Minima"
tags: github_pages jekyll minima
image: /assets/img/projects/blog_setup/blog_setup_initial_title.png
comments: true
summary: "Having my own blog is something I've always been very excited about. In this post I'm sharing why I decided to host my blog using Github Pages and Jekyll, and how you too can set up your own (free!) blog with those tools."
---

{% include toc.html %}

I always wanted to have a blog - being able to share insights I gained during projects, tutorials for setting up my tech or even general learnings from my daily work life is something I've always been excited about.

When I finally decided to get started and set up a blog, I was overwhelmed with the many options there are. Sure, there's the obvious, big blogging providers such as [WordPress](https://wordpress.com/) or [SquareSpace](https://www.squarespace.com/) - but all of those come with limitations, and I definitely wasn't ready to pay the full "expert subscription fee" for those providers just yet.

And then I heard about [Github Pages Blogs](https://pages.github.com/).

## How does Blogging with GithubPages Work?
Github Pages is a **free static site hosting service**, that takes the content to host directly from your Github repository. With Github Pages, you can either implement your own website from scratch _or_ you can use static website generators such as [Jekyll](https://jekyllrb.com/docs/) to generate the site for you (_this is what I decided to do :-)_).

Organising and hosting a blog with Jekyll and GithubPages comes with a bunch of **advantages**:
- getting started with your blog is super **quick** - and it **doesn't cost anything**!
- with Jekyll you can pick from a range of **[free, open source templates](https://jekyllthemes.io/free)** for your blog - and you can very easily **customise each page** to match your own blogging style
- there's a lot of **ready-to-use plugins** for Jekyll, for example for [post comments in Disqus](https://disqus.com/admin/install/platforms/jekyll/) or integration with [Google Analytics](https://analytics.google.com/)

For me, as a software engineer, using GithubPages for blogging sounded like the perfect opportunity to **share my story while simultaniously learning about new frameworks** (such as [Jekyll](https://jekyllrb.com/) and [Liquid](https://shopify.github.io/liquid/)) as well as brushing up my HTML, CSS and JS skills. I decided to go with a very basic Jekyll template called [minima](https://github.com/jekyll/minima) and then customised it piece by piece.

## How do I get started?
There's a lot of great tutorials out there for how to set up your blog with Github Pages - I'd recommend checking out the [official Github documentation](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll) in case of any errors.

Here's the step's that I followed:

### 1. Find the right place for your Github Blog Repository
The hosting URL of your blog depends on where the repository containing the static sources for your blog lives. There's basically three options:

- **Personal Blog**: If you want a blog for **your Github user**, you'll need to create a new repository called `<github_username>.github.io`. The blog URL will then also be `<github_username>.github.io` - you can only have one "user blog" per Github user.

- **Project Blog**: If you already have a Github repository you want to blog about, you can simply push your static blogging sources to a subdirectory in that repository. The blogging URL will then be `<github_username>.github.io/<repository_name>`.

- **Organisation Blog**: If you want a personal blog, but you want it to be separate from your Github user you can use organisation blogs. Organisation blogs work exactly the same as peronal blogs, except that instead of your Github user you'll use a [Github organisation](https://docs.github.com/en/organizations/collaborating-with-groups-in-organizations/about-organizations). Github organisations are free to use - usually organisations are created to allow collaboration between multiple users, but you can totally also be the only person in your organisation. To set up a blog for your organisation, you'll need to create a new repository called `<github_orgname>.github.io`, which will also be the hosting URL for the blog.

### 2. Initialise your Repository
Once you've decided on the right location for your blogging repository, it's time to actually set up and initialise that repo :-)

As said before I wanted to use this blog as an opportunity to learn new stuff, so I decided to go with the full local set up - including installing Ruby, Bundler & Co. You can find the full official instructions for this on the [official Github documentation](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll).

Having the full local setup might seem tedious, but it's going to come in very handy later on once you want to customise and experiment with the different templates. If you want to go with a more lightweight, hands-off blog setup, you can follow templates such as [this one](https://github.com/skills/github-pages) that don't even require a local check-out of your repository.

In any case, after the initial set up you'll end up with a repository structure similar to this one:

```
├── _includes                     # this is where you'll configure additional plugins for your blog, such as google analytics
│   ├── google_analytics.html
│   └── head.html
├── _layouts                      # this is where you can customise the layout of different parts of your blog
│   ├── default.html
│   └── post.html
├── _posts                        # this where the actual blog posts go
│   ├── 2023-01-08-hello-world.markdown
│   └── 2023-02-08-blog-setup.markdown
├── assets                        # here you can put additional assets (eg images) that should appear on your blog
│   └── hello_world_image.png
├── _site                         # jekyll will store the output of the compiled blog site in here
│   └── [...]
├── index.html
├── about.html
└── _config.yml                   # general configuration of your blog (eg url, plugins)

```

At the end of this step, once you've configured your repository and pushed your initial blogging setup, Github Actions will automatically pick up the changes, generate the website sources and deploy your website to your `github.io` URL!

### 3. Add Content & Customise your Blog!
Now that your blog is set up it's time to add some content!

Writing **new blog posts** is fairly straightforward with Jekyll - you just need to add a new file in the format of `<YYY-MM-DD>-<blog_title>.markdown` to your `_posts` directory. The file content has to start with Jekyll frontmatter (*defining the metadata for your post, such as title and date*), the rest of the file will be parsed using markdown. You can check out the [official Jekyll documentation](https://jekyllrb.com/docs/posts/) for details.

Here is what an example for your first blog post could look like:
```
---
layout: post
title: "Hello World!"
date: 2023-01-08
---
Hello World!

This is my very first post - I'm currently setting up this blog,
more content to come soon. Watch this space! :-)
```

In addition to writing posts, you might also want to change the style and format of your blog - for example adjusting the colours and fonts to your personal style, or adding features such as comments or category pages. Check out some free-to-use, open source Jekyll templates [here](https://jekyllthemes.io/free) and keep an eye out for additional blog posts [here](/projects/blog_setup.html) to learn more about how I customised my own blog.


## Conclusion
Setting up my Github Pages Jekyll blog was really easy, and seeing my own website hosted on [emmatheeng.github.io](emmatheeng.github.io) after just a couple of minutes of coding felt amazing. The real exciting work however has just started - adjusting my blog's look & feel to my liking and finally producing content. Check out the [blog setup project page](/projects/blog_setup.html) for more tutorials about setting up and customising your Jekyll blog!

**Let me know in the comments in case there's anything you've learned, missed, or anything additional you'd like to know. I'm looking forward to hearing from you :-)**
