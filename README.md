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
![ISCSI](https://github.com/user-attachments/assets/635501bd-2696-471e-b46a-9b80d5c88e88)
![CONEXÃO](https://github.com/user-attachments/assets/090c7a69-6817-45a7-9e7b-17344b856b5f)
![DISK MANAGER](https://github.com/user-attachments/assets/2126224d-0e7e-40bf-a686-ad2419d7934c)
![WhatsApp Image 2026-03-12 at 14 17 55](https://github.com/user-attachments/assets/d29a8d5a-632d-4530-8bc5-d223c8a7316c)
![No Ar](https://github.com/user-attachments/assets/b75d87c7-d9ba-46fe-a1e9-2e66db76e968)
