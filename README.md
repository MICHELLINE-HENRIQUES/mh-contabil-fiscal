# MH Consultoria — Painel de Ferramentas Fiscais

## Estrutura de pastas

```
painel-mh/
├── index.html              ← Painel central (login + abas por setor)
├── fiscal/
│   └── icms.html           ← Cruzamento ICMS (cole seu HTML aqui)
├── contabil/
│   └── razao.html          ← Conciliação de Razão (em desenvolvimento)
└── rh/
    └── (futuras ferramentas)
```

## Como publicar no GitHub Pages

1. Acesse https://github.com e crie uma conta (gratuita)
2. Clique em "New repository" → nome: `painel-fiscal`
3. Marque "Public" → clique em "Create repository"
4. Faça upload de todos os arquivos desta pasta
5. Vá em Settings → Pages → Source: "main" → pasta "/ (root)"
6. Aguarde ~1 minuto → URL pronta: `https://seuusuario.github.io/painel-fiscal`

## Como adicionar uma nova ferramenta

1. Crie o arquivo HTML na pasta do setor correto (ex: `fiscal/nova.html`)
2. Adicione o cabeçalho padrão com botão "← Painel" (veja modelo nos arquivos existentes)
3. No `index.html`, duplique um `<a class="tool-card">` e ajuste o href, título e descrição
4. Suba os dois arquivos no GitHub → pronto!

## Como configurar o login Google de verdade

1. Acesse https://console.cloud.google.com
2. Crie um projeto → "APIs & Serviços" → "Credenciais"
3. "Criar credenciais" → "ID do cliente OAuth 2.0" → tipo: "Aplicativo da Web"
4. Em "Origens JS autorizadas", adicione sua URL do GitHub Pages
5. Copie o "Client ID" e substitua no index.html onde indicado
6. Configure para aceitar apenas @henriquesconsultoria.com.br

## Contato técnico
Desenvolvido com Claude (Anthropic) — Para novas ferramentas, inicie nova conversa com o Claude e anexe este README.
