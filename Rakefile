desc 'Run portable unit tests with RSpec'
task :unit do
  sh('bundle exec rspec --require rspec/legacy_formatters -r yarjuf -f JUnit -o result.xml spec/unit')
end

desc 'Run integration tests against the local machine with RSpec'
task :integration do
  sh('bundle exec rspec --require rspec/legacy_formatters -r yarjuf -f JUnit -o result.xml spec/integration')
end

desc 'Run remote acceptance tests with RSpec and Beaker'
task :acceptance do
  sh('mkdir -p junit/latest')
  sh('bundle exec rspec --require rspec/legacy_formatters -r yarjuf -f JUnit -o junit/latest/result.xml spec/acceptance')
end

desc 'Run a little bit of this and a little bit of that'
namespace :ci do
  task :spec => [:unit, :integration]
end

desc 'Create nodeset in default location from TEST_TARGET env var'
task :nodeset do
  require 'beaker-hostgenerator'

  target = ENV['TEST_TARGET']
  cli = BeakerHostGenerator::CLI.new([target, '--disable-default-role', '--osinfo-version', '1'])
  nodeset = 'spec/acceptance/nodesets/default.yml'
  File.open(nodeset, 'w') do |fh|
    fh.print(cli.execute)
  end
end
