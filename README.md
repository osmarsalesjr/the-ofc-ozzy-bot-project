# Ozzy (OFC) — Bot Assistente de RH

Ozzy é um bot assistente virtual de RH da **Osmar Finances Corporation (OFC)**, focado em automatizar demandas repetitivas do setor de **Recursos Humanos e Gestão de Pessoas**.

## Funcionalidades (MVP)
1. **Rota 01 — Adequação de Textos**
	- Ajusta textos para um tom corporativo e conciso.
	- Entrada: texto + contexto/objetivo.
	- Saída: texto revisado.

2. **Rota 02 — Resumo de Reuniões Gravadas**
	- Resume reuniões em vídeo a partir de um link.
	- Entrada: URL do vídeo.
	- Saída: resumo.
	- Observação: links de compartilhamento do OneDrive não são suportados no momento.

3. **Rota 03 — Criar Documentos Timbrados**
	- Gera PDF timbrado OFC (logo + marca d’água) a partir do tipo e texto do documento.
	- Entrada: tipo_documento + texto_documento.
	- Saída: link compartilhável do PDF.

## Arquitetura (alto nível)
- **Typebot**: interface de chat e coleta de inputs
- **Make**: orquestração e integrações (roteamento por `rota_menu_inicial`)
- **Google Gemini**: geração de texto, normalização de URL e resumo multimodal
- **Google Drive**: download/upload e link compartilhável
- **CloudConvert**: HTML → PDF

## Como rodar / testar (guia prático)
### 1) Typebot
1. Importe o fluxo do Typebot (JSON) no Typebot.
2. Verifique variáveis principais:
	- `escolha_menu`, `rota_menu_inicial`, `texto_a_ajustar`, `url_video`, `tipo_documento`, `texto_documento`, `resultado`
3. Confirme que os blocos de Webhook apontam para o endpoint do Make (Webhook Bridge).

### 2) Make
1. Importe o cenário/fluxo no Make.
2. Confirme o módulo Webhook que recebe o payload.
3. Garanta que o roteamento por `rota_menu_inicial` está consistente com o Typebot:
	- `rota_01`, `rota_02`, `rota_03`
4. Valide credenciais e conexões:
	- Google Drive
	- Gemini
	- CloudConvert

### 3) Testes mínimos
- Rota 01: enviar texto agressivo e validar reescrita.
- Rota 02: usar Google Drive com permissão “Qualquer pessoa com o link”.
- Rota 02: usar outra cloud storage link com permissão "Qualquer pessoa com a link" 
- Rota 02: validar retorno de erro para OneDrive.
- Rota 03: gerar PDF e abrir link compartilhável.

## Repositório
https://github.com/osmarsalesjr/the-ofc-ozzy-bot-project.git

## Documentação completa
Veja a página [`Ozzy (OFC) — Documentação Técnica`](DOCS/DOCUMENTAÇÃO_OZZY.pdf) (inclui fluxogramas e detalhes ponta a ponta).