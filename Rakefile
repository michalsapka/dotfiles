#!/usr/bin/ruby

require 'rake'
require 'yaml'

task :install do
  tasks = YAML.load_file("config/config.yml")
  tasks["tasks"].each do |task|
   perform_task task
  end
end

def perform_task(task)
  puts "-" * 50
  puts " #{task["info"]}"
  case task["type"]
  when "symlink"
    create_symlink(task["source"], task["destination"])
  else
    raise " Unknown task type"
  end
end

def create_symlink(source, destination)
  if create_file?(destination)
    puts " Creating symlink..."
    `ln -s #{current_dir}/#{source} #{destination}`
  else
    puts " Skipping tak..."
  end
end

def create_file?(file)
  file_exists = File.file?(File.expand_path file)
  create = true
  if file_exists
    create = false
    puts " File #{file} exists. Remove? (Y/N)"
    if STDIN.gets.strip.downcase == "y"
      puts " Deleting old file..."
      remove_file = true
    end
  end

  if remove_file
    `rm #{file}`
    create = true
  end

  create
end

def current_dir
  File.expand_path File.dirname(__FILE__)
end
