# AzureDataFactory

Refeência: https://docs.microsoft.com/pt-br/azure/data-factory/data-movement-security-considerations

Um pipeline é um agrupamento lógico de atividades que juntas executam uma tarefa. Esses pipelines residem na região em que o data factory foi criado.
Mesmo que a fábrica de dados está disponível apenas em algumas regiões, o serviço de movimentação de dados é disponível globalmente para garantir a conformidade de dados, eficiência e rede reduzida os custos de saída.

# Certificados

* ISO/IEC 20000-1:2011 Information Technology Service Management.
* ISO 22301:2012 Business Continuity Management Standard.
* ISO/IEC 27001:2013 Information Security Management Standards.
* ISO/IEC 27017:2015 Code of Practice for Information Security Controls.
* ISO/IEC 27018 Code of Practice for Protecting Personal Data in the Cloud.
* ISO 9001:2015 Quality Management Systems Standards.
* SOC 1, 2, and 3 Reports.
* Microsoft and HIPAA and the HITECH Act.


# Cenário híbrido
Nesse cenário, sua origem ou destino está atrás de um firewall ou dentro de uma rede corporativa local.Ou, o armazenamento de dados está em uma particular ou rede virtual (geralmente a origem) e não está acessível publicamente. Os servidores de banco de dados hospedados em máquinas virtuais também se enquadram nesse cenário.
    
# Cenários de nuvem

Protegendo as credenciais do armazenamento de dados

* Armazene credenciais criptografadas em um armazenamento gerenciado do Azure Data Factory. O Data Factory ajuda a proteger suas credenciais de armazenamento de dados criptografando-as com certificados gerenciados pela Microsoft. Esses certificados são trocados a cada dois anos (que inclui a renovação do certificado e a migração de credenciais). As credenciais criptografadas são armazenadas com segurança em uma conta de armazenamento do Azure gerenciado pelos serviços de gerenciamento do Azure Data Factory. Para obter mais informações sobre a segurança do Armazenamento do Azure, consulte Visão geral de segurança do Armazenamento do Azure.
* Armazenar credenciais no Azure Key Vault. Você também pode armazenar credenciais do repositório de dados em Azure Key Vault. O Data Factory recupera as credenciais durante a execução de uma atividade. Para obter mais informações, consulte Armazenar credenciais no Azure Key Vault.

# Criptografia de dados em trânsito
Caso o armazenamento de dados em nuvem dê suporte a HTTPS ou TLS, todas as transferências de dados entre serviços de movimentação de dados no Data Factory e um armazenamento de dados em nuvem ocorrerão por meio de um canal seguro HTTPS ou TLS.

Em ADF, você pode adicionar EncryptionMethod=1 na cadeia de conexão (no serviço vinculado). Essa opção usará SSL/TLS como o método de criptografia. Para usar essa, é necessário desabilitar as configurações de criptografia não SSL no OAS no lado do servidor Oracle para evitar conflitos de criptografia.

# Repositório Azure Data Lake
O Azure Data Lake Store também fornece criptografia para os dados armazenados na conta. Quando está habilitado, o Data Lake Store criptografa os dados automaticamente antes de persisti-los e descriptografá-los antes da recuperação, tornando-os transparentes para o cliente que acessa os dados. Para obter mais informações, consulte Segurança no Azure Data Lake Store.

# Armazenamento de Blobs do Azure e armazenamento de Tabelas do Azure
O armazenamento de Blobs do Azure e o armazenamento de Tabelas do Azure dão suporte à SSE (Storage Service Encryption), que criptografa os dados automaticamente antes de persisti-los no armazenamento e descriptografa-os antes da recuperação. Para obter mais informações, consulte Criptografia de serviço do Armazenamento do Azure para dados em repouso.

# Cenários híbridos
Os cenários híbridos exigem que o tempo de execução de integração auto-hospedado (INTEGRATION RUNTIME) seja instalado em uma rede local, dentro de uma rede virtual (Azure) ou dentro de uma nuvem privada virtual (Amazon). O tempo de execução de integração auto-hospedado deve ser capaz de acessar os armazenamentos de dados locais. Para obter mais informações sobre o tempo de execução de integração auto-hospedado, consulte https://docs.microsoft.com/azure/data-factory/create-self-hosted-integration-runtime

![alt text](https://docs.microsoft.com/pt-br/azure/data-factory/media/data-movement-security-considerations/data-management-gateway-channels.png)

O canal de comando permite a comunicação entre os serviços de movimentação de dados no Data Factory e no tempo de execução de integração auto-hospedado. A comunicação contém informações relacionadas à atividade. O canal de dados é usado para transferir dados entre armazenamentos de dados locais e armazenamentos de dados em nuvem.

# Portas usadas para criptografar o serviço vinculado no tempo de execução de integração auto-hospedado

# Criptografia em trânsito
Todas as transferências de dados são feitas por meio do canal seguro HTTPS e TLS via TCP para impedir ataques man-in-the-middle durante a comunicação com os serviços do Azure.
Você também pode usar a VPN IPsec ou o Azure ExpressRoute para fornecer proteção adicional ao canal de comunicação entre a rede local e o Azure.
A Rede Virtual do Azure é uma representação lógica de sua rede na nuvem. Você pode conectar uma rede local à rede virtual ao configurar a VPN IPsec (site a site) ou o ExpressRoute (emparelhamento privado).

As imagens a seguir mostram o uso do tempo de execução de integração auto-hospedado para mover dados entre um banco de dados local e os serviços do Azure usando o ExpressRoute e a VPN IPsec (com a Rede Virtual do Azure):

# ExpressRoute

![alt text](https://docs.microsoft.com/pt-br/azure/data-factory/media/data-movement-security-considerations/express-route-for-gateway.png)

# IPSec VPN
![alt text](https://docs.microsoft.com/pt-br/azure/data-factory/media/data-movement-security-considerations/ipsec-vpn-for-gateway.png)

# Configurações de firewall e endereços IP de lista de permissões

* Requisitos de firewall para a rede local/privada
Em uma empresa, um firewall corporativo é executado no roteador central da organização. O Firewall do Windows é executado como um daemon no computador local em que o tempo de execução de integração auto-hospedado está instalado.
A tabela a seguir fornece os requisitos de porta de saída e de domínio dos firewalls corporativos:

Nomes de domínio	        Portas de saída    
*.servicebus.windows.net	    443             
*.frontend.clouddatahub.net	    443             
download.microsoft.com	        443               
*.core.windows.net	            443             
*.database.windows.net	        1433            
*.azuredatalakestore.net	    443             


A tabela a seguir fornece os requisitos de porta de entrada do Firewall do Windows:
Porta de Entrada: 8060 (TCP)
Exigido pelo cmdlet de criptografia do PowerShell conforme descrito em Criptografar credenciais para armazenamentos de dados locais no Azure Data Factory, e pelo aplicativo gerenciador de credenciais para definir credenciais com segurança para armazenamentos de dados locais no tempo de execução de integração auto-hospedado.

![alt text](https://docs.microsoft.com/pt-br/azure/data-factory/media/data-movement-security-considerations/gateway-port-requirements.png)

# Configurações de IP e lista de permissões em armazenamentos de dados

Alguns armazenamentos de dados na nuvem também exigem a lista de permissões do endereço IP do computador que os acessa. Verifique se o endereço IP do computador do tempo de execução de integração auto-hospedado está na lista de permissões ou configurado no firewall corretamente.
Os armazenamentos de dados na nuvem exigem a lista de permissões do endereço IP do computador do tempo de execução de integração auto-hospedado. Por padrão, alguns desses armazenamentos de dados poderão não exigir a lista de permissões.
* Banco de Dados SQL do Azure
* SQL Data Warehouse do Azure
* Repositório Azure Data Lake
* Azure Cosmos DB
* Amazon Redshift

# Quais são os requisitos de porta para o tempo de execução de integração auto-hospedado funcionar?
O tempo de execução de integração auto-hospedado faz conexões com base em HTTP para acessar a internet. As portas de saída 443 devem ser abertas para o tempo de execução de integração auto-hospedado para fazer essa conexão. Abra a porta de entrada 8050 somente no nível do computador (não no nível de firewall corporativo) para o aplicativo gerenciador de credenciais. Se o Banco de Dados SQL do Azure ou o SQL Data Warehouse do Azure for usado como a origem ou o destino, você precisará abrir a porta 1433 também. Para obter mais informações, consulte a seção Configurações de firewall e endereços IP na lista de permissões.
