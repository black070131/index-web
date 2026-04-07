ThePirataFilmes – Indexador de Filmes e Séries Brasileiros integração prowlarr , stremio

O ThePirataFilmes é uma plataforma que centraliza diversos indexadores de filmes e séries brasileiros em um só lugar, facilitando a busca e o acesso a conteúdos nacionais. 

🚀 Funcionalidades
🔎 Busca por filmes e séries
🇧🇷 Foco em conteúdos brasileiros
📂 Organização por categorias (gênero, ano, etc.)

📌 link serve https://www.thepiratafilmes.online 

# 📦 ThepirataFilmes – Indexador Prowlarr

Indexador customizado para **Prowlarr**, focado em filmes e séries com conteúdo em português.

---

## 🚀 Sobre

O **ThepirataFilmes** é um indexador que centraliza resultados de filmes e séries, permitindo integração com:
- stremio
- Prowlarr
- Radarr
- Sonarr
# 🎬 Addon Stremio

Addon integrado para exibição de filmes e séries via indexador.

## 🚀 Como instalar

Para adicionar o addon no Stremio é bem simples:

1. Acesse o link do addon  
2. Clique no botão **"Install" (Instalar no Stremio)**  
3. O Stremio abrirá automaticamente  
4. Confirme a instalação  

Pronto! ✅ O addon já estará disponível no seu Stremio.

## ⚙️ Observações

- O funcionamento depende da disponibilidade de **seeders**  
- Conteúdos com mais seeders carregam mais rápido  
- Conteúdos com poucos seeders podem apresentar lentidão ou não carregar  

## 📌 Requisitos

- Ter o :contentReference[oaicite:0]{index=0} instalado

## 🧩 Sobre

Este addon utiliza fontes baseadas em torrent integradas via indexador, permitindo buscar e reproduzir conteúdos diretamente no Stremio.

Ideal para quem quer melhorar cobertura de buscas sem depender de múltiplas fontes.

---

## 🔧 Instalação no Prowlarr

### Método 1 – Importando manualmente

1. Acesse o Prowlarr
2. Vá em **Settings → Indexers → Add Indexer**
3. Clique em **Custom**
4. Cole o conteúdo abaixo

---

## 📋 Configuração (.yml)

```yaml
id: thepiratafilmes
name: ThepirataFilmes
description: "ThepirataFilmes - Seu catálogo premium de filmes e séries"
language: pt-BR
type: public
encoding: UTF-8

links:
  - https://www.thepiratafilmes.online
  - https://catalago.online/

caps:
  categories:
    2000: Movies
    5000: TV
  modes:
    search: [q]
    tv-search: [q, imdbid, tvdbid, tmdbid]
    movie-search: [q, imdbid, tmdbid]

settings: []

search:
  paths:
    - path: "api/search"
      method: get
      response:
        type: json
      inputs:
        q: "{{ .Keywords }}"
        tmdbid: "{{ .Query.TMDBID }}"
        imdbid: "{{ .Query.IMDBID }}"

  rows:
    selector: "$"

  fields:
    title:
      selector: "title"
    size:
      selector: "size"
    download:
      selector: "magnet_link"
    seeders:
      selector: "seed_count"
    imdbid:
      selector: "imdb"
    details:
      selector: "details"
    category:
      selector: "category"


