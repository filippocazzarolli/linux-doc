## snap info
snap info node

## install node ver 10
sudo snap install node --channel=10/stable --classic

## change version
sudo snap refresh node --channel=10/stable --classic

sudo snap refresh node --channel=12/stable --classic

## list all relaese
snap info pycharm-professional 

## check update
snap refresh --list

## update last version of webstorm
sudo snap refresh webstorm

### angular install 
sudo npm install -g @angular/cli

### per installare correttamente i paccheti npm aggiungere il parametro in fondo
sudo npm install -g @angular/cli  --scripts-prepend-node-path
