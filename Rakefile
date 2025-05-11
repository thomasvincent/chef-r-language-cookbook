require 'rspec/core/rake_task'
require 'rubocop/rake_task'
require 'kitchen/rake_tasks'

namespace :style do
  desc 'Run Ruby style checks'
  RuboCop::RakeTask.new(:ruby)

  desc 'Run Chef style checks with Cookstyle'
  task :chef do
    sh 'cookstyle'
  end
end

desc 'Run all style checks'
task style: ['style:chef', 'style:ruby']

desc 'Run ChefSpec examples'
RSpec::Core::RakeTask.new(:spec)

desc 'Run all tests except Kitchen (default task)'
task default: ['style', 'spec']

namespace :integration do
  desc 'Run Test Kitchen with Vagrant'
  task :vagrant do
    Kitchen.logger = Kitchen.default_file_logger
    Kitchen::Config.new.instances.each do |instance|
      instance.test(:always)
    end
  end
end

desc 'Run all tests including kitchen'
task test: ['style', 'spec', 'integration:vagrant']