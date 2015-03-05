---
layout: post
title: Arguments in rake task
---

### Two ways to pass arguments to a rake task
#### Method 1, environmental variables
```ruby
desc "Example of a multi-argument raketask via environmental variables"
task with_environmentals: :environment do
  name = ENV['name']
  surname = ENV['surname']
  print name; print " "; print surname
end
```
Call with `name=Liene surname=Viktus rake with_environmentals`

#### Method 2, argument hash
```ruby
desc "Example of a multi-argument raketask via argument hash"
task :with_hash, [:name, :surname] => :environment do |t, hash|
  hash.with_defaults(name: :John, surname: :Smith)
  puts "Arguments with defaults were: #{hash}"
  print hash.name; print " "; print hash.surname
end
```
Call with `rake with_hash` #=> John Smith
Call with `rake with_hash[Chris,Brown]` #=> Chris Brown

#### Bonus Method 3, anonymous argument hash
```ruby
desc "Bring it on, parameters!"
task :infinite_parameters do |task, args| 
    puts args.extras.count
    args.extras.each do |params|
        puts params
    end         
end
```
Call with `rake infinite_paramers['The','World','Is','Just','Awesome','Boomdeyada']`
via http://stackoverflow.com/a/28654953/3319298

![rake.jpg]({{ site.baseurl }}/images/rake-04.jpg)


