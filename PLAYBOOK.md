# PLAYBOOK — Rotina de Desenvolvedor Python / Dados / Backend

**MTSCH · Matheus Scherer**  
Última atualização: 23/08/2026

Este documento é o sistema operacional dos seus repositórios.  
Siga. Não improvise. A consistência é o que separa portfólio de bagunça.

---

## 1. Princípios (não negocie)

1. **Tese > código**  
   Todo diagnóstico e todo case existe para provar uma frase clara. Se a frase mudou, o código e o README mudam juntos.

2. **Um hub comercial**  
   MTSCH é o centro. Sites de fitness e utilitários são cases ou ofertas secundárias. Não crie novas marcas.

3. **Mesma estrutura = confiança**  
   Os 5 diagnósticos devem ter o mesmo esqueleto (`src/`, `tests/`, `data/`, `docs/`, CI, tom do README).

4. **Commit só com intenção**  
   Não existe “update readme”. Existe “ajusta tese de hora extra após novo ciclo” ou “adiciona teste de nulo no validador”.

5. **Público = amostra de método**  
   Nunca coloque nome de cliente, planilha real ou credencial. Os READMEs já dizem o que o projeto **não é**. Mantenha.

6. **Verde de verdade**  
   Action verde + teste passando + README alinhado com o site. Quadrado verde vazio não conta.

---

## 2. Mapa dos repositórios

| Tipo | Repositórios | Função |
|------|--------------|--------|
| **Hub** | `matheusscherer` | Perfil. 10 segundos para entender o que você vende. |
| **Comercial** | `mtsch-site` | Landing principal + cases ao vivo |
| **Ofertas** | `mtsfit`, `mtscfit` | Landings de produto/protocolo |
| **Método (core)** | `diagnostico-custo-hora-extra`<br>`diagnostico-estoque`<br>`diagnostico-no-show`<br>`diagnostico-retrabalho`<br>`diagnostico-combustivel-rotas` | Prova de método. CSV → tese clara |
| **Utilitários** | `validador_dados`<br>`sales-report-automation`<br>`mvp_clinicas` | Amostras de automação reutilizável |
| **Ops (privado)** | `mtsch-ops` | Fila de leads, não é portfólio |

---

## 3. Rotina Diária (15–40 min)

### Manhã (ou início do bloco de trabalho)

1. Abra o perfil GitHub + site `mtsch.vercel.app`.
2. Confira se Actions estão verdes nos repos que você tocou recentemente.
3. Abra a fila de leads (Notion / `mtsch-ops`).
4. Priorize **um** item:
   - Lead quente → reutilize diagnóstico existente
   - Bug ou Action vermelha → corrija
   - Nada urgente → vá para a rotina semanal

### Durante o dia (quando trabalhar em código)

- Escolha **um** repositório por bloco.
- Antes de codar: rode os testes (`pytest -v`).
- Depois de codar: rode de novo + atualize `docs/relatorio.md` se o número mudou.
- Commit com mensagem clara (veja template abaixo).
- Se for diagnóstico: o número do README **deve** sair do código, nunca inventado.

### Final do dia (5 min)

- Verifique se o site ainda aponta para o case correto.
- Feche a issue ou deixe comentário do que ficou pendente.
- Nada de “deixar para amanhã” sem registrar.

---

## 4. Rotina Semanal

| Dia | Ação | Tempo |
|-----|------|-------|
| **Segunda** | Revisar Issues abertas + Actions vermelhas de todos os repos públicos | 15–20 min |
| **Quarta** | Um PR pequeno (mesmo solo): teste, CI, README ou documentação | 30–45 min |
| **Sexta** | Alinhar números do perfil + site + diagnósticos. Qualquer divergência = correção imediata | 20 min |
| **Quando fecha case** | Atualizar **os três lugares** na mesma sessão: diagnóstico → site → perfil | 40–60 min |

Regra de ouro da sexta:  
Se o número do site for diferente do que o script gera, o site está mentindo. Corrija antes de qualquer outra coisa.

---

## 5. Como trabalhar nos Diagnósticos (Python / Dados)

### Estrutura obrigatória (não desvie)

```
diagnostico-xxx/
├── .github/workflows/ci.yml
├── data/               # CSVs de exemplo (fictícios ou anonimizados)
├── docs/
│   └── relatorio.md    # gerado pelo script
├── src/
│   └── diagnostico_xxx/
│       ├── __init__.py
│       ├── __main__.py
│       └── analyze.py
├── tests/
│   └── test_analyze.py
├── pyproject.toml
├── LICENSE
└── README.md
```

### Passo a passo de trabalho

1. Clone / entre no repo
2. `python -m venv .venv && source .venv/bin/activate`
3. `pip install -e ".[dev]"`
4. Rode: `python -m diagnostico_xxx`
5. Rode: `pytest -v`
6. Só depois mexa no código
7. Qualquer mudança de regra → atualize o teste
8. Qualquer mudança de número → o README e o `docs/relatorio.md` mudam juntos
9. Commit + push

### Checklist de qualidade do diagnóstico

- [ ] `pytest` passa
- [ ] Action CI verde
- [ ] README tem a seção **“O que isto NÃO é”**
- [ ] Números batem com o que o script imprime
- [ ] Link do case no site está funcionando
- [ ] Nenhum nome de cliente ou dado sensível

---

## 6. Como trabalhar nos Sites (TypeScript / Vercel)

1. Site no ar = prioridade máxima. Link quebrado = repo morto.
2. Um ajuste por vez (headline, prova, CTA, rota do case).
3. Depois do deploy, abra o link em aba anônima e confira mobile.
4. A prova social (4.110 h, R$ 31k, 29,1% etc.) **deve** ser a mesma dos diagnósticos.
5. Não redesenhe a landing inteira. Itere.

---

## 7. Checklist antes de qualquer commit

```
[ ] Rodei os testes localmente
[ ] Action vai passar (ou já sei o que quebrou)
[ ] Mensagem de commit descreve a intenção, não o arquivo
[ ] README / docs atualizados se o comportamento mudou
[ ] Nenhum segredo, .env ou dado real no commit
[ ] No diagnóstico: o número do relatório sai do código
```

---

## 8. Templates

### Commit

```
tipo(escopo): descrição curta

# Exemplos bons
fix(hora-extra): separa custo puro de atraso de turno
docs(perfil): atualiza números do case de estoque
test(validador): cobre CSV com coluna nula
chore(ci): adiciona cache do pip
```

### Issue

```
## Problema
...

## Resultado esperado
...

## Como reproduzir / contexto
...

## Aceite
- [ ] Teste passando
- [ ] README atualizado (se necessário)
```

### Seção obrigatória em todo README de diagnóstico

```markdown
## O que isto NÃO é

- Não conecta em sistema de ponto real
- Não publica nome de cliente, posto ou pessoa
- Não é modelo preditivo — é diagnóstico de ciclo fechado
- O relatório do site é o case. Este repo é a fatia de Pandas que sustenta a tese.
```

---

## 9. Quando você fecha um case real

Faça nesta ordem, na mesma sessão:

1. Atualize o diagnóstico correspondente (código + teste + `docs/relatorio.md`)
2. Atualize a página do case no `mtsch-site`
3. Atualize o bloco de números no README do perfil (`matheusscherer`)
4. Confira se os três lugares contam a **mesma** história
5. Só então marque o case como fechado no Notion

Se pular algum passo, a inconsistência aparece em 48h para o próximo visitante.

---

## 10. Comandos padrão do stack

```bash
# Diagnóstico
python -m venv .venv && source .venv/bin/activate
pip install -e ".[dev]"
python -m diagnostico_xxx
pytest -v

# Site (exemplo mtsch-site)
npm install
npm run dev
npm run build

# Verificação rápida de qualidade
git status
git diff
```

---

## Resumo de 30 segundos

- Segunda: limpeza de Issues e Actions  
- Durante a semana: um repo por vez, testes sempre  
- Sexta: alinhamento de números entre perfil + site + diagnósticos  
- Case fechado: três lugares atualizados na mesma hora  
- Commit só com intenção clara  
- Nunca invente número no Markdown  

Esse é o sistema.  
Execute. Não discuta com ele.

---

**Contato operacional**  
GitHub: [matheusscherer](https://github.com/matheusscherer)  
Site: [mtsch.vercel.app](https://mtsch.vercel.app)  
Email: contatomatheusscherer@gmail.com
