CONTAINER_RUBY_VERSION = '2.2.2' # Keep the same value as the Dockerfile

task :default => :run

desc "Run sinatra app"
task :run do
  # Build if it don't exist container
  build_command unless image_exist?('sinatra-dev')

  # Run sinatra app
  run_command 'ruby app.rb -o 0.0.0.0'
end

desc "Update Gemfile.lock"
task :gem do
  sh %Q|docker run --rm -v "$PWD":/usr/src/app -w /usr/src/app ruby:#{CONTAINER_RUBY_VERSION} bundle install|
  build_command
end

desc "Run shell"
task :shell do
  run_command '/bin/bash'
end

desc "Build image"
task :build do
  build_command
end

desc "Remove image"
task :clean do
  sh %Q|docker rmi sinatra-dev|
end

# ---

def build_command
  sh %Q|docker build -t sinatra-dev .|
end

def run_command(command)
  # Use Ruby's pwd
  sh %Q|docker run -itP --rm -v "$PWD":/usr/src/app -w /usr/src/app sinatra-dev #{command}|
end

def image_exist?(name)
  `docker images -q #{name}` != ""
end
