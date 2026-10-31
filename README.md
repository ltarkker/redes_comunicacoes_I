# Redes e Comunicações I

Material, fichas e projectos Packet Tracer da UC **Redes e Comunicações I (RCOM1)** — LEI, ISTEC Porto.

> **Nota:** UC já concluída com **16 valores**, por equivalência do CTeSP. Frequento as aulas para rever a matéria, e este repositório reúne o trabalho feito nessas aulas.

## Estrutura

| Pasta | Conteúdo |
|---|---|
| `fichas/` | Fichas de exercícios das aulas práticas (PL) |
| `material/` | Material de apoio da UC |
| `projects/` | Ficheiros Packet Tracer (`.pkt`) e configurações (`.txt`) |
| `prints/` | Capturas de ecrã das configurações e testes |

## Projectos

### PL03 — Exercício 3: VLSM 192.168.0.0/24

**Ficheiros:** `projects/VLSM_Fab_IoT_Mark_Cont_Admin.pkt` (Packet Tracer 9.0.1) e `projects/configs_VLSM_Edificio1_Edificio2.txt`

Dois edifícios ligados por fibra (Cisco 2911 com HWIC-1GE-SFP + GLC-LH-SMD), cinco LANs com switches 2960-24TT e encaminhamento estático.

| Rede | Hosts | Rede/prefixo | Máscara | Gateway | Router · interface |
|---|---|---|---|---|---|
| Fábrica | 50 | 192.168.0.0/26 | 255.255.255.192 | 192.168.0.1 | Edificio-1 · G0/1 |
| IoT | 32 | 192.168.0.64/26 | 255.255.255.192 | 192.168.0.65 | Edificio-1 · G0/0 |
| Marketing | 20 | 192.168.0.128/27 | 255.255.255.224 | 192.168.0.129 | Edificio-1 · G0/2 |
| Contabilidade | 10 | 192.168.0.160/28 | 255.255.255.240 | 192.168.0.161 | Edificio-2 · G0/0 |
| Administração | 5 | 192.168.0.176/29 | 255.255.255.248 | 192.168.0.177 | Edificio-2 · G0/1 |
| RT (fibra) | 2 | 192.168.0.184/30 | 255.255.255.252 | .185 / .186 | G0/1/0 nos dois |

Configurado nos routers:

- hostname, `enable secret`, password de consola, `banner motd` e `service password-encryption`
- `no ip domain-lookup`
- interfaces com descrição e endereçamento VLSM
- rotas estáticas entre edifícios
- pools DHCP por LAN

Os PCs estão com IP estático (2.º host de cada rede). O Laptop0 liga ao Edificio-1 por consola (RS 232 → Console, 9600 8N1).

**Resultado:** conectividade total entre as cinco redes, com 0% de perdas depois de resolvido o ARP. O TTL é 127 dentro do mesmo edifício e 126 entre edifícios.

O ficheiro `.txt` tem as configurações completas, os comandos de teste com os resultados obtidos e os erros encontrados durante a configuração, com a resolução de cada um.
