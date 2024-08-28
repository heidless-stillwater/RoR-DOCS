
# [Intro Ruby on Rails 7 For Beginners Tutorial Series](https://www.youtube.com/playlist?list=PL3mtAHT_eRezB9fnoIcKS4vYFjm23vddb)

## [0: Intro to Ruby on Rails 7 Fullstack Tutorial](https://www.youtube.com/watch?v=TlgSp2XPCY4&list=PL3mtAHT_eRezB9fnoIcKS4vYFjm23vddb&index=1)

### install
```
# uninstall
#gem uninstall rails
#gem uninstall railties

#gem uninstall rails -v 6.1.7.7
#gem uninstall railties -v 6.1.7.7

--------------
# install
gem install rails 

gem install rails -v 6.1.7.7
rails  _6.1.7.7_ new rails-test-0 -d postgresql

#/bin/zsh --login
#export PATH="/home/heidless/.rvm/gems/ruby-3.2.2/bin:$PATH"
#rvm use --default 3.2.2

```

#### init project
```
# rails new blog_demo -b bootstrap

rails new blog_demo

rails g controller pages home about 

rails s   
--
http://127.0.0.1:3000/pages/home

--

```

### git
```
git checkout -b style-0
git status
git add .
git commit -m "add styling"
git push
--
git push --set-upstream origin style-0

Github->'deanin-0-blog_demo'->Compare&PullRequest

git pull

--

```

### blog posts
```
rails g scaffold post title body:text
rails db:migrate

rails c
--
@post = Post.new(title: "Hello World!", body: "This is my first post...")
@post
@post.save
@post
@post = Post.create(title: 'Second post!', body: 'This is my second post...')

@post.title
Post.first

--


```