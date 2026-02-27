# banco-de-dados

*Nome do projeto: LocaRoda

*Tema: Aplicativo para empresa de aluguel de carros para motoristas de aplicativo.

*Objetivo: Criar um ambiente confortável e eficiente para a comunicação entre motorista e empresa, e a contratação de carros diversos em disponibilidade, especificando detalhes como modelo e duração do contrato.

```mermaid 
erDiagram
    Usuario ||--o{ Contrato : "assina/atende"
    Empresa ||--o{ Veiculo : "possui"
    Empresa ||--o{ Contrato : "emite"
    Veiculo ||--o{ Contrato : "alocado_em"
    Contrato ||--o{ Pagamento : "gera"
    Veiculo ||--o{ Manutencao : "passa_por"

    Usuario {
        string cpf PK
        string nome
        string sobrenome
        string email
        string endereco
        string dados_bancarios
        string cnh
        string categoria_cnh
        boolean e_atendente "Define se tambem trabalha na empresa"
    }

    Empresa {
        string cnpj PK
        string nome
        string email
        string endereco
    }

    Veiculo {
        string placa PK
        string marca
        string modelo
        string tipo "Moto, Caminhao, Carro de passeio"
        int ano
        string status "Disponivel, Alugado, Manutencao"
        float preco_diaria
    }

    Contrato {
        int numero_contrato PK
        datetime data_emissao
        string motorista_cpf FK "Cliente"
        string veiculo_placa FK
        string empresa_cnpj FK
        string tipo_pagamento "Cartao, Pix"
        datetime periodo_inicio
        datetime periodo_fim
        float valor_total
        string status
    }

    Pagamento {
        int id PK
        int contrato_id FK
        float valor
        datetime data_vencimento
        string status
    }

    Manutencao {
        int id PK
        string veiculo_placa FK
        datetime data
        string descricao
        float custo
    }
