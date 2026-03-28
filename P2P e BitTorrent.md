# P2P (Peer-to-Peer) e BitTorrent
camada: [Camada de Aplicação](./Camada%20de%20Aplicação.md)

## Definição
Arquitetura de rede onde não há dependência de um servidor central dedicado. Os pares (peers) comunicam-se diretamente entre si.
- **Escalabilidade:** A capacidade de serviço *aumenta* conforme mais usuários entram (cada downloader também é um uploader).


## Conceitos do BitTorrent
- **Torrent:** Arquivo de metadados.
- **Tracker:** Um servidor simples que apenas mapeia quais IPs estão no enxame (swarm). Não trafega arquivos.
- **Chunks:** O arquivo é dividido em pedaços (geralmente 256KB).
- **Seeder:** Par que tem o arquivo completo.
- **Leecher:** Par que ainda está baixando.

## Algoritmos
1. **Tit-for-Tat (Olho por olho):** Estratégia de incentivo. O peer envia dados prioritariamente para os 4 peers que estão enviando mais rápido para ele.
2. **Optimistic Unchoking:** A cada 30s, o peer escolhe um vizinho aleatório para enviar dados, na esperança de encontrar uma conexão melhor.

## 🛡️ Cybersec Insight
- **Exposição de IP:** Em redes P2P, seu IP é anunciado publicamente para todos no enxame. Facilita mapeamento e ataques diretos.
- **Integridade:** Risco de baixar arquivos adulterados com malware (embora o Torrent use Hashing para verificar blocos).
- **DDoS:** Botnets usam arquitetura P2P para controle descentralizado (sem servidor C&C único para derrubar).
