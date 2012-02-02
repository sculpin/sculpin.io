
require 'yaml'

def ok_failed(condition)
  if (condition)
    puts "OK"
  else
    puts "FAILED"
  end
end

dumped_config = ".sculpin.yml.dumped"

# Dump the sculpin configuration to a single merged configuration file.
ok_failed system "sculpin configuration:dump --to #{dumped_config} --force"

# Parse the dumped config.
config = YAML::load(File.open(dumped_config))

# Preview stuff is just for this style of Rakefile
# managed site. We generate the preview in a
# non-standard destination.
preview_root          = config['preview_destination']
preview_url           = config['preview_url']

# The deploy root is the usual Sculpin destination
# path.
deploy_root           = config['destination']

desc "Deploy site"
task :deploy do

  deploy_ssh_target     = config['deploy']['ssh']['target']
  begin
    deploy_ssh_port       = config['deploy']['ssh']['port']
  rescue
    deploy_ssh_port       = 22
  end
  deploy_remote_path    = config['deploy']['remote_path']

  ok_failed system "sculpin generate --destination=#{deploy_root}"
  ok_failed system "rsync -avze 'ssh -p #{deploy_ssh_port}' #{deploy_root}/ #{deploy_ssh_target}:#{deploy_remote_path}"

end

desc "Preview site locally"
task :preview do
    system "sculpin generate --watch --url=#{preview_url} --destination=#{preview_root}"
end
