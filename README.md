Pour afficher ce README: 
```sh
curl https://raw.githubusercontent.com/gustavbrlty/tmp_cnfg/refs/heads/main/README.md
```

Première étape, préparer l'installation:
```sh
cd /etc/nixos
sudo mv hardware-configuration.nix ~
sudo mv configuration.nix ~
nix-shell -p git
```

Puis lancer l'installation:
```sh
sudo git clone https://github.com/gustavbrlty/tmp_cnfg.git
sudo mv tmp_cnfg/* . && sudo rm -r tmp_cnfg
cat README.md
# Récupération des UUIDs
NEW_ROOT=$(sed -n '/fileSystems."\/"/,/}/s/.*by-uuid\/\([^"]*\).*/\1/p' ~/hardware-configuration.nix)
NEW_BOOT=$(sed -n '/fileSystems."\/boot"/,/}/s/.*by-uuid\/\([^"]*\).*/\1/p' ~/hardware-configuration.nix)
# Remplacement dans hardware/common.nix
sudo sed -i "/fileSystems.\"\/\"/,/}/ s|by-uuid/[^\"]*|by-uuid/$NEW_ROOT|" hardware/common.nix
sudo sed -i "/fileSystems.\"\/boot\"/,/}/ s|by-uuid/[^\"]*|by-uuid/$NEW_BOOT|" hardware/common.nix
sudo git init .
sudo git config user.email "gustav7777777@icloud.com"
sudo git config user.name "Gustav"
sudo git add *
sudo git config --global --add safe.directory /etc/nixos
sudo nixos-rebuild switch --flake /etc/nixos#default
```
Ensuite s'il n'y a pas eu d'erreur:
```sh
exit
sudo rm ~/configuration.nix ~/hardware-configuration.nix
cd ~
```
