---
slug: the-unthinkable-error-snapshots
id: nkrkc4vyyywt
type: challenge
title: '<span id="assignment.116" lang="pt" hist="vertrex-bank">⏪ Capítulo 6: O Erro Impensável</span>'
teaser: <span id="assignment.117" lang="pt" hist="vertrex-bank">Um cursor escorregado acabou de apagar um registro de acordo de 100 milhões. Volte no tempo com snapshots de VM, verifique a recuperação em um clone de staging seguro e, em seguida, torne a proteção permanente com backups agendados fora do cluster.</span>
tabs:
- id: lygpkmkmyndn
  title: SUSE Virtualization UI
  type: service
  hostname: kvm-host
  path: /
  port: 8443
  protocol: https
- id: gofsbdvdnoyj
  title: Cluster Terminal
  type: terminal
  hostname: kvm-host
- id: 4accqnqjfweo
  title: Rancher Prime UI
  type: service
  hostname: kvm-host
  port: 30002
  protocol: https
difficulty: intermediate
timelimit: 3600
enhanced_loading: null
---
<span id="assignment.118" lang="pt" hist="vertrex-bank">⏪ Capítulo 6: <span id="assignment.118.1" lang="pt" no>O Erro Impensável</span>
===================================</span>

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
    padding: 2px 8px;
    border-bottom: none;
    border-left: 1px solid rgba(255,255,255,.25);
    border-radius: 0;
    display: flex;
    align-items: center;
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
    max-height: 1.5vh;
    max-width: 1.5vh;
    margin: 0;
    padding: 0;
    display: inline-block;
  }

</style>

<img class="logos" alt="Welcome!" src="../assets/06-chapter-img.png"/>

<div id="601" class="story">

<span id="assignment.119" lang="pt" hist="vertrex-bank">Na manhã seguinte, o silêncio exausto do turno da noite é abruptamente quebrado por um palavrão abafado vindo da mesa do administrador júnior de banco de dados.

Você e Sarah vão até lá imediatamente. O administrador júnior está encarando a tela com horror absoluto, as mãos tremendo sobre o teclado. Enquanto tentava limpar arquivos temporários obsoletos no servidor primário de registro de transações, o cursor dele escorregou. Ele executou acidentalmente um comando de exclusão recursiva no diretório errado.

Um registro de liquidação de transação corporativa de cem milhões de dólares, finalizado apenas momentos antes, foi completamente apagado do disco.

*"Eu destruí,"* sussurra o administrador, trêmulo. *"A execução da fita de backup só acontece à meia-noite. Os dados simplesmente sumiram."*

Sarah fecha os olhos, esfregando as têmporas, se preparando para o impacto devastador que isso terá no preço das ações do banco e em sua reputação. Mas você coloca uma mão firme no ombro do administrador.

*"Os dados não sumiram,"* você diz calmamente. *"Nossa nova arquitetura de armazenamento depende de snapshots distribuídos em nível de bloco. Eu tirei uma captura do estado de referência pouco antes do início do turno da manhã."*

Você se aproxima do terminal dele. É hora de voltar no tempo. Mas é preciso ter cuidado: você quer **verificar os dados restaurados em um ambiente isolado seguro antes de sobrescrever a produção**.</span>

</div>

<span id="assignment.120" lang="pt" no>## 🎯 Objetivos da Sua Missão

1. Simular a criação e destruição do registo
2. Clonar um ambiente de staging a partir do snapshot
3. Verificar os dados no sandbox de staging
4. Restaurar o sistema de produção
5. Ligar o <span id="assignment.120.1" lang="nolang" hist="vertrex-bank">bank's off-cluster backup vault</span>
6. Agendar os backups



🔐 Credenciais de Login
====================

A UI do <span id="assignment.69.1" lang="nolang" no>**SUSE Virtualization**</span> e a UI do **Rancher Prime** usam as mesmas credenciais.</span>

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



<span id="assignment.121" lang="pt" no>💥 Tarefa 1: Simule a criação e destruição do registo
==============================================================


  


Vai reproduzir você mesmo os eventos desta manhã, para compreender exatamente o que o snapshot protege.

No</span> [button label="Cluster Terminal" variant="success"](tab-1) <span id="assignment.122" lang="pt" no>, inicie sessão na máquina virtual (pode demorar alguns minutos até a VM arrancar):

```bash,wrap,run
while [[ "${IPA}" ==  "" ]]; do IPA=`kubectl --kubeconfig .rodeo/harvester-kubeconfig get vmi core-services -n prod -o jsonpath='{.status.interfaces[0].ipAddress}'|grep -v ':'`; sleep 5; echo -n '.'; done ; while [[ "$?" != "0" ]] ; do ssh -T -o StrictHostKeyChecking=accept-new sles@${IPA} 2>/dev/null ; sleep 5; done ; ssh -o StrictHostKeyChecking=accept-new sles@${IPA}

```

Gere o registo de transação altamente sensível no disco escrevendo exatamente isto:

```bash,wrap,run
echo "CLIENT: BRUCE WAYNE | AMOUNT: 100,000,000 | STATUS: CLEARED" > /home/sles/ledger.txt
```

**Agora capture a linha de base.** Mude para o</span> [button label="SUSE Virtualization UI" variant="success"](tab-0) <span id="assignment.123" lang="pt" no>1. Navegue hasta <span id="assignment.40.2" lang="nolang" no>**Virtual Machines**</span> y, a continuación, localice la siguiente VM y haga clic en el botón situado junto a ella:</span>

<div class="cred">

```txt
core-services
```

</div>
<span id="assignment.124" lang="pt" no>2. Clique em <span id="assignment.124.1" lang="nolang" no>**Take Virtual Machine Snapshot**</span>
3. Nomeie-o:</span>

<div class="cred">

```txt
pre-disaster-backup
```

</div>

<span id="assignment.125" lang="pt" no>4. Clique em <span id="assignment.19.3" lang="nolang" no>**Create**</span>

5. Navegue até <span id="assignment.125.1" lang="nolang" no>**Backup and Snapshots**</span>, depois clique em <span id="assignment.125.2" lang="nolang" no>**Virtual Machine Snapshots**</span> e aguarde até que o que acabámos de criar tenha o estado <span id="assignment.125.3" lang="nolang" no>**Ready**</span>: o ponto de rollback está definido</span> [button label="Cluster Terminal" variant="success"](tab-1) <span id="assignment.126" lang="pt" no>e simule o erro terrível do administrador júnior:

```bash,run
rm -f /home/sles/ledger.txt
```

Cem milhões de dólares, perdidos do disco. Saia do console da VM:

```bash,run
exit
```


🧪 Tarefa 2: Clonar um ambiente de staging a partir do snapshot
================================================================


  


Em vez de restaurar imediatamente a produção, você criará um **clone** para verificar os dados primeiro; a recuperação não destrutiva é sempre recomendada.

No</span> [button label="SUSE Virtualization UI" variant="success"](tab-0) <span id="assignment.127" lang="pt" no>1. Navegue até <span id="assignment.125.1" lang="nolang" no>**Backup and Snapshots**</span> e, em seguida, clique em <span id="assignment.125.2" lang="nolang" no>**Virtual Machine Snapshots**</span>

2. Clique no snapshot <span id="assignment.127.1" lang="nolang" no>**pre-disaster-backup**</span>:

3. Clique no ícone ao lado dele e selecione <span id="assignment.127.2" lang="nolang" no>**Restore New**</span>

4. Nomeie a nova máquina virtual:</span>


<div class="cred">

```txt
core-services-staging-verify
```

</div>


<span id="assignment.128" lang="pt" no>5. Clique <span id="assignment.19.3" lang="nolang" no>**Create**</span>

> [!Note]
> Devido ao hardware usado neste laboratório, este processo demorará mais do que em condições normais, por favor continue para a próxima tarefa.



🏦 Tarefa 3: Conectar o cofre de backup fora do cluster
======================================================


  


Os snapshots nos salvaram esta manhã, mas os snapshots residem no **mesmo cluster** que a carga de trabalho. Eles protegem contra erros de dedo, mas não contra danos físicos ou ataques cibernéticos. Para uma verdadeira recuperação de desastres, operamos um **cofre de backup** fora do cluster: um compartilhamento NFS num sistema de armazenamento separado. Hora de conectá-lo.

Em</span> [button label="SUSE Virtualization UI" variant="success"](tab-0) <span id="assignment.129" lang="pt" no>1. Vá até <span id="assignment.129.1" lang="nolang" no>**Advanced > Settings**</span> e localize:</span>

<div class="cred">

```txt
backup-target
```

</div>
<span id="assignment.130" lang="pt" no>2. Clique no  na sua linha e selecione <span id="assignment.130.1" lang="nolang" no>**Edit Setting**</span>, adicione o seguinte:

- <span id="assignment.110.2" lang="nolang" no>**Type**</span>: <span id="assignment.130.2" lang="nolang" no><b class="highlightcopy">NFS</b></span>
- <span id="assignment.130.3" lang="nolang" no>**Endpoint**</span>:</span>

<div class="cred">

```txt
192.168.122.1:/srv/backups/
```

</div>

<span id="assignment.131" lang="pt" no>3. Clique em <span id="assignment.114.7" lang="nolang" no>**Save**</span>

O cluster já consegue enviar backups completos de VMs para fora do cluster, o equivalente moderno da gravação em fita à meia-noite, menos a meia-noite. Um bucket **S3** funciona igualmente bem como endpoint; numa implementação em produção, este apontaria para uma instalação fisicamente separada.


⏰ Tarefa 4: Agendar backups
====================================</span>

<div id="602" class="story">
<span id="assignment.132" lang="pt" hist="vertrex-bank">Snapshots pontuais podem salvar o dia uma vez; a política mantém o banco seguro todos os dias depois.</span>
</div>

<span id="assignment.133" lang="pt" no>Coloca o próprio core-services sob um cronograma de backup automático para que ninguém tenha de se lembrar de o fazer manualmente novamente.</span> [button label="SUSE Virtualization UI" variant="success"](tab-0) <span id="assignment.134" lang="pt" no>1. Vá até <span id="assignment.134.1" lang="nolang" no>**Backup & Snapshot > Virtual Machine Schedules**</span> e clique em <span id="assignment.134.2" lang="nolang" no>**Create schedule**</span>
2. Defina os seguintes detalhes:

  - <span id="assignment.39.3" lang="nolang" no>**Namespace**</span>: <span id="assignment.55.2" lang="nolang" no><b class="highlightcopy">prod</b></span>
  - <span id="assignment.134.3" lang="nolang" no>**Virtual Machine Name**</span>: <span id="assignment.134.4" lang="nolang" no><b class="highlightcopy">core-services</b></span>
  - <span id="assignment.134.5" lang="nolang" no>**Basics**</span>:
    - <span id="assignment.134.6" lang="nolang" no>**Retain:**</span> 5
    - <span id="assignment.134.7" lang="nolang" no>**Max Failure:**</span> 2
    - <span id="assignment.134.8" lang="nolang" no>**Cron Schedule:**</span> (no minuto 00, a cada 5 horas)</span>

<div class="cred">

```txt
0 */5 * * *
```

</div>


<span id="assignment.135" lang="pt" no>4. Clique em <span id="assignment.19.3" lang="nolang" no>**Create**</span>

A partir de agora, a plataforma faz backup da VM no cofre NFS a cada cinco horas, mantém as cinco cópias mais recentes e pausa a programação se duas execuções consecutivas falharem. Configure uma vez, proteja para sempre.



🔍 Tarefa 5: Verificar os dados na sandbox de staging
=================================================


  


Agora que o core-services-staging-verify está em funcionamento, vamos verificar se o arquivo está lá.

Desta vez usaremos o console gráfico, já que a VM não tem rede.

No</span> [button label="SUSE Virtualization UI" variant="success"](tab-0) <span id="assignment.136" lang="pt" no>1. Vá até <span id="assignment.40.2" lang="nolang" no>**Virtual Machines**</span>
2. Clique no menu suspenso <span id="assignment.61.1" lang="nolang" no>**Console**</span> e selecione <span id="assignment.136.1" lang="nolang" no>**Open in WebVNC**</span>, uma nova janela aparecerá com o terminal, sinta-se à vontade para redimensioná-la.
3. Faça login usando as seguintes credenciais:
   - <span id="assignment.136.2" lang="nolang" no>**username**</span>: 'sles'
   - <span id="assignment.136.3" lang="nolang" no>**password**</span>: '1234'

4. Uma vez dentro, execute o seguinte comando:</span>


<div class="cred">

```txt
cat /home/sles/ledger.txt
```

</div>

<span id="assignment.137" lang="pt" no>5. Deverá devolver:

**CLIENTE: BRUCE WAYNE | VALOR: 100.000.000 | ESTADO: LIMPO**


O texto imprime na perfeição. <span id="assignment.137.1" lang="pt" hist="vertrex-bank">Os dados estão seguros.</span>


Agora vamos eliminar o clone que já não precisamos.

1. Feche a janela com a consola.
2. Clique no  na linha **core-services-staging-verify** e selecione <span id="assignment.137.2" lang="nolang" no>**Delete**</span>, e novamente <span id="assignment.137.2" lang="nolang" no>**Delete**</span>.



♻️ Tarefa 6: Restaurar o sistema de produção
=========================================


  


Agora que verificou a integridade do snapshot, prossiga para restaurar o sistema de produção:

1. Vá a **<span id="assignment.6.2" lang="nolang" no>Virtual Machines</span>**
2. Clique no  na linha **core-services** e selecione <span id="assignment.137.3" lang="nolang" no>**Stop**</span>, e novamente <span id="assignment.74.2" lang="nolang" no>**Apply**</span>.
3. Assim que estiver completamente parado, navegue até <span id="assignment.125.1" lang="nolang" no>**Backup and Snapshots**</span>, depois clique em <span id="assignment.125.2" lang="nolang" no>**Virtual Machine Snapshots**</span>

4. Clique no snapshot **pre-disaster-backup**:

5. Clique no  ao lado e selecione <span id="assignment.137.4" lang="nolang" no>**Replace Existing**</span>

6. Clique em <span id="assignment.19.3" lang="nolang" no>**Create**</span>

A VM vai ligar-se automaticamente porque é isso que a estratégia de execução define.

Opcionalmente, faça SSH novamente e execute `cat` ao ficheiro uma última vez, depois termine a sessão na VM. <span id="assignment.137.5" lang="pt" hist="vertrex-bank">O disco está de volta onde pertence.</span>


🏋️ Desafios Bónus: veja a maquinaria por trás da rede de segurança (opcional)
======================================================================

- **Para os curiosos da linha de comandos:** cada snapshot de VM é construído a partir de snapshots ao nível do volume, e cada um deles é um objeto de API, tal como o seu novo agendamento de backup:

```bash,wrap,run
kubectl --kubeconfig .rodeo/harvester-kubeconfig get VirtualMachineBackup -A; kubectl --kubeconfig .rodeo/harvester-kubeconfig get volumesnapshots -A; kubectl --kubeconfig .rodeo/harvester-kubeconfig get schedulevmbackups -A
```

> [!NOTE]
> Certifique-se de que termina a sessão na VM antes de executar estes comandos.


💼 Porque é que isto importa?
==============================================

- **O erro humano deixa de ser catastrófico.** A recuperação passou de "esperar pelas cassetes da meia-noite e rezar" para um rollback de autosserviço de cinco minutos.
- **Verifique antes de sobrescrever.** Restaurar para um clone significa que nunca arrisca a produção com um backup não verificado, um padrão com o qual tanto os seus auditores como os seus administradores juniores dormirão melhor.
- **A proteção é agora política, não heroísmo.** Um cofre de backup NFS fora do cluster e um agendamento de backup a cada cinco horas significam que a rede de segurança se mantém sozinha a partir daqui.

Clique em <span id="assignment.32.1" lang="nolang" no>**Check**</span> para continuar. 🤠

📚 Mais informação
===================</span>

- [Virtual Machine Backup and Restore](https://documentation.suse.com/cloudnative/virtualization/latest/en/virtual-machines/backup-restore.html)
