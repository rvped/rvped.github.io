# Site de verificação de certificados — implantação

**Esta pasta é o site inteiro, e nada além do site.** É gerada do zero a cada
execução de `python3 gera_site_verificacao.py` (na raiz do projeto) a partir
de `certificados_emitidos.json`. Não contém nenhum módulo do curso, nenhuma
questão, nenhum gabarito — só nome, data e código de cada certificado emitido,
o mesmo conteúdo que já vai no certificado físico.

**Por isso ela é um repositório Git separado do projeto do curso**, e é
seguro que este repositório seja **público**: o projeto do curso (com a prova
e o gabarito, marcados "não distribuir") permanece privado, no seu lugar.

## Configuração única (a fazer uma vez, por você)

Eu não posso criar contas nem pagar por nada em seu nome — os passos abaixo
são os únicos que exigem você.

1. **Conta no GitHub**, se ainda não tiver uma: github.com → Sign up (grátis).
2. **Criar um repositório novo, público**, por exemplo `certificados-rvp`
   (Settings → Create repository → marcar **Public**, sem README).
3. Nesta pasta (`site_verificacao/`), rodar:
   ```bash
   git init
   git add -A
   git commit -m "site de verificação"
   git branch -M main
   git remote add origin https://github.com/SEUUSUARIO/certificados-rvp.git
   git push -u origin main
   ```
4. No repositório, em **Settings → Pages → Build and deployment → Source**,
   escolher **GitHub Actions** (o workflow em `.github/workflows/deploy.yml`
   já está pronto e publica sozinho a cada `git push`).
5. Em alguns minutos o site está em `https://SEUUSUARIO.github.io/certificados-rvp/`.
6. **Regerar os certificados com a URL real**, na raiz do projeto:
   ```bash
   python3 gera_site_verificacao.py --base-url https://SEUUSUARIO.github.io/certificados-rvp
   ```
   (os QR codes já emitidos apontavam para a URL de exemplo; rodar de novo
   corrige todos de uma vez — os códigos e o registro não mudam.)

## Domínio próprio (opcional, não necessário para funcionar)

Se um dia você registrar um domínio, em **Settings → Pages → Custom domain**
o GitHub cuida do certificado HTTPS sozinho. Até lá, o endereço
`SEUUSUARIO.github.io/...` funciona igual, para sempre, sem custo.

## Rotina de uso, depois de configurado uma vez

Cada vez que emitir um certificado novo:

```bash
python3 gerar_certificado.py --nome "Nome do Aluno" --saida certificado.html
python3 gera_site_verificacao.py --base-url https://SEUUSUARIO.github.io/certificados-rvp
cd site_verificacao && git add -A && git commit -m "novo certificado" && git push
```

O `git push` é a única ação manual. Dali em diante o GitHub publica sozinho.
