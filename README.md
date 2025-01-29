# Dinâmica: Design Estratégico do Projeto

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
| Gerenciamento de Times | Permite a formação de grupos para participação em torneios e partidas.                         | Supporting       |
| Sistema de Localização | Fornece geolocalização de espaços esportivos e filtros de proximidade.                           | Generic          |
Avaliação de Habilidades | Classifica jogadores por nível técnico para compatibilidade em partidas. | Supporting

---

## 4. Desenho dos Bounded Contexts

| **Bounded Context**           | **Responsabilidade**                                                              | **Subdomínios Relacionados** |
|-------------------------------|-----------------------------------------------------------------------------------|------------------------------|
|Agendamento de Partidas| Criação de eventos, gestão de horários, notificação de participantes e integração com locais. | Agendamento de Partidas, Sistema de Localização|
|Gerenciamento de Times| Formação de equipes, convites a jogadores e participação em competições.| Gerenciamento de Times, Avaliação de Habilidades|
Localização Esportiva|Integração com APIs de mapas e filtragem de espaços com base em acessibilidade e avaliações|Sistema de Localização|
Perfil do Jogador|Armazena dados de nível técnico, histórico de partidas e reputação.|Avaliação de Habilidades


---

## 5. Comunicação entre os Bounded Contexts

| **De (Origem)**              | **Para (Destino)**          | **Forma de Comunicação**    | **Exemplo de Evento/Chamada**                  |
|------------------------------|-----------------------------|-----------------------------|-----------------------------------------------|
|Agendamento de Partidas|Perfil do Jogador|API (síncrono)|Consultar nível técnico para sugestão de partidas|
|Gerenciamento de Times|Agendamento de Partidas| Mensageria (Evento)|“Time Formado” → Notificar participantes do evento|
|Localização Esportiva|Agendamento de Partidas|API (síncrono)|Buscar locais disponíveis por raio de distância

---

## 6. Definição da Linguagem Ubíqua

| **Termo**                    | **Descrição**                                                                                   |
|------------------------------|-----------------------------------------------------------------------------------------------|
|Partida|Evento esportivo com data, local, esporte específico e participantes.|
|Nível Técnico|Classificação dos jogadores (iniciante, intermediário ou avançado) baseada no histórico de partidas realizadas.|
|Local Acessível|Espaço esportivo com infraestrutura adequada e avaliação da comunidade.|
Reputação|Pontuação baseada em participação, pontualidade e feedback de outros jogadores.

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
