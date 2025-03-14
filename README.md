# Dinâmica: Design Estratégico do Projeto

# Entrega da Atividade DDD-1
### Alunos:

| Nome                           | RM      |
|--------------------------------|--------|
| FERNANDO REBELATO SAETA       | 359961 |
| INGO HENRIQUE ALMENDROS GIRÃO | 358616 |
| KALEO VIEIRA LEITE            | 359754 |
| NATHAN GRECCO FONSECA         | 359289 |

## 1. Nome do Projeto
**GameNow**

---

## 2. Objetivo Principal do Projeto
**Conectar jogadores de níveis compatíveis a partidas esportivas coletivas, simplificando a organização e facilitando o acesso a locais acessíveis.**  

---

## 3. Identificação dos Subdomínios

| **Subdomínio**              | **Descrição**                                                                                      | **Tipo**         |
|-----------------------------|--------------------------------------------------------------------------------------------------|------------------|
| Agendamento de Partidas | Gerencia a criação, busca e organização de eventos esportivos. | Core Domain  |
| Gerenciador de Players da Partida | Gerencia a criação, busca e organização de eventos esportivos. | Core Domain  |
| Gerenciamento de Times | Permite a formação de grupos para participação em torneios e partidas.                         | Supporting       |
| Sistema de Localização | Fornece geolocalização de espaços esportivos e filtros de proximidade.                           | Generic          |
Avaliação de Habilidades | Classifica jogadores por nível técnico para compatibilidade em partidas. | Supporting

---

## 4. Desenho dos Bounded Contexts

| **Bounded Context**           | **Responsabilidade**                                                              | **Subdomínios Relacionados** |
|-------------------------------|-----------------------------------------------------------------------------------|------------------------------|
|Agendamento de Partidas| Criação de eventos, gestão de horários, notificação de participantes e integração com locais. | Agendamento de Partidas, Sistema de Localização|
|Gerenciamento de Times| Formação de equipes, convites a jogadores e participação em competições.| Gerenciamento de Times, Avaliação de Habilidades, Players |
Localização |Integração com APIs de mapas e filtragem de espaços com base em acessibilidade e avaliações|Sistema de Localização |
| Locais de Esporte | Armazena informações sobre os locais, reputação, localização relacionadas com as modalidades de esportes. | Modalidade de Esportes, Agendamento de Partidas, Localização |
Players | Armazena dados de nível técnico, histórico de partidas e reputação.|Avaliação de Habilidades|
| Esportes | Manter preferências dos players e criação de regras para cada Modalidade. | Agendamento de Partidas, Organização de Players da Partida, Modalidade de Esportes |



---

## 5. Comunicação entre os Bounded Contexts

| **De (Origem)**              | **Para (Destino)**          | **Forma de Comunicação**    | **Exemplo de Evento/Chamada**                  |
|------------------------------|-----------------------------|-----------------------------|-----------------------------------------------|
|Agendamento de Partidas|Perfil do Jogador|API (síncrono)|Consultar nível técnico para sugestão de partidas|
|Agendamento de Partidas|Gerenciamento de times|API (síncrono)|Obter seleção de times disponíveis|
| Agendamento de Partidas | Locais de Esporte | API (síncrono) | Verificar disponibilidade do local para a partida |
| Agendamento de Partidas | Esportes   | API (síncrono)  | Validar regras do esporte para criação de partidas |
|Gerenciamento de Times|Agendamento de Partidas| Mensageria (Evento)|“Time Formado” → Notificar participantes do evento|
| Gerenciamento de Times       | Players                       | API (síncrono)            | Atualizar os times do jogador |
| Gerenciamento de Times       | Avaliação de Habilidades      | API (síncrono)            | Enviar estatísticas da performance dos jogadores |
|Localização Esportiva|Agendamento de Partidas|API (síncrono)|Buscar locais disponíveis por raio de distância|
| Localização Esportiva        | Locais de Esporte             | API (síncrono)            | Obter avaliações e acessibilidade dos locais |
| Locais de Esporte            | Agendamento de Partidas       | Mensageria (Evento)       | “Local Reservado” → Confirmar agendamento da partida |
| Players                      | Avaliação de Habilidades      | API (síncrono)            | Registrar nova avaliação após a partida |
| Players                      | Esportes                      | API (síncrono)            | Atualizar preferências de esporte do jogador |

---

## 6. Definição da Linguagem Ubíqua

| **Termo**                    | **Descrição**                                                                                   |
|------------------------------|-----------------------------------------------------------------------------------------------|
|Partida|Evento esportivo com data, local, esporte específico e participantes.|
|Nível Técnico|Classificação dos jogadores (iniciante, intermediário ou avançado) baseada no histórico de partidas realizadas.|
|Local|Espaço esportivo com infraestrutura adequada e avaliação da comunidade.|
Reputação|Pontuação baseada em participação, pontualidade e feedback de outros jogadores.
|Players da Partida|Formação de players inscritos na partida com base na modalidade do esporte|
|Modalidade|Modalidade do esporte selecionado, limitando e agregando os jogadores.

---

## 7. Estratégia de Desenvolvimento

| **Subdomínio**              | **Estratégia**                         | **Ferramentas ou Serviços (se aplicável)** |
|-----------------------------|---------------------------------------|-------------------------------------------|
|Agendamento de Partidas|Desenvolvimento interno (foco total)|Node.js, RabbitMQ para eventos|
|Gerenciamento de Times|Desenvolvimento interno|Firebase (armazenamento de grupos)|
|Sistema de Localização|Terceirizado via API|Google Maps API, OpenStreetMap|
Avaliação de Habilidades|Desenvolvimento interno utilizando algoritmos personalizados e técnicas de Machine Learning para análise preditiva do desempenho dos jogadores.|Python, TensorFlow (análise de histórico)

---

## 8. Diagrama Visual - GameNow

```
Agendamento de Partidas --> Perfil do Jogador: Consulta API
Agendamento de Partidas --> Sistema de Localização: Busca Locais
Agendamento de Partidas --> Gerenciamento de Times: Publica Evento
Gerenciamento de Times --> Perfil do Jogador: Atualiza Habilidades
Sistema de Localização --> Google Maps API: Integração
Perfil do Jogador --> Machine Learning: Treina Modelo
```

## Dicas para Apresentação
- Explique cada parte do design, focando no **Core Domain** (o coração do negócio).
- Justifique por que certos subdomínios foram classificados como Supporting ou Generic.
- Destaque como a comunicação entre bounded contexts foi pensada para ser escalável.

---

Boa sorte com a dinâmica! 🚀
