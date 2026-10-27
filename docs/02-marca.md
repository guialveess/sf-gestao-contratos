# Construção da Marca

> Seguindo os Prompts 01–03 do mentor (ver [05-prompts-mentor.md](05-prompts-mentor.md)): nome → slogan → identidade visual.
> Critério de avaliação: "Construção da Marca" (Aspectos Gerais).

## Decisão (fechada para a entrega de 27/10)

- **Nome comercial**: **ContratAI**
- **Slogan**: "Cada contrato, no prazo certo."
- **Logotipo**: gerado — ver abaixo. Se o grupo quiser trocar, basta ajustar aqui e eu regenero.

Se o grupo preferir, podem substituir por uma das alternativas abaixo antes da apresentação — é só decisão de time, não trabalho técnico pendente.

### Alternativas de nome (caso quiram trocar)
2. **Renova+** — foco no processo de renovação, nome curto e comercial
3. **ClauseFlow** — foco no fluxo de cláusulas/aditivos, tom mais "enterprise"

### Alternativas de slogan
- "Contratos sob controle, renovações sem surpresa."
- "Previsibilidade do início ao aditivo."

## Identidade visual

Conceito: documento/contrato estilizado combinado com um ícone de ciclo de renovação (seta circular + check), paleta azul-petróleo + verde, tipografia sans-serif bold (Bricolage Grotesque).

Gerado localmente com um script Python (Pillow), sem depender de nenhuma conta ou serviço externo — arquivo versionado neste repositório, pronto para uso.

**Logo:**

![Logo ContratAI](assets/logo-contratai.png)

Arquivo: [`docs/assets/logo-contratai.png`](assets/logo-contratai.png)

## Pendência do grupo

- [x] Nome comercial definido (ContratAI)
- [x] Slogan definido
- [x] Logotipo gerado e versionado (`docs/assets/logo-contratai.png`)
- [x] Aplicar o logo no Lightning App (App Manager → App Settings → upload da imagem), com a exibição habilitada no metadado do app (`shouldOverrideOrgTheme`)
