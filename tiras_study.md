-- =========================================================
-- PROJETO: TIRAS_STUDY
-- BANCO DE DADOS RELACIONAL
-- SGBD: MySQL 8.0
-- =========================================================

CREATE DATABASE IF NOT EXISTS tiras_study
    CHARACTER SET utf8mb4
    COLLATE utf8mb4_unicode_ci;

USE tiras_study;

-- 1. USUARIOS
CREATE TABLE IF NOT EXISTS usuarios (
    id_usuario INT AUTO_INCREMENT PRIMARY KEY,
    nome_completo VARCHAR(150) NOT NULL,
    email VARCHAR(150) NOT NULL UNIQUE,
    senha_hash VARCHAR(255) NOT NULL,
    serie_escolar VARCHAR(50),
    tipo_usuario ENUM('estudante', 'mentor', 'administrador')
        NOT NULL DEFAULT 'estudante',
    foto_perfil VARCHAR(255),
    biografia TEXT,
    data_cadastro DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP
);

-- 2. CONTEUDOS ESCOLARES
CREATE TABLE IF NOT EXISTS conteudos (
    id_conteudo INT AUTO_INCREMENT PRIMARY KEY,
    titulo VARCHAR(150) NOT NULL,
    descricao TEXT,
    materia VARCHAR(100) NOT NULL,
    serie_escolar VARCHAR(50) NOT NULL,
    data_publicacao DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    id_autor INT NOT NULL,
    FOREIGN KEY (id_autor)
        REFERENCES usuarios(id_usuario)
        ON DELETE RESTRICT
        ON UPDATE CASCADE
);

-- 3. MATERIAIS DE ESTUDO
CREATE TABLE IF NOT EXISTS materiais_estudo (
    id_material INT AUTO_INCREMENT PRIMARY KEY,
    titulo VARCHAR(150) NOT NULL,
    tipo_material ENUM('resumo', 'mapa_mental', 'trabalho', 'video', 'outro')
        NOT NULL,
    descricao TEXT,
    arquivo_url VARCHAR(255) NOT NULL,
    data_publicacao DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    id_usuario INT NOT NULL,
    id_conteudo INT,
    FOREIGN KEY (id_usuario)
        REFERENCES usuarios(id_usuario)
        ON DELETE RESTRICT
        ON UPDATE CASCADE,
    FOREIGN KEY (id_conteudo)
        REFERENCES conteudos(id_conteudo)
        ON DELETE SET NULL
        ON UPDATE CASCADE
);

-- 4. PLANOS DE ESTUDO
CREATE TABLE IF NOT EXISTS planos_estudo (
    id_plano INT AUTO_INCREMENT PRIMARY KEY,
    titulo VARCHAR(150) NOT NULL,
    descricao TEXT,
    data_inicio DATE,
    data_fim DATE,
    id_usuario INT NOT NULL,
    FOREIGN KEY (id_usuario)
        REFERENCES usuarios(id_usuario)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);

-- 5. ATIVIDADES DOS PLANOS
CREATE TABLE IF NOT EXISTS atividades_plano (
    id_atividade INT AUTO_INCREMENT PRIMARY KEY,
    titulo VARCHAR(150) NOT NULL,
    descricao TEXT,
    data_prevista DATE,
    concluida BOOLEAN NOT NULL DEFAULT FALSE,
    id_plano INT NOT NULL,
    id_conteudo INT,
    FOREIGN KEY (id_plano)
        REFERENCES planos_estudo(id_plano)
        ON DELETE CASCADE
        ON UPDATE CASCADE,
    FOREIGN KEY (id_conteudo)
        REFERENCES conteudos(id_conteudo)
        ON DELETE SET NULL
        ON UPDATE CASCADE
);

-- 6. SEQUENCIAS DE ESTUDO
CREATE TABLE IF NOT EXISTS sequencias_estudo (
    id_sequencia INT AUTO_INCREMENT PRIMARY KEY,
    data_inicio DATE NOT NULL,
    data_fim DATE,
    dias_consecutivos INT NOT NULL DEFAULT 0,
    id_usuario INT NOT NULL,
    FOREIGN KEY (id_usuario)
        REFERENCES usuarios(id_usuario)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);

-- 7. AMIZADES ENTRE USUARIOS
CREATE TABLE IF NOT EXISTS amizades (
    id_amizade INT AUTO_INCREMENT PRIMARY KEY,
    id_usuario INT NOT NULL,
    id_amigo INT NOT NULL,
    status ENUM('pendente', 'aceita', 'recusada')
        NOT NULL DEFAULT 'pendente',
    data_solicitacao DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    UNIQUE (id_usuario, id_amigo),
    CHECK (id_usuario <> id_amigo),
    FOREIGN KEY (id_usuario)
        REFERENCES usuarios(id_usuario)
        ON DELETE CASCADE
        ON UPDATE CASCADE,
    FOREIGN KEY (id_amigo)
        REFERENCES usuarios(id_usuario)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);

-- 8. CONQUISTAS DISPONIVEIS
CREATE TABLE IF NOT EXISTS conquistas (
    id_conquista INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL UNIQUE,
    descricao TEXT
);

-- 9. CONQUISTAS DOS USUARIOS
CREATE TABLE IF NOT EXISTS usuarios_conquistas (
    id_usuario INT NOT NULL,
    id_conquista INT NOT NULL,
    data_conquista DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (id_usuario, id_conquista),
    FOREIGN KEY (id_usuario)
        REFERENCES usuarios(id_usuario)
        ON DELETE CASCADE
        ON UPDATE CASCADE,
    FOREIGN KEY (id_conquista)
        REFERENCES conquistas(id_conquista)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);

-- 10. AULAS EXTRACURRICULARES
CREATE TABLE IF NOT EXISTS aulas_extracurriculares (
    id_aula INT AUTO_INCREMENT PRIMARY KEY,
    titulo VARCHAR(150) NOT NULL,
    categoria VARCHAR(80) NOT NULL,
    descricao TEXT,
    horario VARCHAR(100),
    local VARCHAR(150),
    link_inscricao VARCHAR(255)
);

-- 11. PROJETOS EXTERNOS
CREATE TABLE IF NOT EXISTS projetos_externos (
    id_projeto INT AUTO_INCREMENT PRIMARY KEY,
    titulo VARCHAR(150) NOT NULL,
    tipo_projeto VARCHAR(100) NOT NULL,
    descricao TEXT,
    prazo_inscricao DATE,
    link_inscricao VARCHAR(255),
    data_publicacao DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP
);

-- 12. AVISOS DA PLATAFORMA
CREATE TABLE IF NOT EXISTS avisos (
    id_aviso INT AUTO_INCREMENT PRIMARY KEY,
    titulo VARCHAR(150) NOT NULL,
    mensagem TEXT NOT NULL,
    data_publicacao DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    id_usuario INT,
    FOREIGN KEY (id_usuario)
        REFERENCES usuarios(id_usuario)
        ON DELETE SET NULL
        ON UPDATE CASCADE
);

-- =========================================================
-- INDICES PARA MELHORAR AS CONSULTAS
-- =========================================================

CREATE INDEX idx_conteudos_serie
    ON conteudos(serie_escolar);

CREATE INDEX idx_conteudos_materia
    ON conteudos(materia);

CREATE INDEX idx_materiais_usuario
    ON materiais_estudo(id_usuario);

CREATE INDEX idx_planos_usuario
    ON planos_estudo(id_usuario);

CREATE INDEX idx_atividades_plano
    ON atividades_plano(id_plano);

CREATE INDEX idx_projetos_prazo
    ON projetos_externos(prazo_inscricao);

-- =========================================================
-- EXEMPLOS DE CONSULTAS (EXECUTE QUANDO DESEJAR)
-- =========================================================

-- Consultar conteudos por serie:
-- SELECT titulo, materia, serie_escolar
-- FROM conteudos
-- WHERE serie_escolar = '2º ano'
-- ORDER BY materia;

-- Consultar materiais publicados por um usuario:
-- SELECT m.titulo, m.tipo_material, m.arquivo_url,
--        c.titulo AS conteudo_relacionado
-- FROM materiais_estudo m
-- LEFT JOIN conteudos c ON m.id_conteudo = c.id_conteudo
-- WHERE m.id_usuario = 1;

-- Consultar atividades de um plano de estudo:
-- SELECT p.titulo AS plano, a.titulo AS atividade,
--        a.data_prevista, a.concluida
-- FROM planos_estudo p
-- INNER JOIN atividades_plano a ON p.id_plano = a.id_plano
-- WHERE p.id_usuario = 1;

-- Consultar projetos externos:
-- SELECT titulo, tipo_projeto, prazo_inscricao, link_inscricao
-- FROM projetos_externos
-- ORDER BY prazo_inscricao;

-- OBSERVACAO:
-- senha_hash deve receber uma senha protegida por hash seguro
-- gerado pela aplicacao. Nunca armazene senhas em texto puro.


-- =========================================================
-- 13. FLUXOGRAMA DO SISTEMA (MERMAID)
-- Este diagrama esta dentro de comentarios SQL para que
-- o arquivo continue executavel no MySQL.
-- Copie o conteudo Mermaid abaixo para um editor Mermaid.
--
-- ```mermaid
-- flowchart TD
--     A[Inicio] --> B{Usuario possui conta?}
--     B -- Nao --> C[Realizar cadastro]
--     C --> D[Entrar na plataforma]
--     B -- Sim --> D
--     D --> E[Painel inicial]
--     E --> F[Consultar conteudos escolares]
--     E --> G[Compartilhar material de estudo]
--     E --> H[Organizar plano de estudos]
--     E --> I[Consultar aulas extracurriculares]
--     E --> J[Consultar projetos externos]
--     F --> K[Selecionar materia e serie]
--     K --> L[Visualizar conteudo e materiais]
--     G --> M[Publicar resumo, mapa mental, trabalho ou video]
--     H --> N[Criar plano e atividades]
--     N --> O[Acompanhar progresso e sequencia de estudos]
--     I --> P[Consultar informacoes e inscricao]
--     J --> Q[Consultar oportunidade e link externo]
--     L --> R[Fim]
--     M --> R
--     O --> R
--     P --> R
--     Q --> R
-- ```
--
-- =========================================================
-- 14. DIAGRAMA ENTIDADE-RELACIONAMENTO (PLANTUML)
-- Este diagrama esta dentro de comentarios SQL para que
-- o arquivo continue executavel no MySQL.
-- Copie o conteudo PlantUML abaixo para um editor PlantUML.
--
-- ```plantuml
-- @startuml
-- hide circle
-- skinparam linetype ortho
--
-- entity "usuarios" as usuarios {
--   * id_usuario : INT <<PK>>
--   --
--   nome_completo : VARCHAR(150)
--   email : VARCHAR(150) <<UNIQUE>>
--   senha_hash : VARCHAR(255)
--   serie_escolar : VARCHAR(50)
--   tipo_usuario : ENUM
--   foto_perfil : VARCHAR(255)
--   biografia : TEXT
--   data_cadastro : DATETIME
-- }
--
-- entity "conteudos" as conteudos {
--   * id_conteudo : INT <<PK>>
--   --
--   titulo : VARCHAR(150)
--   descricao : TEXT
--   materia : VARCHAR(100)
--   serie_escolar : VARCHAR(50)
--   data_publicacao : DATETIME
--   id_autor : INT <<FK>>
-- }
--
-- entity "materiais_estudo" as materiais {
--   * id_material : INT <<PK>>
--   --
--   titulo : VARCHAR(150)
--   tipo_material : ENUM
--   descricao : TEXT
--   arquivo_url : VARCHAR(255)
--   data_publicacao : DATETIME
--   id_usuario : INT <<FK>>
--   id_conteudo : INT <<FK>>
-- }
--
-- entity "planos_estudo" as planos {
--   * id_plano : INT <<PK>>
--   --
--   titulo : VARCHAR(150)
--   descricao : TEXT
--   data_inicio : DATE
--   data_fim : DATE
--   id_usuario : INT <<FK>>
-- }
--
-- entity "atividades_plano" as atividades {
--   * id_atividade : INT <<PK>>
--   --
--   titulo : VARCHAR(150)
--   descricao : TEXT
--   data_prevista : DATE
--   concluida : BOOLEAN
--   id_plano : INT <<FK>>
--   id_conteudo : INT <<FK>>
-- }
--
-- entity "sequencias_estudo" as sequencias {
--   * id_sequencia : INT <<PK>>
--   --
--   data_inicio : DATE
--   data_fim : DATE
--   dias_consecutivos : INT
--   id_usuario : INT <<FK>>
-- }
--
-- entity "amizades" as amizades {
--   * id_amizade : INT <<PK>>
--   --
--   id_usuario : INT <<FK>>
--   id_amigo : INT <<FK>>
--   status : ENUM
--   data_solicitacao : DATETIME
-- }
--
-- entity "conquistas" as conquistas {
--   * id_conquista : INT <<PK>>
--   --
--   nome : VARCHAR(100)
--   descricao : TEXT
-- }
--
-- entity "usuarios_conquistas" as usuarios_conquistas {
--   * id_usuario : INT <<PK, FK>>
--   * id_conquista : INT <<PK, FK>>
--   --
--   data_conquista : DATETIME
-- }
--
-- entity "aulas_extracurriculares" as aulas {
--   * id_aula : INT <<PK>>
--   --
--   titulo : VARCHAR(150)
--   categoria : VARCHAR(80)
--   descricao : TEXT
--   horario : VARCHAR(100)
--   local : VARCHAR(150)
--   link_inscricao : VARCHAR(255)
-- }
--
-- entity "projetos_externos" as projetos {
--   * id_projeto : INT <<PK>>
--   --
--   titulo : VARCHAR(150)
--   tipo_projeto : VARCHAR(100)
--   descricao : TEXT
--   prazo_inscricao : DATE
--   link_inscricao : VARCHAR(255)
--   data_publicacao : DATETIME
-- }
--
-- entity "avisos" as avisos {
--   * id_aviso : INT <<PK>>
--   --
--   titulo : VARCHAR(150)
--   mensagem : TEXT
--   data_publicacao : DATETIME
--   id_usuario : INT <<FK, nullable>>
-- }
--
-- usuarios ||--o{ conteudos : publica
-- usuarios ||--o{ materiais : compartilha
-- conteudos ||--o{ materiais : relaciona
-- usuarios ||--o{ planos : organiza
-- planos ||--o{ atividades : contem
-- conteudos |o--o{ atividades : apoia
-- usuarios ||--o{ sequencias : registra
-- usuarios ||--o{ amizades : solicita
-- usuarios ||--o{ amizades : recebe
-- usuarios ||--o{ usuarios_conquistas : conquista
-- conquistas ||--o{ usuarios_conquistas : atribuida
-- usuarios |o--o{ avisos : publica
--
-- note bottom
--   aulas_extracurriculares e projetos_externos sao entidades
--   independentes neste modelo inicial, sem FK definida.
-- end note
-- @enduml
-- ```
--
-- FIM DOS DIAGRAMAS
-- =========================================================
