---
slug: the-rising-tide-live-migration
id: xjv2r0tfyztq
type: challenge
title: "<span id="assignment.65" lang="pt" hist="vertrex-bank">🌊 Capítulo 4: A Maré Crescente</span>"
teaser: <span id="assignment.66" lang="pt" hist="vertrex-bank">Um vazamento de líquido de refrigeração está inundando o rack que hospeda o Payment Gateway. Execute uma migração ao vivo sem tempo de inatividade antes que o hardware entre em curto-circuito, enquanto as transações continuam fluindo.</span>
tabs:
- id: fpgxlmifoynn
  title: SUSE Virtualization UI
  type: service
  hostname: kvm-host
  path: /
  port: 8443
  protocol: https
- id: dltxk4yfrhwa
  title: Cluster Terminal
  type: terminal
  hostname: kvm-host
- id: js6k1cai9uqc
  title: Rancher Prime UI
  type: service
  hostname: kvm-host
  port: 30002
  protocol: https
difficulty: intermediate
timelimit: 2400
enhanced_loading: null
---
<span id="assignment.67" lang="pt" hist="vertrex-bank">🌊 Capítulo 4: A Maré Crescente
==============================</span>
<style type="text/css">
  * {
    font-family: suse;
    src: url('https://fonts.google.com/specimen/SUSE');
  }
  .suse { color: #30ba78; }
  .virt { color: #30ba78; }
  .bank { color: #d4af37; }
  .danger { color: #ff4d4d; font-weight: bold; }
  .hovereffect {
    border-radius: 25px 25px 25px 25px;
    background: linear-gradient(#30ba78 0 0) var(--hundredpercent, 0) / var(--hundredpercent, 0) no-repeat;
    transition: 0.5s, background-position 0s;
    padding: 5px;
  }
  .hovereffect:hover {
    --hundredpercent: 100%;
    color: white;
    border-radius: 10px 25px 10px 25px;
  }
  .story {
    border-left: 5px solid #d4af37;
    border-radius: 0 15px 15px 0;
    background: linear-gradient(135deg, rgba(48,186,120,.10), rgba(212,175,55,.10));
    padding: 15px 20px;
    margin: 15px 0;
  }
  .story em { color: #d4af37; }
  .missionbox {
    border: 2px dashed #30ba78;
    border-radius: 15px;
    padding: 12px 18px;
    margin: 15px 0;
  }
  .highlightcopy { color: white; font-weight: bold; padding: 0 10px; }
  img.logos { border-radius: 10px; }
  /* compact credential boxes (scoped: only code blocks inside <div class="cred">) */
  .cred > div { margin: 0; }
  .cred .my-3 {
    display: flex;
    flex-direction: row-reverse;   /* put the copy bar on the right */
    align-items: stretch;
    width: fit-content;
    min-width: 14em;
    margin: 4px 0;
    overflow: hidden;
  }
  .cred .my-3 > div:first-child {  /* the bar holding the copy button */
    height: auto;
    padding: 4px 8px;
    border-bottom: none;
    border-left: 1px solid rgba(255,255,255,.25);
    border-radius: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #30ba78;
  }
  .cred .my-3 > div:first-child,
  .cred .my-3 > div:first-child * {
    color: #fff !important;
  }
  .cred .my-3 > div:first-child:hover,
  .cred .my-3 > div:first-child:hover * {
    font-weight: bold;
  }
  .cred .my-3 > pre {
    flex: 1 1 auto;
    margin: 0 !important;
    padding: 2px !important;
    border-radius: 0 !important;
    display: flex;
    align-items: center;
  }
  img.animatedgif {
    --borderthickness: 5pt;
    --colors: #0000 25%,#30ba78 0;
    padding: 10px;
    background:
      conic-gradient(from 90deg  at top    var(--borderthickness) left  var(--borderthickness),var(--colors)) 0    0,
      conic-gradient(from 180deg at top    var(--borderthickness) right var(--borderthickness),var(--colors)) 100% 0,
      conic-gradient(from 0deg   at bottom var(--borderthickness) left  var(--borderthickness),var(--colors)) 0    100%,
      conic-gradient(from -90deg at bottom var(--borderthickness) right var(--borderthickness),var(--colors)) 100% 100%;
    background-size: 50px 50px;
    background-repeat: no-repeat;
    transition: 1s;
  }

  img.animatedgif:hover {
    background-size: 51% 51%;
  }

  .embedded_img {
    width: 100%;
    height: auto;
    max-height: 3vh;
    max-width: 3vh;
    margin: 0;
    padding: 0;
    display: inline-block;
  }

</style>

<img class="logos" alt="Welcome!" src="../assets/04-chapter-img.png"/>

<div id="401" class="story">

<span id="assignment.68" lang="pt" hist="vertrex-bank">A adrenalina do incidente na sala de negociação mal tinha desaparecido do teu sistema quando um gemido metálico e profundo ecoa pelas paredes do datacenter. Tu e a Sarah viram-se simultaneamente para o **Rack 4**. Uma válvula de refrigerante principal rebentou por cima, e um fluxo constante de água refrigerada e tratada quimicamente está a cair diretamente sobre o chassis do servidor físico que aloja o **Payment Gateway** principal do banco.

*"Se esse servidor entrar em curto-circuito, o gateway cai,"* diz a Sarah, o pânico genuíno a instalar-se na sua voz enquanto observa a poça de água a formar-se. *"Se o gateway cair, todas e cada uma das transações de cartão de crédito do Vertex Trust Bank falham. Vamos enfrentar investigações regulatórias federais até de manhã."*

*"Não vamos deixar que isso caia,"* respondes tu, os teus dedos a voar pelo teclado.</span>

</div>

<span id="assignment.69" lang="pt" no>Não pode desligar a máquina para a mover; o fluxo de transações é demasiado crítico, processando milhares de pedidos por segundo. Tem de executar uma **migração ao vivo**, movendo uma VM em execução, memória incluída, para um nó físico diferente com **tempo de inatividade zero**.

Mas primeiro, para garantir a máxima largura de banda disponível para a migração de emergência, decide suspender um servidor de processamento em lote não crítico nas proximidades.

## 🎯 Objetivos da Sua Missão

1. Suspender cargas de trabalho não críticas para libertar recursos
2. Estabelecer um heartbeat de serviço
3. Executar a Migração ao Vivo
4. Monitorizar a transferência sem interrupções
5. Retomar as operações normais
6. Entregar a bastidor danificado à equipa de reparação



🔐 Credenciais de Login
====================

A UI do <span id="assignment.69.1" lang="nolang" no>**SUSE Virtualization**</span> e a UI do **Rancher Prime** utilizam as mesmas credenciais.</span>

<span id="assignment.70" lang="nolang" no>Username:</span>

<div class="cred">

```txt
admin
```

</div>

<span id="assignment.71" lang="nolang" no>Password:</span>

<div class="cred">

```txt
[[ Instruqt-Var key="RANCHER_PASSWORD" hostname="kvm-host" ]]
```

</div>



<span id="assignment.72" lang="pt" no>⏸️ Tarefa 1: Suspender cargas de trabalho não críticas para libertar recursos
===========================================================

No</span> [button label="SUSE Virtualization UI" variant="success"](tab-0) <span id="assignment.73" lang="pt" no>, vá para <span id="assignment.40.2" lang="nolang" no>**Virtual Machines**</span>:

1. Localize a máquina virtual com o nome:</span>

<div class="cred">

```txt
daily-batch-processor
```

</div>

<span id="assignment.74" lang="pt" no>2. Clique no  no lado direito da sua linha
3. Selecione <span id="assignment.74.1" lang="nolang" no>**Pause**</span> e depois clique em <span id="assignment.74.2" lang="nolang" no>**Apply**</span> quando solicitado a confirmar.
4. Aguarde até que o seu estado mude para <span id="assignment.74.3" lang="nolang" no>**Paused**</span>

Isto paralisa os seus ciclos de CPU, dedicando o máximo de recursos de hardware à sua operação de emergência.

> [!NOTE]
> Isto não é realmente necessário, já configurámos uma rede dedicada para o tráfego de live migration, está aqui para fins educativos</span>



<span id="assignment.75" lang="pt" no>📡 Tarefa 2: Estabelecer um heartbeat de serviço
========================================


  


Mude para a</span> [button label="Cluster Terminal" variant="success"](tab-1) <span id="assignment.76" lang="pt" no>Você precisa de um monitor de batimento contínuo para comprovar que a ligação de rede permanece intacta durante a evacuação.

Inicie o monitor de batimento a partir de <span id="assignment.76.1" lang="nolang" no><b class="highlightcopy">webserver-prod</b></span>:

```bash,run
ssh -o StrictHostKeyChecking=accept-new  sles@[[ Instruqt-Var key="PAYMENT_GATEWAY_IP" hostname="kvm-host" ]] 'ping 192.168.122.1'

```

> [!IMPORTANT]
> Deixe o ping a correr continuamente no terminal. **Não o pare.** Este fluxo contínuo de respostas é a sua prova de zero tempo de inatividade. Volte a focar-se na interface <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span>.</span>

<span id="assignment.77" lang="pt" no>🚚 Tarefa 3: Executar a Migração ao Vivo
=========================================


  


No</span> [button label="SUSE Virtualization UI" variant="success"](tab-0) <span id="assignment.78" lang="pt" no>, vá para **<span id="assignment.6.2" lang="nolang" no>Virtual Machines</span>** e localize a seguinte instância:</span>

<div class="cred">

```txt
webserver-prod
```

</div>

<span id="assignment.79" lang="pt" no>1. Consulte a coluna <span id="assignment.79.1" lang="nolang" no>**Node**</span> e **anote** em que nó o gateway está sendo executado: você vai querer provar que ele se moveu
2. Clique em na extremidade direita da linha correspondente
3. Selecione <span id="assignment.79.2" lang="nolang" no>**Migrate**</span> no menu de contexto
4. Escolha um nó de destino diferente e seguro na lista suspensa
5. Clique em <span id="assignment.74.2" lang="nolang" no>**Apply**</span>

Nos bastidores, <span id="assignment.2.3" lang="nolang" no>KubeVirt</span> copia as páginas de memória ativa da VM para o nó de destino pela rede, rastreando e recopiando quaisquer páginas que o gateway ocupado altere durante o processo, até conseguir congelar, alternar e retomar a execução no novo nó em uma fração de segundo.</span>

<span id="assignment.80" lang="pt" no>👀 Tarefa 4: Monitorizar a transferência sem interrupções
========================================


  


Volte imediatamente para o</span> [button label="Cluster Terminal" variant="success"](tab-1) <span id="assignment.81" lang="pt" no>aba e observe a sequência de ping.</span>

<div id="402" class="story">

<span id="assignment.82" lang="pt" hist="vertrex-bank">Prendes fôlego enquanto o <span id="ch1.intro1.1" lang="nolang" no>hypervisor</span> coordena a enorme transferência de memória pela rede. Os pings continuam a percorrer o ecrã, **completamente ininterruptos**. A máquina virtual materializa-se sem esforço no novo nó físico, precisamente quando as faíscas começam a saltar do chassis danificado pela água na Bastidor 4.</span>

</div>

<span id="assignment.83" lang="pt" no>Pressione `Ctrl+C` para encerrar o ping.</span>

<div id="403" class="story">
<span id="assignment.84" lang="pt" hist="vertrex-bank">Você exala bruscamente. O fluxo de transação sobreviveu.</span>
</div>


<span id="assignment.85" lang="pt" no>Rigorosamente falando, *existe* sim um momento de transferência: assim que a cópia de memória converge, a VM congela por um instante final enquanto a execução passa para o novo nó, uma micro-interrupção. Numa infraestrutura devidamente dimensionada, isso passa completamente despercebido; mesmo neste laboratório, que executa virtualização *dentro* de virtualização *dentro* de virtualização, o máximo que poderias ter notado é um tempo de latência ligeiramente mais alto nos pings.

De volta ao</span> [button label="SUSE Virtualization UI" variant="success"](tab-0) <span id="assignment.86" lang="pt" no>, a coluna <span id="assignment.79.1" lang="nolang" no>**Node**</span> para webserver-prod agora mostra um **nó diferente** daquele que você anotou.</span><span id="assignment.87" lang="pt" hist="vertrex-bank">O portal moveu-se fisicamente sem que os seus clientes alguma vez se apercebessem.</span>

<div id="404" class="story">
<span id="assignment.88" lang="pt" hist="vertrex-bank">Agora produzam as provas que a Sarah vai enviar aos reguladores — o contador de tempo de atividade do convidado nunca foi reiniciado, o que significa que o sistema operativo nunca deixou de funcionar:</span>
</div>

```bash,wrap,run
ssh -o StrictHostKeyChecking=accept-new  sles@[[ Instruqt-Var key="PAYMENT_GATEWAY_IP" hostname="kvm-host" ]] "hostname && uptime"
```

<span id="assignment.89" lang="pt" no>▶️ Tarefa 5: Retomar as operações normais
===================================


  


Regressar à</span> [button label="SUSE Virtualization UI" variant="success"](tab-0) <span id="assignment.90" lang="pt" no>Localize a máquina virtual que pausou anteriormente:</span>

<div class="cred">

```txt
daily-batch-processor
```

</div>

<span id="assignment.91" lang="pt" no>1. Clique no  na sua linha
2. Selecione <span id="assignment.91.1" lang="nolang" no>**Unpause**</span> para permitir que as tarefas não críticas sejam retomadas

🛠️ Tarefa 6: Entregar a rack danificada à equipa de reparação
====================================================</span>


<div id="405" class="story">
<span id="assignment.92" lang="pt" hist="vertrex-bank">O gateway está seguro — mas o nó danificado pela água ainda está a pingar, e algumas cargas de trabalho mais pequenas podem continuar a correr nele. Não vais migrá-las uma a uma enquanto se forma uma poça no chão. Deixa a plataforma tratar disso.</span>
</div>


<span id="assignment.93" lang="pt" no>Na</span> [button label="SUSE Virtualization UI" variant="success"](tab-0) <span id="assignment.94" lang="pt" no>, vá para <span id="assignment.94.1" lang="nolang" no>**Hosts**</span>:

1. Encontre o nó no qual o webserver-prod estava a correr **antes** da migração, aquele que anotou.</span>

<i id="406" class="story"><span id="assignment.95" lang="pt" hist="vertrex-bank">Essa é a máquina danificada pela água</span></i>

<span id="assignment.96" lang="pt" no>2. Clique no  na sua fila e selecione <span id="assignment.96.1" lang="nolang" no>**Enable Maintenance Mode**</span>, depois <span id="assignment.96.2" lang="nolang" no>confirm</span>

Agora observe a página **<span id="assignment.6.2" lang="nolang" no>Virtual Machines</span>**: toda VM que ainda vive no nó danificado faz live-migration para fora dele **automaticamente**. A plataforma escolhe nós de destino saudáveis, move as cargas de trabalho uma por uma e deixa o nó vazio. Sem planilhas, sem escolha manual de destino, sem VM esquecida.

> [!NOTE]
> Isso pode levar algum tempo neste ambiente de laboratório.

Assim que o nó mostrar <span id="assignment.96.3" lang="nolang" no>**Maintenance**</span> e sua contagem de VMs chegar a zero, a equipe de reparo (virtual) troca a válvula de refrigerante (virtual). Coloque o nó de volta em serviço:

3. Clique no  na sua fila novamente e selecione <span id="assignment.96.4" lang="nolang" no>**Uncordon**</span> e depois <span id="assignment.96.5" lang="nolang" no>**Disable Maintenance Mode**</span>

O nó se reconecta ao fabric, pronto para aceitar cargas de trabalho novamente.

> [!NOTE]
> A mesma inteligência funciona também na direção oposta: toda vez que uma nova VM é criada, o agendador a coloca no nó adequado com menor carga, mantendo o cluster naturalmente equilibrado, sem necessidade de Tetris manual. Entre a alocação automática na entrada e a evacuação automática na saída, os humanos decidem apenas *o que* deve rodar; a plataforma decide *onde*.</span>

<span id="assignment.97" lang="pt" no>🏋️ Exercícios Bônus: o rasto documental da migração (opcional, para os curiosos de linha de comando)
======================================================================================


  


Novo em <span id="assignment.2.2" lang="nolang" no>Kubernetes</span>? **Podes avançar sem problemas.** Caso contrário: cada migração é, em si, um objeto <span id="assignment.2.2" lang="nolang" no>Kubernetes</span>, o que significa que é auditável. No</span> [button label="Cluster Terminal" variant="success"](tab-1) <span id="assignment.98" lang="pt" no>- **Consulte o registro de migração** (quem foi movido, quando, de onde para onde):

```bash,wrap,run
kubectl --kubeconfig .rodeo/harvester-kubeconfig get virtualmachineinstancemigrations -A
```

- **Inspecione os detalhes da migração concluída:**

```bash,wrap,run
kubectl --kubeconfig .rodeo/harvester-kubeconfig describe virtualmachineinstancemigrations -A | grep -A 10 "Status"
```

- **Pense com antecedência:** o que acontece se um *nó* falhar sem aviso, antes que alguém possa migrar? Verifique a estratégia de execução de cada VM: <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> pode reagendar automaticamente as VMs de um host que falhou:

```bash,wrap,run
kubectl --kubeconfig .rodeo/harvester-kubeconfig get vm -A -o custom-columns=NAME:.metadata.name,RUNSTRATEGY:.spec.runStrategy
```

> [!NOTE]
> **Além da computação:** a mesma ideia de zero downtime também se aplica a *discos*. <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> suporta **live migration de armazenamento in-place** (mover os volumes de uma VM em execução entre backends de armazenamento, por exemplo de <span id="assignment.2.8" lang="nolang" no>Longhorn</span> para uma matriz <span id="assignment.2.9" lang="nolang" no>CSI</span> externa) sem parar a VM. Computação evacuada esta noite, armazenamento evacuado no próximo trimestre, e o gateway nunca percebe nenhum dos dois.</span>

<span id="assignment.99" lang="pt" no>💼 Por que isso importa?
==============================================

- **As falhas de hardware deixam de ser interrupções.** Vazamentos de refrigerante, atualizações de firmware, reinicializações de host: as cargas de trabalho simplesmente migram para nós saudáveis enquanto os seus serviços continuam a funcionar.
- **Manutenção planeada sem janelas à meia-noite.** Um clique em **Maintenance Mode** esvazia automaticamente um nó inteiro. As correções de rotina acontecem às 14h em vez de às 2h da manhã, e ninguém precisa de manter uma folha de cálculo com a localização de cada VM.
- **Um registo de auditoria que os reguladores conseguem ler.** Cada migração é um objeto de API registado, sem necessidade de reconstruir o que aconteceu a partir de capturas de ecrã da consola.

Clique em **Check** para continuar. 🕵️

📚 Mais informação
===================</span>

- [Live Migration](https://documentation.suse.com/cloudnative/virtualization/latest/en/virtual-machines/live-migration.html)
