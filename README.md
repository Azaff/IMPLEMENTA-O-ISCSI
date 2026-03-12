🚀 Implementando Storage iSCSI no Windows Server para Virtualização (LAB)
Recentemente montei um laboratório de infraestrutura com o objetivo de separar camada de armazenamento (storage) da camada de processamento (compute) em um ambiente de virtualização.

A ideia foi utilizar um servidor dedicado para armazenamento centralizado e outro servidor, com hardware mais robusto, apenas para executar as máquinas virtuais.

🧱 Arquitetura do ambiente
Servidor 1 – Storage

Windows Server

Discos HDD (2.5TB)

Configurado como iSCSI Target

Servidor 2 – Compute

Windows Server com Hyper-V

Conectado ao storage via iSCSI Initiator

Rede dedicada para storage

Conexão direta entre servidores

Sem switch intermediário

Baixa latência

Servidor Hyper-V (Compute)
NIC1 → Rede produção
NIC2 → iSCSI
        │
        │ Conexão direta
        │
Servidor Storage
NIC1 → Rede produção
NIC2 → iSCSI
⚙️ Etapas principais da implementação
1️⃣ Instalação da role iSCSI Target Server no Windows Server
2️⃣ Criação de um iSCSI Virtual Disk (VHDX) no servidor storage
3️⃣ Configuração do iSCSI Target permitindo acesso do servidor Hyper-V
4️⃣ Conexão via iSCSI Initiator no servidor de virtualização
5️⃣ Inicialização e formatação do disco no Gerenciamento de Disco

Após a conexão, o disco remoto passou a ser reconhecido pelo Hyper-V como um disco local, permitindo armazenar as VMs diretamente nele.

📊 Resultados do laboratório
Durante os testes de transferência de arquivos:

Arquivo de 4GB transferido em ~8 a 15 segundos

Taxa média observada próxima de 180MB/s

Desempenho consistente para ambiente com HDD via iSCSI

🎯 Benefícios da arquitetura
✔ Separação entre compute e storage
✔ Melhor aproveitamento do hardware mais potente para VMs
✔ Possibilidade de expansão futura do armazenamento
✔ Estrutura semelhante a arquiteturas usadas em datacenters

🔧 Próximos passos no laboratório
Implementar MPIO (Multipath I/O) para redundância e performance

Testar RAID 10 no storage

Avaliar upgrade para rede 10Gb

Criar um ambiente Hyper-V Failover Cluster
