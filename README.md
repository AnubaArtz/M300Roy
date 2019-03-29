## **M300 - LB1 Roman Roy Dokumentation**

Im Modul 300 wurde uns die Arbeit mit Virtuellen Maschienen und deren autmatisierung näher gebracht.

## **Auftrag**

Unser auftrag war es automatisiert verschiedene VMs aufzusetzen. Dies machten wir mittels einem sogenanntem Vagrant File und Github.

## **Unser Vorgehen**

Wir arbeiteten nach dem IPERKA system. Wir schauten uns den Auftrag genau an und informierten uns. Anschliessen planten wir unser Vorgehen. Die Vorgehensweise wurde vom Auftragsdokument übernommen, da dort alles genau beschrieben wurde. Wir arbeiteten somit das Skript durch. Wir hatten Startprobleme, da es bei Roman nicht geklappt hat Vagrant aufzusetzen. Wir lösten dieses Problem am zweiten Modultag, indem wir alles nochmals neu installierten. Nachdem folgte die Arbeit am Skript. Leider verstanden wir nicht ganz alles, was uns zu einem unseren Mitstiften führte, mit welchem wir ein Vagrant-File erstellten.

**GITHUB**

Um unsere Scripts unter einander zu teilen und zu vergleichen und dem Lehrer bereitzustellen wannten wir Github an. Wir haben unser Vagrant File sowie diese Dokumentation mittels GITHUB für den Lehrer und oder den anderen Schülern freigegeben.

**Produktive Nutzung**

Man kann mit unserer umgebung einfach die gewünschten VMs binnen sekunden Dadurch kann man sich viel arbeit sparen die man beim manuel erstellen der VMs ansonnsten hätte.

Mit unserer umgebung kann er ganz einfach ins Github gehen einen Vagrant up befehl ausführen und schon hat man seine VM.

In diesem Vagrant-File ist definiert von wo er sich das OS grabben soll, welche konfigurationen er vornehemen soll und wie ist installiert wird.

## **Eigener Service**

Zuerst haben wir uns darüber informiert was ist Vagrant wie funktioniert es und wie können wir die gewünschte umgebung am besten umsetzen. Dann haben wir ein paar beispielle und Tutorials angesehen bis wir es gut genug verstanden hatten um es selber zu machen. Ich hatte einige Probleme beim aufsetzen der umgebung weswegen dies leider relativ lange dauerte.
Sie sehen gleich ein Vagrant-File bei dem Ubuntu mit einer Firewall Reproxy installiert wird. die Ports haben wir so abgeändert, dass jegliche kommunikation von der IP 10.0.2.2 zugelassen wird.
Ausserdem das Protokoll TCP über den Port 80 in jedem Fall zugelassen.
Um sicherzugehen, dass diese Commands auch ausgeführt werden, führen wir den Command _Force_ ein.

Vagrant.configure(2) do |config|   config.vm.box = &quot;ubuntu/trusty64&quot;   config.vm.network &quot;private\_network&quot;, ip:&quot;192.168.10.1&quot;   config.vm.network &quot;forwarded\_port&quot;, guest:80, host:8080, auto\_correct: true   config.vm.synced\_folder &quot;.&quot;, &quot;/var/www/html&quot;  config.vm.provider &quot;virtualbox&quot; do |vb|   vb.memory = &quot;512&quot;  end   config.vm.provision &quot;shell&quot;, inline: \&lt;\&lt;-SHELL

    sudo apt-get update

    sudo apt-get install apache2 -y

    sudo apt-get install ufw -y

    sudo ufw allow from 10.0.2.2 to any port 22

    sudo ufw allow 80/tcp

    sudo ufw --force enable

    sudo apt-get install libapache2-mod-proxy-html -y

    sudo apt-get install libxml2-dev -y

    a2enmod proxy

    a2enmod proxy\_html

    a2enmod proxy\_http/41

    sed -i &#39;$aServerName localhost&#39; /etc/apache2/apache2.conf

    service apache2 restart

    cd /etc/apache2/sites-enabled

    wget https://pastebin.com/raw/GbjFC2ii

    cp GbjFC2ii 001-reverseproxy.conf   SHELL end

## **Testing**

Um das Testing durchzuführen haben wir verschiedene Testcases aufgeschrieben und nach diesen Fällen die Tests druchgeführt.
Dokumentiert wurde ebenfalls das erwartete und das tatsächliche Ergebnis festgehalten.

|  **Test** | _Erwartete Ausg._ | Tatächliche Ausg.

|  **Erstellung VM**  | _Nach ausführen des Vagrant files, wird die VM erstellt_. | Nach ausführen des Vagrant files, wird die VM erstellt.

|  **SSH Verbindung**  | _Die Verbindung zu dieser VM ist mit SSH möglich._ | Die Verbindung zu dieser VM ist mit SSH möglich.

|  **Firewall**  | _Die Firewall ist gestartet_. | Die Firewall ist gestartet.

|  **Betrieb**  | _Die Website ist ansprechbar._ | Die Website ist ansprechbar.

|  **Apache**  | _Apache ist als Prozess sichtbar._ | Apache ist als Prozess sichtbar.
