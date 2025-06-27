https://drive.google.com/drive/folders/1G36RmcFYUPF9cZGkqYQfm0aW9e5_XhZD

A receita de preenchimento manual da instituição está no link acima 

Pensei em uma prescrição médica em 2 vias com as mesmas ocupando todo o espaço de um papel A4 sendo lado a lado em formato paisagem. A receita replica tudo que é escrito na primeira na segunda via. E insere-se o nome no médico, CRM E ESPECIALIDADE. E logo a baixo os dados do paciente. Cada item tem um título fixo e a edição de inserção começa após o título. O primeiro título é profissional com cabeçalho descrevendo a receita, a via e o logo do hospital nossa senhora da Conceição. Logo após o nome do profissional vem o CRM e por último a especialidade porém o preenchimento começa pelo CRM pois quando digitados todos os dados do médico eles são salvos e acessados pelo CRM. Na caixa de prescrição 1 linha o uso podendo permitir a seleção do uso.
A segunda linha o princípio ativo com uma indentação em relação a primeira linha. Após o princípio ativo a dose por unidade posoligica. E no final desta linha preenchido com "-" o número total de comprimidos ou frascos o qual é preenchido automático pois após o princípio ativo ocorre o preenchimento da posologia que fica na próxima linha com indentação em relação a linha anterior.
Na última linha e último dados ser preenchido tem nova indentação em relação a linha anterior e após digitar o valor o mesmo é utilizado para calcular o número de comprimidos e a palavra dias aparece posteriormente. O processo de preenchimento do medicamento pode ser repetido .
Dentro da caixa da prescrição a data e colocada automaticamente no canto inferior esquerdo e no canto inferior direito aparece o nome e o CRM do médico em baixo e superior mete ao nome do médico uma linha para assinatura do mesmo.
O banco de dados salva o nome do médico e do medicamento prescrito com variação no número de dias. Isso tudo dentro de um HTML com possibilidade de geração de um banco de dados completo. Teste a receita e mostre o resultado

O modelo ficou ótimo mas queria mais próximo deste padrão. Sem salvar o nome do paciente no banco de dados. E que já tivesse uma impressão automática no modo paisagem ocupando toda a folha e sem os dados externos a prescrição


Preciso do redimensionamento da receita final ocupando toda a folha A4 com 2 bancos de dados editáveis para os dados dos médicos e para os dados dos princípios ativos e posologia. Do banco de dados digitada as 4 primeiras letras do princípio ativo ele completa o medicamento e a posologia e preenchimento automático do número total de comprimidos.



PROMPT  DE BANCO DE DADOS

# Prompt para Copilot: Sistema de Receitas Médicas com Banco de Dados Local

## Contexto
Você precisa modificar o sistema de receitas médicas HTML/JavaScript existente para incluir funcionalidades de banco de dados local com sincronização em nuvem.

## Requisitos Principais

### 1. Banco de Dados Local
- **Implementar IndexedDB** para armazenamento persistente no navegador
- **Estrutura de dados:**
  - Tabela `medicos`: CRM, nome, especialidade, data_cadastro
  - Tabela `medicamentos`: id, nome, concentracao, posologia, data_atualizacao
  - Tabela `receitas`: id, crm_medico, paciente, medicamentos, data_emissao
  - Tabela `configuracoes`: ultima_sync_medicamentos, ultima_sync_receitas

### 2. Sistema de Sincronização
- **Medicamentos**: Atualização automática 3x por semana (segunda, quarta, sexta)
- **Receitas**: Download automático na primeira execução + upload 3x por semana
- **URLs configuráveis** para GitHub/nuvem
- **Fallback offline** quando não há conexão

### 3. Interface de Gerenciamento
Adicionar nova seção "Gerenciamento de Dados" com botões:
- 🔄 "Sincronizar Medicamentos Agora"
- 📥 "Baixar Dicionário de Receitas"
- 📤 "Fazer Backup dos Dados"
- 🗑️ "Limpar Cache Local"
- ⚙️ "Configurar URLs de Sincronização"
- 📊 "Ver Status da Sincronização"

### 4. Funcionalidades Específicas

#### Inicialização Automática:
```javascript
// Ao carregar a página:
1. Verificar se existe banco local
2. Se não existir, criar estrutura inicial
3. Baixar dicionário de medicamentos e receitas
4. Configurar timers de sincronização automática
```

#### Sistema de Logs:
- Log de todas as receitas emitidas
- Histórico de sincronizações
- Backup automático dos dados locais

#### Configuração de URLs:
```javascript
const CONFIG_URLS = {
    medicamentos: 'https://raw.githubusercontent.com/usuario/repo/main/medicamentos.json',
    receitas: 'https://raw.githubusercontent.com/usuario/repo/main/receitas_template.json',
    backup: 'endpoint-para-backup'
};
```

### 5. Melhorias na Interface

#### Autocomplete Avançado:
- Busca por nome comercial e princípio ativo
- Sugestões baseadas em histórico
- Cache inteligente de buscas frequentes

#### Histórico de Receitas:
- Lista das últimas receitas emitidas
- Possibilidade de reimprimir
- Estatísticas de uso

#### Indicadores Visuais:
- Status de conectividade (🟢 online / 🔴 offline)
- Data da última sincronização
- Contador de receitas no cache local

### 6. Compatibilidade Multiplataforma
- **Funcionamento em qualquer navegador moderno**
- **Não depende de Python ou Node.js**
- **Arquivo HTML único e portátil**
- **Armazenamento 100% local com IndexedDB**

### 7. Estrutura de Arquivos na Nuvem
```
repositorio/
├── medicamentos.json          # Base completa de medicamentos
├── receitas_template.json     # Templates de receitas comuns
├── updates/
│   ├── medicamentos_update.json
│   └── changelog.json
└── backup/
    └── [backups opcionais]
```

### 8. Tratamento de Erros
- **Retry automático** em falhas de rede
- **Modo offline** com dados em cache
- **Validação de integridade** dos dados baixados
- **Notificações amigáveis** ao usuário

## Implementação Técnica Sugerida

### IndexedDB Setup:
```javascript
// Estrutura do banco de dados
const DB_NAME = 'ReceitasMedicasDB';
const DB_VERSION = 1;
const STORES = ['medicos', 'medicamentos', 'receitas', 'configuracoes'];
```

### Sistema de Sincronização:
```javascript
// Verificar e executar sync automático
function setupAutoSync() {
    // Verificar se é hora de sincronizar (seg/qua/sex)
    // Executar download/upload conforme necessário
    // Agendar próxima verificação
}
```

### Melhorias na UX:
- **Progress bars** durante sincronização
- **Toasts/notifications** para feedback
- **Modal de configurações** mais intuitivo
- **Indicadores de status** sempre visíveis

## Resultado Esperado
Um sistema completo que funciona offline, sincroniza automaticamente dados da nuvem, mantém histórico local e pode ser usado em qualquer computador sem instalação de dependências adicionais.

## Instruções Adicionais
- Manter **compatibilidade total** com o código existente
- **Progressivamente aprimorar** sem quebrar funcionalidades atuais
- Implementar **verificações de segurança** nos dados baixados
- Criar **documentação inline** para facilitar manutenção
- Usar **padrões web modernos** mas com boa compatibilidade

---

**Nota**: O sistema deve ser robusto o suficiente para funcionar mesmo em ambientes com conectividade limitada, priorizando sempre a experiência offline com sincronização inteligente em background.
