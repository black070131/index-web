ThePirataFilmes – Indexador de Filmes e Séries Brasileiros integração prowlarr

O ThePirataFilmes é uma plataforma que centraliza diversos indexadores de filmes e séries brasileiros em um só lugar, facilitando a busca e o acesso a conteúdos nacionais.

📌 Sobre o Projeto
link https://www.thepiratafilmes.online 

🔄 Método 2: Arquivo local (.yml)
1. Localize a pasta do Prowlarr

2. https://github.com/black070131/index-web/blob/main/prowlarr.yml

Se estiver usando Docker, normalmente:

/config/Definitions/Custom/

Se não existir, você pode criar.

2. Copie o arquivo .yml

Exemplo:

meu-indexador.yml

Coloque dentro da pasta:

/config/Definitions/Custom/
3. Reinicie o Prowlarr
Docker:
docker restart prowlarr
Ou reinicie o serviço
4. Adicione o indexador
Vá em:
Indexers
Clique em Add Indexer
Procure pelo nome do indexador custom

O projeto foi criado com o objetivo de reunir links de diferentes fontes disponíveis na internet, permitindo que usuários encontrem filmes e séries brasileiras de forma rápida, prática e organizada.


🚀 Funcionalidades
🔎 Busca por filmes e séries
🇧🇷 Foco em conteúdos brasileiros
📂 Organização por categorias (gênero, ano, etc.)
