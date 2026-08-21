---
slug: the-stampede-automation
id: euwnv5ojhvfl
type: challenge
title: "<span id="assignment.138" lang="pt" no>🤠 Capítulo 7: A Debandada</span>"
teaser: <span id="assignment.139" lang="pt" hist="vertrex-bank">Os mercados estão em queda livre e os quants precisam que a frota de cálculo seja escalada de três nós para cinco, agora. Forje um template de VM padrão e produza máquinas idênticas sob demanda.</span>
tabs:
- id: xxc2ymjtxzih
  title: SUSE Virtualization UI
  type: service
  hostname: kvm-host
  path: /
  port: 8443
  protocol: https
- id: uclhjzflraeo
  title: Cluster Terminal
  type: terminal
  hostname: kvm-host
- id: inaridrpaxka
  title: Rancher Prime UI
  type: service
  hostname: kvm-host
  port: 30002
  protocol: https
difficulty: intermediate
timelimit: 3000
enhanced_loading: null
---
<span id="assignment.140" lang="pt" no>🤠 Capítulo 7: A Debandada
===========================</span>
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

<img class="logos" alt="Welcome!" src="../assets/07-chapter-img.png"/>

<div id="701" class="story">

<span id="assignment.141" lang="pt" hist="vertrex-bank">Uma mudança repentina e agressiva nas taxas de juros globais lança os mercados financeiros num frenesim caótico. Os algoritmos de análise de risco do Vertex Trust Bank gritam por mais capacidade de computação para processar a torrente de dados voláteis do mercado.

*"Um motor de cálculo já não é suficiente!"* grita o **Chefe de Quant** pela sala, agitando um relatório impresso. *"Preciso de uma frota de cinco motores idênticos imediatamente, ou voamos às cegas para dentro deste colapso de mercado!"*

Construir cinco máquinas à mão, um ecrã de cada vez, convida exatamente àquilo que não podes dar-te ao luxo agora: um tamanho de memória mal digitado aqui, uma rede esquecida ali. Deriva de configuração sob pressão — e neste momento, o erro humano custa milhões de dólares **por segundo**.

Estalas os dedos. O que o banco precisa é de um **modelo dourado**: definir a máquina perfeita uma vez, depois produzir cópias idênticas a pedido.</span>

</div>

<span id="assignment.142" lang="pt" no><span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> tem exatamente isso: **Templates de VM**. Um template captura CPU, memória, discos, redes e cloud-init num único objeto versionado. Combinado com a **criação multi-instância**, um único blueprint transforma-se numa frota inteira com um único clique.



## 🎯 Objetivos da Sua Missão

1. Forjar o template dourado
2. Escalar a frota sob pressão
3. Desativar a frota



🔐 Credenciais de Login
====================

A interface do <span id="assignment.69.1" lang="nolang" no>**SUSE Virtualization**</span> e a interface do **Rancher Prime** utilizam as mesmas credenciais.</span>

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



<span id="assignment.143" lang="pt" no>📜 Tarefa 1: Forjar o modelo de ouro
====================================


  


Você precisa de um modelo que acelere a implantação de máquinas virtuais e as padronize.
Em</span> [button label="SUSE Virtualization UI" variant="success"](tab-0) <span id="assignment.144" lang="pt" no>navegue até <span id="assignment.144.1" lang="nolang" no>**Advanced > Templates**</span> e clique em <span id="assignment.19.3" lang="nolang" no>**Create**</span>, depois preencha os seguintes detalhes:

- <span id="assignment.39.3" lang="nolang" no>**Namespace**</span>: prod
- <span id="assignment.144.2" lang="nolang" no>**Template Name**</span>:</span>

<div class="cred">

```txt
prod-basic
```

</div>

<span id="assignment.145" lang="pt" no>Precisamos minimizar o uso de recursos, e todas as VMs devem ser acessíveis usando a chave SSH de produção, que é protegida com segurança.

- Básico:
  - <span id="assignment.42.1" lang="nolang" no>**CPU**</span>: 1
  - <span id="assignment.145.1" lang="nolang" no>**Memory**</span>: 1
  - <span id="assignment.45.1" lang="nolang" no>**SSHKey**</span>: prod/default

O nosso sistema operativo base predefinido é o SLES 16.

- <span id="assignment.6.4" lang="nolang" no>Volumes</span>:
  - <span id="assignment.45.2" lang="nolang" no>**Image**</span>: official-images/SLES-16.0-Minimal-VM.x86_64-Cloud-GM.qcow2
  - <span id="assignment.45.3" lang="nolang" no>**Size**</span>: 5

Queremos que os servidores de produção disponibilizem os seus serviços na rede de serviços de produção.

- <span id="assignment.49.1" lang="nolang" no>Networks</span>:
  - <span id="assignment.49.2" lang="nolang" no>**Network**</span>: prod/service

Todas as VMs de produção devem ser executadas apenas em hosts prontos para produção.

- <span id="assignment.51.1" lang="nolang" no>Node Scheduling</span>:
  1. Selecione <span id="assignment.51.5" lang="nolang" no>**Run virtual machine on node(s) matching scheduling rules**</span>
  2. Clique em <span id="assignment.51.6" lang="nolang" no>**Add Node Selector**</span> e depois em <span id="assignment.51.7" lang="nolang" no>**Add Rule**</span>:


- <span id="assignment.51.8" lang="nolang" no>**Key**</span>:</span>

<div class="cred">

```txt
stage
```

</div>

<span id="assignment.52" lang="pt" no>- **Valor**:</span>

<div class="cred">

```txt
prod
```

</div>


<span id="assignment.146" lang="pt" no>Queremos que as VMs estejam devidamente identificadas:

- <span id="assignment.53.1" lang="nolang" no>Labels</span>:
  - Clique em <span id="assignment.53.3" lang="nolang" no>**Add Label**</span>:


- <span id="assignment.51.8" lang="nolang" no>**Key**</span>:</span>
<div class="cred">

```txt
stage
```

</div>

<span id="assignment.52" lang="pt" no>- **Valor**:</span>
<div class="cred">

```txt
prod
```

</div>


<span id="assignment.147" lang="pt" no>Finalmente, queremos que todas las máquinas de producción... espera, la traducción es al portugués.

Por fim, queremos que todas as máquinas de produção estejam padronizadas em um conjunto de pacotes e configurações:

- <span id="assignment.54.1" lang="nolang" no>Advanced Options</span>:
  - <span id="assignment.54.4" lang="nolang" no>**User Data Template**</span>: prod/prod

Para finalizar, clique em <span id="assignment.19.3" lang="nolang" no>**Create**</span>.

Consegue imaginar preencher todos esses detalhes toda vez? As pessoas desistiriam, e o ambiente ficaria cheio de inconsistências, e a inconsistência torna a automação futura ainda mais difícil.


> [!NOTE]
> Os templates são **versionados**. Se você editar o template mais tarde, uma nova versão é criada, enquanto as máquinas construídas a partir de versões mais antigas mantêm sua linhagem: um registro de auditoria completo do que foi implantado a partir de qual blueprint, o que seus reguladores irão apreciar.


📈 Tarefa 2: Escalar a frota sob pressão
=========================================

Como o template já existe, implantar múltiplos servidores leva apenas alguns cliques.


  


Em</span> [button label="SUSE Virtualization UI" variant="success"](tab-0) <span id="assignment.148" lang="pt" no>vá até **<span id="assignment.6.2" lang="nolang" no>Virtual Machines</span>** e clique em <span id="assignment.19.3" lang="nolang" no>**Create**</span>, depois preencha os seguintes detalhes:

1. Selecione <span id="assignment.148.1" lang="nolang" no>**Multiple Instance**</span>
2. Defina <span id="assignment.39.3" lang="nolang" no>**Namespace**</span> como prod
3. Defina <span id="assignment.148.2" lang="nolang" no>**Name Prefix**</span> como:</span>

<div class="cred">

```txt
appcluster
```

</div>


<span id="assignment.149" lang="pt" no>4. Defina o <span id="assignment.149.1" lang="nolang" no>**Count**</span> para 2
5. Marque <span id="assignment.149.2" lang="nolang" no>**Use VM Template**</span> e defina o <span id="assignment.149.3" lang="nolang" no>**Template**</span> para prod/prod-basic
6. Clique em <span id="assignment.19.3" lang="nolang" no>**Create**</span></span>




<div id="702" class="story">

<span id="assignment.150" lang="pt" hist="vertrex-bank">A equipa de análise de risco começa a alimentar dados na frota expandida, estabilizando a posição de mercado do banco mesmo a tempo.</span>

</div>


<span id="assignment.151" lang="pt" no>🧹 Tarefa 3: Desmobilizar a frota
===============================</span>

<div id="703" class="story">

<span id="assignment.152" lang="pt" hist="vertrex-bank">A onda do mercado diminui. As máquinas virtuais ficam ociosas, à espera da próxima vaga — mas será que ela virá hoje? Amanhã? No próximo mês? Para estes nobres servidores, esperar é mais doloroso do que processar todos os números.</span>

</div>

<span id="assignment.153" lang="pt" no>Já não precisa de tantas máquinas virtuais, apague-as todas de uma vez (não se preocupe se ainda estiverem a iniciar).</span> [button label="SUSE Virtualization UI" variant="success"](tab-0) <span id="assignment.154" lang="pt" no>navegue até a seção <span id="assignment.40.2" lang="nolang" no>**Virtual Machines**</span>:

1. Marque a caixa <span id="assignment.154.1" lang="nolang" no>**checkboxes**</span> ao lado de todas as novas máquinas virtuais que você criou
2. Clique em <span id="assignment.137.2" lang="nolang" no>**Delete**</span>, marque <span id="assignment.154.2" lang="nolang" no>**Delete All**</span>, e clique em <span id="assignment.154.3" lang="nolang" no>**Delete**
</span></span>

<div id="704" class="story">

<span id="assignment.155" lang="pt" hist="vertrex-bank">O sofrimento destas nobres máquinas virtuais chegou ao fim. Vês as chamas, minha filha? Agora repousam no Valhalla.</span>

</div>




<span id="assignment.156" lang="pt" no>Novo em <span id="assignment.2.2" lang="nolang" no>Kubernetes</span>? **Salte à vontade.** Caso contrário, prove na</span> [button label="Cluster Terminal" variant="success"](tab-1) <span id="assignment.157" lang="pt" no>Elasticidade em hardware próprio. <span id="assignment.157.1" lang="pt" hist="vertrex-bank">Escalabilidade horizontal ao estilo cloud (para cima e para baixo) no próprio datacenter do banco: sem questões de residência de dados, sem custos de saída de dados.</span>
- **O erro humano é eliminado por design.** As máquinas são criadas a partir de um blueprint dourado com controlo de versões, não da memória ou da rotina: a deriva de configuração não pode acontecer às 2 da manhã.
- **Economia do ciclo de vida completo.** A desativação é uma checkbox e um clique, pelo que a capacidade temporária nunca se torna um custo permanente, o oposto exato da velha proliferação de <span id="ch1.intro1.1" lang="nolang" no>hypervisor</span>.

Clique em <span id="assignment.32.1" lang="nolang" no>**Check**</span> para continuar. ⚔️

📚 Mais informação
===================</span>

- [<span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span>: Overview](https://documentation.suse.com/cloudnative/virtualization/latest/en/introduction/overview.html)
- [Creating <span id="assignment.6.2" lang="nolang" no>Virtual Machines</span>](https://documentation.suse.com/cloudnative/virtualization/latest/en/virtual-machines/create-vm.html)
