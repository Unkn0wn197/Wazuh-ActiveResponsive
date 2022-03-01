# Wazuh Active Responsive.
Documentation of rules created by me for active responsive.

#### Ejemplo de comandos, reglas y como crearlas
Un comando es lo que ejecutara el active response cuando este lo llame. Esta es su sintaxis.
```
<command>
    <name>firewall-drop</name> #Nombre de la regla
    <executable>firewall-drop.sh</executable> #Script que ejecutara el comando
    <expect>srcip</expect> #Parametro que nos devuelve la ip de la maquina que activó el active response
    <timeout_allowed>yes</timeout_allowed> 
</command>
```
Un active response es un evento que se ejecutara cuando se active una serie de condiciones, en general una alerta de Wazuh.
```
<active-response>
    <command>firewall-drop</command> #Nombre del comando que vamos a llamar
    <location>local</location> #Donde se aplicara la regla
    <rules_id>2502</rules_id> #La id de la alerta de seguridad que da wazuh
    <timeout>1800</timeout> #El tiempo que dura la regla 
</active-response>
```


#### Regla para bloquear una ip que haga tres intentos fallidos por el protocolo ssh.
Colocamos este comando en el archivo /var/ossec/etc/ossec.conf
```
<command>
    <name>firewall-drop</name> 
    <executable>firewall-drop.sh</executable>
    <expect>srcip</expect>
    <timeout_allowed>yes</timeout_allowed>
</command>
```
Y luego colocamos este active responsive
```
<active-response>
    <command>firewall-drop</command>
    <location>local</location>
    <rules_id>2502</rules_id>
    <timeout>1800</timeout>
</active-response>
```
