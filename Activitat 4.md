# Activitat 4 - Rèplica i Backup

## ACTIVITAT 1. CONFIGURACIÓ D’UN SISTEMA DE RÈPLICA (5 punts)

### Configuracions previes:

Desactivar el firewall de les dues maquines

![image](https://user-images.githubusercontent.com/101892290/170793943-dd532260-a22e-4332-9efd-19c4564ba41f.png)

(Maquina slave) Aturar el servei mysql, entrar a /var/lib/mysql i borrar el arxiu auto.cnf (si es una maquina copia de la master)

![image](https://user-images.githubusercontent.com/101892290/170794048-7a98e105-dc06-4d36-a3ba-b7a563e91a9b.png)

Comprovar que les maquines es fan ping entre elles.

![image](https://user-images.githubusercontent.com/101892290/170796351-51d29107-54a9-43fa-9eff-bde56d6a570a.png)

### CONFIGURACIÓ MASTER

Entrem a my.cnf, i posem el server-id = 1 i el log-bin el nom que volguem

![image](https://user-images.githubusercontent.com/101892290/170796433-5d8ca828-5f99-4017-9b65-082b4c21415d.png)

Creem una database (o importem una), afegim una taula i valors dintre d'aquesta taula:

![image](https://user-images.githubusercontent.com/101892290/170796505-b14b523c-197c-4366-bcac-a2cd858c4eb8.png)

Fem un flush logs i despres un SHOW MASTER STATUS, i podem observar que s'han creat logs nou amb el nom que hem posar a log-bin:

![image](https://user-images.githubusercontent.com/101892290/170796551-bd35d99a-5d3d-4423-9ca6-0a4471bd21bc.png)

Afegim l'usuari slave amb l'IP de la maquina MASTER amb el permis de REPLICATION SLAVE:

![image](https://user-images.githubusercontent.com/101892290/170796870-c4b002ac-8a57-4ac4-a942-397e389297e8.png)

Fem un backup de la ultima base de dades amb la seguent comanda:

![image](https://user-images.githubusercontent.com/101892290/170796989-635e4d83-5350-4567-b265-59cb6ba77f2a.png)

I aquesta base de dades, amb el WinSCP, la copiem i enganxem a la nostre maquina SLAVE, al mateix lloc on hem creat aquest backup a la maquina master (/tmp/)

![image](https://user-images.githubusercontent.com/101892290/170797038-a2476a52-07a9-48b2-b4e1-91dadde2f341.png)




