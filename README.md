# Docker Sinatra Dev

Sinatra Develop Environment using Docker.

You can develop a Sinatra application without pollute the host OS.

## Installation

```
$ git clone https://github.com/ongaeshi/docker-sinatra-dev.git
$ cd docker-sinatra-dev
```

Build image & run container. (Need docker)

```
$ rake
docker build -t sinatra-dev .
Sending build context to Docker daemon 98.82 kB
Sending build context to Docker daemon 
Step 0 : FROM ruby:2.2.2-onbuild
# Executing 4 build triggers
Trigger 0, COPY Gemfile /usr/src/app/
.
.
docker run -itP --rm -v "/Users/ongaeshi/Documents/docker-sinatra-dev":/usr/src/app -w /usr/src/app sinatra-dev ruby app.rb -o 0.0.0.0
[2015-07-19 06:40:44] INFO  WEBrick 1.3.1
[2015-07-19 06:40:44] INFO  ruby 2.2.2 (2015-04-13) [x86_64-linux]
== Sinatra (v1.4.6) has taken the stage on 4567 for development with backup from WEBrick
[2015-07-19 06:40:44] INFO  WEBrick::HTTPServer#start: pid=1 port=4567
```

Start-up of the web application has been completed.

## Open web app

Examine the bound URL to open it in the browser.

![docker-sinatra-dev-01](http://f.st-hatena.com/images/fotolife/t/tuto0621/20150719/20150719155652_original.png?1437289028)

If you use [Kitematic](https://kitematic.com/) find here.

![docker-sinatra-dev-02](http://f.st-hatena.com/images/fotolife/t/tuto0621/20150719/20150719155651_original.png?1437289057)

## Develop app

Open the `docker-sinatra-dev/app.rb` on **HOST-OS**.

```
$ emacs app.rb
```

Edit the file.

```diff
require 'sinatra'
require 'sinatra/reloader' if development?

get '/' do
-  'Hello world!'
+  'Hello world!!!!!!'
end
```

Reload browser.

![docker-sinatra-dev-03](http://f.st-hatena.com/images/fotolife/t/tuto0621/20150719/20150719155650.png?1437289106)

## Add new gem

Edit Gemfile and Run `rake gem` command.

```
$ rake gem
```

## Rake commands

```
$ rake -T
rake build  # Build image
rake clean  # Remove image
rake gem    # Update Gemfile.lock
rake run    # Run sinatra app
rake shell  # Run shell
```
