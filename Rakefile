# frozen_string_literal: true

require 'rspec/core/rake_task'

namespace :test do
  namespace :spec do
    desc 'Run spec tests'
    RSpec::Core::RakeTask.new(:run) do |t|
      t.rspec_opts = ['--color']
      t.pattern = 'spec/'
    end
  end
end

desc 'run static analysis with rubocop'
task(:rubocop) do
  require 'rubocop'
  cli = RuboCop::CLI.new
  exit_code = cli.run(%w[--display-cop-names --format simple])
  raise 'RuboCop detected offenses' if exit_code != 0
end

# namespace-named default tasks.
# these are the default tasks invoked when only the namespace is referenced.
# they're needed because `task :default` in those blocks doesn't work as expected.
task 'test:spec' => 'test:spec:run'
task 'test:acceptance' => 'test:acceptance:quick'

# global defaults
task test: 'test:spec'
task default: :test
