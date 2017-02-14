# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  
  config.vm.box = "boxcutter/ubuntu1610-desktop"

  config.vm.synced_folder ".", "/vagrant", disabled: false  
  
  config.vm.provider "virtualbox" do |v|
    v.gui = true
    v.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
    v.customize ["modifyvm", :id, "--draganddrop", "bidirectional"]
    v.customize ["modifyvm", :id, "--vram", "256"]
    v.memory = 2048
    v.cpus = 2
  end

  # Fix no tty
  config.vm.provision "fix-no-tty", type: "shell" do |s|
    s.privileged = false
    s.inline = "sudo sed -i '/tty/!s/mesg n/tty -s \\&\\& mesg n/' /root/.profile"
  end

  # Updade system
  config.vm.provision "shell", inline: "sleep 120"
  config.vm.provision "shell", inline: "apt-get update"
  config.vm.provision "shell", inline: "apt-get upgrade -y"
  config.vm.provision "shell", inline: "apt-get dist-upgrade -y"
  config.vm.provision "shell", inline: "apt-get autoremove -y"
  config.vm.provision "shell", inline: "apt-get clean -y"  

  # Setup dev env
  config.vm.provision "shell", privileged: false, inline: "curl -s http://get.sdkman.io | bash"
  config.vm.provision "shell", privileged: false, inline: "source '/home/vagrant/.sdkman/bin/sdkman-init.sh' && yes | sdk install java 8u121"
  config.vm.provision "shell", privileged: false, inline: "source '/home/vagrant/.sdkman/bin/sdkman-init.sh' && yes | sdk install groovy 2.4.8"
  config.vm.provision "shell", privileged: false, inline: "source '/home/vagrant/.sdkman/bin/sdkman-init.sh' && yes | sdk install gradle 3.3"

  # Nodejs
  config.vm.provision "shell", inline: "add-apt-repository ppa:ubuntu-desktop/ubuntu-make -y"
  config.vm.provision "shell", inline: "apt-get update"
  config.vm.provision "shell", inline: "apt install ubuntu-make -y"
  config.vm.provision "shell", privileged: false, inline: "echo 'N' | umake nodejs /home/vagrant/.local/share/umake/nodejs/nodejs-lang"

  # Install Ide  
  config.vm.provision "shell", privileged: false, inline: "echo 'N' | umake ide idea /home/vagrant/.local/share/umake/ide/idea"
  config.vm.provision "shell", privileged: false, inline: "echo 'N' | umake ide eclipse-jee /home/vagrant/.local/share/umake/ide/eclipse-jee"
  config.vm.provision "shell", privileged: false, inline: "echo 'N' | umake ide visual-studio-code /home/vagrant/.local/share/umake/ide/visual-studio-code --accept-license"
  config.vm.provision "shell", privileged: false, inline: "echo 'N' | umake ide lighttable /home/vagrant/.local/share/umake/ide/lighttable"

  # Sublime
  config.vm.provision "shell", inline: "add-apt-repository ppa:webupd8team/sublime-text-3 -y"
  config.vm.provision "shell", inline: "apt-get update"
  config.vm.provision "shell", inline: "apt-get install sublime-text-installer -y"

  # Gitkraken
  config.vm.provision "shell", inline: "wget -nc https://release.gitkraken.com/linux/gitkraken-amd64.deb"
  config.vm.provision "shell", inline: "dpkg -i gitkraken-amd64.deb"

  # Set language
  config.vm.provision "shell", inline: "apt-get install language-pack-pt -y"
  config.vm.provision "shell", inline: "locale-gen pt_BR.UTF-8"
  config.vm.provision "shell", inline: "dpkg-reconfigure --frontend=noninteractive locales"
  config.vm.provision "shell", inline: "update-locale LC_ALL=pt_BR.UTF-8 LANG=pt_BR.UTF-8 LANGUAGE=pt_BR:pt"
  config.vm.provision "shell", inline: "L='br' && sudo sed -i 's/XKBLAYOUT=\"\w*\"/XKBLAYOUT=\"\'$L'\"/g' /etc/default/keyboard"
  config.vm.provision "shell", inline: "M='pc105' && sudo sed -i 's/XKBMODEL=\"\w*\"/XKBMODEL=\"\'$M'\"/g' /etc/default/keyboard"

  # Set timezone
  config.vm.provision "shell", inline: "timedatectl set-timezone America/Sao_Paulo"

  # Reboot
  config.vm.provision "shell", inline: "reboot"

end
