MagnetBR – Indexador de Filmes e Séries Brasileiros integração prowlarr

O MagnetBR é uma plataforma que centraliza diversos indexadores de filmes e séries brasileiros em um só lugar, facilitando a busca e o acesso a conteúdos nacionais. 

🚀 Funcionalidades
🔎 Busca por filmes e séries
🇧🇷 Foco em conteúdos brasileiros
📂 Organização

📌 link serve https://magnetbr.flixbr.online 

# 📦 MagnetBR – Indexador Prowlarr

Indexador customizado para **Prowlarr**, focado em filmes e séries com conteúdo em português.

---

## 🚀 Sobre

O **MagnetBR** é um indexador que centraliza resultados de filmes e séries, permitindo integração com:
- Prowlarr
- Radarr
- Sonarr
  
## 🔧 Instalação no Prowlarr

### Método 1 – Importando manualmente

1. Acesse o Prowlarr
2. Vá em **Settings → Indexers → Add Indexer**
3. Clique em **Custom**
4. Cole o conteúdo abaixo

---

## 📋 Configuração (.yml)

```yaml
---
id: magnetbr
name: MagnetBR
description: "MagnetBR - Indexador de Torrents Magnet Brasileiro (Radarr & Sonarr)"
language: pt-BR
type: public
encoding: UTF-8
links:
  - https://magnetbr.flixbr.online/

caps:
  categories:
    Movies: Movies
    TV: TV

  modes:
    search: [q]
    tv-search: [q, season, ep, imdbid]
    movie-search: [q, imdbid]

settings:
  - name: scraper_type
    type: select
    label: Fonte (todas respondem do catálogo; o bot alimenta em segundo plano)
    default: db
    options:
      db: "Catálogo completo (recomendado)"
      hybrid: "Catálogo completo (nome antigo: Híbrido)"
      all: "Catálogo completo (nome antigo: Todos)"
      starck: "Só itens do Starck"
      rede: "Só itens do Rede"
      tfilme: "Só itens do Tfilme"
      comand: "Só itens do Comando"
      bludv: "Só itens do Bludv"
      torrentclaw: "Só itens do TorrentClaw (Animes)"

search:
  paths:
    - path: "/indexers/{{ .Config.scraper_type }}"
      response:
        type: json
  inputs:
    q: "{{ if .Query.IMDBID }}{{ .Query.IMDBID }}{{ else }}{{ .Keywords }}{{ end }}"
    # busca por IMDb perde a temporada/episódio: manda separado para o servidor filtrar só aquela temporada
    season: "{{ .Query.Season }}"
    ep: "{{ .Query.Ep }}"
  keywordsfilters:
    - name: tolower
    - name: re_replace
      args: ["(?i)(S0)(\\d{1,2})$", "temporada $2"]
    - name: re_replace
      args: ["(?i)(S)(\\d{1,3})$", "temporada $2"]

  rows:
    selector: $.results
    count:
      selector: $.count
      optional: true

  fields:
    download:
      selector: magnet_link
    title:
      selector: title
    description:
      selector: original_title
    details:
      selector: details
    infohash:
      selector: info_hash
    date:
      selector: date
    size:
      selector: size
      optional: true
      filters:
        - name: re_replace
          args: ["^(|0 B|0B)$", "2,5 GB"]
    seeders:
      selector: seed_count
      filters:
        - name: re_replace
          args: ["^(|null|0)$", "1"]
    leechers:
      selector: leech_count
      filters:
        - name: re_replace
          args: ["^(|null|0)$", "1"]
    imdb:
      selector: imdb
      optional: true
    category_is_tv_show:
      selector: title
      filters:
        - name: regexp
          args: "(?i)(temporada|season|S\\d{1,3}E\\d{1,3}|\\bS\\d{1,3}\\b|\\d+x\\d+|série|series|episódio|episode|EP\\d+|1ª|2ª|3ª|4ª|5ª|6ª|7ª|8ª|9ª|10ª|completa|\\[jap\\]|anime)"
    category:
      text: "{{ if .Result.category_is_tv_show }}TV{{ else }}Movies{{ end }}"


