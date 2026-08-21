---
slug: the-flash-crash-first-vm
id: 09d4eiczcvaw
type: challenge
title: '<span id="assignment.33" lang="pt" hist="vertrex-bank">⚡ Capítulo 3: O Colapso Relâmpago</span>'
teaser: <span id="assignment.34" lang="pt" hist="vertrex-bank">Os mercados asiáticos estão em colapso e os quants precisam de um motor de cálculo AGORA. Implante uma VM totalmente configurada com armazenamento e credenciais em minutos, não em dias.</span>
tabs:
- id: 6byxu4pxkfpm
  title: SUSE Virtualization UI
  type: service
  hostname: kvm-host
  path: /
  port: 8443
  protocol: https
- id: 381amyptjwzi
  title: Cluster Terminal
  type: terminal
  hostname: kvm-host
- id: wxzurljjianr
  title: Rancher Prime UI
  type: service
  hostname: kvm-host
  port: 30002
  protocol: https
difficulty: basic
timelimit: 3000
enhanced_loading: null
---
<span id="assignment.35" lang="pt" hist="vertrex-bank">⚡ Capítulo 3: O Crash Instantâneo</span>

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
    max-height: 1.5vh;
    max-width: 1.5vh;
    margin: 0;
    padding: 0;
    display: inline-block;
  }

</style>

<img class="logos" alt="Welcome!" src="../assets/03-chapter-img.png"/>

<div id="301" class="story">

<span id="assignment.36" lang="pt" hist="vertrex-bank">Está sentado num escritório improvisado mesmo ao lado do centro de dados, a meio da revisão da topologia de rede, quando as luzes de emergência do teto pulsam subitamente num amarelo intenso. O rádio ganha vida com um estalido. É o **Chefe de Trading Quantitativo**, e ele parece em pânico.

*"Temos uma anomalia enorme nos mercados asiáticos!"* grita ele por cima do ruído caótico de uma sala de negociação frenética. *"Os nossos modelos algorítmicos atuais não estão a conseguir processar o fluxo de dados que está a chegar suficientemente depressa. Precisamos de um novo motor de cálculo de alto desempenho, dedicado, implementado imediatamente, com um volume de dados secundário de alta velocidade, ou vamos perder milhões nos próximos dez minutos!"*

No passado, satisfazer este pedido de emergência no Vertex Trust Bank significava abrir um ticket prioritário, esperar que a equipa de infraestrutura reservasse alocações de armazenamento e instalar manualmente um sistema operativo. Era um processo que demorava **dias**.

Não tem dias. **Tem minutos.**

Ignora completamente o sistema de tickets legado e prepara-se para implementar uma máquina virtual <span id="assignment.2.6" lang="nolang" no>Linux</span> totalmente configurada (com credenciais de segurança injetadas e armazenamento associado) em meros segundos.</span>
</div>


<span id="assignment.37" lang="pt" no>## 🎯 Objetivos da Sua Missão

1. Verificar a imagem do sistema operativo
2. Provisionar o <span id="assignment.37.1" lang="pt" hist="vertrex-bank">motor de cálculo</span>
3. Aceder à Consola Web



🔐 Credenciais de Login
====================

A interface do **<span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span>** e a interface do **Rancher Prime** usam as mesmas credenciais.</span>

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




<span id="assignment.38" lang="pt" no>📀 Tarefa 1: Verificar a imagem do sistema operativo
============================================

Vá até</span> [button label="<span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> UI" variant="success"](tab-0) <span id="assignment.39" lang="pt" no>, navegue até **<span id="assignment.6.3" lang="nolang" no>Images</span>** no painel lateral esquerdo e confirme que a imagem do sistema operacional base <span id="assignment.39.1" lang="nolang" no>**SLES-16.0-Minimal-VM.x86_64-Cloud-GM.qcow2**</span> está presente e marcada como **<span id="assignment.6.17" lang="nolang" no>Active</span>**.

> [!NOTE]
> <span id="assignment.6.3" lang="nolang" no>Images</span> em <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> são imagens-mestre globais para todo o cluster. Cada VM que você iniciar a partir desta imagem obtém seu próprio disco copy-on-write. A imagem em si nunca é modificada.

**Se a imagem estivesse ausente**, você mesmo poderia adicioná-la em segundos, sem esperar por um administrador de armazenamento.

As imagens podem ser criadas a partir de uma URL, carregadas a partir da sua estação de trabalho, ou exportadas de um volume existente através de <span id="assignment.39.2" lang="nolang" no>**Images > Create**</span>:


  


Por exemplo, vamos adicionar uma nova imagem:

1. Vá para **<span id="assignment.6.3" lang="nolang" no>Images</span>** no painel esquerdo e clique em <span id="assignment.19.3" lang="nolang" no>**Create**</span>, depois preencha os seguintes detalhes:
   - <span id="assignment.39.3" lang="nolang" no>**Namespace**</span>: official-images
   - <span id="assignment.19.4" lang="nolang" no>**Name**</span>: preenchido automaticamente
   - Básico:
     - <span id="assignment.39.4" lang="nolang" no>**URL**</span>:</span>

<div class="cred">

```txt
http://192.168.122.1:8889/SLES15-SP7-Minimal-VM.x86_64-Cloud-GM.qcow2
```

</div>


<span id="assignment.40" lang="pt" no>2. Clique em <span id="assignment.19.3" lang="nolang" no>**Create**</span>

A imagem que você acabou de criar aparece na lista com o estado <span id="assignment.40.1" lang="nolang" no>**Downloading**</span>. Você pode acompanhá-la na coluna de progresso.

Avance para a próxima tarefa; assim que o download for concluído, um alerta aparece no **sino de notificações** no canto superior direito da tela.

> [!NOTE]
> O download acontece do lado do servidor, a partir de um espelho local na rede deste laboratório, por isso é concluído em segundos. A imagem se torna **<span id="assignment.6.17" lang="nolang" no>Active</span>** assim que <span id="assignment.2.8" lang="nolang" no>Longhorn</span> a tiver replicado.

🚀 Tarefa 2: Provisionar o mecanismo de cálculo
===========================================

Para esta tarefa vamos criar nossa primeira VM.

> [!NOTE]
> Por favor, não clique em <span id="assignment.19.3" lang="nolang" no>**Create**</span> até que seja instruído.

Navegue até <span id="assignment.40.2" lang="nolang" no>**Virtual Machines**</span> e clique no botão <span id="assignment.19.3" lang="nolang" no>**Create**</span>.

<span id="assignment.40.3" lang="pt" hist="vertrex-bank">Configure o motor exatamente como os quants precisam.</span>

- <span id="assignment.19.4" lang="nolang" no>**Name**</span>:</span>
<div class="cred">

```txt
the-engine-01
```

</div>

<span id="assignment.41" lang="nolang" no>
- **Namespace**:
</span>
<div class="cred">

```txt
prod
```

</div>


<span id="assignment.42" lang="pt" no>Se o namespace não existir, crie-o.

- <span id="assignment.42.1" lang="nolang" no>**CPU**</span>:</span>
<div class="cred">

```txt
2
```

</div>


<span id="assignment.43" lang="nolang" no>
- **Memory**:
</span>
<div class="cred">

```txt
2
```

</div>


<span id="assignment.44" lang="pt" hist="vertrex-bank">Note o baixo consumo de recursos: nossa futura equipa de quants é altamente qualificada, e a sua aplicação é extremamente otimizada para baixa latência e baixo uso de recursos.</span>

<span id="assignment.45" lang="pt" no>- <span id="assignment.45.1" lang="nolang" no>**SSHKey**</span>: prod/default




No separador <span id="assignment.6.4" lang="nolang" no>Volumes</span> (verde, não confundir com o preto), preencha os seguintes detalhes:

- <span id="assignment.45.2" lang="nolang" no>**Image**</span>: official-images/SLES-16.0-Minimal-VM.x86_64-Cloud-GM.qcow2
- <span id="assignment.45.3" lang="nolang" no>**Size**</span>:</span>
<div class="cred">

```txt
5
```

</div>

<span id="assignment.46" lang="pt" no>Depois adicione um novo volume clicando em <span id="assignment.46.1" lang="nolang" no>**Add Volume**</span>, e preencha os seguintes detalhes:

- <span id="assignment.19.4" lang="nolang" no>**Name**</span>:</span>
<div class="cred">

```txt
market-data-vol
```

</div>

<span id="assignment.47" lang="nolang" no>
- **Size**:
</span>
<div class="cred">

```txt
1
```

</div>

<span id="assignment.48" lang="pt" hist="vertrex-bank">Agora vamos ligar o motor à rede do banco.</span><span id="assignment.49" lang="pt" no>Na aba <span id="assignment.49.1" lang="nolang" no><b style="color:#30ba78;">Networks</b></span> (verde, não confundir com a preta):

- <span id="assignment.49.2" lang="nolang" no>**Network**</span>: <span id="assignment.49.3" lang="nolang" no><b class="highlightcopy">prod/service</b></span></span>
<div id="302" class="story">


<span id="assignment.50" lang="pt" hist="vertrex-bank">Isso atende ao pedido do trader de uma segunda unidade de dados de alta velocidade. Nos bastidores, ambos os discos passam a ser volumes <span id="assignment.2.8" lang="nolang" no>Longhorn</span> replicados, e os dados de mercado sobrevivem mesmo que um disco físico falhe no meio de uma negociação.</span>

</div>


<span id="assignment.51" lang="pt" no>Como se trata de un clúster de entorno mixto, asegurémonos de que la VM se ejecute solo en nodos de producción.

Haz clic en <span id="assignment.51.1" lang="nolang" no><b style="color:#30ba78;">Node Scheduling</b></span>: <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> ofrece tres opciones:

- <span id="assignment.51.2" lang="nolang" no>**Any available node**</span>: el planificador de <span id="assignment.2.2" lang="nolang" no>Kubernetes</span> elige dónde colocar la VM, y **la migración en vivo permanece activada**
- <span id="assignment.51.3" lang="nolang" no>**Specific node**</span>: fijar la VM a un nodo (no es posible la migración)
- <span id="assignment.51.4" lang="nolang" no>**Scheduling rules**</span>: reglas de afinidad basadas en etiquetas de nodo (capacidad de GPU, topología NUMA, zona de red…)

Configura la regla de producción:

1. Selecciona <span id="assignment.51.5" lang="nolang" no>**Run virtual machine on node(s) matching scheduling rules**</span>
2. Haz clic en <span id="assignment.51.6" lang="nolang" no>**Add Node Selector**</span>, luego en <span id="assignment.51.7" lang="nolang" no>**Add Rule**</span>:

- <span id="assignment.51.8" lang="nolang" no>**Key**</span>:</span>
<div class="cred">

```txt
stage
```

</div>

<span id="assignment.52" lang="nolang" no>
- **Value**:
</span>
<div class="cred">

```txt
prod
```

</div>


<span id="assignment.53" lang="pt" no>Agora atribua-lhe uma etiqueta:

Vá ao separador <span id="assignment.53.1" lang="nolang" no><b style="color:#30ba78;">Labels</b></span> (não confundir com <span id="assignment.53.2" lang="nolang" no>"Instance Labels"</span>) e clique em <span id="assignment.53.3" lang="nolang" no>**Add Label**</span>:

- <span id="assignment.51.8" lang="nolang" no>**Key**</span>:</span>
<div class="cred">

```txt
stage
```

</div>

<span id="assignment.52" lang="nolang" no>
- **Value**:
</span>
<div class="cred">

```txt
prod
```

</div>

<span id="assignment.54" lang="pt" no>Isso ajudará a gerir a VM com automação futura.

Navegue até <span id="assignment.54.1" lang="nolang" no><b style="color:#30ba78;">Advanced Options</b></span> (não confunda com <span id="assignment.54.2" lang="nolang" no>'Advanced'</span> na coluna da esquerda), depois selecione <span id="assignment.54.3" lang="nolang" no>**Cloud Configuration**</span>, para garantir que o sistema arranca com todas as configurações e pacotes necessários instalados.

Clique em <span id="assignment.54.4" lang="nolang" no>**User Data Template**</span> e selecione <span id="assignment.54.5" lang="nolang" no>**Create New**</span> para definir um template padrão. Dê-lhe o nome:

- <span id="assignment.19.4" lang="nolang" no>**Name**</span>:</span>
<div class="cred">

```txt
prod
```

</div>


<span id="assignment.55" lang="pt" no>Para o <span id="assignment.55.1" lang="nolang" no>**User Data**</span>, insira:

```yaml
#cloud-config
packages:
  - qemu-guest-agent
runcmd:
  - - systemctl
    - enable
    - --now
    - qemu-guest-agent.service
write_files:
  - path: /etc/issue
    content: |
      \e{red}Production\e{reset}
    append: true
ssh_authorized_keys:
  - ssh-ed25519
    AAAAC3NzaC1lZDI1NTE5AAAAIFdt8wX4G0WGg/l4uDq/LntBO7WiNyqh0+pNUzF/NfMa
```

Guarde o template clicando em <span id="assignment.19.3" lang="nolang" no>**Create**</span> (dentro da caixa do template)

Como o template está no namespace <span id="assignment.55.2" lang="nolang" no><b class="highlightcopy">prod</b></span> e tem o próprio nome <span id="assignment.55.2" lang="nolang" no><b class="highlightcopy">prod</b></span>, ele se torna prod/prod: o padrão de produção, pronto para ser usado em todas as VMs.</span>
<div id="303" class="story">
<span id="assignment.56" lang="pt" hist="vertrex-bank">A equipa de firewall da mesa de negociação tem mais uma exigência:</span>
</div>

<span id="assignment.57" lang="pt" no>O motor deve subir num **endereço previsível**, não no que o DHCP atribuir. No campo <span id="assignment.57.1" lang="nolang" no>**Network Data**</span>, introduza:

```yaml
version: 2
ethernets:
  enp1s0:
    addresses:
      - 192.168.122.50/24
    gateway4: 192.168.122.1
    nameservers:
      addresses:
        - 192.168.122.1
```

O cloud-init aplica ambos no primeiro arranque: <span id="assignment.57.2" lang="nolang" no><b class="highlightcopy">the-engine-01</b></span> ficará online em `192.168.122.50` sem qualquer configuração manual pós-implementação.

> [!NOTE]
> Isto é **cloud-init**, o mesmo mecanismo padrão da indústria usado por todas as grandes clouds públicas.
> Num cenário real haveria automação mais completa e templates dedicados para a finalidade deste servidor.


Agora que terminámos a configuração, clique em <span id="assignment.19.3" lang="nolang" no>**Create**</span> para iniciar a implementação da Máquina Virtual.

Não espere que termine o arranque, por favor avance para a próxima tarefa.</span>

<div id="304" class="story">
<span id="assignment.58" lang="pt" hist="vertrex-bank">As regras de agendamento permitem separar sistemas críticos de outras cargas de trabalho, por exemplo, fixando os motores de negociação a nós de baixa latência enquanto as tarefas em lote partilham o resto. Manter "qualquer nó disponível" aqui é importante: é isso que torna possível a evacuação sem tempo de inatividade no próximo capítulo.</span>

</div>

<span id="assignment.59" lang="pt" hist="vertrex-bank">> [!NOTE]
> **Cuando los microsegundos son dinero:** el escritorio de trading de alta frecuencia exigirá más que reglas de ubicación y hardware dedicado. <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> puede **asignar núcleos de CPU dedicados** a una VM, pasar hardware directamente, virtualizar hardware usando **SR-IOV** (tanto para NICs como para GPUs), y dividir las GPU del centro de datos en **particiones MIG** aisladas por hardware para que varias VMs compartan una GPU sin vecinos ruidosos. Dedicar recursos físicos a una VM proporciona **latencia predecible y consistente**. Este ejercicio es solo para fines educativos y no es una recomendación sobre cómo configurar una aplicación de trading de alta frecuencia.</span>

<span id="assignment.60" lang="pt" no>> [!IMPORTANT]
> Como este laboratório é executado numa **configuração aninhada**, o desempenho de I/O é um pouco mais lento do que o habitual, e o processo de provisionamento levará alguns minutos. Enquanto a sua VM arranca, temos algum entretenimento preparado para si! Vá até Bonus Drills para aprender como interagir com a API do <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> através da CLI. Tudo no <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> é um objeto <span id="assignment.2.2" lang="nolang" no>Kubernetes</span>, o que significa que pode geri-lo através da API do <span id="assignment.2.2" lang="nolang" no>Kubernetes</span> através do cluster RKE2 subjacente.
> Quando terminar, volte à Task 3.

🖥️ Task 3: Aceder à Consola Web
=================================

Monitorize o</span> [button label="SUSE Virtualization UI" variant="success"](tab-0) <span id="assignment.61" lang="pt" no>até que a máquina virtual passe para o estado de **Em execução**.


  



1. Clique no botão <span id="assignment.61.1" lang="nolang" no>**Console**</span> na linha da máquina virtual para abrir a consola web VNC
2. Repare que podemos aceder ao sistema sem ligação usando este método, **não esperes que a instalação termine, avança já para o próximo passo**.
3. Fecha a janela da consola



🏋️ Exercícios Bónus: ver através da abstração (opcional, para os curiosos da linha de comandos)
========================================================================================

Novo em <span id="assignment.2.2" lang="nolang" no>Kubernetes</span>? **Avança à vontade.** Caso contrário, de volta ao</span> [button label="Cluster Terminal" variant="success"](tab-1) <span id="assignment.62" lang="pt" no>, veja o que a plataforma realmente criou para você:

- **As imagens de ouro também são objetos de API:**

```bash,wrap,run
kubectl --kubeconfig .rodeo/harvester-kubeconfig get virtualmachineimages -A
```

- **A VM é um recurso <span id="assignment.2.2" lang="nolang" no>Kubernetes</span>:**

```bash,wrap,run
kubectl --kubeconfig .rodeo/harvester-kubeconfig get virtualmachines -n prod
```

- **A instância em execução, com seu nó e IP** (o mesmo IP que você usou para SSH):

```bash,wrap,run
kubectl --kubeconfig .rodeo/harvester-kubeconfig get vmi -n prod -o wide
```

- **Os discos são <span id="assignment.62.1" lang="nolang" no>PersistentVolumeClaims</span> comuns, suportados por <span id="assignment.2.8" lang="nolang" no>Longhorn</span>:**

```bash,wrap,run
kubectl --kubeconfig .rodeo/harvester-kubeconfig get pvc -n prod
```

Você deve reconhecer `market-data-vol` na lista: <span id="assignment.62.2" lang="pt" hist="vertrex-bank">um disco de dados bancários, expresso como armazenamento nativo em nuvem</span>.

💼 Por que isso importa?
========================

- **Dias se tornam minutos.** Um processo de provisionamento multiequipe, orientado por tickets, se transformou em um fluxo de autoatendimento de dois minutos, <span id="assignment.62.3" lang="pt" hist="vertrex-bank">durante uma crise de mercado em tempo real.</span>
- **Consistência por construção.** Imagens de ouro somadas ao cloud-init significam que todo engine que os quants solicitam inicializa idêntico, configurado e pronto.
- **Nenhum armazenamento isolado.** <span id="assignment.6.4" lang="nolang" no>Volumes</span> são retirados sob demanda do pool compartilhado de <span id="assignment.2.8" lang="nolang" no>Longhorn</span>.</span>

<div id="305" class="story">

<span id="assignment.63" lang="pt" hist="vertrex-bank">Você retransmite pela rádio para o pregão. *"Seu motor está online e o volume de dados está conectado."* A crise foi evitada — mas o dia está longe de terminar.</span>

</div>

<span id="assignment.64" lang="pt" no>Clique em <span id="assignment.32.1" lang="nolang" no>**Check**</span> para continuar. 🌊

📚 Mais informações
===================</span>

- [Creating <span id="assignment.6.2" lang="nolang" no>Virtual Machines</span>](https://documentation.suse.com/cloudnative/virtualization/latest/en/virtual-machines/create-vm.html)
- [<span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span>: Overview](https://documentation.suse.com/cloudnative/virtualization/latest/en/introduction/overview.html)
