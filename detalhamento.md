# Engenharia de Knowledge Bases para Reforma Tributária
Proposta de processo operacional | Versão 1.0 | Material conceitual, sem dados internos.

## Objetivo
Produzir conhecimento confiável, estruturado, rastreável, reutilizável e versionado para agentes de IA, com humano no loop, avaliações independentes e atualização contínua. Uma KB não é apenas um documento: é um conjunto de conceitos, regras, evidências, cenários, metadados e critérios testáveis.

## Organização multidimensional
- Pilar: Regulatório; Operacional; Jornadas do cliente; Arranjos e canais; Produtos bancários; Tecnologia e dados.
- Tema: por exemplo IBS/CBS, split payment, RAD, apuração assistida, documentos fiscais.
- Subtema: decomposição de obrigações, liquidação, exceções e participantes.
- Artefato: conceito, regra, exceção, fluxo, caso, decisão ou evidência.
- Contexto: segmento, produto, canal, arranjo, jornada, data de vigência.
- Relação: depende de; complementa; contradiz; substitui; aplica-se a.

## 01 · Mapeamento e planejamento
**Inputs:** demanda de conhecimento; objetivos do agente; pilares; jornadas de compra, cobrança, pagamento, recebimento e conciliação; produtos e canais; fontes iniciais.
**Processamento:** IA sugere taxonomia, subtemas, dependências, cenários e perguntas; humano revisa o escopo. Construir matriz tema x jornada x arranjo x segmento x tempo. Identificar lacunas e priorizar por impacto, risco, proximidade de vigência, volume e dependências.
**Outputs:** domain_catalog, coverage_matrix, backlog priorizado, responsáveis, critérios de completude.
**Controle:** especialista aprova escopo, define o que fica explicitamente fora; nenhum tema pode ser considerado coberto só porque existe documento.

## 02 · Curadoria de fontes
**Inputs:** backlog, textos legais e regulamentares, notas técnicas, decisões internas aprovadas, documentação de produtos.
**Processamento:** coletar fonte autorizada, registrar origem, URL ou ID, versão, data de publicação e vigência; extrair passagens; mapear afirmações e evidências; detectar conflito e lacunas. Separar autoridade normativa de interpretação e decisão operacional.
**Outputs:** source_registry, evidence_map, unresolved_questions, lista de documentos substituídos.
**Gate 1:** fontes suficientes, admissíveis e atuais? Se não, devolver à curadoria. IA nunca inventa norma ausente.

## 03 · Estruturação do conhecimento
**Inputs:** taxonomia, registros de fontes aprovadas, KBs publicadas, glossário.
**Processamento:** normalizar conceitos; extrair regras na forma condição → resultado → exceções; modelar atores, fluxos, jornadas, eventos e integrações; criar relações e dependências; desambiguar termos; marcar fato normativo, interpretação, decisão interna, hipótese ou pendência. Distinguir vigente_desde de confirmado_em.
**Outputs:** knowledge_model, dependency_graph, rule_catalog, scenario_catalog.
**Controle:** deduplicação, detecção de contradições e rastreabilidade para cada regra.

## 04 · Geração da KB
**Inputs:** conhecimento estruturado, template, fontes, política editorial e terminologia.
**Processamento:** redigir seis camadas: conceitual, normativa, funcional, operacional, aplicada e decisória; citar evidências em afirmações críticas; incluir exemplos e contraexemplos; documentar exceções, limitações e aspectos ainda não definidos; gerar perguntas candidatas.
**Outputs:** kb_candidate versionada, traceability_map, changelog, pendências.
**Gate 2:** esquema válido, campos obrigatórios completos, fontes vinculadas, conceitos consistentes e inexistência de inconsistências estruturais.

### Template mínimo de uma KB
ID; título; escopo; objetivo; público; glossário; conceitos; regras e exceções; fontes por afirmação; atores; fluxos; impactos; cenários; perguntas frequentes; limitações; dependências; status de certeza; data de vigência; data da última checagem; versão; owner; aprovações; resultados de avaliação.

## 05 · Validação humana especializada
**Inputs:** KB candidata, mapa de evidências, checklist, alterações desde versão anterior.
**Processamento:** Tributário/Jurídico revisa norma e interpretação; Produto/Negócio confirma aplicação ao cliente; Operações/TI valida processos, integrações e sistemas; responsável pela KB resolve comentários e conflitos. Roteamento de revisores proporcional ao risco.
**Outputs:** expert_review, approval_records, change_requests e KB tecnicamente validada.
**Gate 3:** aprovações exigidas concluídas; pendência crítica bloqueia evolução. Toda decisão tem autor, data, evidência e versão.

## 06 · Evals independentes
**Inputs:** versão congelada da KB, agente sob teste, suíte golden humana, conjunto sintético, adversarial, configurações de RAG e rubricas.
**Processamento:** testar separadamente correção do conteúdo, recuperação do conhecimento e geração da resposta. Executar perguntas; comparar afirmações, fatos obrigatórios, exceções e evidências, não semelhança textual apenas. Avaliador A e B devem ser independentes preferencialmente de famílias diferentes da IA produtora; adicionar testes determinísticos. Registrar concordância, divergência e incerteza, enviando casos críticos a humano.
**Outputs:** evaluation_report, per_question_results, failure_registry, risk_decisions.
**Gate 4:** nenhuma falha normativa crítica, limites de métricas calibrados atendidos e testes de regressão aprovados. Não permitir compensação de erro grave por média alta.

### Golden Dataset
Cada caso contém question_id; pergunta; resposta validada; fatos obrigatórios; fatos proibidos; contexto e premissas; evidências; risco; versão; criador e aprovador. Parte do dataset deve ficar reservada da produção para mitigar ajuste artificial aos testes. Perguntas sintéticas não viram verdade de referência automaticamente.

### Métricas
Cobertura por cenário, correção factual, groundedness/faithfulness, recall de recuperação, relevância, completude, contradição, precisão das citações, abstenção apropriada, concordância entre juízes e regressão. Registrar modelo, prompt, dados, índice, versão da KB e timestamp em cada rodada.

### Triagem de falhas
- Conteúdo ausente ou errado: voltar às etapas 3/4 e revisar com especialista.
- Retrieval falhou: ajustar fragmentação, indexação, metadados e estratégia de busca.
- Conteúdo encontrado mas resposta incorreta: investigar instruções e comportamento do agente.
- Teste ambíguo ou incorreto: revisar golden humano com independência.
- Fonte mudou: voltar à curadoria e reavaliar dependências.

## 07 · Homologação e publicação
**Inputs:** KB validada, Evals, pareceres, release candidate e configuração do sistema.
**Processamento:** conferir política de risco; aprovação humana final; criar release imutável e manifesto; indexar representação consumível via RAG; controlar acesso; executar smoke tests; habilitar observabilidade; permitir rollback.
**Outputs:** published_kb, release_manifest, audit_log, retrieval_index versionado.
**Gate 5:** autorização explícita de publicação e auditoria. Separar fonte canônica do conhecimento da representação para RAG, para permitir mudar chunking sem reescrever as regras.

## 08 · Monitoramento e atualização
**Inputs:** normas e notas atualizadas, incidentes, feedback, telemetria, perguntas sem resposta, novas demandas.
**Processamento:** monitorar fontes autorizadas, detectar diffs, realizar análise de impacto em KBs e testes, abrir change request, priorizar, recalcular cobertura e executar regressões. Alterações tributárias nunca são publicadas automaticamente sem aprovação aplicável.
**Outputs:** change_requests, alerts, quality_metrics, backlog e novas versões validadas.
**Controle:** SLA por criticidade, expiração e revalidação de conhecimento, trilha de auditoria.

## Papéis e accountability
- IA pesquisadora: descobre fontes e extrai evidências.
- IA taxonomista: modela pilares, temas, dependências e lacunas.
- IA redatora: constrói KBs a partir de evidências aprovadas.
- IA verificadora: valida estrutura, referências e consistência.
- IA avaliadora A/B: valida respostas e identifica omissões independentemente.
- Especialista tributário/jurídico: responsável pela interpretação normativa.
- Responsável de negócio: responsável pelos impactos no cliente.
- Especialista operacional/TI: responsável por fluxos e viabilidade técnica.
- Owner da KB: responsável por publicação, SLA, mudanças e histórico.

## Contratos de saída
1 domain_catalog + coverage_matrix + backlog
2 source_registry + evidence_map
3 knowledge_model + dependency_graph
4 kb_candidate + traceability_map
5 expert_review + approval_records
6 evaluation_report + failure_registry
7 release_manifest + published_kb
8 change_requests + quality_metrics

Metadados mínimos de todos os artefatos: artifact_id, version, owner, status, created_at, updated_at, source_ids, approval_ids, dependency_ids.

## Indicadores executivos
Cobertura validada, Evals aprovados, taxa de erro crítico, fontes vigentes, revisão dentro do SLA, tempo de produção, esforço humano, retrabalho, divergência entre avaliadores e incidentes pós-publicação.

## Plano incremental
Ciclo 1: taxonomia, catálogo, fontes, templates e gates.
Ciclo 2: piloto split payment, relações com RAD e apuração assistida, produção e revisão.
Ciclo 3: golden humano, sintético, adversarial e duas IAs avaliadoras.
Ciclo 4: homologação, publicação, monitoramento e dashboard.
