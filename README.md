# Fluxzee Hotelaria

**IA para hotelaria independente.** Agente de atendimento 24h que responde leads em 28 segundos, qualifica, apresenta quartos e fecha reservas diretas — sem comissão de OTA.

---

## Visão geral do projeto

Este repositório contém a vertical de hotelaria da Fluxzee. O produto resolve um problema específico: hotéis e pousadas independentes perdem reservas porque demoram horas para responder leads no Instagram e WhatsApp. O lead não recebe resposta, abre o Booking ou Airbnb, reserva em 3 minutos e vai embora. O quarto fica vazio. A diária, perdida.

A solução é um agente de IA que responde em 28 segundos, qualifica o lead, apresenta as opções de quarto e fecha a reserva direta — sem comissão para OTA, com os dados do hóspede salvos no CRM.

---

## Stack técnica

### Landing page
- **HTML puro** — sem framework, sem dependências externas
- - Todas as imagens embutidas em base64 (arquivo único ~5MB)
  - - Slideshow hero automático (4 imagens, troca a cada 5s)
    - - Calculadora de ROI com sliders interativos
      - - GTM-T2JVGSVQ instalado
        - - **Deploy:** Cloudflare Pages via Direct Upload
         
          - ### Identidade visual
          - - Verde #00c96e — destaques e confirmações
            - - Laranja #e8600a — CTAs e impacto
              - - Fundo #0a1f14 — dark forest green
                - - Amarelo #f5c842 — NUNCA usar em conteúdo de hotelaria
                  - - Fonte: Arial Black para headlines
                   
                    - ### Automação de leads
                    - - Typebot — bot de qualificação conversacional (4 fluxos por plano)
                      - - Calendly — agendamento da reunião de diagnóstico (embutido no Typebot)
                        - - n8n — orquestração: recebe webhook Typebot, salva Notion, notifica WhatsApp
                          - - Notion — CRM de leads qualificados
                            - - Claude API — agente de atendimento 24h no Instagram DM e WhatsApp
                              - - WhatsApp Business API — canal principal de atendimento ao hóspede
                               
                                - ---

                                ## Fluxo de qualificação de leads

                                CTA da LP (?plano=starter|pro|premium|diagnostico)
                                    ↓
                                Typebot — fluxo específico por plano
                                    Perguntas: nome, WhatsApp, e-mail, tipo estabelecimento,
                                    nº quartos, diária média, % OTA atual, principal dor
                                    ↓
                                Calendly embed dentro do Typebot
                                    Lead escolhe horário para reunião de diagnóstico
                                    ↓
                                Webhook Typebot → n8n
                                    → Notion CRM (todos os dados + plano + link reunião)
                                    → WhatsApp (notificação para Diogo com resumo do lead)

                                ### Parâmetros CTAs por plano
                                - Estúdio (Starter): ?plano=starter — Apart-hotel, Flat, Studio — 1–20 quartos
                                - - Hotel / Pousada (Pro): ?plano=pro — 21–50 quartos
                                  - - Resort / Gran Hotel (Premium): ?plano=premium — 50+ quartos
                                    - - Diagnóstico padrão: ?plano=diagnostico — CTAs genéricos da LP
                                     
                                      - ---

                                      ## Pricing

                                      - Estúdio: R$ 5.000 impl. + R$ 1.500/mês = R$ 23.000 ano 1 (ROI 3x–6x)
                                      - - Hotel / Pousada: R$ 10.000 impl. + R$ 3.000/mês = R$ 46.000 ano 1 (ROI 5x–16x)
                                        - - Resort / Gran Hotel: R$ 20.000 impl. + R$ 5.000/mês = R$ 80.000 ano 1 (ROI 10x–100x+)
                                         
                                          - ---

                                          ## Deploy — Cloudflare Pages

                                          A LP é um arquivo HTML único (lp/index.html) com todas as imagens embutidas em base64. Não há build step nem dependências.

                                          Para publicar: Cloudflare Pages → Direct Upload → lp/index.html
                                          Domínio sugerido: hotelaria.fluxzee.io

                                          Para atualizar: edite o lp/index.html → Cloudflare Pages → Create new deployment → Direct Upload

                                          ---

                                          ## Instruções para Claude Code

                                          **O que já está pronto:**
                                          - Landing page completa em lp/index.html — não recriar do zero
                                          - - Logos SVG em logo/ — usar sempre estas versões
                                            - - Guia de marca em identidade-visual/guia-de-marca.md — seguir obrigatoriamente
                                             
                                              - **O que está pendente:**
                                              - - Fluxos Typebot em automacao/typebot/fluxos.json
                                                - - Fluxo n8n em automacao/fluxo-n8n.json
                                                  - - Prompts de qualificação em automacao/prompts/
                                                    - - CTAs da LP com URLs Typebot por plano
                                                     
                                                      - **Contexto de negócio:**
                                                      - - Fundador: Diogo Fernandes (GitHub: DiogoFernandes-IA)
                                                        - - Nicho: Hotelaria independente no Brasil (expansão futura: Alicante, Espanha)
                                                          - - Narrativa ancora: Ilha Grande — lead perdido por falta de resposta rápida
                                                            - - Problema central: tempo de resposta (2h+ vs 28s)
                                                              - - Meta imediata: 2 pilotos — pousada em Santos + hotel independente
                                                               
                                                                - ---

                                                                ## Contexto da marca

                                                                "Sem resposta, o lead abre o Airbnb ou o Booking, reserva em outro lugar em 3 minutos e vai embora. Você não recebe nada. O quarto fica vazio. A diária, perdida."

                                                                Esse é o momento de dor que o produto resolve. Toda comunicação deve partir daqui.

                                                                Canais ativos: Instagram (principal) → LinkedIn (ativar após 30 dias com resultados dos pilotos)
