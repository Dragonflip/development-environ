Vagrant.configure("2") do |config|

  config.vm.define "ansible_main" do |main|

    main.vm.box = "archlinux/archlinux"
    main.vm.network "public_network", use_dhcp_assigned_default_route: true#, bridge: "wlp2s0"

    main.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.name = "ansible_main"
    end

    main.vm.provision "shell", inline: <<-SHELL
      pacman -Syu --noconfirm
      pacman -S ansible git --noconfirm
    SHELL

  end

  config.vm.define "arch" do |arch|
    arch.vm.box = "archlinux/archlinux"
    arch.vm.network "public_network", use_dhcp_assigned_default_route: true#, bridge: "wlp2s0"

    arch.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
    end

    arch.vm.provision "shell", inline: <<-SHELL
      pacman -Syu --noconfirm
    SHELL
  end

end
