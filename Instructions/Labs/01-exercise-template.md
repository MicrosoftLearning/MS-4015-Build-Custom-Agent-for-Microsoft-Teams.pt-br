---
lab:
  title: Criar um Agente personalizado
---
<!--
Edit the metadata above to manage the list of exercises in the home page of the GitHub site that gets generated.
You can delete the module and edit index.md in the root of the repo to customize the display so that only the exercises are listed
To enable GitHub page publishing, edit the Page settings for the repo and publish from the main branch
-->

# Criar e testar um Agente personalizado

Neste exercício, você criará um recurso OpenAI do Azure que serve como base para criar o agente personalizado.

Este exercício deve levar aproximadamente **30** minutos para ser concluído. <!-- update with estimated duration -->

**Observação:** espera-se que os alunos concluam este laboratório em seus próprios ambientes.

##  Tarefa 1: criar um recurso OpenAI do Azure 

Primeiro, você precisa...

1. Navegue até **https://portal.azure.com** no navegador Edge.
1. Entre no portal do Azure usando a credencial fornecida neste ambiente de laboratório.
2. No canto superior esquerdo da tela, clique em **+ Criar um recurso**.
1. Na caixa de pesquisa, digite **openai do azure** e pressione Enter.
1. Um resultado chamado **OpenAI do Azure** deve aparecer como uma opção. No canto inferior esquerdo desta opção há um botão denominado **Criar**. Pressione> **Criar** > **Azure OpenAI**.
1. Na página **Criar OpenAI do Azure**, defina os seguintes campos: **Observação:** como este laboratório deve ser concluído no próprio ambiente do aluno, os alunos terão que usar seu próprio critério ao selecionar valores para os campos **Assinatura**, **Tipo de preço** e **Grupo de recursos**.
   
   a. **Assinatura** Use seu próprio critério ao preencher este campo.
   
   b. **Grupo de recursos**: Use seu próprio critério ao preencher este campo.
   
   c. **Nome**: Digite qualquer nome que você escolher.
   
   d. **Tipo de preço**: o valor padrão é **Standard S0**, mas use seu próprio critério ao preencher este campo.
   
Selecione **Avançar**.

7. Na próxima página, na guia **Rede**, selecione a opção **Todas as redes, incluindo a Internet, podem acessar este recurso.**
Selecione **Avançar**.
8. Na próxima página na guia **Tags**, deixe os campos Nome e Valor em branco.
Selecione **Avançar**.
9. Na próxima página, na guia **Examinar + enviar**, pressione **Criar**.
10. Você será levado a uma página em que esse recurso OpenAI do Azure recém-criado está sendo criado. Você verá as palavras **Implantação em andamento**. Aguarde alguns segundos para que esse recurso termine de ser implantado. Depois que o recurso for implantado, clique no botão **Ir para o recurso**.
11. **Resultado:** agora você estará na página com o recurso OpenAI do Azure recém-criado. Você pode verificar conferindo o nome do recurso no canto superior esquerdo da página. Esse nome deve corresponder ao nome escolhido para a etapa 5c acima.


## Tarefa 2: Implementar o RAG para o modelo OpenAI do Azure

Agora vamos...

1. Na página do recurso OpenAI do Azure criado recentemente, clique em **Ir para o Azure OpenAI Studio** na faixa de opções na parte superior da página.
2. Na nova página intitulada **Bem-vindo ao serviço OpenAI do Azure**, clique em **Chat** no menu de navegação à esquerda da tela.
3. Na nova página intitulada **Playground do Chat**, em **Configuração**, selecione **+ Criar nova implantação** > **De modelos base**.
4. Na janela pop-up intitulada **Selecione um modelo de conclusão de chat**, role para baixo e selecione a opção **gpt-4o** > **Confirmar**.
5. Na janela **Implantar modelo gtp-4o**, deixe tudo na configuração padrão e selecione **Implantar**.
6. Na página **Playground do Chat**, selecione **Adicionar seus dados** localizado próximo à parte inferior da tela > **+ Adicionar uma fonte de dados**.
7. Na janela **Selecionar ou adicionar fonte de dados**, selecione o menu suspenso para **Selecionar fonte de dados** e selecione **Upload de arquivos (versão prévia)**.
8. Na próxima página de **Fonte de dados**, verifique se a lista suspensa de **Selecionar fonte de dados** está definida como **Carregar arquivos (visualização)**
   
   a. No campo **Assinatura**, verifique se o valor padrão está selecionado.
   
    b. No campo **Selecionar recurso de Armazenamento de Blobs do Azure**, selecione **Criar um novo recurso de Armazenamento de Blobs do Azure** > na nova janela intitulada **Criar uma conta de armazenamento**, na guia **Básico**, verifique se os campos **Assinatura** e **Grupo de recursos** estão definidos com os valores padrão. Escolha o único valor disponível para **Grupo de recursos**. Em **Detalhes da instância**, defina um **nome para a conta de armazenamento**. Deixe o restante dos campos como estão. Selecione **Examinar + criar**. Na guia **Examinar + criar**, selecione o botão **Criar**. O recurso de Armazenamento de Blobs do Azure levará um momento para ser implantado.
   
   c. Navegue de volta para a janela do **Playground do Chat**. Selecione o botão de atualização ao lado do campo **Selecionar recurso de Armazenamento de Blobs do Azure** > selecione o recurso que você criou na etapa b acima. Selecione o botão **Ativar CORS**.
   
9. Para o campo **Selecine o recurso da Pesquisa de IA do Azure**, selecione **Criar um novo recurso da Pesquisa de IA do Azure**.  Verifique se os campos **Assinatura** e **Grupo de recursos** estão definidos com os valores de sua escolha. **Observação:** como este laboratório deve ser concluído no próprio ambiente do aluno, os alunos terão que usar seu próprio critério ao selecionar valores para os campos **Assinatura** e **Grupo de recursos**. Clique no valor suspenso de **Grupo de recursos** para selecionar a opção de sua escolha. Insira um **Nome de serviço**> Garanta que todos os outros campos estejam definidos com os valores padrão > selecione **Examinar + criar** > **Criar**. O recurso da Pesquisa de IA do Azure levará um momento para ser implantado.
10. Navegue de volta para a janela do **Playground do Chat**. Selecione o botão de atualização ao lado do campo **Selecionar recurso de Armazenamento de Blobs do Azure** > selecione o recurso que você criou na etapa 9 acima.
11. Insira um nome para o campo **Insira o nome do índice** > **Avançar**. Copie e cole esse nome em algum lugar acessível, pois você precisará dele nas próximas tarefas.
12. Na seção **Upload de arquivos**, selecione **Procurar um arquivo** > No explorador de arquivos, navegue até **Documentos** > selecione todos os três arquivos: **ContosoAI ChipEnhance Perks Program.docx**, **ContosoAI Insurance Plans.docx** e **Overview of ContosoAI.docx** > **Abrir** > os três arquivos agora estarão na página **Upload de arquivos** da janela > selecione **Upload de arquivos** > **Avançar**.
13. Na seção **Gerenciamento de dados**, deixe tudo com os valores padrão em selecione **Avançar**.
14. Na **Conexão de dados**, selecione **Chave de API** > **Avançar** > **Salvar e fechar**.
15. Na janela do **Playground do Chat**, selecione **Exibir código**, que está na faixa de opções na parte superior esquerda da janela.
16. Na janela **Código de exemplo**, selecione o menu suspenso à direita do primeiro campo e selecione **json** > mude para a guia **Autenticação de chave**:
    
    a. Copie e cole os seguintes valores, pois você precisará deles nas próximas tarefas: **Ponto de extremidade**, **Chave de API** e **Chave de Recurso da Pesquisa do Azure**. Você também pode deixar essa janela aberta para coletar esses valores para as próximas tarefas.

 ## Tarefa 3: Criar e testar o agente personalizado na Ferramenta de Teste e no Teams

Agora vamos...

1. Abra o **Visual Studio Code**.
2. No lado direito da janela do Visual Studio Code, selecione o ícone do **Kit de Ferramentas do Teams** > selecione **Criar um novo app** > no menu suspenso, selecione **Agente de mecanismo personalizado** (observação: dependendo da versão do Kit de Ferramentas do Teams, talvez você precise selecionar **Copilot personalizado**) > **Chatbot de IA básico** > **JavaScript** > **OpenAI do Azure**.
3. Na caixa em branco na parte superior da tela, digite primeiro:

   a. **Chave de API** da tarefa anterior > **Enter**.

   b. **Ponto de extremidade** da tarefa anterior > **Enter**.

   c. Para o **nome da implantação do Open AI do Azure** digite **gpt-4o** > **Enter**.

   d. Em **Escolha a pasta onde a pasta raiz do projeto estará localizada**, selecione **Pasta padrão**.

   e. Em **Insira o nome do aplicativo**, digite qualquer nome > **Enter**> na janela pop-up, selecione **Sim, confio nos autores**.

   f. Na nova janela do VS Code do aplicativo recentemente criado nas etapas a-f acima, navegue até o ícone do **Kit de Ferramentas do Teams** no lado esquerdo da tela.

   g. Na seção **Contas**, clique em **Entrar no Microsoft 365**. Uma nova janela será aberta no navegador. Faça logon usando as credenciais fornecidas.

   .h Navegue de volta para a página do VS Code do seu aplicativo. Agora você deve ver uma marca de seleção verde ao lado das palavras **Upload de aplicativo personalizado ativado** em **Contas.

   i. Na seção **Contas**, clique em **Entrar no Azure**. Clique em **OK** em todas as janelas pop-up. Uma nova janela será aberta no navegador. Faça logon usando as credenciais fornecidas.
   
4. Navegue até **src/prompts/chat/skprompt.txt** na janela VS Code do seu aplicativo. Exclua qualquer texto no arquivo e cole o seguinte: "A seguir está uma conversa com um assistente de IA, que é especialista em responder a perguntas sobre o contexto fornecido. 

As respostas devem ser em um estilo jornalístico curto, com no máximo 80 palavras." 

5. Navegue até o arquivo **config.json** em prompts/chat na janela VS Code do seu aplicativo. Exclua o código atualmente presente nos colchetes e cole o código a seguir entre colchetes.

```json
"data_sources": [ 
    { 
        "type": "azure_search", 
        "parameters": { 
            "endpoint": "AZURE-AI-SEARCH-ENDPOINT", 
            "index_name": "YOUR-INDEX_NAME",
            "in_scope": false,
            "authentication": { 
                "type": "api_key", 
                "key": "AZURE-AI-SEARCH-KEY" 
            } 
        } 
    } 
]
```

6. No código acima, substitua o seguinte pelos valores que você salvou da tarefa anterior (observação: os valores devem estar entre aspas):

   a. **AZURE-AI-SEARCH-ENDPOINT** é o **ponto de extremidade** da tarefa anterior.

   b. **index_name** é o **Nome do índice**do índice da etapa 11 da Tarefa 2 na tarefa anterior.

   c. **key** é a **chave de recurso da Pesquisa do Azure** da tarefa anterior.

7. Vá para o **arquivo src/app/app.js** e adicione a seguinte variável dentro de  **OpenAIModel** logo após a linha azureEndpoint: config.azureOpenAIEndpoint, : 

    a. azureApiVersion: '2024-02-15-preview',
   
8. **Arquivo** > **Salvar tudo**
    
9. Pressione **Ctrl+Shift+d** no teclado e aparecerá um menu suspenso no canto superior esquerdo com um botão de reprodução verde e a palavra Depurar > Selecione o menu suspenso> selecione **Depurar na ferramenta de teste** > pressione **F5**.
10. O agente de mecanismo personalizado é executado na ferramenta de depuração que você escolheu, que é aberta no navegador. Você pode fazer ao bot qualquer pergunta relacionada aos dados RAG carregados na etapa 12 da Tarefa 2.
11. Navegue de volta para a janela do VS Code do seu aplicativo. Selecione o menu suspenso do botão **Depurar** e selecione **Depurar no Teams (Edge)**. Em seguida, pressione **F5** ou o botão verde de reprodução.
13. Uma nova janela será aberta no navegador Edge. Será solicitado que você entre. Use as informações de login fornecidas para entrar. Depois de conseguir entrar, feche a janela.
14. Repita a etapa 11 novamente. Deve haver uma janela com o título do seu aplicativo recém-criado. Selecione **Adicionar** > **Abrir**.
15. Parabéns! Agora você pode fazer qualquer pergunta ao agente contendo os arquivos de dados RAG. 
