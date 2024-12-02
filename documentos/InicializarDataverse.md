# Inicializa o dataverse

Para inicializar, parar ou reiniciar o Dataverse existem bach no diretório /home/dataverse

***Start***

Para executar um start no Dataverse
<pre>/home/dataverse/start</pre>

Conteúdo do start
<pre>
export PAYARA=/usr/local/payara6/glassfish
echo "Starting Payara 6..."
$PAYARA/bin/asadmin start-domain
</pre>

***Stop***

Para executar uma parada no Dataverse (start) no Dataverse
<pre>/home/dataverse/stot</pre>

Conteúdo do stop
<pre>
export PAYARA=/usr/local/payara6/glassfish
echo "PAYARA 6 Stoping..."
$PAYARA/bin/asadmin stop-domain
</pre>

***Restart***

Para executar uma reinicialização do Dataverse
<pre>/home/dataverse/restart</pre>

Conteúdo do restart
<pre>
echo "Restarting Payara...."
/home/dataverse/stop
/home/dataverse/start
</pre>