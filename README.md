# Introdução ao Vagrant
## O que é o Vagrant?
- Ferramenta de código aberto para criação e gerenciamento de ambientes de desenvolvimento e produção;

- Desenvolvido pela HashiCorp;

- Baseado em linha de comando.


## A ideia por trás do Vagrant: 
- Provisionar máquinas virtuais com todo o ambiente necessário para testar sua aplicação sem que você faça isso manualmente.

## Problemas de configuração de ambiente
- Diferenças entre ambientes de desenvolvimento e produção;

- Configuração manual propensa a erros;

- Incompatibilidade entre configurações de equipe.

## Como o Vagrant funciona?
- Arquivo de configuração (Vagrantfile)

- Fornecedores (providers) - VirtualBox, VMware, Hyper-V, etc.

- Boxes (caixas) - Imagens de máquinas virtuais pré-configuradas

## Pré-requisitos (Instalação)
- Certifique-se de que o VirtualBox e o Vagrant estejam instalados em sua máquina host;

- VirtualBox: Instale o software a partir do site oficial;

- Vagrant: Instale o software a partir do site oficial.

## Configurando o Projeto Vagrant
- Crie um novo diretório para o seu projeto e inicialize o Vagrant:
  - Crie e navegue para o diretório do projeto:

      ```bash
            mkdir ubuntu-server-2510
            cd ubuntu-server-2510
    ``` 

- Inicialize o Vagrant usando a box para Ubuntu 25.10. Vou usar a box mencionada nos resultados da pesquisa:
  ```bash
    vagrant init alvistack/ubuntu-25.10
  ```
Isso criará o arquivo de configuração principal, o Vagrantfile, nesse diretório.

- Ajustando o Vagrantfile (Opcional, mas Recomendado) Edite o arquivo Vagrantfile que foi criado. Por padrão, ele usará a box especificada. Você pode adicionar configurações de rede, memória e provisionamento neste arquivo.

```bash
RubyVagrant.configure("2") do |config|
  # Define a box que será utilizada
  config.vm.box = "alvistack/ubuntu-25.10"

  # Define o nome da sua VM no VirtualBox
  config.vm.hostname = "ubuntu-2510-server"

  # Configurações do VirtualBox Provider
  config.vm.provider "virtualbox" do |vb|
    # Define a quantidade de RAM (ex: 2048 MB = 2 GB)
    vb.memory = "2048"
    # Define o número de CPUs
    vb.cpus = "2"
    # Desabilita a interface gráfica
    vb.gui = false
  end
  
  # Exemplo de rede privada (Host-Only)
  # Acesso via SSH para o IP: 192.168.56.10
  # config.vm.network "private_network", ip: "192.168.56.10"

  # ⚙️ Provisionamento (Automação de Configuração)
  # Este é o passo chave para *automatizar* a instalação de software/configurações
  # Você pode usar um script shell, Ansible, Chef, Puppet, etc.
  
  # Exemplo de provisionamento com Shell:
  # config.vm.provision "shell", inline: <<-SHELL
  #   echo "Instalando Nginx..."
  #   sudo apt update
  #   sudo apt install -y nginx
  #   echo "Nginx instalado."
  # SHELL
end
```

## Inicializando a VM
- Execute o comando principal no Bash ``` vagrant up ``` para iniciar o processo automatizado. O Vagrant fará o seguinte:
   - Baixar a box (alvistack/ubuntu-25.10) se ainda não estiver em cache;
   - Criar a VM no VirtualBox com base na box e nas configurações do Vagrantfile; 
   - Executará quaisquer scripts de Provisionamento definidos; 
   - Por fim, Subirá e iniciará a VM.

## Acessando a VM 
- Após o processo ``` vagrant up ``` ser concluído com sucesso, você pode acessar a máquina virtual via SSH, usando ``` vagrant ssh ```.

## Comandos Úteis do VagrantComandoDescrição


- ``` vagrant status ``` - Mostra o estado atual da sua VM;
- ``` vagrant reload ``` - Reinicia a VM, aplicando alterações no Vagrantfile;
- ``` vagrant halt ``` - Desliga a VM;
- ``` vagrant suspend ``` - Suspende a VM (salva o estado, mais rápido para voltar);
- ``` vagrant destroy ``` -  Remove a VM e todos os seus recursos do VirtualBox.
