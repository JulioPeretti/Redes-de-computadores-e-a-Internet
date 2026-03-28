# CDN e DASH (Streaming de Vídeo)

## DASH (Dynamic Adaptive Streaming over HTTP)
- **Chunks:** Vídeo dividido em pedaços de 2-10s.
- **Multi-qualidade:** Várias taxas de bits (480p até 4K).
- **Manifest File (.mpd):** O "cardápio" com as URLs dos chunks.

## CDN (Content Distribution Network)
Rede de servidores distribuídos para entregar conteúdo rápido.
- **Enter Deep:** Servidores dentro dos ISPs locais.
- **Bring Home:** Mega-clusters em pontos de troca de tráfego.

## 🛡️ Cybersec Insight
- **DDoS Mitigation:** CDNs absorvem ataques volumétricos.
- **Side-Channel Attacks:** Análise do tamanho dos chunks pode revelar o que o usuário está assistindo mesmo via HTTPS.
