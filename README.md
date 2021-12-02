Laboratório 4528 - Devops: Práticas de Continuos Monitoring para uma Infraestrutura Ágil
=============================

Repositório para armazenar o Laboratório do curso Devops: Práticas de Continuos Monitoring para uma Infraestrutura Ágil da [4Linux][1]

Dependências
------------

Para a criação do laboratório é necessário ter pré instalado os seguintes softwares:

* [Git][2]
* [VirtualBox][3]
* [Vagrant][4]

> Para as máquinas com Windows aconselhamos que as instalações, provisionamento e execução de comandos sejam feitos pelo  **[Cygwin][5]**. Caso você opte por outro cmd ou gerenciador git, como o **[gitforwindows][10]**, antes de iniciar o provisionamento, execute o comando `git config --global core.autocrlf false` para evitar quebras de linhas.

> Para as máquinas com Windows, é necessário que o [Hyper-V][9] esteja `desabilitado`.

> Para as máquinas com MAC OS aconselhamos que as instalações sejam feitas pelo gerenciador de pacotes **brew**.

Laboratório
-----------

O Laboratório será criado utilizando o [Vagrant][6]. Ferramenta para criar e gerenciar ambientes virtualizados (baseado em Inúmeros providers) com foco em automação.

Nesse laboratório, que está centralizado no arquivo [Vagrantfile][7], sera criada 1 maquina com a seguinte característica:

Nome       | vCPUs | Memoria RAM | IP            | S.O.¹           
---------- |:-----:|:-----------:|:-------------:|:---------------:
zabbix     | 1     | 1024MB | 192.168.99.10 | ubuntu/bionic64
prometheus      | 1     | 1024MB | 192.168.99.11 | centos/7
4flix      | 1     | 1024MB | 192.168.99.12 | centos/7
graylog      | 1     | 1024MB | 192.168.99.13 | ubuntu/bionic64

>  Esses Sistemas operacionais estão sendo utilizado no formato de Boxes, é a forma como o vagrant chama as imagens do sistema operacional utilizado.
>  A memória inicial de cada VM está definida com 1024MB (1GB). Este valor pode ser aumentado, caso necessário através do arquivo `Vagrantfile`.

Criação do Laboratório
----------------------

Para criar o laboratório é necessário fazer o `git clone` desse repositório e, dentro da pasta baixada realizar a execução do `vagrant up`, conforme abaixo:

```bash
git clone https://github.com/4linux/4528
cd 4528/
vagrant up
```

Utilização
----------

Todos os comandos devem ser utilizados dentro do diretório clonado.

Para listar as máquinas:

```bash
vagrant status
```

Para entrar em uma máquina:

```bash
vagrant ssh <machine>
```

Para iniciar todas as máquinas:

```bash
vagrant up
```

Para salvar o estado de todas as máquinas:

```bash
vagrant suspend
```

Retomar as máquinas suspensas:

```bash
vagrant resume
```

Para desligar todas as máquinas:

```bash
vagrant halt
```

Dicas
-----

Opcionalmente, para a agilidade no processo de religar as VMs, você pode apenas efetuar o `vagrant suspend/resume` da VM após terminar sua utilização em determinado período, tendo em vista que o comando `vagrant up` realiza algumas verificações que podem demorar.

> Em caso de erro na criação das máquinas sempre valide se sua conexão está boa, os logs de erros na tela e, se necessário, o arquivo **/var/log/vagrant_provision.log** dentro da máquina que apresentou a falha.

Por fim, abaixo há alguns comandos básicos do vagrant para a gerencia das máquinas virtuais.

Comandos                | Descrição
:----------------------:| ---------------------------------------
`vagrant init`          | Gerar o VagrantFile
`vagrant box add <box>` | Baixar a  imagem do sistema
`vagrant box status`    | Verificar o status dos boxes criados
`vagrant up`            | Criar/Ligar as VMs baseado no VagrantFile
`vagrant provision`     | Provisionar mudanças logicas nas VMs
`vagrant status`        | Verificar se VM estão ativas ou não.
`vagrant ssh <vm>`      | Acessar a VM
`vagrant ssh <vm> -c <comando>` | Executa comando via ssh
`vagrant reload <vm>`   | Reiniciar a VM carregando uma nova configuração aplicada no Vagrantfile
`vagrant halt`          | Desligar as VMs

> Para maiores informações acesse a [Documentação do Vagrant][8]

[1]: https://4linux.com.br
[2]: https://git-scm.com/downloads
[3]: https://www.virtualbox.org/wiki/Downloads
[4]: https://www.vagrantup.com/downloads
[5]: https://cygwin.com/install.html
[6]: https://www.vagrantup.com/
[7]: ./Vagrantfile
[8]: https://www.vagrantup.com/docs
[9]: https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/about/
[10]: https://gitforwindows.org/