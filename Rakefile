require 'rake'
require 'rake/clean'
require 'rake/testtask'

CLEAN.include('**/*.gem', '**/*.rbc', '**/*.rbx')

desc "Run the test suite"
Rake::TestTask.new("test") do |t|
  if File::ALT_SEPARATOR
    t.libs << 'lib/windows'
  else
    t.libs << 'lib/unix'
  end

  t.warning = true
  t.verbose = true
  t.test_files = FileList['test/test_sys_filesystem.rb']
end

desc "Run the example program"
task :example do |t|
  sh "ruby -Ilib -Ilib/unix -Ilib/windows examples/example_stat.rb"
end

namespace :gem do
  desc "Build the sys-filesystem gem"
  task :create do |t|
    spec = eval(IO.read('sys-filesystem.gemspec'))
    if Gem::VERSION >= "2.0.0"
      require 'rubygems/package'
      Gem::Package.build(spec)
    else
      Gem::Builder.new(spec).build
    end
  end

  desc "Install the sys-filesystem gem"
  task :install => [:create] do
    file = Dir['*.gem'].first
    sh "gem install #{file}"
  end
end

task :default => :test
