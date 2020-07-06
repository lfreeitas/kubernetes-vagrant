# 0. Instalar (ou atualizar) dependencias

## OSX com homebrew (https://brew.sh/)

~~~bash
brew cask upgrade virtualbox vagrant packer
~~~

ou

~~~bash
brew cask install virtualbox vagrant packer
~~~

## Windows com chocolatey

~~~bash
choco upgrade virtualbox vagrant packer
~~~

ou

~~~bash
choco install virtualbox vagrant packer
~~~

## Linux, FreeBSD, OpenBSD, outros

Você deve saber o que está fazendo. Mas aqui seguem alguns links para ajudar:

- https://www.virtualbox.org/wiki/Downloads
- https://www.vagrantup.com/downloads.html
- https://learn.hashicorp.com/packer/getting-started/install#installing-packer

# 1. Construindo as imagens com Packer

Acessar a pasta packer:

~~~bash
cd packer/
~~~

Para cada box rodar o respectivo comando e aguardar. Uma janela do virtualbox vai abrir mas ignore ela.

~~~bash
packer build -parallel-builds=1 k8s-docker.json
packer build -parallel-builds=1 k8s-containerd.json
packer build -parallel-builds=1 k8s-crio.json
~~~

# 2. Adicionar as criadas ao Vagrant

Basta rodar os respectivos comandos de acordo com o nome do tipo de contêiner.

~~~bash
vagrant box add output/k8s-docker-virtualbox.box --name wsilva/k8s-docker-virtualbox --provider virtualbox --force

vagrant box add output/k8s-containerd-virtualbox.box --name wsilva/k8s-containerd-virtualbox --provider virtualbox --force

vagrant box add output/k8s-crio-virtualbox.box --name wsilva/k8s-crio-virtualbox --provider virtualbox --force
~~~

>Atenção ao nome da Box `wsilva/k8s-...`, se quiser alterar para seu nome então também deve ser alterado no `Vagrantfile`.