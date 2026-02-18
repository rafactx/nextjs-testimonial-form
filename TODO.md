# Portfolio Enhancement Backlog

Este documento lista melhorias futuras que elevariam o projeto para um nível ainda mais sênior e production-ready. Cada item está organizado por prioridade e esforço estimado.

---

## 🧪 Testing Infrastructure (High Priority)

**Por que é importante**: Aumenta confiabilidade, facilita refactoring, e demonstra maturidade técnica para recrutadores.

### Tasks
- [ ] Setup Vitest com React Testing Library
  - Configurar `vitest.config.ts`
  - Adicionar helpers (`@testing-library/react`, `@testing-library/user-event`)
  - Criar setup file com mocks básicos
  
- [ ] Testes unitários do formulário
  - Testar cada step do fluxo conversacional
  - Validação de inputs (caracteres, campos obrigatórios)
  - Estados de loading e erro
  - Coverage mínimo: 80%

- [ ] Testes de integração da API
  - Mock do Google Sheets API
  - Validação de request/response
  - Error handling scenarios

- [ ] E2E com Playwright
  - Fluxo completo: preenchimento → review → submissão → sucesso
  - Testes de acessibilidade com `@axe-core/playwright`
  - Screenshots em diferentes viewports

- [ ] CI integration
  - Adicionar job de testes no workflow
  - Coverage report (Codecov ou Coveralls)
  - Fail build se coverage < 80%

**Esforço**: 6-8 horas  
**Valor**: ⭐⭐⭐⭐⭐  
**Dependências**: Nenhuma

---

## 🔒 Security & Rate Limiting (High Priority)

**Por que é importante**: Protege contra abuso, spam, e ataques DDoS. Essencial para produção real.

### Tasks
- [ ] Implementar rate limiting com Upstash Redis
  - Setup Upstash account
  - Instalar `@upstash/redis` e `@upstash/ratelimit`
  - Criar middleware com sliding window (5 req/min por IP)
  - Retornar `429 Too Many Requests` com Retry-After header

- [ ] CSRF protection
  - Implementar tokens CSRF para POST requests
  - Validar origin/referer headers
  - Double submit cookie pattern

- [ ] Input validation com Zod
  - Criar schemas para testimonial API (`z.object({...})`)
  - Validar no server-side antes do Sheets API
  - Type-safe error messages

- [ ] Content Security Policy avançado
  - Refinar CSP headers no `next.config.mjs`
  - Adicionar nonce para inline scripts
  - Report-uri para violações

- [ ] Honeypot field
  - Campo oculto no formulário (CSS: `display: none`)
  - Rejeitar submissões se preenchido (bots)

**Esforço**: 4-6 horas  
**Valor**: ⭐⭐⭐⭐⭐  
**Dependências**: Nenhuma

---

## 📊 Observability (Medium Priority)

**Por que é importante**: Visibilidade de erros e performance em produção. Demonstra pensamento operacional.

### Tasks
- [ ] Integrar Sentry para error tracking
  - Setup projeto no Sentry.io
  - Instalar `@sentry/nextjs`
  - Configurar `sentry.client.config.ts` e `sentry.server.config.ts`
  - Adicionar error boundaries customizados
  - Source maps upload no CI

- [ ] Lighthouse CI com badges
  - Criar workflow `.github/workflows/lighthouse.yml`
  - Rodar Lighthouse em cada PR
  - Gerar badge com scores (Performance, A11y, Best Practices, SEO)
  - Fail se Performance < 90

- [ ] Bundle size monitoring
  - Instalar `@next/bundle-analyzer`
  - Criar comando `bun analyze`
  - GitHub Action para comentar size diff em PRs
  - Alertar se bundle crescer > 10%

- [ ] Custom analytics events
  - Track eventos: `testimonial_started`, `testimonial_completed`, `testimonial_abandoned`
  - Enviar para Vercel Analytics ou Google Analytics
  - Dashboard com métricas (conversion rate, drop-off points)

**Esforço**: 3-4 horas  
**Valor**: ⭐⭐⭐⭐  
**Dependências**: Nenhuma

---

## 🌍 Internationalization (Low Priority)

**Por que é importante**: Expande alcance do projeto. Mostra capacidade de arquitetura escalável.

### Tasks
- [ ] Setup next-intl
  - Instalar `next-intl`
  - Criar estrutura `messages/` com `pt-BR.json` e `en-US.json`
  - Configurar middleware para locale detection
  - Wrapper de provider no `layout.tsx`

- [ ] Traduzir conteúdo
  - Mensagens do bot (chat flow)
  - Labels e placeholders
  - Mensagens de erro
  - README (criar `README.en.md`)

- [ ] Locale switcher
  - Componente no header para trocar idioma
  - Persistir preferência em cookie
  - Atualizar URL com locale (`/pt-BR/`, `/en-US/`)

- [ ] Formatação local-aware
  - Datas (Intl.DateTimeFormat)
  - Números (Intl.NumberFormat)

**Esforço**: 4-5 horas  
**Valor**: ⭐⭐⭐  
**Dependências**: Nenhuma

---

## ⚡ Performance Enhancements (Medium Priority)

**Por que é importante**: Otimizações adicionais para edge cases e escala.

### Tasks
- [ ] React Error Boundary
  - Criar `components/error-boundary.tsx`
  - Fallback UI amigável
  - Log erros para Sentry
  - Recovery actions (reload, go back)

- [ ] Suspense boundaries estratégicos
  - Lazy load form steps (code splitting)
  - Skeleton loaders para cada step
  - Reduzir initial bundle size

- [ ] Service Worker para offline
  - PWA setup com `next-pwa`
  - Cache de assets estáticos
  - Offline fallback page
  - Manifest.json com ícones

- [ ] Prefetch otimizado
  - Prefetch próximo step do form
  - Preconnect para Google Sheets API
  - Resource hints (`<link rel="preconnect">`)

**Esforço**: 2-3 horas  
**Valor**: ⭐⭐⭐  
**Dependências**: Nenhuma

---

## 🛠️ DevEx Improvements (Low Priority)

**Por que é importante**: Facilita onboarding de contribuidores. Mostra preocupação com DX.

### Tasks
- [ ] Storybook para componentes
  - Setup `@storybook/nextjs`
  - Stories para `<TestimonialForm />` e componentes UI
  - Controles interativos (Knobs)
  - Acessibility addon
  - Deploy Storybook no Chromatic

- [ ] Dockerfile para self-hosting
  - Multi-stage build otimizado
  - Alpine base image (menor footprint)
  - Health check endpoint (`/api/health`)
  - Docker Compose com variáveis

- [ ] GitHub Templates
  - `.github/ISSUE_TEMPLATE/bug_report.md`
  - `.github/ISSUE_TEMPLATE/feature_request.md`
  - `.github/PULL_REQUEST_TEMPLATE.md`
  - Checklist e guidelines

- [ ] Conventional Commits enforcement
  - Setup Commitlint
  - Hook `commit-msg` no Husky
  - CI check com `commitlint-github-action`

**Esforço**: 5-6 horas  
**Valor**: ⭐⭐⭐  
**Dependências**: Nenhuma

---

## 📝 Documentation (Low Priority)

**Por que é importante**: Facilita compreensão e adoção por outros desenvolvedores.

### Tasks
- [ ] ADRs (Architecture Decision Records)
  - `docs/adr/0001-use-google-sheets.md`
  - `docs/adr/0002-biome-over-eslint.md`
  - `docs/adr/0003-chat-ui-pattern.md`

- [ ] API documentation
  - OpenAPI spec para `/api/testimonials`
  - Swagger UI ou Scalar
  - Request/response examples

- [ ] Video walkthrough
  - Gravar demo do projeto (3-5 min)
  - Upload no YouTube
  - Embed no README

- [ ] Contributing guide refinement
  - Setup instructions mais detalhado
  - Code style guide
  - PR review process
  - How to run tests

**Esforço**: 3-4 horas  
**Valor**: ⭐⭐  
**Dependências**: Testing infrastructure (para mencionar nos docs)

---

## 🎯 Resumo Executivo

### Ordem Recomendada (Path to Senior-Level)

1. **Testing Infrastructure** (⭐⭐⭐⭐⭐) - Fundação de confiabilidade
2. **Security & Rate Limiting** (⭐⭐⭐⭐⭐) - Proteção essencial
3. **Observability** (⭐⭐⭐⭐) - Visibilidade operacional
4. **Performance Enhancements** (⭐⭐⭐) - Otimizações incrementais
5. **DevEx Improvements** (⭐⭐⭐) - Facilita colaboração
6. **Internationalization** (⭐⭐⭐) - Expansão de alcance
7. **Documentation** (⭐⭐) - Refinamento final

### Esforço Total Estimado
**24-32 horas** de desenvolvimento (3-4 dias de trabalho focado)

### Impacto no Portfolio
Implementar os itens de **High Priority** já eleva significativamente o projeto para nível sênior. Os demais são "cherry on top" que demonstram atenção a detalhes e pensamento holístico.

---

## 🚀 Como Contribuir

Para trabalhar em qualquer item deste backlog:

1. Crie issue no GitHub referenciando a task
2. Comente na issue manifestando interesse
3. Fork, crie branch `feature/nome-da-task`
4. Implemente com testes
5. Abra PR com referência à issue (`Closes #N`)

**Dúvidas?** Abra uma discussion no repo!
