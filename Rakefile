require "spec"
require "spec/rake/spectask"
require './lib/typhoeus.rb'
require 'rake/extensiontask'

begin
  require 'jeweler'
  jeweler_tasks = Jeweler::Tasks.new do |gemspec|
    gemspec.name = "typhoeus"
    gemspec.summary = "A library for interacting with web services (and building SOAs) at blinding speed."
    gemspec.description = "Like a modern code version of the mythical beast with 100 serpent heads, Typhoeus runs HTTP requests in parallel while cleanly encapsulating handling logic."
    gemspec.email = "paul@pauldix.net"
    gemspec.homepage = "http://github.com/pauldix/typhoeus"
    gemspec.authors = ["Paul Dix"]
    gemspec.add_dependency "rack"
    gemspec.add_development_dependency "rspec"
    gemspec.add_development_dependency "jeweler"
    gemspec.add_development_dependency "diff-lcs"
    gemspec.add_development_dependency "sinatra"
    gemspec.add_development_dependency "json"
    gemspec.files.include('.')
    gemspec.files.exclude('tmp')
  end

  $gemspec         = jeweler_tasks.gemspec
  $gemspec.version = jeweler_tasks.jeweler.version

  Jeweler::GemcutterTasks.new
rescue LoadError
  puts "Jeweler not available. Install it with: gem install jeweler"
end

Rake::GemPackageTask.new($gemspec) do |pkg|
end

Rake::ExtensionTask.new('native', $gemspec) do |ext|
  ext.lib_dir = "lib/typhoeus"
  ext.ext_dir = "ext/typhoeus"
end

CLEAN.include 'lib/**/*.so'

Spec::Rake::SpecTask.new do |t|
  t.spec_opts = ['--options', "\"#{File.dirname(__FILE__)}/spec/spec.opts\""]
  t.spec_files = FileList['spec/**/*_spec.rb']
end

task :install do
  rm_rf "*.gem"
  puts `gem build typhoeus.gemspec`
  puts `sudo gem install typhoeus-#{Typhoeus::VERSION}.gem`
end

desc "Run all the tests"
task :default => :spec
