Arquitetura do Fluxo e Nós Utilizados
O arquivo Relatórios.json estrutura a esteira de dados em 4 etapas principais:

1. Gatilhamento e Coleta de Dados:
   - Schedule Trigger: Configurado para rodar de forma agendada a cada mês.
   - Obter Data Filtragem (Set): Define a janela temporal de análise estática (inicialmente configurada para 2025-08-01).
   - Obter dados (Google Sheets): Puxa a listagem bruta da planilha atividades_empresa.
   
2. Tratamento e Filtragem:
   - Filter: Filtra as linhas da planilha, mantendo apenas os registros com datas posteriores ao período definido.
   - Aggregate: Agrupa todos os itens filtrados em um único payload JSON estruturado para consumo da inteligência artificial.
   
3. Camada de Inteligência Artificial (LangChain):
   - Análise (Chain LLM): Atua como analista estratégico para a diretoria, processando os dados brutos, avaliando riscos de tarefas atrasadas e gerando recomendações sem formatação complexa (asteriscos).
   - Resumo (Chain LLM): Consome a saída da análise anterior para criar um resumo condensado em tópicos e Markdown, ideal para o corpo de e-mails executivos.
   - Google Gemini Chat Model: O motor de IA (lmChatGoogleGemini) que abastece ambos os prompts anteriores.

4. Formatação e Publicação:
   - Conversão em HTML: Transforma o Markdown estruturado do nó Resumo em tags HTML limpas.
   - Criar e Adicionar ao Documento (Google Docs): Cria um arquivo dinâmico nomeado com data/hora na pasta do Drive e insere o texto completo da Análise Executiva.
   - Send a message (Gmail): Dispara o e-mail para o destinatário final contendo o resumo já convertido em HTML corporativo.
 
