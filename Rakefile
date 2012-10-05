require "bundler/gem_tasks"
require 'rake/testtask'

task :default => :test

desc "Compile extension"
task :compile do
  path = File.expand_path("ext/cld/cld.so", File.dirname(__FILE__))

  if !File.exists?(path) || ENV['RECOMPILE']
    puts "Compiling extension..."
    `cd #{File.expand_path("ext/cld/")} && make`
  else
    puts "Extension already compiled. To recompile set env variable RECOMPILE=true."
  end
end

Rake::TestTask.new(:test) do |test|
  Rake::Task["compile"].invoke

  test.libs << 'lib' << 'test'
  test.test_files = FileList['test/*_test.rb']
  test.verbose = true
end
