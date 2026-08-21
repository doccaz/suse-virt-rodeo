---
slug: a-new-horizon-whats-next
id: qzmycpm7jtwa
type: challenge
title: "<span id="assignment.158" lang="pt" no>🌅 Capítulo 8: Um Novo Horizonte</span>"
teaser: <span id="assignment.159" lang="pt" hist="vertrex-bank">O banco funciona inteiramente em <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span>.
  Faça uma volta da vitória, reveja tudo o que você dominou e trace até onde suas novas habilidades podem levar o seu próprio datacenter.</span>
tabs:
- id: jw4tji5y1jbv
  title: SUSE Virtualization UI
  type: service
  hostname: kvm-host
  path: /
  port: 8443
  protocol: https
- id: gjstzqppnxay
  title: Cluster Terminal
  type: terminal
  hostname: kvm-host
- id: ohjx4w0pk1mb
  title: Rancher Prime UI
  type: service
  hostname: kvm-host
  port: 30002
  protocol: https
difficulty: basic
timelimit: 1800
enhanced_loading: null
---
<span id="assignment.160" lang="pt" no>🌅 Capítulo 8: Um Novo Horizonte
============================</span>
<style type="text/css">
  * {
    font-family: suse;
    src: url('https://fonts.google.com/specimen/SUSE');
  }
  .suse { color: #30ba78; }
  .virt { color: #30ba78; }
  .bank { color: #d4af37; }
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


</style>

<img class="logos" alt="Welcome!" src="../assets/chapter-img-a_new_horizon.png"/>

<div id="901" class="story">

<span id="assignment.161" lang="pt" hist="vertrex-bank">A poeira finalmente assentou. O datacenter está silencioso, banhado no suave brilho verde dos nós <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> operando em perfeita harmonia.

O Vertex Trust Bank não está mais preso ao passado. Agora funciona inteiramente numa stack de virtualização enxuta, de alto desempenho e nativa da nuvem.

Sarah está ao seu lado, olhando para o painel unificado na tela principal. *"Eu não achava que fosse possível,"* ela admite, balançando a cabeça em descrença. *"Estamos executando microsserviços em contêineres e livros-razão monolíticos exatamente na mesma malha. Nosso armazenamento é distribuído, nossas redes são definidas por software, e nossos custos de licenciamento simplesmente despencaram."*

Ela se vira para você e estende a mão. *"Obrigada. Você não apenas salvou nossa infraestrutura — você salvou o banco."*</span>

</div>

<span id="assignment.162" lang="pt" no>## 🏆 Suas Ações Heroicas

Você superou desafios incríveis durante sua estadia aqui:

| Capítulo | Crise | Habilidade que você dominou |
|:--------|:-------|:-------------------|
| 🏦 A Chegada | Um datacenter legado à beira do colapso | Inspecionando o painel da plataforma, <span id="assignment.2.8" lang="nolang" no>Longhorn</span> armazenamento e Rancher Prime |
| 🛗 A Divisão Subterrânea | Dois silos de hardware em guerra | Unindo VMs e contêineres em uma única <span id="assignment.2.2" lang="nolang" no>Kubernetes</span> |
| ⚡ O Flash Crash | Um colapso de mercado | Implantando VMs em minutos com imagens, volumes e cloud-init |
| 🌊 A Maré Crescente | Um rack de servidores inundado | Migração ao vivo sem downtime e evacuação de nós com um clique |
| 🕵️ O Intruso Invisível | Um caminho de ataque lateral | VLANs definidas por software e sub-redes SDN isoladas |
| ⏪ O Erro Inimaginável | Um registro de $100 milhões apagado | Snapshots, clones de staging, camadas de armazenamento e backups agendados fora do cluster |
| 🤠 A Debandada | Uma fome de computação | Templates de VM padrão, criando frotas idênticas sob demanda |</span>


<div id="902" class="story">

<span id="assignment.163" lang="pt" hist="vertrex-bank">Seu trabalho no Vertex Trust Bank está concluído — mas a fronteira digital é vasta e está em constante evolução. Há sempre novas arquiteturas para projetar e novos sistemas para modernizar.</span>

</div>


<span id="assignment.164" lang="pt" no>🔐 Credenciales de inicio de sesión
====================

Las UI de <span id="assignment.69.1" lang="nolang" no>**SUSE Virtualization**</span> y de **Rancher Prime** utilizan las mismas credenciales.</span>

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



<span id="assignment.165" lang="pt" no>🧭 Volta de vitória: o laboratório ainda é seu
=======================================

O ambiente do laboratório permanecerá ativo até que o seu temporizador expire. Sinta-se à vontade para explorar o painel e experimentar a infraestrutura que você construiu. Algumas ideias:

- **Faça um inventário final do império que você construiu.** Percorra o</span>[button label="SUSE Virtualization UI" variant="success"](tab-0)<span id="assignment.166" lang="pt" no>a página <span id="assignment.40.2" lang="nolang" no>**Virtual Machines**</span>, as **Redes** que definiste, o modelo de **Templates**, e o histórico de **Backup & Snapshot**: cada crise da semana deixou aqui a sua marca.

- **Cria a tua própria crise.** Cria uma nova VM do zero: escolhe a imagem, define o tamanho, configura o cloud-init, tira um snapshot, faz live-migrate. Desta vez sem instruções. Já sabes o caminho.

- **Para os curiosos de linha de comandos (opcional):** a API é toda tua:

```bash,run
kubectl --kubeconfig .rodeo/harvester-kubeconfig get vm -A && kubectl  --kubeconfig .rodeo/harvester-kubeconfig get network-attachment-definitions -A && kubectl --kubeconfig .rodeo/harvester-kubeconfig get VirtualMachineBackup -A
```</span>


<span id="assignment.167" lang="pt" no>🚀 Que próximos passos te esperam?
===============================

- 📖 Mantém as tuas competências afiadas aprofundando a arquitetura técnica na [Documentação do SUSE Virtualization](https://documentation.suse.com/cloudnative/virtualization/latest/en/introduction/overview.html).

- 🐮 Aprende a gerir **frotas destes clusters em grande escala** (um único Rancher Prime a gerir todos os clusters <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> em todos os datacenters de filial) com o [<span id="assignment.2.15" lang="nolang" no>SUSE Rancher Prime</span>](https://documentation.suse.com/cloudnative/rancher-manager/latest/en/rancher-manager.html).

- 🧪 Reconstrói isto em casa: o <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> é open source. Obtém a ISO, instala-o em qualquer máquina x86 disponível e executa as tuas próprias VMs.

- 🤝 Nunca estás sozinho neste percurso: os clientes da SUSE avaliam consistentemente o <span id="assignment.167.1" lang="nolang" no>**SUSE Support**</span> entre os melhores da indústria, e o feedback dos clientes molda diretamente a evolução dos produtos. Trabalhar com a SUSE significa ter um lugar à mesa, não um bilhete numa fila. Essa é a diferença do open source.

- 💬 Fala com o teu representante SUSE sobre como esta história se aplicaria ao **teu** cluster legado no canto mais escuro da sala.</span>

<div id="903" class="story">

<span id="assignment.168" lang="pt" hist="vertrex-bank">Foi uma honra absoluta trabalhar ao seu lado!

**Boa migração!** 🎉</span>

</div>

<span id="assignment.169" lang="pt" no>📚 Mais informação
===================

- [<span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span>: Visão geral](https://documentation.suse.com/cloudnative/virtualization/latest/en/introduction/overview.html)
- [Criar <span id="assignment.6.2" lang="nolang" no>Virtual Machines</span>](https://documentation.suse.com/cloudnative/virtualization/latest/en/virtual-machines/create-vm.html)
- [Migração ao Vivo](https://documentation.suse.com/cloudnative/virtualization/latest/en/virtual-machines/live-migration.html)
- [Cópia de Segurança e Restauro](https://documentation.suse.com/cloudnative/virtualization/latest/en/virtual-machines/backup-restore.html)
- [Rede de Cluster](https://documentation.suse.com/cloudnative/virtualization/latest/en/networking/cluster-network.html)</span>
