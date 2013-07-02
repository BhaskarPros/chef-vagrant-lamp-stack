Vagrant.configure("2") do |config|
  config.vm.box = "precise32"
  config.vm.box_url = "http://files.vagrantup.com/precise32.box"
  config.vm.network :forwarded_port, guest: 80, host: 8080

  config.vm.provision :shell, :inline => "apt-get clean; apt-get update" 

  config.vm.provision :chef_solo do |chef|

    chef.json = {
      "apache" => {
        "default_site_enabled" => false
      },
      "mysql" => {
      "server_root_password" => "blahblah",
      "server_repl_password" => "blahblah",
      "server_debian_password" => "blahblah"
      },
      "mysite" => {
        "name" => "My AWESOME site",
        "web_root" => "/var/www/mysite",
        "database" => "great_cartoons"
      }
    }

    chef.cookbooks_path = ["cookbooks","site-cookbooks"]
    chef.add_recipe "mysql::server"
    chef.add_recipe "mysite"
  end
end