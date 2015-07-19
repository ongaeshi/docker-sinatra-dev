task :default => :run

task :build do
  sh %Q|docker build -t sinatra-dev .|
end

task :clean do
  sh %Q|docker rm sinatra-dev|
end

task :run do
  # Build if it don't exist container
  run_command 'ruby app.rb -o 0.0.0.0'
end

task :shell do
  run_command '/bin/bash'
end

def run_command(command)
  # Use Ruby's pwd
  sh %Q|docker run -itP --rm -v "$PWD":/usr/src/app -w /usr/src/app sinatra-dev #{command}|
end
