rails new my_blog --api
cd my_blog


rails g scaffold user email:string password:string auth_token:string
rails g scaffold post title:string body:text user:references
rails g scaffold comment body:text user:references post:references
rake db:migrate



db/seeds.rbRuby

u1 = User.create(email: 'user@example.com', password: 'password')
u2 = User.create(email: 'user2@example.com', password: 'password')

p1 = u1.posts.create(title: 'First Post', body: 'An Airplane')
p2 = u1.posts.create(title: 'Second Post', body: 'A Train')

p3 = u2.posts.create(title: 'Third Post', body: 'A Truck')
p4 = u2.posts.create(title: 'Fourth Post', body: 'A Boat')

p3.comments.create(body: "This post was terrible", user: u1)
p4.comments.create(body: "This post was the best thing in the whole world", user: u1)


app/model/user.rbRuby

class User < ActiveRecord::Base
  has_many :posts
  has_many :comments
end

app/model/post.rbRuby

class Post < ApplicationRecord
  belongs_to :user
  has_many :comments
end

class Comment < ApplicationRecord
  belongs_to :user
  belongs_to :post
end

rake db:seed



Añadir swagger

gem 'swagger-blocks'
