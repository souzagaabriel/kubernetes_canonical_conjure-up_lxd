# kubernetes_canonical_conjure-up_lxd

Baseado em [tutoriais ubuntu](https://tutorials.ubuntu.com/tutorial/install-kubernetes-with-conjure-up?backURL=%2F&_ga=2.107852226.1958800830.1510430718-2088419650.1510430718#0), com adição de alguns pontos que acredito terem faltado no tutorial básico da Canonical.

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
conjure-up
```

Escolha a opção "The Canonical Distribution of Kubernetes
" e ... Esse procedimento é bastante demorado dependendo do hardware utilizado.

![Conjure-up](conjure-up.png)
 
