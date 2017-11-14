# kubernetes_canonical_single_machine

Este tutorial irá guiá-lo através da instalação da distribuição da Canonical do Kubernetes em um único host usando [conjure-up](https://conjure-up.io/) em cima de [contêineres LXD](https://linuxcontainers.org/).

Baseado em [tutoriais ubuntu](https://tutorials.ubuntu.com/tutorial/install-kubernetes-with-conjure-up?backURL=%2F&_ga=2.107852226.1958800830.1510430718-2088419650.1510430718#0), com adição de alguns pontos que acredito terem faltado no tutorial da Canonical.

Esse tutorial foi testado no SO Ubuntu 16.04 AMD64 com 16GB de memória RAM.

Primeiramente desinstalar qualquer versão do LXD do repositório:
```sh
sudo apt remove --purge lxd lxd-client
```

Adicionar o usuário lxd:
```sh
sudo groupadd --system lxd
```

Adicionar o usuário desejado ao grupo lxd:
```sh
sudo usermod -G lxd -a user
```

Instalar o lxd via snap (não via repositório):  
```sh
sudo snap install lxd
```

Execute o newgroup:
```sh
newgrp lxd
```

**Fazer logout e logar novamente na sessão do usuário (se estiver via ssh, só sair e conectar novamente)**:

Inicie o LXD:
```sh
/snap/bin/lxd init --auto
```

Crie uma rede:
```sh
/snap/bin/lxc network create lxdbr0 ipv4.address=auto ipv4.nat=true ipv6.address=none ipv6.nat=false
```

Instale o conjure-up:
```sh
sudo snap install conjure-up --classic
```

Execute o conjure-up:
```sh
conjure-up canonical-kubernetes
```

Escolha a opção localhost, a rede criada anteriormente (lxdbr0), a senha de sudo e "Deploy all 6 Remaining Applications".
Esse procedimento é bastante demorado dependendo do hardware utilizado.

 
