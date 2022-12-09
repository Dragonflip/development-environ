<h1 align="center">
📄<br>README Ambiente de desenvolvimento
</h1>

## Arquivos de configuração

[![Perfil](https://img.shields.io/badge/perfil%20-%23323330.svg?&style=for-the-badge&logo=perfil&logoColor=black&color=F745B5)](https://github.com/Dragonflip)
[![Repositório](https://img.shields.io/badge/repositório%20-%23323330.svg?&style=for-the-badge&logo=repositório&logoColor=black&color=8000FF)](https://github.com/Dragonflip/development-environ)



---
## Configurando ambiente 
### Instalando Vagrant e Virtualbox


#### **Obs:** para usuários de windows pode-se instalar o chocolatey com o seguinte comando.
```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

#### Pode-se instalar o Virtualbox utilizando os seguintes comandos:
```
paru -S virtualbox                # Arch
choco install virtualbox          # Windows
sudo apt-get install virtualbox   # Ubuntu
```

#### Pode-se instalar o Vagrant utilizando os seguintes comandos:
```
paru -S vagrant           # Arch
choco install vagrant     # Windows
sudo apt install vagrant  # Ubuntu
```
---
## Subindo maquinas virtuais
### Utilizando a combinação Vagrant + Virtualbox
#### Para subir as máquinas utilizando o Vagrant podemos executar o seguinte comando (garantindo que a execução do comando esteja no mesmo diretório do arquivo [Vagrantfile](https://github.com/Dragonflip/development-environ/Vagrantfile))
```
vagrant up
```

#### Para utilizar o ansible precisamos saber o ip da máquina de desenvolvimento, para isto podemos executar o seguinte comando:
```
vagrant ssh arch -c "ip addr"
```
#### O resultado deverá ser algo do tipo:
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:54:1c:12 brd ff:ff:ff:ff:ff:ff
    altname enp0s3
    inet 10.0.2.15/24 metric 1024 brd 10.0.2.255 scope global dynamic eth0
       valid_lft 73521sec preferred_lft 73521sec
    inet6 fe80::a00:27ff:fe54:1c12/64 scope link
       valid_lft forever preferred_lft forever
3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:2b:4f:97 brd ff:ff:ff:ff:ff:ff
    altname enp0s8
    inet >>192.168.1.17/24<< metric 1024 brd 192.168.1.255 scope global dynamic eth1
       valid_lft 7030sec preferred_lft 7030sec
    inet6 2804:29b8:50cf:453b:a00:27ff:fe2b:4f97/64 scope global dynamic mngtmpaddr noprefixroute
       valid_lft 259199sec preferred_lft 172799sec
    inet6 fe80::a00:27ff:fe2b:4f97/64 scope link
       valid_lft forever preferred_lft forever
Connection to 127.0.0.1 closed.
```
---
## Configurando as maquinas com Ansible
### para configurar as maquinas com ansible é necessário indicar o ip das máquinas a serem controladas, nesse caso a máquina de desenvolvimento
#### Para entrar na maquina master utilizamos o seguinte comando:
```
vagrant ssh ansible_main
```
#### Para gerar a chave ssh e copiar o id dessa chave na maquina de desenvolvimento utilizamos o seguinte comando:
```
ssh-keygen
ssh-copy-id vagrant@192.168.1.17
echo $'[dev]\n192.168.1.17'>/etc/ansible/hosts
```
---
## Executando o playbook com ansible
#### Para configurar a maquina de desenvolvimento precisamos apenas baixar os arquivos deste repositorio, instalar as dependencias do ansible-galaxy e executar o ansible-playbook
```
git clone https://github.com/Dragonflip/development-environ.git
cd development-environ/playbook
ansible-galaxy role install -r requirements.yml
ansible-playbook play_tasks.yml
```
---

## 🍜 Licença

Esse projeto está sob licença. Veja o arquivo [LICENÇA](LICENSE.md) para mais detalhes.<br>
