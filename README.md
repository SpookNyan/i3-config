# i3-config
Quantos menos melhor! *entao...*
Quero deixar alguns comandos pra usar no caso de eu esquecer:

# Data e Hora 
```
sudo timedatectl set-ntp true 
sudo hwclock --systohc 
```

# Pacotes
*Coisa pra pos instalacao do Arch*
```
sudo pacman -S base-devel
sudo pacman -S archlinux-keyring
sudo pacman -S git go
```

# Comandos pra instalacao

# limpar cache
```
sudo pacman -Scc
```

# Atualizar sistema
```
sudo pacman -Syyu
sudo pacman -Syuu
sudo Pacman -Syu
```

# Procurar Pacostes
```
pacman -Ss {nome do pacote}
```

Exemplo:
```
pacman -Ss gimp
```

# Pesquisar pacotes instalados
```
pacman -Qs package_name
```

# Atualizar e instalar o pacote:
```
sudo pacman -Syu package1 package2
```

# Para instalar pacotes de n oficiais
```
sudo pacman -U https://packagesite.com/repo/packagename.pkg.tar.xz
```

# Listar Pacotes Instalados
```
pacman -Qi
or 
pacman -Ql
```

# Baixar pacote mas n instalar:
```
pacman -Sw package_name
```

# Apaga o pacote mas n dependecias
```
pacman -R package
```

# Se você deseja remover um pacote e suas dependências que não são usadas por outros pacotes, execute este comando:
```
sudo pacman -Rsu package
```

# Para verificar se há arquivos órfãos:
```
pacman -Qdt
```

# Você pode combiná-lo com o seguinte comando para remover pacotes / órfãos não usados de seus arquivos de configuração:
```
sudo pacman -Rsnu $(pacman -Qtdq)
```

# Remova tudo, exceto o sistema básico
# Primeiro, precisamos fazer com que todos os pacotes instalados se tornem uma “dependência:”

```
sudo pacman -D --asdeps $(pacman -Qqe)
```

# Em seguida, precisamos alterar o motivo da instalação de pacotes essenciais (sistema básico) para “tão explicitamente”, para que não sejam tratados como órfãos e sejam removidos:
```
sudo pacman -D --asexplicit base linux linux-firmware
```

# Por último, removeremos todos os arquivos “órfãos”:
```
sudo pacman -Rns $(pacman -Qtdq)
```

# Limpando Cache de Pacote

# O Pacman não limpa automaticamente as versões antigas ou desinstaladas dos pacotes. Isso permite downgrades e reinstalação fáceis a partir da pasta de cache. No entanto, à medida que o cache cresce internamente, ele pode ficar fora de controle. Temos um artigo dedicado sobre como limpar o cache do Pacman, mas aqui está a essência, este comando limpa todas as versões em cache de pacotes instalados e desinstalados, exceto os três mais recentes.
``
paccache -r
``

# Para limpar apenas os pacotes em cache que não estão instalados atualmente, execute o seguinte:
```
pacman -Sc
```

# Se você deseja limpar completamente o cache, execute o comando abaixo. Isso deixará sua pasta de cache completamente vazia.
```
pacman -Scc
```
# Reflector 
# Usar o reflector para achar mirrors

# Antes de prosseguir, faça um backup do arquivo "mirrorlist" do seu pacman. Pode-se utilizar o seguinte comando:
```
cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup
```

# =========== USANDO O REFLECTOR ============
Faça um teste com o Reflector para ver quantos servidores totalemente populados estão disponível em cada país:
```
reflector --list-countries
```

Você irá verificar que há poucos servidores no Brasil, 12 servidores hoje em 10/08/2018, mas Reflector só vai considerar os que estão 100% populados naquele momento. Portanto, não muita razão para pedirmos para classificar somente os n melhores... Vamos deixar ele classificar todos servidores brasileiros disponíveis. Para verificar a lista que será gerada com esses parâmetros, rode:
```
reflector -c Brazil
```
Depois, criar o arquivo com:
```
reflector -c Brazil --save /etc/pacman.d/mirrorlist
```
Se Possuir muitos servers:
```
reflector -c 'United States' -p https -f 5 --score 5
```
Depois, criar o arquivo com:
```
reflector -c 'United States' -p https -f 5 --score 5 --save /etc/pacman.d/mirrorlist
```

# Yay Install
*clone Repo*
```
git clone https://aur.archlinux.org/yay.git
```

*Entrar na past*
cd yay

*Compilar build*
```
makepkg -si
```

*(Se precisar achar as dependecias)*
```makepkg --syncdeps```

# Screenshot (Scrot)
*dpends: scrot, xclip*
```
#mod+printscrn: take full screenshot, place in ~/img/scrot, copy to clipboard
bindsym --release Print exec "scrot 'scrot-%Y-%m-%d_%h-%m-%s_$wx$h.png' -e 'mv $f ~/img/scrot/ && xclip -t image/png ~/img/scrot/$f -sel clip'"
```

```
#mod+shift+printscrn: take selection screenshot, place in ~/img/scrot, copy to clipboard
bindsym --release Shift+Print exec "scrot --select 'scrot-%Y-%m-%d_%h-%m-%s_$wx$h_snip.png' -e 'mv $f ~/img/scrot/ && xclip -t image/png ~/img/scrot/$f -sel clip'"
```
