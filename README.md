# banco-de-dados

*Nome do projeto: LocaRoda

*Tema: Aplicativo para empresa de aluguel de carros para motoristas de aplicativo.

*Objetivo: Criar um ambiente confortável e eficiente para a comunicação entre motorista e empresa, e a contratação de carros diversos em disponibilidade, especificando detalhes como modelo e duração do contrato.

```mermaid 
erDiagram
    Motorista ||--o{ Contrato : "assina"
    Empresa ||--o{ Veiculo : "possui"
    Empresa ||--o{ Contrato : "emite"
    Veiculo ||--o{ Contrato : "alocado_em"
    Contrato ||--o{ Pagamento : "gera"
    Veiculo ||--o{ Manutencao : "passa_por"

    Motorista {
        string cpf PK
        string nome
        string telefone
        string cnh
        string categoria_cnh
        string email
    }

    Empresa {
        string cnpj PK
        string nome
        string email
        string endereco
        float avaliacao
    }

    Veiculo {
        string placa PK
        string modelo
        string marca
        int ano
        string status "Disponivel, Alugado, Manutencao"
        float preco_diaria
        string empresa_cnpj FK
    }

    Contrato {
        int id PK
        string motorista_cpf FK
        string veiculo_placa FK
        string empresa_cnpj FK
        datetime data_inicio
        datetime data_fim_prevista
        float valor_caucao
        string status "Ativo, Finalizado, Cancelado"
    }

    Pagamento {
        int id PK
        int contrato_id FK
        float valor
        datetime data_vencimento
        datetime data_pagamento
        string status "Pendente, Pago, Atrasado"
    }

    Manutencao {
        int id PK
        string veiculo_placa FK
        datetime data
        string descricao
        float custo
    }
