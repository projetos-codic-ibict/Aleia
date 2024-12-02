# Armazenamento

O Aleia utiliza armazenado virtual.

O **Aleia** utiliza armazenamento virtual.

O servidor está no **Cydibua**, com o IP interno **172.16.16.113**.

A alocação de disco é feita sob demanda, com uma reserva de **50GB livres**.

Em dezembro de 2024, o disco estava com **27% de uso**:

 <pre>/dev/mapper/cydonia--vg-root 153.010.424 39157828 107098564 27% /</pre>

 # Gestão de Riscos e Integridade dos Dados

O repositório adota uma abordagem baseada em riscos para a gestão de armazenamento e dados, incluindo:

* Manutenção de múltiplas cópias redundantes de todos os conjuntos de dados em locais geograficamente separados, fincando um em Brasília e outra no Servidor do Ibict no Rio de Janeiro.
* Avaliação regular dos meios de armazenamento para identificar sinais de deterioração e adoção de ações corretivas, como migração dos dados para mídias mais confiáveis. Relizada pela equipe técnica do Ibict, equipe fixa de avaliação.
* Execução de backups periódicos, snapshot diários, e backup completos semanais, conforme definido no Protocolo de Backup do Dataverse [1]. Os backups incluem banco de dados[1], Payara6[2], armazenamento de dados e arquivos de personalização. Os procedimentos de backup são monitorados para garantir confiabilidade e conformidade com os cronogramas.

** Pastas
[1] Dump do Posgresql, database "dnvdb" com o usuário "dvnapp"
[2] Backup da pasta /usr/local/payara6/glasfish/domains/domain1
[3] Armazenamento de dados estão na subpasta /data/