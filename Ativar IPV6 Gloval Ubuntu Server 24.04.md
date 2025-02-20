
# Ativar IPV6 Global em um instância Ubuntu Server 24.04 LTS

Navegue até o diretório:

```bash
  cd /etc/netplan/
```

Crie o arquivo e o abra:

```bash
  sudo nano 00-interfaces.yaml
```

Com o arquivo aberto no edito do Linux, cole o código abaixo:

```bash
  network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s6:
      dhcp4: true
      dhcp6: no
      addresses:
        - 2a07:85ff:0:1234::2/64
      accept-ra: true
      nameservers:
        addresses:
          - 1.1.1.1
          - 8.8.8.8
          - 2606:4700:4700::1111
          - 2001:4860:4860::8888
      routes:
        - to: default
          via: 2a07:85ff::1
          metric: 1
          on-link: true
```

Depois de salvar o arquivo, aplique as configurações:

```bash
  sudo netplan apply
```

Depois de aplicar as configurações, verifique se seu IPV6 Global foi configurado corretamente

```bash
  ip -6 addr show
```
