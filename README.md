# R. Chavarría's blog

Project to write a [blog] like a hacker

It's been migrated from Octopress to plain Jekyll, and it's using the
[Primer Jekyll theme].

# TODOs

- [ ] Add notes from articles, videos, and so on that are for years in gmail
- [ ] Categories for posts:
    1. the post url should not include any category, just start with the date and title :heavy_check_mark:
    2. how could I create a link to show all posts within a single category, this way, I could
    create links to a single category in the `archives.md` page
- [ ] Improve header UI
- [ ] Improve footer UI, specially Libre Counter logo
- [ ] ¿Quiero habilitar los comentarios con disquss?

# DONEs

- [x] Migrate posts from Octopus to Jekyll 
- [x] Navigation bar
- [x] Pages (about, reading list,...)
- [x] Header
- [x] Footer
- [x] Move posts from [notes]
- [x] RSS button, with link to `/feed.xml` file
- [x] Fix image links. It seems (/images/...) doesn't work. Review all posts from notes
- [x] Favicon
- [x] On the index page, show date instead of just numbers
- [x] Archives (copy from old blog)
- [x] Blog header must be same width that content
- [x] Add books from gmail
- [x] Run blog locally with docker compose
- [x] Add affiliate links to book reviews
- [x] Merge PWA course
- [x] **PUBLISH**

# Run Jekyll locally with docker

Install ruby bundles:

```bash
docker run \
  -v .:/srv/jekyll \
  -v ./vendor/bundle:/usr/local/bundle \
  --name local-jekyll \
  jekyll/jekyll \
  bundle install
```

Run with docker compose:

```bash
cd docker
docker-compose up &
```

# Help

- [GitHub Flavored Markdown]
- [GitHub pages documentation] 

[blog]: https://rchavarria.github.io
[Primer Jekyll theme]: https://github.com/pages-themes/primer
[GitHub Flavored Markdown]: https://guides.github.com/features/mastering-markdown/
[GitHub pages documentation]: https://help.github.com/categories/github-pages-basics/ 
[notes]: https://github.com/rchavarria/notes
