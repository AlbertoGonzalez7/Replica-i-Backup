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


### CONFIGURACIÓ SLAVE

Primer, posem un server-id diferent al de la nostre maquina master (per exemple = 2)

![image](https://user-images.githubusercontent.com/101892290/170797194-faed7997-3a88-4bb1-bcea-3de35dc5a7ca.png)

Importem el backup de la base de dades que ens em pasat amb el WinSCP:

![image](https://user-images.githubusercontent.com/101892290/170797248-79be580e-83f1-4ecd-bb21-7aae290a365d.png)

Afegim les seguents comandes a la nostre slave:

![image](https://user-images.githubusercontent.com/101892290/170797424-8bf69898-42a2-4a9f-83ba-8469e9d9e40e.png)

##### Nota: per trobar els valors de MASTER_LOG_FILE i de MASTER_LOG_POS, hem de editar el nostre backup (amb la comanda nano /tmp/backup-master.slq) i hem de buscar els valors de MASTER_LOG_FILE i POS (normalment al principi del arxiu) Un exemple:

![image](https://user-images.githubusercontent.com/101892290/170797546-b2801711-dd8e-481a-9e62-4312720834b0.png)

Ara, hem de fer un start slave per que aixi comenci a funcionar el nostre slave:

![image](https://user-images.githubusercontent.com/101892290/170797584-f26a0e1d-ca69-42ae-bfa0-05dee3dec264.png)

Amb la comanda SHOW SLAVE STATUS \G: Podem observar si tot funciona correctament:

![image](https://user-images.githubusercontent.com/101892290/170797620-3c9c3652-2d61-45ec-9c9f-a3bd7d9a464a.png)

Per asegurarse completament de que la nostre SLAVE esta funcionant, podem crear una DATABASE al nostre MASTER i veurem com instantaniament es creara a la nostre SLAVE:

![image](https://user-images.githubusercontent.com/101892290/170797674-206fcb4e-2fe1-499a-81eb-c090c9905b23.png)





