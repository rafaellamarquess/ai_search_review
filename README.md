# Configuração de Pesquisa no Microsoft Azure

**Este é um trabalho foi desenvolvido para um desafio do BootCamp Decola Tech da DIO.**

Este documento fornece um guia passo a passo para configurar uma pesquisa no Microsoft Azure, explorando insights, ferramentas que podem se beneficiar dessa solução e aprendizados adquiridos durante o processo.

## Índice
1. [Introdução](#introdução)
2. [Requisitos](#requisitos)
3. [Passo a Passo para Configuração](#passo-a-passo-para-configuração)
4. [Ferramentas Beneficiadas](#ferramentas-beneficiadas)
5. [Insights e Aprendizados](#insights-e-aprendizados)
6. [Conclusão](#conclusão)

---

## Introdução
O Microsoft Azure oferece um serviço robusto de pesquisa chamado **Azure Cognitive Search**, que permite criar índices personalizados para facilitar a recuperação de informações de diferentes fontes de dados. Esse serviço é útil para aplicações que precisam de buscas eficientes, como e-commerce, portais de conhecimento e aplicativos corporativos.

## Requisitos
Antes de iniciar a configuração, certifique-se de ter:
- Uma conta no **Microsoft Azure** ([Criar conta gratuita](https://azure.microsoft.com/pt-br/free/))
- Um recurso de **Azure Cognitive Search** provisionado
- Uma fonte de dados compatível (SQL Server, Blob Storage, CosmosDB, etc.)

## Passo a Passo para Configuração

### 1. Criar um Recurso Azure AI Search
1. Acesse o [Azure Portal](https://portal.azure.com/).
2. Crie um recurso **Azure AI Search** com as configurações:
   - Assinatura e grupo de recursos.
   - Nome único e região.
   - Plano **Basic**.
3. Confirme a criação e acesse o recurso.

### 2. Criar um Recurso Azure AI Services
1. Crie um recurso **Azure AI Services** na mesma região do Azure AI Search.
2. Escolha o plano **Standard S0** e confirme a criação.

### 3. Criar uma Conta de Armazenamento
1. Crie um recurso **Storage Account**.
2. Selecione o mesmo grupo de recursos.
3. Escolha **Locally Redundant Storage (LRS)**.
4. Ative o acesso anônimo para blobs.

### 4. Upload de Documentos no Azure Storage
1. No menu esquerdo, vá até **Containers** e crie um container chamado `coffee-reviews` com acesso público.
2. Baixe e extraia os arquivos de [coffee reviews](https://aka.ms/mslearn-coffee-reviews).
3. No container, faça o upload dos arquivos extraídos.

### 5. Indexação de Documentos no Azure AI Search
1. No **Azure AI Search**, vá para **Import data**.
2. Escolha **Azure Blob Storage** e configure:
   - Nome da fonte de dados: `coffee-customer-data`.
   - Dados a extrair: Conteúdo e metadados.
   - Conecte-se ao container `coffee-reviews`.
3. Anexe o serviço Azure AI e crie um conjunto de habilidades `coffee-skillset`.
4. Ative OCR e enriqueça os campos **locations, keyphrases, sentiment, imageTags, imageCaption**.
5. Crie um **knowledge store** chamado `knowledge-store`.
6. Defina o nome do índice como `coffee-index` e marque os campos como filtráveis.
7. Crie um indexador `coffee-indexer`, execute e verifique o status.

![coffee-indexer](https://github.com/user-attachments/assets/2094bdeb-bfff-4471-8156-adba96f37751)


### 6. Fazendo a análise
Pronto, agora é o momento de explorar sua pesquisa. Volte para o o Azure AI Search, selecione sua pesquisa e clique em "Search Explorer"

![search-explorer-button](https://github.com/user-attachments/assets/9a113401-2f05-4102-8a5c-d9afd534e18b)

A título de exemplo foi explorado por região e sentimentos:
#### Buscar todos os documentos:
```json
{
    "search": "*",
    "count": true
}
```
Essa busca retorna todos os documentos no índice de pesquisa.

#### Filtrar por localização (Chicago):
```json
{
 "search": "locations:'Chicago'",
 "count": true
}
```
Retorna os documentos que possuem "Chicago" como localização.
![search-explorer](https://github.com/user-attachments/assets/841cd371-5ba9-4a2a-a7ab-93bbc518333a)


#### Filtrar por sentimento negativo:
```json
{
 "search": "sentiment:'negative'",
 "count": true
}
```
Permite encontrar os documentos com sentimento negativo.
![search-explorer-sentiment](https://github.com/user-attachments/assets/3abe3ae6-0fb4-494f-9454-eb8de8d3aa61)

## Ferramentas Beneficiadas
O **Azure AI Search** pode ser integrado a diversas aplicações, incluindo:
- **Aplicações Web e Mobile**: para fornecer uma busca eficiente.
- **E-commerce**: melhorar a experiência do usuário com pesquisas rápidas.
- **Sistemas de Gestão de Documentos**: facilitar a recuperação de informações.
- **Chatbots e Assistentes Virtuais**: aprimorar respostas baseadas em conteúdo indexado.

## Insights e Aprendizados
Durante o processo de configuração, algumas lições importantes foram aprendidas:
- **Estruturação dos Dados**: A qualidade dos resultados de pesquisa depende de uma boa modelagem do índice.
- **Uso de Inteligência Artificial**: Funcionalidades como reconhecimento de imagem e NLP melhoram a experiência de busca.
- **Automação**: O uso do **Azure CLI** facilita a configuração repetitiva.
- **Monitoramento**: É essencial acompanhar logs e métricas para otimizar o desempenho.

## Conclusão
Configurar uma pesquisa no Azure permite criar soluções poderosas e escaláveis para busca de informações. Com uma configuração bem planejada, é possível melhorar significativamente a experiência dos usuários e a eficiência dos sistemas que dependem de busca de dados.

Para mais detalhes, consulte a [documentação oficial](https://learn.microsoft.com/pt-br/azure/search/) do Azure AI Search.
