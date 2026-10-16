
# PRD — Tiras_Study

Documento de Requisitos do Produto · Desenvolvimento Web II

## 1. Visão geral e objetivo

O Tiras_Study é uma plataforma educacional desenvolvida para ajudar estudantes a compreender conteúdos escolares de maneira mais divertida, didática e colaborativa.

O projeto busca resolver a dificuldade de aprendizagem de alunos que precisam de explicações mais acessíveis, oferecendo um ambiente para compartilhar resumos, mapas mentais, trabalhos e vídeos explicativos, além de organizar os estudos e divulgar oportunidades educacionais.

Objetivo principal: facilitar a aprendizagem entre colegas, incentivar a constância nos estudos e ampliar o acesso a conteúdos escolares e atividades extracurriculares.

## 2. Público-alvo

- Estudantes: público principal da plataforma, que poderá acessar conteúdos, compartilhar materiais e organizar os estudos.
- Alunos de diferentes séries: poderão consultar conteúdos de anos anteriores e ajudar outros estudantes.
- Mentores e colaboradores educacionais: poderão contribuir com orientações e apoiar a aprendizagem.
- Comunidade escolar: poderá acompanhar informações sobre aulas extracurriculares e projetos educacionais.

## 3. Escopo do projeto

| Dentro do escopo                          | Fora do escopo inicial                       |
| ----------------------------------------- | -------------------------------------------- |
| Cadastro e login de alunos                | Sistema de notas e boletins escolares        |
| Perfil acadêmico e foto de perfil         | Integração automática com sistemas escolares |
| Página inicial com avisos e conteúdos     | Aulas ao vivo com videoconferência própria   |
| Conteúdos organizados por série           | Correção automática de provas                |
| Compartilhamento de materiais de estudo   | Emissão de certificados oficiais             |
| Plano e sequências de estudos             | Aplicativo móvel nativo                      |
| Divulgação de aulas extracurriculares     | Pagamentos dentro da plataforma              |
| Divulgação de projetos externos e editais | Inscrição automática em eventos externos     |

Observação: os itens fora do escopo são delimitações propostas para a primeira versão, não restrições explicitamente definidas no PDF.

## 4. Requisitos funcionais

Os requisitos funcionais descrevem as ações que o sistema deverá permitir aos usuários.

| Código | Requisito funcional                                                                               |
| ------ | ------------------------------------------------------------------------------------------------- |
| RF01   | Permitir o cadastro de alunos com nome completo, e-mail, série escolar e senha.                   |
| RF02   | Permitir que alunos cadastrados realizem login na plataforma.                                     |
| RF03   | Permitir a personalização do perfil com foto, nome, série e biografia.                            |
| RF04   | Exibir na página inicial avisos, novidades, conteúdos recomendados e projetos em destaque.        |
| RF05   | Permitir a visualização e organização do plano de estudos.                                        |
| RF06   | Disponibilizar conteúdos escolares organizados por série.                                         |
| RF07   | Permitir o acesso a conteúdos de séries anteriores.                                               |
| RF08   | Disponibilizar materiais de estudo, como resumos, mapas mentais, trabalhos e vídeos explicativos. |
| RF09   | Permitir a criação e o acompanhamento de sequências de estudos com amigos.                        |
| RF10   | Exibir conquistas e atividades realizadas pelo aluno.                                             |
| RF11   | Disponibilizar informações sobre aulas extracurriculares, horários, eventos e apresentações.      |
| RF12   | Exibir projetos externos, como olimpíadas, feiras científicas e concursos.                        |
| RF13   | Disponibilizar links para editais e inscrições de projetos externos.                              |
| RF14   | Oferecer acesso às áreas de interação com amigos e mentores.                                      |

Os requisitos RF08 e RF14 representam funcionalidades coerentes com a proposta colaborativa descrita no PDF; os detalhes de implementação ainda precisam ser definidos.

## 5. Requisitos não funcionais

| Categoria       | Requisito                                                                                                                   |
| --------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Desempenho      | As páginas e os conteúdos devem carregar em tempo adequado, mesmo com vários alunos acessando a plataforma.                 |
| Segurança       | Senhas devem ser armazenadas com proteção criptográfica adequada, e o acesso às contas deve ser controlado.                 |
| Usabilidade     | A interface deve ser intuitiva, organizada e fácil de utilizar.                                                             |
| Compatibilidade | A plataforma deve funcionar nos principais navegadores e adaptar-se a computadores e celulares.                             |
| Disponibilidade | O sistema deve permanecer acessível durante os períodos de estudo, com tratamento adequado de falhas.                       |
| Privacidade     | Os dados pessoais dos estudantes devem ser utilizados somente para finalidades informadas.                                  |
| LGPD            | A plataforma deve respeitar a Lei Geral de Proteção de Dados, com medidas de segurança, transparência e controle de acesso. |
| Acessibilidade  | Textos, botões e elementos de navegação devem ser legíveis e acessíveis a diferentes usuários.                              |

Observação: os requisitos acima são propostas para o projeto. Metas numéricas de desempenho, tecnologias e procedimentos de segurança ainda precisam ser estabelecidos.

## 6. Regras de negócio

- RN01: o cadastro deve exigir os dados necessários para identificar e autenticar o estudante.
- RN02: somente usuários autenticados poderão acessar as áreas que exigem login.
- RN03: os perfis deverão apresentar as informações acadêmicas e pessoais cadastradas pelo aluno.
- RN04: os conteúdos escolares deverão ser organizados por série para facilitar a localização.
- RN05: os estudantes poderão consultar materiais de séries anteriores.
- RN06: as sequências de estudos deverão permitir o acompanhamento da rotina de aprendizagem.
- RN07: as informações sobre aulas extracurriculares deverão apresentar os dados disponíveis sobre horários e eventos.
- RN08: os projetos externos deverão apresentar informações e links relacionados às oportunidades divulgadas.
- RN09: o tratamento de dados pessoais deverá respeitar a legislação aplicável, incluindo as exigências pertinentes à proteção de crianças e adolescentes.

## 7. Fluxos principais

### Fluxo 1 — Cadastro e login

Acessar a plataforma

Criar conta ou realizar login

Validar os dados de acesso

Acessar a página inicial

### Fluxo 2 — Acesso aos conteúdos escolares

Entrar na plataforma

Acessar conteúdos por série

Selecionar uma matéria ou material

Consultar o conteúdo de estudo

### Fluxo 3 — Consulta de projetos externos

Acessar projetos externos

Visualizar as oportunidades disponíveis

Consultar o edital e acessar o link de inscrição

## 8. Critérios de aceitação

| Código | Critério de aceitação                                                                               |
| ------ | --------------------------------------------------------------------------------------------------- |
| CA01   | O aluno consegue criar uma conta preenchendo os campos obrigatórios.                                |
| CA02   | O sistema permite login com credenciais válidas e rejeita credenciais inválidas.                    |
| CA03   | O aluno consegue visualizar e personalizar seu perfil.                                              |
| CA04   | A página inicial apresenta os principais acessos e informações da plataforma.                       |
| CA05   | O aluno consegue localizar conteúdos de sua série e de séries anteriores.                           |
| CA06   | Os materiais disponibilizados podem ser acessados de acordo com seu formato e suas permissões.      |
| CA07   | O aluno consegue visualizar suas sequências de estudos e atividades registradas.                    |
| CA08   | As informações sobre aulas extracurriculares são exibidas de forma organizada.                      |
| CA09   | Os projetos externos apresentam informações e links funcionais quando disponíveis.                  |
| CA10   | Os dados pessoais são protegidos por controles de acesso e medidas de segurança apropriadas.        |
| CA11   | As páginas principais podem ser utilizadas nos navegadores e dispositivos previstos para o projeto. |

## 9. Priorização (MVP) e riscos

### 9.1. Funcionalidades do MVP

O MVP é a primeira versão funcional da plataforma, contendo os recursos essenciais para validar a proposta.

Prioridade alta — Essencial

Cadastro e login, perfil do aluno, página inicial e conteúdos organizados por série.

Prioridade média — Complementar

Plano de estudos, sequências de estudo, conquistas e compartilhamento de materiais.

Prioridade posterior — Expansão

Recursos ampliados de interação com mentores e amigos, além de melhorias na divulgação e organização de atividades extracurriculares e projetos externos.

### 9.2. Principais riscos

| Risco                              | Impacto | Mitigação proposta                                                    |
| ---------------------------------- | ------- | --------------------------------------------------------------------- |
| Divulgação de informações pessoais | Alto    | Implementar controles de acesso e proteção de dados.                  |
| Publicação de conteúdos incorretos | Médio   | Criar mecanismos de revisão e denúncia de materiais.                  |
| Links externos indisponíveis       | Médio   | Verificar periodicamente os links divulgados.                         |
| Baixa participação dos estudantes  | Médio   | Incentivar o compartilhamento de materiais e as sequências de estudo. |
| Dificuldade de navegação           | Médio   | Testar a interface com estudantes e simplificar os fluxos.            |
| Crescimento do volume de acessos   | Médio   | Monitorar o desempenho e otimizar o sistema conforme a demanda.       |

## Resultado esperado

O Tiras_Study deverá oferecer um ambiente educacional organizado, intuitivo e colaborativo, no qual os estudantes possam encontrar conteúdos escolares, compartilhar conhecimentos, planejar seus estudos e descobrir oportunidades educacionais.

O sucesso do projeto poderá ser avaliado pela facilidade de utilização, pelo acesso aos materiais, pela participação dos estudantes e pela capacidade da plataforma de incentivar uma rotina de estudos mais constante.

Base do documento: PDF “Trabalho de desenvolvimento web 2”, páginas 2 a 10. As regras técnicas, prioridades, critérios de aceitação e riscos foram propostos para completar o PRD, pois não estão detalhados integralmente no material original.
