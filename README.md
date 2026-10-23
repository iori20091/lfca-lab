# Laboratório LFCA - Fundamentos e Instalação

Este diretório contém as evidências e o passo a passo da configuração inicial do ambiente e instalação do sistema operacional com particionamento manual, como parte dos estudos para a certificação LFCA.

## Etapa 0: Preparação do Ambiente

**Objetivo (1h):** Preparar o hipervisor, baixar as imagens e criar a máquina virtual de teste.

- [ ] **1. Hipervisor:** Instalação do VirtualBox (ou KVM/virt-manager).
- [ ] **2. Imagens (ISOs):** Download do Ubuntu Server 24.04 LTS e Rocky Linux 9 (Minimal ou DVD).
- [ ] **3. Criação da VM:** 
  - **Especificações:** 2 vCPUs, 2 GB de RAM e disco de 25 GB.
  - **Sistema:** Habilitar EFI (para simular o boot de um servidor real).
- [ ] **4. Repositório:** Criação do repositório `lfca-lab` no GitHub e da estrutura de pastas `01-fundamentos/1.1-instalacao`.

 **Evidência:** 
*(Adicione aqui o link ou a imagem do print da VM criada e do repositório vazio)*
`![Print da VM](caminho/para/imagem.png)`

---

## Etapa 1: Instalação do Ubuntu com Particionamento Manual

**Objetivo (2h):** Instalar o Ubuntu Server configurando o layout de armazenamento customizado (*Custom storage layout*).

### Layout de Disco Configurado

| Ponto de montagem | Tamanho | Sistema de arquivos |
| :--- | :--- | :--- |
| `/boot/efi` | 512 MB | FAT32 (ESP) |
| `/boot` | 1 GB | ext4 |
| `/` (raiz) | 12 GB | ext4 |
| `/home` | 6 GB | ext4 |
| `swap` | 2 GB | swap |

*Nota: Durante a instalação, o OpenSSH server foi marcado para instalação e um usuário comum foi criado (sem uso direto do root).*

### Validação Pós-Instalação

Para validar se o particionamento ficou como planejado, os seguintes comandos foram executados:

```bash
lsblk -f
df -hT
findmnt --real
sudo fdisk -l /dev/sda
free -h
cat /etc/os-release
```

📷 **Evidência:** 
*(Adicione aqui os prints ou blocos de código com a saída dos comandos acima)*

---

### Pergunta de Prova

**Por que separar a partição `/home` da partição raiz `/`?**
> **Resposta:** Separar o `/home` permite reinstalar, atualizar ou reparar o sistema operacional (a partição raiz `/`) sem perder os dados e arquivos pessoais dos usuários. Além disso, ajuda a controlar e isolar o uso de disco, evitando que um usuário lote o disco inteiro e trave o sistema.