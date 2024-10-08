# Proj01_Eng_SW
Autor: Abner Lohan Caçula Silva.


Meu repositório de Engenharia de Software.

# 1. Descrição do sistema
Nome da clínica: Zé Pulguinha

01. Uma clínica veterinária atende apenas os animais: gatos e cachorros.
02. Os clientes devem fazer um cadastro de si e dos animais.
03. Os clientes devem informar as condições nas quais os animais chegam.
04. Os clientes devem informar o tipo de ração que o animal come.
05. O cliente deve informar hábitos do animal.
06. Para cada animal é possível que mais de um veterinário o atenda.
07. Os animais podem chegar e serem atendidos de acordo com uma agenda do dia.
08. Cada animal atendido receberá uma ficha e um prontuário.
09. Outros donos podem querer marcar horários de atendimento futuro.
10. O atendimento gera uma receita para o animal.
11. Quando um cliente chega na clínica veterinária ele é atendido por um atendente.
12. O atendente deve verificar se existe agenda disponível com um veterinário.
13. O atendente deve colocar o cliente e seu animal na fila de espera, se for o caso.
14. O atendente deve levar o cliente e o animal até o veterinário.
15. O veterinário deve realizar uma entrevista com o dono do animal.
16. O resultado da entrevista deve ir para um formulário.
17. O veterinário deverá examinar o animal e anotar em prontuário (ficha) suas observações.
18. Dependendo da situação do animal este receberá uma receita.
19. A clínica tem horário de funcionamento normal de 07h00 às 18h00, de segunda-feira à sexta-feira.
20. Atendimentos fora do horário normal são considerados emergência.
21. A clínica faz atendimentos também por plantões.
22. A escala de plantões é definida semanalmente.
23. A clínica trabalha também com a hospedagem de cães e gatos.
    
# 2. Diagrama do banco de dados

```mermaid
erDiagram
    CLIENTE ||--o{ ANIMAL : "possui"
    CLIENTE ||--o{ ATENDIMENTO : "faz"
    ANIMAL ||--o{ ATENDIMENTO : "participa"
    ANIMAL ||--|| FICHA : "possui"
    ANIMAL ||--|| RECEITA : "recebe"
    ANIMAL ||--o{ HOSPEDAGEM : "é hospedado em"
    VETERINARIO ||--o{ ATENDIMENTO : "realiza"
    VETERINARIO ||--o{ ESCALA : "participa"
    ESCALA ||--o{ PLANTAO : "define"
    ATENDIMENTO ||--|| RECEITA : "pode gerar"

    CLIENTE {
        int id
        string nome
        string contato
    }
    
    ANIMAL {
        int id
        string nome
        string especie
        string condicoes
        string tipoRacao
        string habitos
    }

    ATENDIMENTO {
        int id
        datetime dataHora
        string tipo
    }

    VETERINARIO {
        int id
        string nome
        string especialidade
    }

    FICHA {
        int id
        datetime dataHora
        string observacoes
    }

    RECEITA {
        int id
        datetime dataHora
        string descricao
    }

    ESCALA {
        int id
        datetime dataInicio
        datetime dataFim
    }

    PLANTAO {
        int id
        datetime dataHora
    }

    HOSPEDAGEM {
        int id
        datetime dataInicio
        datetime dataFim
    }
```

# 3. Diagrama de casos de uso

![Usecase](https://github.com/AbnerLohan/Abner_Lohan_projeto01_engsw/blob/main/imagens/Usecase.png)

# 4. Principais telas do sistema

![Imagem 1](https://github.com/AbnerLohan/Abner_Lohan_projeto01_engsw/blob/main/imagens/Captura%20de%20tela%202024-08-14%20215714.png)

![Imagem 2](https://github.com/AbnerLohan/Abner_Lohan_projeto01_engsw/blob/main/imagens/Captura%20de%20tela%202024-08-14%20215730.png)

![Imagem 3](https://github.com/AbnerLohan/Abner_Lohan_projeto01_engsw/blob/main/imagens/Captura%20de%20tela%202024-08-14%20215747.png)

![Imagem 4](https://github.com/AbnerLohan/Abner_Lohan_projeto01_engsw/blob/main/imagens/Captura%20de%20tela%202024-08-14%20215810.png)

![Imagem 5](https://github.com/AbnerLohan/Abner_Lohan_projeto01_engsw/blob/main/imagens/Captura%20de%20tela%202024-08-14%20215827.png)

# 5. Arquitetura do sistema
```mermaid
flowchart TB
    subgraph Cliente
        CW[Cliente Web]
    end

    subgraph Servidor_Web
        SW[Servidor Web]
        PHP[Aplicação PHP]
    end

    subgraph Banco_Dados
        DB[Servidor de Banco de Dados]
    end

    CW -- Requisição HTTP --> SW
    SW -- Processamento --> PHP
    PHP -- Consulta/Inserção/Atualização --> DB
    DB -- Resposta --> PHP
    PHP -- Resposta HTTP --> SW
    SW -- Resposta HTTP --> CW
```