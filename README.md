# README the RSS
Pulls your most recent blog posts through an RSS feed

## How to use
* Add the following section tags to your `README.md` file

```
## My Blog
<!-- BLOGPOSTS:START -->
<!-- BLOGPOSTS:END -->
```
* Create a file in `.github/workflows/blogposts.yml`
```yml
name: Blog post workflow
on:
  schedule:
    # Runs every day at 3pm UTC (11pm SG)
    - cron: '0 15 * * *'

jobs:
  pull_blog_rss:
    name: Update with latest blog posts
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Get RSS Feed
        uses: ./
        with:
          feed_url: https://blog.rongying.co/feed.xml
          count: 6 # default 6
      - name: Commit file changes
        run: |
            git config --global user.name 'YOUR_USERNAME'
            git config --global user.email 'YOUR_GMAIL'
            git add README.md
            git commit -m "Update README"    
      - name: Push changes
        uses: ad-m/github-push-action@master
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
```

## Arugments

|Inputs | Default | Description    |
|---|---|---|
|`feed_url`|`""`|Required. RSS Url|
|`count`   |`5`   |Number of posts to display   |


## Demo
<!-- BLOGPOSTS:START -->
- [Created an IG filter with PickerUI!](https://blog.rongying.co/posts/2020/08/Building-an-IG-filter-with-PickerUI/)
- [Deploy deno with Github Actions](https://blog.rongying.co/posts/2020/08/Building-a-CICD-Pipeline-with-Github/)
- [Learning Flutter - Implicit Animations](https://blog.rongying.co/posts/2020/07/Learning-Flutter---Implicit-Animations/)
- [I moved to 11ty](https://blog.rongying.co/posts/2020/07/I-moved-to-11ty/)
- [Building a Single-Spa](https://blog.rongying.co/posts/2020/06/Building-a-Single-Spa/)
<!-- BLOGPOSTS:END -->

<!--
How to run

Generate the build file in dist/index.js
npm run build 
-->