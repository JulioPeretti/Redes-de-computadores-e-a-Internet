# CDN e DASH (Streaming de Vídeo)
camada: [Camada de Aplicação](./Camada%20de%20Aplicação.md)

## O Problema
O vídeo consome a maior parte da banda da internet.
- **Problema:** Arquivos gigantes e usuários espalhados pelo mundo. Um único servidor não aguenta.
- **Solução:** Compressão e Distribuição (CDN).

## DASH (Dynamic Adaptive Streaming over HTTP)
É a tecnologia padrão para streaming moderno (YouTube, Netflix).
- **Funcionamento:**
    1. **Chunks (Pedaços):** O vídeo é dividido em pequenos arquivos de 2 a 10 segundos.
    2. **Multi-qualidade:** Cada chunk é codificado em várias taxas de bits (ex: 480p, 720p, 1080p, 4K).
    3. **Manifest File (.mpd):** Um arquivo "cardápio" que lista as URLs de todos os chunks e suas qualidades.
- **Inteligência no Cliente:**
    - Diferente da TV (onde o servidor manda), no DASH o **Cliente (Player)** decide.
    - O Player mede a banda da rede em tempo real e pede o próximo chunk na melhor qualidade possível sem travar (buffer).

## CDN (Content Distribution Network)
Uma rede de servidores distribuídos geograficamente para entregar conteúdo rápido e aliviar o servidor de origem.

### Estratégias de Posicionamento
1. **Enter Deep:** Colocar servidores de cache *dentro* das redes dos provedores de acesso (ISPs) locais. (Ex: Akamai). Menor latência, mais complexo de gerenciar.
2. **Bring Home:** Construir mega-clusters em pontos estratégicos de troca de tráfego (IXPs). (Ex: Google, Limelight). Menos servidores, mas conexões muito rápidas.

### Como Funciona (DNS Redirection)
A CDN usa o [DNS](./DNS.md) para direcionar o usuário.
1. Usuário pede `video.netflix.com`.
2. DNS da Netflix retorna um registro `CNAME` apontando para a CDN.
3. DNS da CDN analisa o IP do usuário e retorna o IP do servidor de cache mais próximo fisicamente.

## 🛡️ Cybersec Insight
- **DDoS Mitigation:** CDNs agem como um "escudo gigante". Elas têm tanta banda que conseguem absorver ataques de Negação de Serviço volumétricos antes que eles atinjam o servidor de origem ("Matriz").
- **DRM (Digital Rights Management):**
