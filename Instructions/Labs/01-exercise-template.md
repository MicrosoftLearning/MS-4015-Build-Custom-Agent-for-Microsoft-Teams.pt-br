
laboratório: 'Criar um agente de mecanismo personalizado com o SDK de Agentes do Microsoft 365'
---
<!--
Edit the metadata above to manage the list of exercises in the home page of the GitHub site that gets generated.
You can delete the module and edit index.md in the root of the repo to customize the display so that only the exercises are listed
To enable GitHub page publishing, edit the Page settings for the repo and publish from the main branch
-->

# Criar e testar um Agente personalizado

Neste exercício, você criará um recurso OpenAI do Azure que serve como base para criar o agente personalizado.

Este exercício deve levar aproximadamente**60** minutos para ser concluído. <!-- update with estimated duration -->

**Observação:** os alunos podem concluir este laboratório com estas opções
1) Um ambiente de laboratório fornecido para os alunos.
2) Espera-se que os alunos concluam este laboratório em seus próprios ambientes para todos os outros ALHs.

##  Tarefa 1: criar um recurso OpenAI do Azure 

Primeiro, você precisa...

1. Navegue até**https://portal.azure.com** no navegador Edge.
1. Faça logon no Portal do Azure.
2. No canto superior esquerdo da tela, clique em **+ Criar um recurso**.
1. Na caixa de pesquisa, digite**openai do azure** e pressione Enter.
1. Um resultado chamado**OpenAI do Azure** deve aparecer como uma opção. No canto inferior esquerdo desta opção há um botão denominado**Criar**. Pressione>**Criar** >**Azure OpenAI**.
1. Na página**Criar OpenAI do Azure**, defina os seguintes campos:

**Observação:** os alunos usando o próprio ambiente deles terão que usar seu próprio critério ao selecionar valores para os campos**Assinatura**,**Tipo de preço** e**Grupo de recursos**. Para alunos que estiverem usando o ambiente de laboratório, selecione os valores padrão para os campos nas etapas a-d abaixo.
   
   a. **Assinatura** Use seu próprio critério ao preencher este campo.
   
   b. **Grupo de recursos**: Use seu próprio critério ao preencher este campo.
   
   c. **Nome**: Digite qualquer nome que você escolher.
   
   d. **Tipo de preço**: o valor padrão é**Standard S0**, mas use seu próprio critério ao preencher este campo.
   
Selecione**Avançar**.

7. Na próxima página, na guia**Rede**, selecione a opção**Todas as redes, incluindo a Internet, podem acessar este recurso.**
Selecione**Avançar**.
8. Na próxima página na guia**Tags**, deixe os campos Nome e Valor em branco.
Selecione**Avançar**.
9. Na próxima página, na guia**Examinar + enviar**, pressione**Criar**.
10. Você será levado a uma página em que esse recurso OpenAI do Azure recém-criado está sendo criado. Você verá as palavras**Implantação em andamento**. Aguarde alguns segundos para que esse recurso termine de ser implantado. Depois que o recurso for implantado, clique no botão**Ir para o recurso**.
11. **Resultado:** agora você estará na página com o recurso OpenAI do Azure recém-criado. Você pode verificar conferindo o nome do recurso no canto superior esquerdo da página. Esse nome deve corresponder ao nome escolhido para a etapa 5c acima.


## Tarefa 2: Implementar o RAG para o modelo OpenAI do Azure

Nesta tarefa, você aprenderá a implementar o RAG usando uma fonte de dados para seu próprio ambiente de teste.

1. Na página do recurso OpenAI do Azure criado recentemente, clique em**Ir para o Portal da Fábrica de IA do Azure** na faixa de opções na parte superior da página.
2. No lado esquerdo, em**Playgrounds**, selecione**Chat**. Agora, na página**Playground de chat**, na seção chamada**Configuração**, selecione **+ Criar nova implantação**.
3. Na janela pop-up intitulada**Selecionar um modelo de conclusão de chat**, role para baixo e selecione a opção**gpt-4** >**Confirmar**.
4. Na janela**Implantar modelo gpt-4**, mantenha todas as configurações padrão e selecione**Implantar**.
5. Na página**Playground do Chat**, selecione**Adicionar seus dados** localizado próximo à parte inferior da tela >**+ Adicionar uma fonte de dados**.
6. Na janela**Selecionar ou adicionar fonte de dados**, selecione o menu suspenso para**Selecionar fonte de dados** e selecione**Upload de arquivos (versão prévia)**.
7. Na próxima página de**Fonte de dados**, verifique se a lista suspensa de**Selecionar fonte de dados** está definida como**Carregar arquivos (visualização)**

**Observações:** no caso de alunos usando o próprio ambiente, os usuários talvez tenham que usar seu próprio critério ao preencher os campos das etapas a-c abaixo. No caso de alunos que usarem o ambiente de laboratório fornecido, siga os valores padrão conforme instruído nas etapas a-b abaixo. 
  
   a. No campo**Assinatura**, verifique se o valor padrão está selecionado.
   
   b. No campo**Selecionar recurso de Armazenamento de Blobs do Azure**, selecione**Criar um novo recurso de Armazenamento de Blobs do Azure** > na nova janela intitulada**Criar uma conta de armazenamento**. Na guia**Básico**, verifique se os campos**Assinatura** e**Grupo de recursos** estão definidos com os valores padrão. Escolha o único valor disponível para**Grupo de recursos**. Em**Detalhes da instância**, defina um**nome para a conta de armazenamento**. Deixe o restante dos campos como estão. Selecione**Examinar + criar**. Na guia**Examinar + criar**, selecione o botão**Criar**. O recurso de Armazenamento de Blobs do Azure levará um momento para ser implantado.
   
   c. Navegue de volta para a janela do**Playground do Chat**. Selecione o botão de atualização ao lado do campo**Selecionar recurso de Armazenamento de Blobs do Azure** > selecione o recurso que você criou na etapa b acima. Selecione o botão**Ativar CORS**.
   
8. Para o campo**Selecine o recurso da Pesquisa de IA do Azure**, selecione**Criar um novo recurso da Pesquisa de IA do Azure**.  Verifique se os campos**Assinatura** e**Grupo de recursos** estão definidos com os valores de sua escolha.

   **Observação:** no caso de alunos usando o próprio ambiente deles, use seu próprio critério ao selecionar valores para os campos**Assinatura** e**Grupo de recursos**.

9. Clique no valor suspenso de**Grupo de recursos** para selecionar a opção de sua escolha. Insira um**Nome de serviço**> Garanta que todos os outros campos estejam definidos com os valores padrão > selecione**Examinar + criar** >**Criar**. O recurso da Pesquisa de IA do Azure levará um momento para ser implantado.
10. Navegue de volta para a janela do**Playground do Chat**. Selecione o botão de atualização ao lado do campo**Selecionar recurso de Armazenamento de Blobs do Azure** > selecione o recurso que você criou na etapa 9 acima.
11. Insira um nome para o campo**Insira o nome do índice** >**Avançar**. Copie e cole esse nome em algum lugar acessível, pois você precisará dele nas próximas tarefas.
12. Na seção**Upload de arquivos**, selecione**Procurar um arquivo** > No explorador de arquivos, navegue até**Documentos** > selecione todos os três arquivos:**ContosoAI ChipEnhance Perks Program.docx**,**ContosoAI Insurance Plans.docx** e**Overview of ContosoAI.docx** >**Abrir** > os três arquivos agora estarão na página**Upload de arquivos** da janela > selecione**Upload de arquivos** >**Avançar**.
13. Na seção**Gerenciamento de dados**, deixe tudo com os valores padrão em selecione**Avançar**.
14. Na**Conexão de dados**, selecione**Chave de API** >**Avançar** >**Salvar e fechar**.
15. Na janela do**Playground do Chat**, selecione**Exibir código**, que está na faixa de opções na parte superior esquerda da janela.
16. Na janela**Código de exemplo**, selecione o menu suspenso à direita do primeiro campo e selecione**json** > mude para a guia**Autenticação de chave**:
    
    a. Copie e cole os seguintes valores, pois você precisará deles nas próximas tarefas:**Ponto de extremidade**,**Chave de API** e**Chave de Recurso da Pesquisa do Azure**. Você também pode deixar essa janela aberta para coletar esses valores para as próximas tarefas.

 ## Tarefa 3: Criar e testar o agente personalizado na Ferramenta de Teste e no Teams

Nesta tarefa, você criará o agente personalizado e testará o agente.

1. Abra o**Visual Studio Code**.
2. No lado direito da janela do Visual Studio Code, selecione**Exibir** na faixa superior >**Extensões** > pesquise por**Toolkit do Agentes do Microsoft 365** > selecione**Atualizar** >** Reiniciar Extensões** > selecione**Criar um novo agente/aplicativo** > no menu suspenso, selecione**Agente de mecanismo personalizado**  >**Agente de mecanismo personalizado básico** >**JavaScript** >**OpenAI do Azure**. **Observação** talvez seja necessário fechar e reabrir o VS Code após atualizar o toolkit.
3. Na caixa em branco na parte superior da tela, digite primeiro:

   a. **Chave de API** da tarefa anterior >**Enter**.

   b. **Ponto de extremidade** da tarefa anterior >**Enter**.

   c. Para**Nome da implantação do OpenAI do Azure**, digite**gpt-4** >**Enter** >**JavaScript**. 

   d. Em**Escolha a pasta onde a pasta raiz do projeto estará localizada**, selecione**Pasta padrão**.

   e. Em**Inserir nome do aplicativo**, digite qualquer nome >**Enter**> na janela pop-up, selecione**Sim, confio nos autores**.

   f. Na nova janela do VS Code do aplicativo recém-criado nas etapas de “a” a “f” acima, navegue até o ícone**Toolkit do M365** no lado esquerdo da tela.

   **Observação:** as etapas g-i devem ser concluídas para o ambiente de um usuário que não tem acesso de administrador ao Centro de Administração do Microsoft Teams e/ou para alunos que usarem o ambiente de laboratório fornecido.
  Para alunos com seus próprios ambientes, execute as etapas j-m.

   g. Na seção**Contas**, clique em**Entrar no Microsoft 365**. Uma nova janela será aberta no navegador. Faça logon usando as credenciais fornecidas.

   .h Navegue de volta para a página VS Code do seu agente. Agora você deve ver uma marca de seleção verde ao lado das palavras**Upload de aplicativo personalizado ativado** em **Contas.

   i. Na seção**Contas**, clique em**Entrar no Azure**. Clique em**OK** em todas as janelas pop-up. Uma nova janela será aberta no navegador. Faça logon usando as credenciais fornecidas.

   Para usuários que têm uma licença de locatário do M365 com acesso de administrador ao Centro de Administração do Microsoft Teams, execute as seguintes etapas em vez das etapas g-i acima:

   j. Entre nohttps://admin.teams.microsoft.com com suas credenciais de administrador.

   k. Acesse **aplicativos do Teams**  na barra lateral e selecione **Configurar políticas**.

   l. Selecione a política **Global (padrão em toda a organização)**  e, em seguida, ative a opção **Upload de aplicativos personalizados** .

   m. Role para baixo e clique no botão **Salvar** para salvar as alterações. Seu locatário agora permitiá o sideload de aplicativos personalizados. 

4. No VS Code, na janela do seu aplicativo, navegue até o arquivo**src/config.js** em prompts/chat. Exclua todo o texto que segue**azureOpenAIKey:**,**azureOpenAIEndpoint:** e**azureOpenAIDeploymentName:**.

5. Após concluir o passo anterior, substitua o texto que você excluiu após **:** pelos valores que você salvou na tarefa anterior (observação: os valores devem estar entre aspas):

   a. **azureOpenAIKey** é a**chave de API** da tarefa anterior.

   b. **azureOpenAIEndpoint** é o**Ponto de extremidade** da tarefa anterior.
   
   c. **azureOpenAIDeploymentName** digite **"gpt-4"**
   
**Observe** que todo o texto está entre aspas.
   
6. **Arquivo** >**Salvar tudo**
    
7. Pressione**Ctrl+Shift+D** no teclado e um menu suspenso aparecerá no canto superior esquerdo com um botão verde de reprodução e a palavra Depurar > selecione o menu suspenso > selecione**Depurar no Playground de Agentes do Microsoft 365**  > pressione**F5**.
8.O agente de mecanismo personalizado é executado na ferramenta de depuração que você selecionou, a qual é aberta no navegador. 
9. Navegue de volta para a janela do VS Code do seu aplicativo. Selecione o menu suspenso do botão**Depurar** e selecione**Depurar no Teams (Edge)**. Em seguida, pressione**F5** ou o botão verde de reprodução.
10. Uma nova janela será aberta no navegador Edge. Talvez você seja solicitado a fazer logon, ou não. Use as informações de login fornecidas para entrar. Depois de conseguir entrar, feche a janela.
11. Deve haver uma janela com o título do seu aplicativo recém-criado. Selecione**Adicionar** >**Abrir**.
12. Parabéns! Agora você pode fazer qualquer pergunta ao agente contendo os arquivos de dados RAG.
13. **Observação:** para os alunos fazendo este laboratório em seu próprio ambiente, esse agente foi criado para fins educacionais usando a sua própria assinatura; os usuários devem prosseguir com a exclusão do agente após a conclusão deste laboratório. Para excluir um agente personalizado no Microsoft Teams:
- Selecione o agente que você quer excluir, clique no**ícone Mais opções (...)** e escolha**Excluir**.
- Remova o agente de um chat selecionando as reticências no thread e escolhendo**Gerenciar aplicativos**.
- Na experiência de criação de um agente, selecione as**reticências (...)** e escolha**Excluir**.- Na experiência de criação de um agente, selecione as**reticências (...)** e escolha**Excluir**.

**FIM DO LABORATÓRIO**

