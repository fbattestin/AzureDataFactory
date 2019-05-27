# AzureDataFactory

Refeência: https://docs.microsoft.com/pt-br/azure/data-factory/data-movement-security-considerations

Um pipeline é um agrupamento lógico de atividades que juntas executam uma tarefa. Esses pipelines residem na região em que o data factory foi criado.
Mesmo que a fábrica de dados está disponível apenas em algumas regiões, o serviço de movimentação de dados é disponível globalmente para garantir a conformidade de dados, eficiência e rede reduzida os custos de saída.

# Certificados

ISO/IEC 20000-1:2011 Information Technology Service Management.
ISO 22301:2012 Business Continuity Management Standard.
ISO/IEC 27001:2013 Information Security Management Standards.
ISO/IEC 27017:2015 Code of Practice for Information Security Controls.
ISO/IEC 27018 Code of Practice for Protecting Personal Data in the Cloud.
ISO 9001:2015 Quality Management Systems Standards.
SOC 1, 2, and 3 Reports.
Microsoft and HIPAA and the HITECH Act.


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

