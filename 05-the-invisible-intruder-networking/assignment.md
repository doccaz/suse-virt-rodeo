---
slug: the-invisible-intruder-networking
id: 6y9uhwn9zyll
type: challenge
title: "<span id="assignment.100" lang="pt" hist="vertrex-bank">Capítulo 5: O Intruso Invisível</span>"
teaser: <span id="assignment.101" lang="pt" hist="vertrex-bank">Um alerta de segurança às 2h da manhã. O servidor web público partilha uma rede plana com a base de dados mais sensível do banco. Construa um cofre definido por software e tranque a base de dados no seu interior.</span>
tabs:
- id: 69jpoti7gjds
  title: SUSE Virtualization UI
  type: service
  hostname: kvm-host
  path: /
  port: 8443
  protocol: https
- id: hssojxkhutjx
  title: Cluster Terminal
  type: terminal
  hostname: kvm-host
- id: pg01vcvbyns3
  title: Rancher Prime UI
  type: service
  hostname: kvm-host
  port: 30002
  protocol: https
difficulty: intermediate
timelimit: 3000
enhanced_loading: null
---
<span id="assignment.102" lang="pt" hist="vertrex-bank">🕵️ Capítulo 5: O Intruso Invisível
=====================================</span>

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

<img class="logos" alt="Welcome!" src="../assets/05-chapter-img.png"/>

<div id="501" class="story">

<span id="assignment.103" lang="pt" hist="vertrex-bank">São agora duas da manhã. O datacenter está silencioso, exceto pelo zumbido rítmico das ventoinhas de refrigeração. Está a beber café frio e a rever os registos diários de telemetria quando o seu ecrã pisca a vermelho. Um alerta crítico e de alta prioridade do Centro de Operações de Segurança sobrepõe-se ao seu painel de controlo.

Uma verificação automática de vulnerabilidades detetou uma falha arquitetónica grave: o **servidor web** de marketing do banco, voltado para o público, encontra-se exatamente na mesma camada de rede plana que a máquina virtual altamente classificada insider-threat-db.

Se um agente de ameaça conseguisse comprometer o site público, teria um caminho lateral direto e sem obstáculos até à base de dados de segurança interna mais sensível do banco. Numa infraestrutura tradicional, corrigir isto exigiria acordar a equipa sénior de engenharia de redes, recablear fisicamente as portas dos switches no escuro, e arriscar loops de encaminhamento catastróficos.

Não precisa de cabos físicos. Tem ao seu alcance o poder das **redes definidas por software**. Tem de construir um cofre digital impenetrável e trancar a base de dados lá dentro — antes que uma intrusão possa ocorrer.</span>

</div>

<span id="assignment.104" lang="pt" no>## Duas camadas de rede definida por software

<span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> oferece o espectro completo, desde a segmentação clássica de VLAN até SDN empresarial, capacidades pelas quais o banco costumava pagar uma licença SDN separada de código fechado:

| Camada | Tecnologia | Uso desta noite |
|-------|-----------|-------------|
| L2 / bridging VLAN | **<span id="assignment.2.14" lang="nolang" no>Multus</span>** | A VLAN de cofre isolando a base de dados |
| SDN / zonas de overlay isoladas | **<span id="assignment.2.13" lang="nolang" no>Kube-OVN</span>** | Sub-redes privadas sem caminho externo, mesmo com CIDRs sobrepostos |



## 🎯 Objetivos da Sua Missão

1. Conectar uma rede física de circuito fechado para produção
2. Construir uma SDN igualmente isolada para desenvolvimento
3. Aprender a mover VMs para as novas redes



🔐 Credenciais de Login
====================

A UI do <span id="assignment.69.1" lang="nolang" no>**SUSE Virtualization**</span> e a UI do <span id="assignment.2.12" lang="nolang" no>**Rancher Prime**</span> usam as mesmas credenciais.</span>

<span id="assignment.10" lang="nolang" no>Username</span>:

<div class="cred">

```txt
admin
```

</div>

<span id="assignment.105" lang="nolang" no>*Password</span>:

<div class="cred">

```txt
[[ Instruqt-Var key="RANCHER_PASSWORD" hostname="kvm-host" ]]
```

</div>



<span id="assignment.106" lang="pt" no>🧱 Tarefa 1: Ligar uma rede física em loop fechado
=================================================

A nossa equipa configurou os nós <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> com uma placa de rede (NIC) dedicada adicional, ligada num loop fisicamente fechado. Vamos usá-la para o nosso tráfego mais precioso e criar uma rede de produção isolada.

No</span> [button label="SUSE Virtualization UI" variant="success"](tab-0) <span id="assignment.107" lang="pt" no>, navegue hasta <span id="assignment.107.1" lang="nolang" no>**Networks**</span> en el menú de la izquierda, luego seleccione <span id="assignment.107.2" lang="nolang" no>**Cluster Network Configuration**</span>:

1. Haga clic en <span id="assignment.107.3" lang="nolang" no>**Create a Cluster Network**</span>
2. Configure el <span id="assignment.19.4" lang="nolang" no>**Name**</span> con:</span>

<div class="cred">

```txt
closed-loop
```

</div>

<span id="assignment.108" lang="pt" no>3. Clique em <span id="assignment.19.3" lang="nolang" no>**Create**</span>

A nova rede de cluster aparece na lista. Agora atribua-lhe uma interface física: clique em <span id="assignment.108.1" lang="nolang" no>**Create Network Configuration**</span> na mesma linha da rede de cluster de circuito fechado e preencha os seguintes detalhes:

1. Defina o <span id="assignment.19.4" lang="nolang" no>**Name**</span> como:</span>

<div class="cred">

```txt
closed-loop
```

</div>

<span id="assignment.109" lang="pt" no>Observe a seção <span id="assignment.27" lang="nolang" no>**Node Selector**</span>, aqui podemos especificar onde a rede estará disponível.

2. Em <span id="assignment.109.1" lang="nolang" no>**Uplink**</span>, defina <span id="assignment.109.2" lang="nolang" no>**NICs**</span> como ens5

3. Clique em <span id="assignment.19.3" lang="nolang" no>**Create**</span>



  


Agora defina a rede voltada para as VMs sobre ela. Selecione <span id="assignment.109.3" lang="nolang" no>**Virtual Machine Networks**</span> e clique em <span id="assignment.19.3" lang="nolang" no>**Create**</span> para definir um novo perímetro seguro:

- <span id="assignment.39.3" lang="nolang" no>**Namespace**</span>: prod
- <span id="assignment.19.4" lang="nolang" no>**Name**</span>:</span>

<div class="cred">

```txt
secure-loop-prod
```

</div>

<span id="assignment.110" lang="pt" no>- <span id="assignment.110.1" lang="nolang" no>Basics</span>:
  - <span id="assignment.110.2" lang="nolang" no>**Type**</span>: UntaggedNetwork
  - <span id="assignment.110.3" lang="nolang" no>**Cluster Network**</span>: closed-loop

Clique em <span id="assignment.19.3" lang="nolang" no>**Create**</span>.


  


De volta à lista <span id="assignment.109.3" lang="nolang" no>**Virtual Machine Networks**</span>, secure-loop-prod aparece com o status <span id="assignment.110.4" lang="nolang" no>**Active**</span>.



🔒 Tarefa 2: Criar uma SDN de circuito fechado
===================================

Agora crie o mesmo tipo de isolamento para o ambiente de desenvolvimento. <span id="assignment.110.5" lang="pt" hist="vertrex-bank">Adicionar novas placas de rede e cablagem é caro; um ambiente de desenvolvimento não precisa de tantos recursos dedicados, por isso desta vez vais usar uma **rede definida por software**.</span>


  


Vá até <span id="assignment.110.6" lang="nolang" no>**Networks > Virtual Machine Networks**</span> e clique em <span id="assignment.19.3" lang="nolang" no>**Create**</span>, depois preencha os seguintes detalhes:

- <span id="assignment.39.3" lang="nolang" no>**Namespace**</span>: prod
- <span id="assignment.19.4" lang="nolang" no>**Name**</span>:</span>

<div class="cred">

```txt
secure-loop-dev
```

</div>

<span id="assignment.111" lang="pt" no>- <span id="assignment.110.1" lang="nolang" no>Basics</span>:
  - <span id="assignment.110.2" lang="nolang" no>**Type**</span>: OverlayNetwork

Clique em <span id="assignment.19.3" lang="nolang" no>**Create**</span>.


  


Agora crie a sub-rede SDN. Vá para <span id="assignment.111.1" lang="nolang" no>**Virtual Private Cloud**</span> e, na aba da Virtual Private Cloud ovn-cluster, clique em <span id="assignment.111.2" lang="nolang" no>**Create Subnet**</span>, depois preencha os seguintes detalhes:

- <span id="assignment.19.4" lang="nolang" no>**Name**</span>:</span>

<div class="cred">

```txt
secure-vpc-dev
```

</div>

<span id="assignment.112" lang="pt" no>- <span id="assignment.112.1" lang="nolang" no>Basic</span>:
  - <span id="assignment.112.2" lang="nolang" no>**CIDR**</span>:</span>

<div class="cred">

```txt
192.168.32.0/24
```

</div>

<span id="assignment.113" lang="pt" no>- <span id="assignment.113.1" lang="nolang" no>**Provider**</span>: prod/secure-loop-dev
- <span id="assignment.113.2" lang="nolang" no>**Gateway IP**</span>:</span>

<div class="cred">

```txt
192.168.32.1
```

</div>

<span id="assignment.114" lang="pt" no>- <span id="assignment.114.1" lang="nolang" no>**Dynamic Host Configuration Protocol (DHCP)**</span>: <span id="assignment.114.2" lang="nolang" no><b class="highlightcopy">Enabled</b></span>
  - <span id="assignment.114.3" lang="nolang" no>**Private Subnet**</span>: <span id="assignment.114.2" lang="nolang" no><b class="highlightcopy">Enabled</b></span>

Clique em <span id="assignment.19.3" lang="nolang" no>**Create**</span>.

Agora você pode atribuir a rede prod/secure-loop-dev a qualquer VM, e ela só poderá se comunicar com as VMs na mesma rede.


Se tiver curiosidade em ver a topologia na aba da Virtual Private Cloud ovn-cluster, clique em <span id="assignment.114.4" lang="nolang" no>**Topology**</span>, o que é especialmente útil ao ter múltiplas sub-redes,


🎯 Tarefa 3: Configurar VMs com as novas redes
=====================================================


Você tem duas novas redes isoladas. Agora é hora de mostrar aos seus colegas como conectá-las a uma VM.


  


<span id="assignment.114.5" lang="pt" hist="vertrex-bank">Você não está fazendo a alteração você mesmo, apenas explicando como isso é feito, para isso escolheremos o servidor de produção:</span>

Volte ao painel <span id="assignment.40.2" lang="nolang" no>**Virtual Machines**</span> e localize a máquina virtual alvo ( **webserver-prod** ):

1. Clique no  na sua linha e selecione <span id="assignment.114.6" lang="nolang" no>**Edit Config**</span>
2. Vá até a aba <span id="assignment.107.1" lang="nolang" no>**Networks**</span>
3. Selecione a rede prod/secure-loop-prod para sistemas de produção, ou prod/secure-loop-dev para sistemas de desenvolvimento
4. Clique em <span id="assignment.114.7" lang="nolang" no>**Save**</span>
5. Clique no  novamente e selecione <span id="assignment.114.8" lang="nolang" no>**Restart**</span>

A VM inicia conectada à nova rede. Não espere que ela termine.



> [!IMPORTANT]
> Na maioria dos casos, se uma VM estiver em execução, você deve **pará-la primeiro** para ativar a modificação de hardware.



🏋️ Exercícios Bônus: para os curiosos de linha de comando (opcional)
==========================================================

Novo em <span id="assignment.2.2" lang="nolang" no>Kubernetes</span>? **Pule à vontade**: já temos as redes isoladas criadas. Estes exercícios opcionais adicionam uma rede isolada extra com ferramentas puras de <span id="assignment.2.2" lang="nolang" no>Kubernetes</span>.

**Uma rede isolada extra é necessária para o QA: políticas de rede <span id="assignment.2.2" lang="nolang" no>Kubernetes</span>.** Precisamos ser capazes de replicar essa configuração no QA para garantir que não haja surpresas ao mover para produção, aplicar uma política estrita que descarta tráfego não autorizado no nível do pod, abaixo do isolamento de VLAN. Em</span> [button label="Cluster Terminal" variant="success"](tab-1) <span id="assignment.115" lang="pt" no>, aplica una política de ingress de denegación por defecto a la secure namespace:

```bash,run
cat << EOF | kubectl --kubeconfig .rodeo/harvester-kubeconfig apply -f -
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  name: default-deny-all
  namespace: prod
spec:
  podSelector: {}
  policyTypes:
    - Ingress
EOF
```

Confirma que la política está aplicada:

```bash,wrap,run
kubectl --kubeconfig .rodeo/harvester-kubeconfig get networkpolicy -n prod
```


Crea una zona completamente independiente para el equipo forense:

```bash,run
cat << EOF | kubectl --kubeconfig .rodeo/harvester-kubeconfig apply -f -
apiVersion: k8s.cni.cncf.io/v1
kind: NetworkAttachmentDefinition
metadata:
  name: forensics-zone
  namespace: prod
  labels:
    network.harvesterhci.io/clusternetwork: secure-loop-prod
    network.harvesterhci.io/type: OverlayNetwork
spec:
  config: '{"cniVersion":"0.3.1","name":"forensics-zone","type":"kube-ovn","provider":"forensics-zone.prod.ovn","server_socket":"/run/openvswitch/kube-ovn-daemon.sock"}'
EOF
```

```bash,run
cat << EOF | kubectl --kubeconfig .rodeo/harvester-kubeconfig apply -f -
apiVersion: kubeovn.io/v1
kind: Subnet
metadata:
  name: forensics-zone
spec:
  cidrBlock: "172.16.1.0/24"
  gateway: "172.16.1.1"
  excludeIps:
    - "172.16.1.1"
  protocol: IPv4
  natOutgoing: false
  private: true
  provider: forensics-zone.prod.ovn
  vpc: ovn-cluster
EOF
```

> [!NOTE]
> Cada zona obtiene su propia red dedicada (y por tanto su propio switch lógico aislado), que es lo que hace que el aislamiento sea real. <span id="assignment.2.13" lang="nolang" no>Kube-OVN</span> sigue aplicando una regla por VPC: dos subnets de la misma VPC (`ovn-cluster`) no pueden compartir CIDR, ni siquiera en redes distintas, por lo que `forensics-zone` usa un bloque diferente. Un solapamiento real de espacio de direcciones entre zonas también es posible, solo que requiere una segunda VPC personalizada, fuera del alcance de este ejercicio.

Verifica que ambas zonas existen con `natOutgoing: false`: sin salida, sin entrada:

```bash,wrap,run
kubectl --kubeconfig .rodeo/harvester-kubeconfig get subnets.kubeovn.io -o custom-columns=NAME:.metadata.name,CIDR:.spec.cidrBlock,PRIVATE:.spec.private,NAT:.spec.natOutgoing
```

Dos bóvedas, dos redes privadas independientes, cero paquetes compartidos. Una VM conectada a cualquiera de las zonas puede hablar con sus vecinos en la misma subnet y con **nada más**: microsegmentación sin licencia de SDN propietaria, construida y desmontada por completo en software.

💼 ¿Por qué importa esto?
==============================================

- **Segmentación a las 2 AM, en software.** Lo que antes era un proyecto de recableado con reuniones de control de cambios se convirtió en tres minutos de configuración, mientras la ventana de amenaza seguía cerrada.
- **Defensa en profundidad por defecto.** Aislamiento VLAN en la capa 2, políticas de red en la capa de pods y subnets SDN privadas: tres muros independientes desde una sola plataforma.
- **Evidencia de cumplimiento integrada.** Cada red, política y subnet es un objeto YAML versionable: los auditores de seguridad obtienen pruebas, no promesas.

Haz clic en <span id="assignment.32.1" lang="nolang" no>**Check**</span> para continuar. ⏪

📚 Más información
===================</span>

- [Cluster Networking](https://documentation.suse.com/cloudnative/virtualization/latest/en/networking/cluster-network.html)
