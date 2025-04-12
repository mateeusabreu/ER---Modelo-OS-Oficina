# ER - Modelo OS Oficina

| Entidades                            | Tipo |
|--------------------------------------|------|
| Cliente ↔ Veículo                    | 1:N  |
| Veículo ↔ Ordem de Serviço (OS)      | 1:N  |
| Ordem de Serviço (OS) ↔ Equipe       | N:1  |
| Equipe ↔ Mecânicos                   | N:N  |
| Ordem de Serviço (OS) ↔ Serviços     | N:N  |
| Ordem de Serviço (OS) ↔ Peças        | N:N  |
| Serviço Executado ↔ Tabela Referência| N:1  |

