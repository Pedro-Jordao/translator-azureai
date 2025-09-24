# Tradutor de Artigos Técnicos com Azure AI

📘 **Projeto de Desafio - Bootcamp DIO**  
⚠️ O seguinte README refere-se a um projeto para a obtenção de nota ou aprovação em um Bootcamp da DIO e está de acordo com a respectiva "Descrição do Desafio" que possuir.

## 📝 Descrição do Projeto

Este projeto implementa um fluxo inteligente de tradução e enriquecimento de textos ou documentos técnicos (ex.: artigos, especificações e trechos de estudo) para o português do Brasil, utilizando serviços do Azure AI. O sistema realiza detecção automática de idioma e tradução.

Gera arquivos traduzidos em diretório de saída e registra resultados para acompanhamento e validação.

## 🎯 Objetivos do Projeto

Ao concluir este desafio, você será capaz de:

• ✅ Configurar e consumir os serviços Azure AI Translator e Azure OpenAI
• ✅ Detectar automaticamente o idioma de entrada antes de traduzir
• ✅ Traduzir texto livre e documentos `.docx`, preservando estrutura básica
• ✅ Aplicar refinamento semântico opcional via modelo Azure OpenAI
• ✅ Planejar extensões futuras (glossário técnico, múltiplos formatos, batch)

## 🗂️ Sumário

- [Arquitetura Conceitual](#-arquitetura-conceitual)
- [Tecnologias e Serviços](#-tecnologias-e-serviços)
- [Pré-requisitos](#-pré-requisitos)
- [Configuração dos Serviços Azure](#-configuração-dos-serviços-azure)
- [Variáveis de Ambiente](#-variáveis-de-ambiente)
- [Como Usar](#-como-usar)
- [Estrutura de Pastas](#-estrutura-de-pastas)
- [Exemplos de Execução](#-exemplos-de-execução)
- [Boas Práticas Aplicadas](#-boas-práticas-aplicadas)
- [Contribuição](#-contribuição)
- [Licença](#-licença)
- [Autor](#-autor)

## 🏗️ Arquitetura Conceitual

1. Entrada: texto bruto ou documento `.docx` (exemplos em `sample/`).
2. Detecção de idioma (Azure Translator Detect).
3. Tradução principal (Azure Translator Translate).
4. Pós-processamento opcional: prompt controlado no Azure OpenAI para ajustes.
5. Exportação de documento traduzido (`sample/result/`).
6. Registro de execução em `Result/Result.md` + evidências em `img/`.

```
[Input .docx / Texto] --> [Detecção Idioma] --> [Tradução Base] --> (OpenAI Refinamento?) --> [Geração Saída] --> [Registro]
```

## ⚙️ Tecnologias e Serviços

| Camada             | Serviço / Ferramenta              | Função                                  |
| ------------------ | --------------------------------- | --------------------------------------- |
| Tradução           | Azure AI Translator               | Detecção e tradução de idioma           |
| Enriquecimento     | Azure OpenAI (`gpt-4o-mini`)      | Refinamento opcional de estilo/contexto |
| Processamento DOCX | Python + `python-docx` (sugerido) | Leitura e escrita estruturada           |
| Registro           | Markdown simples                  | Histórico e evidências                  |

## ✅ Pré-requisitos

- Conta Azure ativa
- Grupo de Recursos criado
- Serviços provisionados: Translator + Azure OpenAI (deployment do modelo)
- Python 3.10+ (se optar por script local)

## 🛠️ Configuração dos Serviços Azure

1. Criar recurso Translator (anotar Endpoint + Key + Region).
2. Criar Azure OpenAI / usar Azure AI Foundry, implantar `gpt-4o-mini`.
3. Gerar chave e endpoint do deployment.
4. Definir variáveis de ambiente (abaixo).
5. Testar no Playground (ver imagens em `img/`).

## 🔑 Variáveis de Ambiente

Defina (Windows CMD):

```
set AZURE_TRANSLATOR_ENDPOINT=https://<seu-endpoint-translator>.cognitiveservices.azure.com/
set AZURE_TRANSLATOR_KEY=<sua-key-translator>
set AZURE_TRANSLATOR_REGION=<regiao-ex: brazilsouth>

set AZURE_OPENAI_ENDPOINT=https://<seu-endpoint-openai>.openai.azure.com/
set AZURE_OPENAI_KEY=<sua-key-openai>
set AZURE_OPENAI_DEPLOYMENT=gpt-4o-mini
```

## ▶️ Como Usar

Fluxo sugerido (exemplo de script Python futuro):

1. Colocar arquivo `.docx` em `sample/`.
2. Executar script: detecta idioma → traduz → gera novo DOCX em `sample/result/`.
3. (Opcional) Ativar flag `--refinar` para pós-processamento com OpenAI.
4. Checar `Result/Result.md` para metadados (tempo, tokens, etc.).

## 💻 Exemplo de Pseudocódigo (Tradução)

```python
# Pseudocódigo simplificado
text = extrair_texto_docx("sample/CrazyTrain-Lyrics.docx")
lang = detectar_idioma(text)
traducao = traduzir(text, target="pt-br")
refinado = refinar_com_openai(traducao) if usar_refino else traducao
salvar_docx(refinado, "sample/result/CrazyTrain-Lyrics_pt-br.docx")
registrar_execucao(lang, len(text), "Result/Result.md")
```

## 📂 Estrutura de Pastas

```
img/                 # Evidências de configuração e testes
sample/              # Arquivos de entrada
sample/result/       # Arquivos traduzidos gerados
aResult/             # Relatórios / logs gerais
README.md            # Documentação principal
```

## 🧪 Exemplos (Imagens)

Ver capturas em `img/` demonstrando:

- Configuração dos serviços
- Testes no Playground
- Tradução de texto e documento

## ♻️ Boas Práticas Aplicadas

- Organização clara de entradas e saídas
- Documentação padronizada reutilizável para Bootcamps
- Planejamento explícito de extensões
- Separação conceitual entre tradução base e enriquecimento semântico

## 🤝 Contribuição

1. Faça um fork
2. Crie uma branch: `feat/minha-feature`
3. Commit: `git commit -m "feat: descrição"`
4. Push: `git push origin feat/minha-feature`
5. Abra um Pull Request

## 🧾 Notas Finais

Este README é um modelo padrão reutilizável para projetos desenvolvidos em bootcamps da [Digital Innovation One](https://www.dio.me/en).
Adapto conforme o desafio proposto, mantendo a estrutura clara e objetiva.

## 📄 Licença

Distribuído sob a Licença MIT. Consulte o arquivo LICENSE (ou texto abaixo) para mais informações.

```
MIT License

Copyright (c) 2025 Pedro Jordão

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## ✍️ Autor

Pedro Jordão
[LinkedIn Pedro Jordão] ([https://www.dio.me/en](https://www.linkedin.com/in/pedro-p-27219226b/)

---

