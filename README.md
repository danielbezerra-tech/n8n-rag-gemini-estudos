\# Sistema de RAG (Retrieval-Augmented Generation) com n8n e Google Gemini



Este é um projeto prático desenvolvido para estudar a construção de fluxos de \*\*RAG\*\* utilizando o \*\*n8n\*\* e modelos de linguagem da \*\*Google (Gemini)\*\*.



&#x20;O fluxo combina ingestão de documentos brutos e uma interface de chat capaz de recuperar contexto relevante para responder às perguntas do usuário.



\---



\## 🛠️ Tecnologias Utilizadas



\* \*\*\[n8n](https://n8n.io/):\*\* Orquestrador do fluxo de automação e integração de IA.

\* \*\*Google Gemini Chat Model:\*\* Modelo de linguagem (LLM) responsável por gerar as respostas finais.

\* \*\*Google Gemini Embeddings:\*\* Modelo para vetorização dos textos e das perguntas.

\* \*\*Simple Vector Store:\*\* Banco de dados vetorial em memória para armazenamento temporário e busca por similaridade.



\---



\## 🧠 Arquitetura do Fluxo



O projeto está dividido em duas partes principais dentro do mesmo workflow:



1\. \*\*Pipeline de Ingestão (Indexação):\*\*

&#x20;  \* Pega o texto bruto inserido manualmente no nó `Edit Fields`.

&#x20;  \* Fatora e vetoriza o conteúdo usando o `Embeddings Google Gemini`.

&#x20;  \* Armazena os vetores no `Simple Vector Store`.



2\. \*\*Pipeline de Consulta (Chat RAG):\*\*

&#x20;  \* Recebe a mensagem do usuário via nó de Chat.

&#x20;  \* Converte a pergunta em vetor e busca os 4 trechos mais relevantes no `Simple Vector Store`.

&#x20;  \* Envia os trechos recuperados + a pergunta do usuário para o `Basic LLM Chain` com o `Google Gemini`.



\---



\## 🚀 Como Importar e Executar no Seu n8n



\### Pré-requisitos

\* n8n rodando localmente (via Docker ou Node/npx).

\* Uma chave de API da Google Gemini (Google AI Studio).



\### Passo a passo

1\. Faça o download do arquivo `workflows/fluxo\_rag\_gemini.json` deste repositório.

2\. Abra o painel do seu \*\*n8n\*\*.

3\. No canto superior direito da tela de edições, clique no menu de três pontos (`...`) e selecione \*\*Import from File\*\*.

4\. Escolha o arquivo `.json` baixado.

5\. Em \*\*Credentials\*\*, adicione a sua chave de API do Google Gemini nos nós correspondentes.

6\. Clique em \*\*Execute workflow\*\* no fluxo superior para indexar o texto e, em seguida, abra a janela de Chat no fluxo inferior para testar as perguntas!



\---



> 📌 \*\*Nota de estudo:\*\* Este fluxo utiliza o \*Simple Vector Store\*, que guarda os dados na memória RAM temporária. Ao reiniciar a instância do n8n, os vetores precisam ser reindexados.

