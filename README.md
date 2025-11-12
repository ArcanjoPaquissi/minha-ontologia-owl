# minha-ontologia-owl
A ontologia de música tem como objetivo estruturar formalmente os conceitos do domínio musical, permitindo a representação de músicas, artistas, álbuns, instrumentos e gêneros musicais, bem como seus atributos e relacionamentos.

#  Ontologia de Música (OntoMusic)

Ontologia desenvolvida para representar o domínio musical, descrevendo entidades como músicas, artistas, álbuns, instrumentos e gêneros musicais.  
O projeto segue princípios de **Linked Data**, integrando dados reais da **DBpedia**.

**Formato:** RDF/OWL (RDF/XML)  
**Ferramenta:** Protégé / WebProtégé  
**Autor:** Arcanjo Paquissi  

---

##  Objetivo

Modelar o domínio da música de forma semântica, permitindo interoperabilidade entre dados musicais, sistemas e repositórios de conhecimento.

---

##  Escopo

A ontologia abrange os seguintes conceitos:

- Músicas e seus atributos (título, duração, data de lançamento)
- Artistas (cantores, compositores, instrumentistas, bandas)
- Instrumentos musicais
- Álbuns
- Gêneros musicais

---

##  Estrutura de Classes

- **Música**
  - Subclasses: MúsicaPop, MúsicaRock, MúsicaClássica, MúsicaSertaneja
- **Artista**
  - Subclasses: Cantor, Compositor, Instrumentista, Banda
- **Álbum**
- **InstrumentoMusical**
  - Subclasses: Violão, Piano, Guitarra, Bateria
- **GêneroMusical**

---

##  Propriedades Principais

| Tipo | Propriedade | Domínio | Alcance | Descrição |
|------|--------------|----------|----------|------------|
| Data | temTitulo | Música | string | Título da música |
| Data | temDuracao | Música | integer | Duração em segundos |
| Data | foiLancadaEm | Música | date | Data de lançamento |
| Data | temNomeArtistico | Artista | string | Nome artístico do artista |
| Data | temNacionalidade | Artista | string | Nacionalidade |
| Objeto | temArtista | Música | Artista | Liga uma música ao artista |
| Objeto | fazParteDoAlbum | Música | Álbum | Liga uma música ao álbum |
| Objeto | temGenero | Música | GêneroMusical | Liga uma música ao gênero |
| Objeto | tocouInstrumento | Artista | InstrumentoMusical | Indica o instrumento tocado |
| Objeto | ehCompostaPor | Banda | Artista | Define os membros da banda |

---

##  Integração com DBpedia

A ontologia conecta-se a recursos reais da **DBpedia** por meio das propriedades `owl:equivalentClass` e `owl:sameAs`.

### Classes com equivalência
- `MúsicaPop` → <http://dbpedia.org/resource/Pop_music>
- `MúsicaRock` → <http://dbpedia.org/resource/Rock_music>
- `MúsicaClássica` → <http://dbpedia.org/resource/Classical_music>
- `MúsicaSertaneja` → <http://dbpedia.org/resource/Sertanejo>
- `GêneroMusical` → <http://dbpedia.org/resource/Music_genre>

### Instâncias conectadas
- `JohnLennon` → <http://dbpedia.org/resource/John_Lennon>
- `Imagine (música)` → <http://dbpedia.org/resource/Imagine_(John_Lennon_song)>
- `Imagine (álbum)` → <http://dbpedia.org/resource/Imagine_(John_Lennon_album)>

---

##  Exemplo de Instâncias

| Entidade | Tipo | Propriedades |
|-----------|------|---------------|
| JohnLennon | Cantor, Compositor | temNomeArtistico = "John Lennon", temNacionalidade = "Reino Unido" |
| ImagineMusica | Música | temTitulo = "Imagine", temArtista = JohnLennon, temGenero = Pop |
| AlbumImagine | Álbum | temNomeDoAlbum = "Imagine", temAnoDeLancamento = 1971 |

---

##  Exemplos Visuais (para adicionar no GitHub)

Coloque na pasta `/docs/` prints do Protégé mostrando:
- Hierarquia de classes (*Classes tab*)
- Object properties (*Object Properties tab*)
- Individuals com links DBpedia (*Individuals tab*)

---

##  Consultas SPARQL (Exemplo)

```sparql
# Listar todas as músicas e seus artistas
SELECT ?musica ?artista
WHERE {
  ?musica rdf:type :Musica .
  ?musica :temArtista ?artista .
}
