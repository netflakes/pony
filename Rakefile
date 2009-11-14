require 'rake'
require 'spec/rake/spectask'

desc "Run all specs"
Spec::Rake::SpecTask.new('spec') do |t|
	t.spec_files = FileList['spec/*_spec.rb']
end

desc "Print specdocs"
Spec::Rake::SpecTask.new(:doc) do |t|
	t.spec_opts = ["--format", "specdoc", "--dry-run"]
	t.spec_files = FileList['spec/*_spec.rb']
end

desc "Run all examples with RCov"
Spec::Rake::SpecTask.new('rcov') do |t|
	t.spec_files = FileList['spec/*_spec.rb']
	t.rcov = true
	t.rcov_opts = ['--exclude', 'examples']
end

task :default => :spec

######################################################

require 'rake'
require 'rake/testtask'
require 'rake/clean'
require 'rake/gempackagetask'
require 'fileutils'

version = "0.4"
name = "pony"

spec = Gem::Specification.new do |s|
	s.name = name
	s.version = version
	s.summary = "Send email in one command: Pony.mail(:to => 'someone@example.com', :body => 'hello')"
	s.description = "Send email in one command: Pony.mail(:to => 'someone@example.com', :body => 'hello')"
	s.author = "Adam Wiggins, maint: Ben Prew"
	s.email = "ben.prew@gmail.com"
	s.homepage = "http://github.com/benprew/pony"
	s.rubyforge_project = "pony"

	s.platform = Gem::Platform::RUBY
	s.has_rdoc = false

	s.files = %w(Rakefile) + Dir.glob("{lib,spec}/**/*")

	s.require_path = "lib"
	s.add_dependency( 'tmail', '~> 1.0' )
end

Rake::GemPackageTask.new(spec) do |p|
	p.need_tar = true if RUBY_PLATFORM !~ /mswin/
end

task :install => [ :package ] do
	sh %{sudo gem install pkg/#{name}-#{version}.gem}
end

task :uninstall => [ :clean ] do
	sh %{sudo gem uninstall #{name}}
end

Rake::TestTask.new do |t|
	t.libs << "spec"
	t.test_files = FileList['spec/*_spec.rb']
	t.verbose = true
end

CLEAN.include [ 'pkg', '*.gem', '.config' ]

