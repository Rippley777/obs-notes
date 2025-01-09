```
aa() {
  local alias_name="$1"
  local alias_command="$2"
  local alias_file="$HOME/.zshrc.aliases"
  local zshrc_file="$HOME/.zshrc"

  # Create the alias file if it doesn't exist
  if [[ ! -f $alias_file ]]; then
    touch "$alias_file"
    echo "# Aliases" > "$alias_file"
    echo "Alias file created at $alias_file."
  fi

  # Check if the alias already exists in the alias file
  if grep -q "alias $alias_name=" "$alias_file"; then
    echo "Alias '$alias_name' already exists in $alias_file."
  else
    # Add the alias to the alias file
    echo "alias $alias_name='$alias_command'" >> "$alias_file"
    echo "Alias '$alias_name' added to $alias_file."
  fi

  # Ensure the alias file is sourced in .zshrc
  if ! grep -q "source $alias_file" "$zshrc_file"; then
    echo "source $alias_file" >> "$zshrc_file"
    echo "Alias file sourced in $zshrc_file."
  fi

  # Reload .zshrc to apply changes
  source "$zshrc_file"
}
alias sa='source ~/.zshrc.aliases'

alias updateSys='sudo apt update && sudo apt upgrade -y'
alias updateLocalDB='sudo updatedb'
alias mountUbuntu='sudo mount /dev/sda4 /mnt/ubuntu'
alias addUser='sudo adduser $1'
alias userMod='sudo usermod -aG sudo $1'

alias installDocker='sudo apt install -y docker.io'
alias startDocker='sudo systemctl start docker'
alias enableDocker='sudo systemctl enable docker'

alias installVpn='sudo apt install openvpn -y'
alias loginVpn='nordvpn login'
alias connectVpn='nordvpn connect'
alias addVpnConfig='sudo openvpn --config $1'
alias verifyVpn='curl ifconfig.me'

alias ghConfigName='git config user.name $1'
alias ghConfigEmail='git config user.email $1'


alias obsidian='/opt/Obsidian-1.7.7.AppImage'
alias gono='~/Documents/Notes/Notes'

alias printOutWithErrors='find $1 name $2 2> $3 1> $4'

alias getNvimPkgMgr='git clone --depth 1 https://github.com/wbthomason/packer.nvim ~/.local/share/nvim/site/pack/packer/start/packer.nvim'
alias updateNvimPgks=':PackerSync'

# TODO check if virtualenv is preferred to python3-venv
alias installPython='sudo apt install -y python3 python3-pip virtualenv'
alias bootstrapPythonVenv='sudo apt install python3 python3-venv python3-pip'
alias createPythonVenv='python3 -m venv $1'
alias usePythonVenv='source $1/bin/activate'
```