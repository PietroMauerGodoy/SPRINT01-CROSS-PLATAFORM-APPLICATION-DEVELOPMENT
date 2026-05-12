#  Monitoramento Inteligente de Vegetação Rodoviária

> Projeto desenvolvido para o **Challenge CCR Motiva – 2º Ano | Ciência da Computação | FIAP**

---

## 👥 Integrantes

| Nome | RM |
|------|----|
| Fernando Melo | 564397 |
| Patrick Mansour | 562970 |
| Pedro Henrique Ribeiro | 565090 |
| Pietro Mauer | 564345 |
| Samir Assad | 561562 |


---

## 🔗 Links

- 📁 **Repositório GitHub:** `https://github.com/PietroMauerGodoy/SPRINT01-CROSS-PLATAFORM-APPLICATION-DEVELOPMENT/edit/main`
- 🎨 **Protótipo Figma:** `https://www.figma.com/design/xDrv0Gh5IBisznjjxVvkSe/Prot%C3%B3tipo---Motiva?node-id=0-1&t=YSunzYBv0ezLlhi9-1`

---

## 🧩 Sobre o Desafio

A **Motiva** é uma das maiores empresas de infraestrutura de mobilidade do Brasil, administrando milhares de quilômetros de rodovias federais e estaduais.

O desafio proposto consiste em criar uma solução tecnológica para **monitorar e gerenciar a vegetação ao longo das rodovias de forma inteligente**, substituindo o modelo atual — baseado em cronogramas fixos e inspeções presenciais — por um sistema orientado a dados, com priorização dinâmica e tomada de decisão mais eficiente.

### Problema atual

Hoje, equipes realizam a roçada em intervalos fixos (ex: a cada 30 dias), independentemente do real estado da vegetação no trecho. Isso gera:

- Intervenções desnecessárias em trechos que não precisam (custo elevado)
- Atraso em trechos críticos que crescem mais rápido (risco à segurança)
- Falta de dados históricos por trecho
- Decisões baseadas em percepção humana, não em evidências

---

## 💡 Nossa Solução

É um aplicativo mobile voltado para operadores de campo e gestores da Motiva, que permite:

1. **Registrar ocorrências por trecho** com foto, observação e dados do último serviço realizado
2. **Classificar automaticamente o nível de crescimento** via IA, com base nos dados coletados
3. **Visualizar o painel Kanban** com os trechos organizados por criticidade
4. **Receber notificações em tempo real** quando um trecho muda de nível de risco
5. **Acessar o detalhe completo** de cada ocorrência com a previsão da IA

---

## 👤 Usuários do App

| Perfil | Responsabilidade |
|--------|-----------------|
| **Operador de Campo** | Registra o estado da vegetação no trecho com foto, observação e histórico do último serviço |
| **Gestor / Supervisor** | Acompanha o painel Kanban, recebe notificações e toma decisões sobre prioridade de intervenção |

---

## 📱 Funcionalidades do MVP (Sprint 1)

### Telas entregues no protótipo

| Tela | Descrição |
|------|-----------|
| **Login** | Autenticação do usuário com nome e senha |
| **Gerenciamento de Equipes** | Listagem das equipes operacionais com status, rodovia, trecho e responsável |
| **Visibilidade das Equipes (Kanban)** | Painel de ocorrências organizadas por criticidade de crescimento |
| **Detalhe da Ocorrência (Popup)** | Expansão do card com foto do trecho, observação, último serviço e previsão da IA |
| **Nova Ocorrência** | Formulário para registro de novo trecho pelo operador |

### Funcionalidades core

- ✅ Cadastro de ocorrência (com foto, observação, trecho e último serviço)
- ✅ Listagem de ocorrências por equipe
- ✅ Classificação de risco por nível de criticidade
- ✅ Painel Kanban com movimentação automática por IA
- ✅ Notificação ao gestor quando card muda de coluna
- ✅ Visualização de detalhe via popup expansível

---

## 🤖 Lógica de IA e Automação

Nosso diferencial está na **automação inteligente do Kanban**.

### Como funciona

```
Operador registra o trecho
        ↓
Sistema analisa: tempo desde último serviço + altura atual + tipo de vegetação
        ↓
IA estima o crescimento e classifica o card automaticamente
        ↓
Card é posicionado na coluna correta do Kanban
        ↓
Quando o card muda de coluna → Gestor recebe notificação
        ↓
Gestor clica no card → Popup com todos os detalhes + previsão da IA
```

### Colunas do Kanban

| Coluna | Faixa de Crescimento | Ação esperada |
|--------|----------------------|---------------|
| 🟢 **Todos os KMs** | Monitoramento geral | Nenhuma urgência |
| 🟡 **Leve** | 5cm a 15cm | Agendar intervenção |
| 🟠 **Grave** | 15cm a 25cm | Priorizar intervenção |
| 🔴 **Crítico** | 25cm a 30cm | Intervenção imediata |

### Exemplo de previsão da IA

```
Trecho: BR-116 | KM 0.0 → 5.0
Vegetação: Grama Bermuda (Rasteira)
Altura Atual: 12cm
→ Previsão da IA: Grave em ~4 dias
```

Esse modelo aprende com os dados históricos de cada trecho, identificando quais trechos têm crescimento mais acelerado e ajustando as previsões ao longo do tempo.

---

## 🎨 Design e Identidade Visual

O app segue a identidade visual da **Motiva**, com:

- Paleta roxa (#6B21A8 e variações) como cor primária
- Glassmorphism nos cards e modais
- Fundo com gradiente orgânico em tons de roxo
- Tipografia limpa e hierarquia visual clara
- Ícones intuitivos para uso em campo

---

## 🔄 Fluxo de Navegação (Protótipo)

```
[Login]
   ↓
[Gerenciamento de Equipes]  ←→  [Visibilidade das Equipes - Kanban]
                                          ↓
                                  [Detalhe da Ocorrência - Popup]
```

Todas as telas possuem navegação bidirecional conforme definido no protótipo Figma.

---

## 🗂️ Estrutura Técnica do Projeto

**Stack obrigatória:**
- React Native com Expo
- TypeScript

```plaintext
src/
├── screens/
│   ├── LoginScreen.tsx
│   ├── TeamManagementScreen.tsx
│   ├── KanbanScreen.tsx
│   ├── OccurrenceDetailScreen.tsx
│   └── NewOccurrenceScreen.tsx
├── components/
│   ├── KanbanCard.tsx
│   ├── OccurrencePopup.tsx
│   ├── TeamListItem.tsx
│   └── NotificationBadge.tsx
└── types/
    ├── Occurrence.ts
    ├── Team.ts
    └── RiskLevel.ts
```

---

## 📊 Conexão com o Desafio da Motiva

| Dor apresentada pela Motiva | Como o VegeTrack resolve |
|-----------------------------|--------------------------|
| Cronogramas fixos sem considerar o estado real | IA classifica e prioriza com base em dados reais |
| Falta de dados atualizados em tempo real | Operador registra em campo, painel atualiza instantaneamente |
| Dificuldade de priorização das áreas críticas | Kanban com 4 níveis de criticidade e movimentação automática |
| Dependência de inspeções humanas | Previsão de crescimento reduz necessidade de vistorias desnecessárias |
| Intervenções desnecessárias ou tardias | Gestor é notificado no momento certo, nem antes nem depois |
