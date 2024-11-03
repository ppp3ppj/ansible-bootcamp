Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu2204"

  username = "vagrant"
  branch = "main"

  config.ssh.username = username
  config.ssh.password = 'vagrant'
  config.ssh.insert_key = 'true'

  config.vm.provider 'virtualbox' do |vb|
    #v.gui = true
    vb.memory = '2048'
    vb.cpus = 2
  end

#  config.vm.provision "shell", inline: <<-SHELL
#     apt-get update
     #apt-get upgrade -y
     #curl -o- https://raw.githubusercontent.com/ppp3ppj/ansible-bootcamp/main/resources/setup | bash
  #   chown -R #{username}:#{username} /home/#{username}/ansible-bootcamp
  # SHELL
  #config.vm.provision :shell, inline: "sudo apt upgrade -y"
  config.vm.provision "shell", inline: <<-SHELL
     set -euo pipefail
     apt-get update
     apt-get upgrade -y
     apt-get install -y software-properties-common git make

     # Clone the repository with a specified branch
     REPO_URL="https://github.com/ppp3ppj/ansible-bootcamp"
     BRANCH="#{branch}"
     CLONE_DIR="/home/#{username}/ansible-bootcamp"

     if [ ! -d "$CLONE_DIR" ]; then
         git clone --branch "$BRANCH" "$REPO_URL" "$CLONE_DIR"
     else
         echo "Repository already cloned in $CLONE_DIR"
         cd "$CLONE_DIR" && git fetch && git checkout "$BRANCH" && git pull
     fi

     # Run the setup script from the cloned repository
     # bash "$CLONE_DIR/resources/setup"

     chown -R #{username}:#{username} "$CLONE_DIR"
   SHELL
end
