# Armazenamento

O Aleia utiliza armazenado virtual.

O **Aleia** utiliza armazenamento virtual.

O servidor está no **Cydibua**, com o IP interno **172.16.16.113**.

A alocação de disco é feita sob demanda, com uma reserva de **50GB livres**.

Em dezembro de 2024, o disco estava com **27% de uso**:

 <pre>/dev/mapper/cydonia--vg-root 153.010.424 39157828 107098564 27% /</pre>

Os procedimentos téncicos atendem

 # Gestão de Riscos e Integridade dos Dados

O repositório adota uma abordagem baseada em riscos para a gestão de armazenamento e dados, incluindo:

* Manutenção de múltiplas cópias redundantes de todos os conjuntos de dados em locais geograficamente separados, fincando um em Brasília e outra no Servidor do Ibict no Rio de Janeiro.
* Avaliação regular dos meios de armazenamento para identificar sinais de deterioração e adoção de ações corretivas, como migração dos dados para mídias mais confiáveis. Relizada pela equipe técnica do Ibict, equipe fixa de avaliação.
* Execução de backups periódicos, snapshot diários, e backup completos semanais, conforme definido no Protocolo de Backup do Dataverse [1]. Os backups incluem banco de dados[1], Payara6[2], armazenamento de dados e arquivos de personalização. Os procedimentos de backup são monitorados para garantir confiabilidade e conformidade com os cronogramas.
* De forma manual, para casos de atualização do sistema, é possível fazer um backup diretamente pelo Payara6 veja Backup Manual Payara

** Pastas
[1] Dump do Posgresql, database "dnvdb" com o usuário "dvnapp".

[2] Backup da pasta /usr/local/payara6/glasfish/domains/domain1.

[3] Armazenamento de dados estão na subpasta /data/.

# Seguranção da informação

As informações sobre a segurança estão descirtos no item 2 da infraestrutura tecnológica na página https://www.gov.br/ibict/pt-br/assuntos/informacao-cientifica/repositorios-digitais

# Backup Manual Payara

A segurança e infraestruta tecnológica está descrita no item 1 e 2 na página https://www.gov.br/ibict/pt-br/assuntos/informacao-cientifica/repositorios-digitais

* No primeiro nível o backup fica armazenado no mesmo servidor
* Os Snapshot:
** Local no Host: Snapshots são armazenados no sistema de arquivos do servidor físico que hospeda a VM. Em diretórios separados da VM. (Snapshots temporários)
** Rede Corporativa: Os snapshots são armazenados em um sistema de armazenamento em rede (NAS) ou em uma rede de área de armazenamento (SAN), que oferece maior capacidade, redundância e segurança. (Snapshots de longo prazo)
** Snapshots com mais de 30 dias são eliminados.

***Backup Payara Domain***
<pre>
 mkdir /home/dataverse/payara
 chown postgres /home/dataverse/payara
 service payara stop

 cd /home/dataverse/payara # diretorio onde ficará os arquivos
 $PAYARA/bin/asadmin backup-domain --backupdir /home/dataverse/payara domain1
</pre>

***Restore Payara Domain***
Informe o Domain do Payara, normalmente domain1
<pre>
 asadmin restore-domain --backupdir /home/glassfish/domain1/domain1_2020_12_17_v00001.zip domain1
 /usr/local/payara5/glassfish/domains
</pre>

***Backup do Postgres***
<pre>
 Backup do PostGres
 mkdir /home/dataverse/backup
 chown postgres /home/dataverse/backup
 su postgres
 cd /home/dataverse/backup # diretorio onde ficará os arquivos
 pg_dump dvndb > dvndb.sql
</pre>

***Restore DataBase no PostGres***
<pre>
 psql dvndb < /home/dataverse/payara/dvndb.sql
 psql -d dvndb
 GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public to dvnapp;
 GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA public to dvnapp;
 GRANT ALL PRIVILEGES ON ALL FUNCTIONS IN SCHEMA public to dvnapp;
</pre>