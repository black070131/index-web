ThePirataFilmes – Indexador de Filmes e Séries Brasileiros integração prowlarr

O ThePirataFilmes é uma plataforma que centraliza diversos indexadores de filmes e séries brasileiros em um só lugar, facilitando a busca e o acesso a conteúdos nacionais.

📌 Sobre o Projeto
link https://www.thepiratafilmes.online 

O projeto foi criado com o objetivo de reunir links de diferentes fontes disponíveis na internet, permitindo que usuários encontrem filmes e séries brasileiras de forma rápida, prática e organizada.

🚀 Funcionalidades
🔎 Busca por filmes e séries
🇧🇷 Foco em conteúdos brasileiros
📂 Organização por categorias (gênero, ano, etc.)

prowlarr

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

