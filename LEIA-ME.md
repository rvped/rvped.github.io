# Site de verificação de certificados — no ar

**URL:** https://rvped.github.io/

**Esta pasta é o site inteiro, e nada além do site.** É gerada do zero a cada
execução de `python3 gera_site_verificacao.py` (na raiz do projeto) a partir
de `certificados_emitidos.json`. Não contém nenhum módulo do curso, nenhuma
questão, nenhum gabarito — só nome, data e código de cada certificado emitido,
o mesmo conteúdo que já vai no certificado físico.

**Por isso ela é um repositório Git separado do projeto do curso** —
`github.com/rvped/rvped.github.io`, público — e é seguro que seja público: o
projeto do curso (com a prova e o gabarito, marcados "não distribuir")
permanece privado, no seu lugar.

## Configuração — já feita

Conta GitHub renomeada para `rvped`; repositório `rvped.github.io` criado e
publicado; GitHub Pages ativo com fonte = GitHub Actions
(`.github/workflows/deploy.yml`, publica sozinho a cada `git push`). Testado
ponta a ponta duas vezes, com certificado real emitido e removido.

## Rotina de uso, a partir de agora

Cada vez que emitir um certificado novo, na raiz do projeto:

```bash
python3 gerar_certificado.py --nome "Nome do Aluno" --saida certificado.html
python3 gera_site_verificacao.py --base-url https://rvped.github.io
cd site_verificacao && git add -A && git commit -m "novo certificado" && git push
```

O `git push` é a única ação manual. Dali em diante o GitHub publica sozinho,
em menos de um minuto.

## Domínio próprio (opcional, não necessário para funcionar)

Se um dia você registrar um domínio, em **Settings → Pages → Custom domain**
do repositório `rvped/rvped.github.io` o GitHub cuida do certificado HTTPS
sozinho. Até lá, `rvped.github.io` funciona igual, para sempre, sem custo.

## O que mudou nesta rodada, e por quê

O site pedia `rvped.github.io` (sem caminho depois). O GitHub só serve esse
formato — sem `/nome-do-repo/` no meio — quando o repositório se chama
exatamente `<usuário>.github.io`. Isso exigia uma conta ou organização
chamada `rvped`; você escolheu **renomear sua conta pessoal**
(`vsaragao97-droid` → `rvped`) em vez de criar uma organização separada.
GitHub avisa, e vale registrar: **não criou redirecionamento para o Pages
antigo** — por isso o site foi republicado do zero na URL nova, e o link
antigo (`vsaragao97-droid.github.io/certificados-rvp/`) parou de funcionar
(nenhum certificado tinha sido emitido de verdade até este ponto, então
nenhum código ficou órfão). O repositório foi renomeado de `certificados-rvp`
para `rvped.github.io` — o GitHub manteve a configuração do Pages através da
renomeação, sem precisar reconfigurar nada além da URL base nos scripts.
