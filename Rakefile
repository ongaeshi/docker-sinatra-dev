NAME = 'sinatra-dev'
CONTAINER_RUBY_VERSION = '2.2.2' # Keep the same value as the Dockerfile

task :default => :run

desc "Run sinatra app"
task :run do
  # Build if it don't exist container
  build_command unless image_exist?(NAME)

  # Run sinatra app
  run_command 'ruby app.rb -o 0.0.0.0'
end

desc "Update Gemfile.lock"
task :gem do
  sh %Q|docker run --rm -v "#{Dir.pwd}":/usr/src/app -w /usr/src/app ruby:#{CONTAINER_RUBY_VERSION} bundle install|
  build_command
end

desc "Run shell"
task :shell do
  build_command unless image_exist?(NAME)
  run_command '/bin/bash'
end

desc "Build image"
task :build do
  build_command
end

desc "Remove image"
task :clean do
  sh %Q|docker rmi #{NAME}| if image_exist?(NAME)
end

# ---

def build_command
  sh %Q|docker build -t #{NAME} .|
end

def run_command(command)
  sh %Q|docker run -itP --rm -v "#{Dir.pwd}":/usr/src/app -w /usr/src/app --name #{NAME} #{NAME} #{command}|
end

def image_exist?(name)
  `docker images -q #{name}` != ""
end
