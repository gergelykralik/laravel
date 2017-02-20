[Laravel](./index.html)
=======================

## Vyvojove prostredie

Bud nainstalovat PHP, nginx/apache, mysql/mariadb a dalsie lokalne, a vsetko nakonfigurovat pre Laravel, alebo pouzivat prednastavene aplikacie, pre macOS je vytvoreny [Valet](https://laravel.com/docs/5.4/valet) alebo [Homestead](https://laravel.com/docs/5.4/homestead) -> toto pouzivam ja, obahuje kompletne vsetky potrebne nastroje.

### [Composer](https://getcomposer.org/)

[Nette dokumentacia dobre opise na co vlastne je](https://doc.nette.org/cs/2.4/composer) ako aj zaklady. Composer manazuje PHP kniznice, a autoload v projekte.

#### Subor `composer.json`

Obsahuje vsetky dolezite informacie o projekte, a balicky ktore su potrebne pre projekt. Pridavanie novych balickov treba urobit cez `terminal`, priama editacia suboru `composer.json` moze byt problematicke. Tento subor treba davat na `Git`, ale nainstalovane veci v adresari `vendor` nie.

#### Dolezite prikazy

*instalacia balicka (vytvorenie noveho projektu)*

```bash
# Prvy projekt (globalna instalacia kniznice)
composer global require "laravel/installer"

# Projekt
cd /www
laravel new my-app
```	

*instalacia balikov z composer.json*

```bash
composer update
```

*pridavanie balicka*

```bash
composer require "laravelcollective/html"
```

*pregenerovanie autoloadera*

```bash
composer dump-autoload --optimize
```

##### Autoload

Autoload je vopred nastavena, je v nom zadefinovane v ktorom adresari je dany namespace

```json
"autoload": {
    \\ ... konfig
}
```

### [VirtualBox](https://www.virtualbox.org)

Nastroj na manazovanie virtualnych strojov. [download](https://www.virtualbox.org/wiki/Downloads). 


### [Vagrant](https://www.vagrantup.com)

Nastroj na jednoduchu spravu vyrtualnych strojov. [download](https://www.vagrantup.com/downloads.html)

Cez vagrant je mozne kompletne nakonfigurovat virtual, aj modifikovat konfiguraciu pomocou konfig suboru.

#### Konfiguracia

Nakonfigurovany virtualny stroj je vagrant box, v ktorom je konfig subor.

Vagrant box bude inicializovany v aktualnom adresari.

### [Homestead](https://laravel.com/docs/5.4/homestead)

Homestead je Vagrant box, v ktorom je vsetko nakonfigurovany na vyvoj Laravel aplikacii.

#### Instalacia + inicializacia

```bash
mkdir ~/homestead-vm
cd ~/homestead-vm
vagrant box add laravel/homestead

cd ~
git clone https://github.com/laravel/homestead.git homestead-vm
cd ~/homestead-vm
bash init.sh
```

**Hlavny konfiguracny subor:**

```bash
~/homestead-vm/Homestead.yaml
```

##### Konfiguracia

Vseobecne nastavenia:

```yaml
ip: "192.168.10.10"
memory: 2048
cpus: 2
provider: virtualbox
```

Mapovanie adresarov:

```yaml
folders:
    - map: ~/Code
      to: /www
```

Mapovanie webov:

```yaml
sites:
    - map: php-myadmin
      to: /www/php-myadmin/
    - map: laravel.admin
      to: /www/admin-app-laravel-admin/public
```

**Aby vytvoreny web fungoval treba uviest IP adresu a domenu v `/etc/hosts`**

```bash
sudo vim /etc/hosts
```

```bash
192.168.10.10      php-myadmin
192.168.10.10      laravel.admin
```

#### Dolezite prikazy

Vagrant prikazy funguju iba v adresari, v ktorom je vagrant box nainstalovany, ale vieme to rozsirit, pomocou `alias`ov.

```bash
vim ~/.bash_profile
```

Pridavame alias pre `homestead`

```bash
# Vagrant
export VAGRANT_DEFAULT_PROVIDER=virtualbox
 
# Homestead
export PATH=/Users/-user-/homestead-vm:${PATH}
function homestead() {
    (cd /Users/-user-/homestead-vm && vagrant $* )
}
```

Po ulozeni:

```bash
source ~/.basrh_profile
```

##### Samotne prikazy

```bash
homestead up            # spustenie
homestead suspend       # pozastavenie (graceful)
homestead halt          # pozastavenie
homestead status        # stav
homestead reload        # restart
homestead provision     # reinicializacia (potrebne po pridavani novych webov)

# Po pridavani webov, alebo adresarov:
homestead reload --provision

# SSH pristup na stroj
homestead ssh
```

Uzivatel je `vagrant`, `sudo` funguje bez hesla.

- - - -

[Inicializacia a konfiguracia >](./inicializacia.html)
