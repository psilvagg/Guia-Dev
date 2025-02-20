
# Hospedando um site no Ubuntu Server 24.04 LTS

Conecte-se na instância via SSH

```bash
  ssh -i suachaveprivada.key usuario@ip.da.instância
```
- Observação: A chave privada deve estar do mesmo diretório em que CMD é executado.

Mude para o usuário root 

```bash
  sudo su
```

Atualize o Sistema operacional

```bash
  sudo apt update -y && sudo apt upgrade -y
```

Baixe e instale o Apache2

```bash
  sudo apt install apache2 -y
```

Baixe e instale o serviço UFW

```bash
  sudo apt install ufw -y
```

Após a conclusão da instalação, será necessário liberar as portas para o serviço do Apache no Firewall. O comando abaixo irá listar os metodos correspondentes a cada protocolo (HTTP e HTTPS).

```bash
  sudo ufw app list
```

A saída deve ser algo como:

![image](https://github.com/user-attachments/assets/61312305-e523-4c71-86a4-ad26b30e9e21)



Você deve selecionar uma das opções abaixo para continuar:
- Apache: Abre apenas a porta 80 (HTTP)
- Apache Full: Abre a porta 80 (HTTP) e a porta 443 (HTTPS)
- Apache Secure: Abre apenas a porta 443 (HTTPS)

```bash
  sudo ufw allow in "Apache Full"
```

Abra também a porta SSH

```bash
  sudo ufw allow in "OpenSSH"
```

Ative o serviço do Firewall

```bash
  sudo ufw enable
```

Reinicie o Sistema para aplicar as alterações

```bash
  sudo reboot
```
- Observação: Após a inicialização do sistema você pode acessar o iP público da instância e verá a página padrão do Apache2.

- Caso não esteja aparecendo nada, verifique se o Apache está rodando:

```bash
  sudo systemctl status apache2
```

Se o Apache não estiver rodando, execute:

```bash
  sudo systemctl start apache2
```

## Instalando MySQ e PHP

Baixe e instale o MySQL Server

```bash
  sudo apt install mysql-server
```

Em seguinda execute o comando a seguir para definição de senha para o usuário ROOT

```bash
  ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'SUA-SENHA';
```

Após alteração, saia do prompt do MySQL

```bash
  exit
```

Baixe e instale o PHP

```bash
  sudo apt install php libapache2-mod-php php-mysql
```

Quando a instalação estiver concluída, execute o seguinte comando para confirmar sua versão do PHP:

```bash
  php -v
```

O sistema deve retornar algo como:

```bash
PHP 8.1.2 (cli) (built: Mar  4 2022 18:13:46) (NTS)
Copyright (c) The PHP Group
Zend Engine v4.1.2, Copyright (c) Zend Technologies
    with Zend OPcache v8.1.2, Copyright (c), by Zend Technologies
```