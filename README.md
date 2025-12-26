Première étape, préparer l'installation:
```sh
cd /etc/nixos
sudo mv hardware-configuration.nix ~
sudo mv configuration.nix ~
nix-shell -p git
sudo git clone https://github.com/gustavbrlty/tmp_cnfg.git
cat README.md
```

Puis lancer l'installation:
```sh
# Récupération des UUIDs
NEW_ROOT=$(sed -n '/fileSystems."\/"/,/}/s/.*by-uuid\/\([^"]*\).*/\1/p' hardware-configuration.nix) && \
NEW_BOOT=$(sed -n '/fileSystems."\/boot"/,/}/s/.*by-uuid\/\([^"]*\).*/\1/p' hardware-configuration.nix) && \
# Remplacement dans hardware/common.nix
sed -i "/fileSystems.\"\/\"/,/}/ s|by-uuid/[^\"]*|by-uuid/$NEW_ROOT|" hardware/common.nix && \
sed -i "/fileSystems.\"\/boot\"/,/}/ s|by-uuid/[^\"]*|by-uuid/$NEW_BOOT|" hardware/common.nix
sudo git init .
sudo git config user.email "gustav7777777@icloud.com"
sudo git config user.name "Gustav"
sudo git add *
sudo git config --global --add safe.directory /etc/nixos
sudo nixos-rebuild switch --flake /etc/nixos#default
```
Ensuite s'il n'y a pas eu d'erreur:
```sh
sudo rm ~/configuration.nix ~/hardware-configuration.nix
cd ~
```
