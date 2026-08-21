---
slug: the-subterranean-divide-cluster-prep
id: tmmoesxdhg4b
type: challenge
title: "<span id="assignment.12" lang="pt" hist="vertrex-bank">Capítulo 2: A Divisão Subterrânea</span>"
teaser: <span lang="pt" hist="vertrex-bank" id="ts2">Dois silos de hardware, duas equipas que mal falam entre si. Desce ao datacenter, mapeia a topologia dos nós e dá a cada disco na fabric um preço que o banco consiga aceitar.</span>
tabs:
- id: gix6w5fqkxd6
  title: SUSE Virtualization UI
  type: service
  hostname: kvm-host
  path: /
  port: 8443
  protocol: https
- id: duhbmh2ml3qo
  title: Cluster Terminal
  type: terminal
  hostname: kvm-host
- id: zgpgmllqoznu
  title: Rancher Prime UI
  type: service
  hostname: kvm-host
  port: 30002
  protocol: https
difficulty: basic
timelimit: 2400
enhanced_loading: null
---
<span lang="pt" hist="vertrex-bank" id="ts2">Dois silos de hardware, duas equipas que mal falam entre si. Desce ao datacenter, mapeia a topologia dos nós e dá a cada disco na fabric um preço que o banco consiga aceitar.</span>

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
  .cred-sparkle {
    animation: cred-sparkle 0.8s ease-out;
  }
  @keyframes cred-sparkle {
    0%   { text-shadow: 0 0 2px #fff, 0 0 10px #30ba78, 0 0 20px #ffd700; }
    100% { text-shadow: none; }
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
<script>
document.querySelectorAll('.cred .my-3 > div:first-child button').forEach(function(btn){
  if (btn.dataset.sparkleBound) return;
  btn.dataset.sparkleBound = '1';
  btn.addEventListener('click', function(){
    var pre = btn.closest('.my-3').querySelector('pre');
    if (!pre) return;
    pre.classList.remove('cred-sparkle');
    void pre.offsetWidth;
    pre.classList.add('cred-sparkle');
    setTimeout(function(){ pre.classList.remove('cred-sparkle'); }, 800);
  });
});
</script>
<img class="logos" alt="Welcome!" src="../assets/02-chapter-img.png"/>

<div id="201" class="story">

<span id="assignment.13" lang="pt" hist="vertrex-bank">Sarah lidera-te para fora dos silenciosos gabinetes executivos, entra num elevador seguro e desce até ao datacenter subterrâneo do banco. A temperatura ambiente desce abruptamente enquanto as pesadas portas biométricas de aço se trancam atrás de ti. A sala vibra com o rugido ensurdecedor e implacável dos sistemas de refrigeração industrial.

Ela aponta para o lado esquerdo da sala, onde filas de chassis de servidor elegantes e densamente compactados piscam com luzes azuis rápidas. *"Esses correm as nossas APIs de banca móvel,"* grita ela por cima do ruído das ventoinhas. *"Puros microsserviços. Totalmente containerizados e ágeis."*

Depois aponta para o lado direito da sala, dominado por armários de servidor colossais e arcaicos que irradiam um calor desconfortável. *"E esses são as máquinas virtuais monolíticas legadas que guardam os livros-razão de transações principais. Dois mundos completamente diferentes. Dois silos de hardware diferentes. Duas equipas de engenharia diferentes que mal falam entre si."*

Caminhas entre as duas filas, sentindo a diferença de temperatura nítida. *"Essa divisão acaba hoje,"* dizes-lhe.</span>

</div>

<span id="assignment.14" lang="pt" no>Um único tecido para dois mundos

Você explica a arquitetura elegante de <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span>: ao usar tecnologias open-source avançadas sobre uma **fundação <span id="assignment.2.2" lang="nolang" no>Kubernetes</span>**, a plataforma não apenas *tolera* máquinas virtuais: ela as trata como **cidadãs nativas do ecossistema de contêineres**. As máquinas virtuais pesadas rodarão lado a lado com os contêineres ágeis, geridas pelo mesmo mecanismo de orquestração:

| Mundo da virtualização | Mundo <span id="assignment.14.1" lang="nolang" no>Container</span> | Unificado em <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> |
|---------------------|----------------|-------------------------------|
| Hosts hipervisores | Nós <span id="assignment.2.2" lang="nolang" no>Kubernetes</span> | **Um único conjunto de nós executa ambos** |
| Console de gestão do hipervisor | Ferramentas de contêiner | **Uma única plataforma por baixo**. <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> executa as VMs, o Rancher Prime comanda os clusters e os contêineres |
| Arrays de armazenamento SAN | Volumes <span id="assignment.2.9" lang="nolang" no>CSI</span> | **<span id="assignment.2.8" lang="nolang" no>Longhorn</span> serve VMs e pods igualmente** |

Essa última linha é onde você começa. Cada disco de VM, cada volume persistente de contêiner, tudo isso corre sobre o mesmo tecido de armazenamento distribuído, e nem toda carga de trabalho merece o mesmo preço.

🎯 Objetivos da Sua Missão

1. Inspecionar a topologia física dos nós
2. Preparar um espaço de trabalho dedicado
3. Compreender como o <span id="assignment.2.8" lang="nolang" no>Longhorn</span> replica os seus dados
4. Construir uma classe de armazenamento em nível de custo para a equipa de desenvolvimento

🔐 Credenciais de Login
====================

A interface do **<span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span>** e a interface do <span id="assignment.2.12" lang="nolang" no>**Rancher Prime**</span> usam as mesmas credenciais.</span>

<span id="assignment.10" lang="nolang" no>Username</span>:

<div class="cred">

```txt
admin
```

</div>

<span id="assignment.11" lang="nolang" no>Password</span>:

<div class="cred">

```txt
[[ Instruqt-Var key="RANCHER_PASSWORD" hostname="kvm-host" ]]
```

</div>


<span id="assignment.15" lang="pt" no>☁️ O que é <span id="assignment.2.8" lang="nolang" no>Longhorn</span>?
====================

<span id="assignment.2.8" lang="nolang" no>Longhorn</span> é o sistema de armazenamento distribuído integrado no <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> que pode ser utilizado. Ele agrupa os discos brutos presentes em cada nó e transforma-os numa única infraestrutura de armazenamento partilhada.

Por predefinição, cada volume que cria é replicado por vários nós, para que uma falha de disco ou o reinício de um nó nunca resulte em perda de dados. Sem SAN, sem equipa de armazenamento separada, um único sistema tanto para VMs como para contentores.

Está pronto a ser utilizado, mas se preferir usar outro <span id="assignment.2.9" lang="nolang" no>CSI</span> é livre de o fazer, sem dependência de fornecedor.


🖥️ Tarefa 1: Inspecionar a topologia física dos nós
=============================================



  



Vá até</span> [button label="SUSE Virtualization UI" variant="success"](tab-0) <span id="assignment.16" lang="pt" no>, navegue até o menu do lado esquerdo e clique em **<span id="assignment.6.1" lang="nolang" no>Hosts</span>**.

1. Clique no nome de **um dos hosts** na lista
2. Navegue pela interface e verifique as diferentes opções para entender melhor como as coisas funcionam. Observe como os dispositivos de bloco brutos são provisionados para os discos das máquinas virtuais. Cada disco que você vê aqui passa a fazer parte do pool de armazenamento distribuído <span id="assignment.2.8" lang="nolang" no>Longhorn</span> <span id="assignment.16.1" lang="pt" hist="vertrex-bank">que guardará os livros-razão do banco</span>.</span>


<div id="203" class="story">
<span id="assignment.17" lang="pt" hist="vertrex-bank">Bancos crescem, e este tecido também. Ficar com pouco espaço já não é uma atualização complexa. Instale um novo nó em rack, adicione os seus discos brutos ao pool, e o <span id="assignment.2.8" lang="nolang" no>Longhorn</span> reequilibra as réplicas automaticamente em todo o tecido expandido, sem tempo de inatividade, sem fins de semana de migração de dados. A capacidade de armazenamento escala da mesma forma que a computação: de forma incremental, conforme a procura.</span>
</div>


<span id="assignment.18" lang="pt" no>🏗️ Tarefa 2: Preparar um espaço de trabalho dedicado
========================================



  


A plataforma isola cargas de trabalho em **namespaces**, espaços de trabalho separados e governáveis no mesmo cluster.

No</span> [button label="SUSE Virtualization UI" variant="success"](tab-0) <span id="assignment.19" lang="pt" no>, selecione <span id="assignment.19.1" lang="nolang" no>**Namespaces**</span> no menu à esquerda. Vai reparar que o prod já está presente na lista. <span id="assignment.19.2" lang="pt" hist="vertrex-bank">A equipe de plataforma o provisionou antes de você chegar, e é lá que as cargas de trabalho de produção do banco vão residir.</span>

Agora crie o seu equivalente para desenvolvimento:

1. Clique em <span id="assignment.19.3" lang="nolang" no>**Create**</span>
2. Defina o <span id="assignment.19.4" lang="nolang" no>**Name**</span> para:</span>

<div class="cred">

```txt
dev
```

</div>

<span id="assignment.20" lang="pt" no>3. Defina o <span id="assignment.20.1" lang="nolang" no>**Description**</span> para:</span>

<div class="cred">

```txt
VMs from dev
```

</div>


<span id="assignment.21" lang="pt" no>4. Clique <span id="assignment.19.3" lang="nolang" no>**Create**</span>

O espaço de trabalho dos desenvolvedores está agora pronto, no futuro podemos atribuir-lhe quotas, políticas e controlos de acesso.

💾 Tarefa 3: Entenda como o <span id="assignment.2.8" lang="nolang" no>Longhorn</span> replica os seus dados
========================================================

Vamos ver *como* o backend de armazenamento se mantém saudável. Cada disco que o <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> atribui a uma VM ou a um pod é um **volume <span id="assignment.2.8" lang="nolang" no>Longhorn</span>**, e cada volume <span id="assignment.2.8" lang="nolang" no>Longhorn</span> é criado a partir de uma <span id="assignment.21.1" lang="nolang" no>**StorageClass**</span>: uma política que decide, entre outras coisas, quantas cópias dos seus dados existem em cada momento.

No</span> [button label="SUSE Virtualization UI" variant="success"](tab-0) <span id="assignment.22" lang="pt" no>, vá para <span id="assignment.22.1" lang="nolang" no>**Advanced > Storage Classes**</span> e clique em harvester-longhorn.

Repare no campo <span id="assignment.22.2" lang="nolang" no>**Number Of Replicas**</span>: está definido como **3**. Cada volume criado a partir desta classe recebe três cópias completas, distribuídas por três nós diferentes.</span>

<div id="204" class="story">
<span id="assignment.23" lang="pt" hist="vertrex-bank">É exatamente isso para os livros-razão de transações — perde-se um nó, ou até um disco a meio de uma escrita, e os dados sobrevivem intactos.</span>
</div>

<span id="assignment.24" lang="pt" no>Vamos abrir o capô e ver como <span id="assignment.2.8" lang="nolang" no>Longhorn</span> armazena os dados:

1. Vá para o</span> [button label="Cluster Terminal" variant="success"](tab-1) <span id="assignment.25" lang="pt" no>e SSH para uma das hosts <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span>:
```bash,run
rodeo ssh harvester1
```
2. Verifique a pasta <span id="assignment.2.8" lang="nolang" no>Longhorn</span> no nó <span id="assignment.25.1" lang="nolang" no>harvester1</span>: verá algumas pastas e ficheiros:
```bash,run
ls /var/lib/harvester/defaultdisk
```
3. Dentro da pasta replicas, encontre uma pasta por cada réplica de volume que este nó contém:
```bash,wrap,run
ls /var/lib/harvester/defaultdisk/replicas/
```
4. Saia do host digitando exit:
```bash,run
exit
```

> [!NOTE]
> Três réplicas significam três vezes o espaço em disco ocupado. Essa é a troca correta para dinheiro de produção. É um desperdício para uma VM de teste descartável de um developer que será eliminada até sexta-feira. O número de réplicas é uma **política**, não uma lei da física, e as políticas podem ser ajustadas por carga de trabalho.

🧅 Tarefa 4: Construir uma storage class de custo reduzido para a equipa de desenvolvimento
=====================================================================



  



A equipa de desenvolvimento não precisa de replicação de nível produção para os seus sandboxes, precisa de iteração barata e rápida. <span id="assignment.25.2" lang="pt" hist="vertrex-bank">Você terá seu próprio nível de armazenamento, precificado pelo que ele realmente é: descartável.</span>

No</span> [button label="SUSE Virtualization UI" variant="success"](tab-0) <span id="assignment.26" lang="pt" no>, em <span id="assignment.22.1" lang="nolang" no>**Advanced > Storage Classes**</span>:

1. Clique em <span id="assignment.19.3" lang="nolang" no>**Create**</span>
2. Defina <span id="assignment.19.4" lang="nolang" no>**Name**</span> como:</span>

<div class="cred">

```txt
harvester-longhorn-1rep
```

</div>


3. Set <span id="assignment.22.2" lang="nolang" no>**Number Of Replicas**</span> to:


<div class="cred">

```txt
1
```

</div>

4. Set <span id="assignment.27" lang="nolang" no>**Node Selector**</span> to: <span id="assignment.28" lang="nolang" no>**dev**</span> so that it is only scheduled on dev nodes.


5. Click <span id="assignment.19.3" lang="nolang" no>**Create**</span>

Two StorageClasses sit side by side in the list: `harvester-longhorn` (3 replicas, production) and <b class="highlightcopy">harvester-longhorn-1rep</b> (1 replica for dev sandboxes, at a third of the disk cost). <span id="assignment.29" lang="pt" hist="vertrex-bank">A equipa de desenvolvimento vai recorrer a este nível sempre que criarem uma VM descartável nos capítulos seguintes.</span>

> [!NOTE]
> One replica means **zero redundancy**, lose that single node and the volume is gone. That is an acceptable risk for a sandbox nobody depends on overnight, and a very deliberate trade-off you are making on the record, not an accident. Storage classes can also encode disk tags to steer workloads to specific hardware, production on fast NVMe, development on cheaper spindles.

🏋️ Bonus Drills: for the command-line curious (optional)
==========================================================

<div style='align: middle; margin: 15px;'>
  <img class="animatedgif" src="../assets/chapter2_video5.gif"/>
</div>


New to <span id="assignment.2.2" lang="nolang" no>Kubernetes</span>? **Skip ahead freely.** If you are curious, everything you just did in the UI is also visible through the <span id="assignment.2.2" lang="nolang" no>Kubernetes</span> API, open the </span> [button label="Cluster Terminal" variant="success"](tab-1) <span id="assignment.30" lang="pt" no>**See your UI storage classes as API objects**: the workspace and both storage tiers:

```bash,wrap,run
kubectl --kubeconfig .rodeo/harvester-kubeconfig get namespace dev -o wide; kubectl --kubeconfig .rodeo/harvester-kubeconfig get storageclasses;
```

**Label the new workspace** so future automation can target it easily:

```bash,wrap,run
kubectl --kubeconfig .rodeo/harvester-kubeconfig label namespace dev stage=dev
```

💼 ¿Por qué es esto importante?
==============================================

- **Los silos desaparecen.** Las VM y los contenedores comparten nodos, almacenamiento y un único equipo de operaciones. La "división de temperatura" del centro de datos ha desaparecido.
- **Sin abismo de reciclaje.** Las habilidades <span id="assignment.2.2" lang="nolang" no>Kubernetes</span> del equipo de contenedores ahora también gestionan el parque de VM; el equipo de VM obtiene una interfaz gráfica familiar basada en la API de <span id="assignment.2.2" lang="nolang" no>Kubernetes</span>.
- **Los namespaces aportan gobernanza.** Las cargas de trabajo financieras residen en `prod` con sus propias cuotas, políticas y controles de acceso. A los auditores les encantará.
- **El almacenamiento ahora tiene una lista de precios.** La replicación es un dial, no un valor predeterminado. Los datos de producción obtienen tres copias porque deben tenerlas; los entornos de prueba desechables obtienen una porque no deberían costar más de lo necesario.</span>

<div id="202" class="story">

<span id="assignment.31" lang="pt" hist="vertrex-bank">Sarah observa por cima do seu ombro enquanto o novo espaço de trabalho e os dois níveis de armazenamento aparecem no painel, um após o outro. Um leve sorriso surge em seu rosto. *"A base está sólida. Vamos ao trabalho."*</span>

</div>

<span id="assignment.32" lang="pt" no>Clique <span id="assignment.32.1" lang="nolang" no>**Check**</span> para continuar. ⚡


📚 Mais informações
===================</span>

- [<span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span>: Overview](https://documentation.suse.com/cloudnative/virtualization/latest/en/introduction/overview.html)
- [Storage: Overview](https://documentation.suse.com/cloudnative/virtualization/latest/en/storage/overview.html)
