### iodine
---
https://github.com/boazsegev/iodine

```
gem 'iodine', '~>0.6'
bundler exec iodine -p $PORT -t 16 -w 4
bundler exec iodine -p $PORT -t 16 -w 1
bundler exec iodine -p $PORT -t 16 -www /my/public/folder

bundler exec iodine -p $PORT -t 16 -w 4 -www /my/punlic/folder -v

gzip -k -9 style.css
```

```ruby
require 'iodine'
Iodine.listen2http public: '/my/public/folder'
Iodine.threads = 1
Iodine.start

# config.rb
app = proc do |env|
  request = Rack::Request.new(env)
  if request.path_info == '/source'.freeze
    []
  elsif request.path_info == '/file'.freeze
    []
  else
    []
  end
end
run app




```

```
```


