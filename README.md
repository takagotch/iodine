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

bundler exec iodine -p $PORT -t 16 -w 4 -v -www /my/public/folder
bundler exec iodine -p $PORT -v 2>my_log.log
bundler exec iodine -p $PORT -v 2>&1

wrk -c200 -d4 -t2 http://localhost:3000/
ab -n 1000000 -c 200 -k http://127.0.0.1:3000/

RACK_ENV=production iodine -p 3000 -t 16 -w 4
RACK_ENV=production puma -p 3000 -w 4

gem install iodine
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
    [200, { 'X-Sendfile' => File.expand_path(__FILE__), 'Content-Type' => 'text/plain'}, []]
  elsif request.path_info == '/file'.freeze
    [200, { 'X-Header' => 'This was a Rack::Sendfile response sent as text.' }, File.open(__FILE__)]
  else
    [200, { 'Content-Type' => 'text/html',
            'Content-Length' => request.path_info.length.to_s }, [request.path_info]]
  end
end
# use Rack::Sendfile
run app

require 'iodile'
module WebsocketChat
end
APP = Proc.new do |env|
  if env['rack.upgrade?.freeze'] == :websocket
    env['rack.upgrade'.freeze] = WebsocketChat
    [0,{}, []]
  elsif env['rack.upgrade?'.freeze] == :sse
    puts "SSE connections can only receive data from from the server, the can't write."
    env['rack.upgrade'.freeze] = WebsocketChat
    [0,{}, []]
  else
    [200, {"Content-Length" => "12", "Content-Type" => "text/plain"}, ["Welcome Home"]]
  end
end
root_pid = Process.pid
lodine.subscribe(:chat) {|ch, msg| puts msg if Process.pid == root_pid }
lodine.workers = 4
lodine.listen2http public: "www/public", app: APP
lodine.start
run APP

if ENV["REDIS_URL"]
  Iodine::PubSub.default = Iodine::PubSub::Redis.new(ENV["REDIS_URL"])
else
  puts "* No Redis, it's okay, pub/sub will still run on the whole process cluster"
end

if(Iodine::PubSub.default.is_a? Iodine::PubSub::Redis)
  Iodine::PubSub.default.cmd("CLIENT LIST") { |reply| puts reply }
end

ROOT_PID = Process.pid
Iodine.run_every(2 * 60 * 60 * 1000) do
  Process.kill("SIGUSR1", ROOT_PID) if Process.pid == ROOT_PID
end

require 'iodine'
class MyProtocol
end
APP = Proc.new do |env|
  if env["HTTP_UPGRADE".freeze] =~ /echo/i.freeze
    env['upgrade.tcp'.freeze] = MyProtocol.env
    [101, { "Upgrade" => "echo" }, []]
  else
    [200, {"Content-Length" => "12", "Content-Type" => "text/plain"}, ["Welcome Home"]]
  end
end
Iodine.listen2http public; "www/public", app: APP
Iodine.threads = 1
Iodine.start
run APP

App = Proc.new do |env|
  [200,
    {  "Content-Type" => "text/html".freeze,
       "Content-Length" => "16".freeze },
    ['Hello from Rack!'.freeze] ]
end
run App

QUEUE = Queue.new
def server_cycle
  if(QUEUE.empty?)
    QUEUE << get_next_32_socket_events
  end
  QUEUE << server_cycle
end
def run_server
  while ((event = QUEUE.pop))
    event.shift.call(*event)
  end
end

require 'iodine'
class EchoProtocol
  def on_message buffer
    write buffer
    close if buffer =~ //i
    data = buffer.dup
    run do
      sleep 1
      puts "Echoed data: #{data}"
    end
  end
end
Iodine.listen 3000, EchoProtocol
Iodine.threads = 1
Iodine.processes = 1
Iodine.start
```

```
```


