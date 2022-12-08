Vagrant.configure("2") do |config|

  config.vm.define "main" do |main|
    main.vm.box = "archlinux/archlinux"
    main.vm.network = "publick_network"

    main.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.name = "ansible_main"
    end

    main.vm.provision "shell", inline: <<-SHEL
      pacman -Syu --noconfirm
      pacman -S ansible --noconfirm
    SHELL
  end

  config.vm.define "arch" do |arch|
    arch.vm.box = "archlinux/archlinux"
    arch.vm.network = "publick_network"

    arch.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.name = "ansible_development
    end

    arch.vm.provision "shell", inline: <<-SHEL
      pacman -Syu --noconfirm
    SHELL
  end

end
