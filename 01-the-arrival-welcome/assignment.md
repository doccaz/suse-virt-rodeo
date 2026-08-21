---
slug: the-arrival-welcome
id: ermykdy1tbse
type: challenge
title: "<span id="assignment.7" lang="pt" hist="vertrex-bank">🏦 Capítulo 1: A Chegada</span>"
teaser: <span id="assignment.8" lang="pt" hist="vertrex-bank">O Vertex Trust Bank está a afogar-se em custos de legado <span id="ch1.intro1.1" lang="nolang" no>hypervisor</span>
  Entre na sala de reuniões, assuma o comando do SUSE Virtualization,
  e inspecione o seu novo centro de comando.</span>
notes:
- type: text
  contents: |
    <span id="assignment.1" lang="pt" no># Bem-vindo ao <span id="assignment.1.1"  lang="nolang" no>SUSE Virtualization Rodeo!</span>

    Aguarde enquanto preparamos o seu ambiente de laboratório.</span><span lang="pt" id="ch1.waiting1" hist="vertrex-bank">A chuva bate contra as janelas da sede do Vertex Trust Bank...
    Sarah, a CTO, está à sua espera na sala de reuniões.</span>
    <img class="logos" src="../assets/logos/suse_logo.svg"/>
tabs:
- id: 3veafppy6ial
  title: SUSE Virtualization UI
  type: service
  hostname: kvm-host
  path: /
  port: 8443
  protocol: https
- id: ljaolp3q406m
  title: Cluster Terminal
  type: terminal
  hostname: kvm-host
- id: ihjqc1cl533q
  title: Rancher Prime UI
  type: service
  hostname: kvm-host
  port: 30002
  protocol: https
difficulty: basic
timelimit: 2400
enhanced_loading: null
---

<span id="assignment.9" lang="pt" hist="vertrex-bank">🏦 Capítulo 1: A Chegada</span>
==========================

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
    border-left: 1px solid white;
    border-radius: 0;
    display: flex;
    align-items: center;
    background-color: #30ba78;   /* new: green copy-bar background */
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

<img class="logos" alt="Welcome!" src="../assets/01-chapter-img.png"/>


<div id="101" class="story">
<span lang="pt" id="ch1.intro1" hist="vertrex-bank">A chuva batia contra as janelas do chão ao teto da sede do Vertex Trust Bank, distorcendo o horizonte da cidade num borrão cinzento e aquoso. Dentro da sala de reuniões executiva de paredes de vidro, a atmosfera era igualmente turbulenta. Sarah, a Diretora de Tecnologia, andava de um lado para o outro na sala, com os olhos fixos num enorme monitor suspenso que projetava um mar de alertas vermelhos e avisos de desempenho.

Ela virou-se para si, com a voz tensa de exaustão. *"Estamos a perder milissegundos preciosos em cada transação de mercado. Os nossos <span id="ch1.intro1.1" lang="nolang" no>hypervisor</span>s legados estão a ceder sob o volume brutal do tráfego bancário digital moderno. A infraestrutura é frágil, os arrays de armazenamento estão constantemente a perder a sincronização, e os custos de licenciamento estão a esgotar por completo o nosso orçamento de engenharia. Não podemos sobreviver mais um ano presos a estes sistemas monolíticos e antiquados."*

Você senta-se em silêncio na ponta da mesa de mogno, revendo os esquemas arquitetónicos que ela forneceu. Como um **Arquiteto de Infraestrutura** de elite, foi trazido para um propósito específico: salvar o Vertex Trust Bank de um bloqueio operacional total. Precisam de uma ponte para o mundo nativo da cloud sem reconstruir toda a sua pilha de aplicações do zero.

*"Temos um plano, Sarah,"* diz você finalmente, fechando o portátil com um clique tranquilizador. *"Vamos transitar todo o datacenter para <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span>. Vamos trazer os seus sistemas legados para a era moderna, e vamos fazê-lo sem perder o ritmo."*</span>
</div>


<span id="assignment.2" lang=pt no>Sua jornada começa agora mesmo. Antes de poder desmontar o velho mundo, você precisa estabelecer uma base no novo e mergulhar no ambiente.



## O que é <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span>?

<span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> (também conhecido como **<span id="assignment.2.1" lang="nolang" no>Harvester</span>**) é uma plataforma de infraestrutura hiperconvergente (HCI) moderna e de código aberto, construída sobre <span id="assignment.2.2" lang="nolang" no>Kubernetes</span>. Ela roda diretamente em bare metal e oferece ao banco **máquinas virtuais** de nível empresarial sobre uma base cloud-native, <span id="ch1.intro2"  lang="pt" hist="vertrex-bank">exatamente a ponte que o Vertex Trust Bank precisa</span>:

- **<span id="assignment.2.3" lang="nolang" no>KubeVirt</span> + <span id="assignment.2.4" lang="nolang" no>KVM</span>/<span id="assignment.2.5" lang="nolang" no>QEMU</span>**: virtualização empresarial como cargas de trabalho nativas de <span id="assignment.2.2" lang="nolang" no>Kubernetes</span>. Por baixo, está a mesma dupla **<span id="assignment.2.4" lang="nolang" no>KVM</span>/<span id="assignment.2.5" lang="nolang" no>QEMU</span>**, testada e comprovada, que impulsiona a virtualização <span id="assignment.2.6" lang="nolang" no>Linux</span> há décadas, motivo pelo qual a plataforma consegue rodar uma enorme variedade de sistemas operacionais convidados, <span id="ch1.intro3"  lang="pt" hist="vertrex-bank">incluindo os muito antigos ainda em funcionamento nos cantos legados mais empoeirados do banco, aguardando pacientemente a sua migração</span>
- **<span id="assignment.2.7" lang="nolang" no>SUSE Storage</span> (<span id="assignment.2.8" lang="nolang" no>Longhorn</span>)**: armazenamento em bloco distribuído e replicado em todos os nós, configurado e pronto para uso imediato. <span id="ch1.intro4"  lang="pt" hist="vertrex-bank">E se o banco alguma vez preferir um armazenamento diferente</span>, **qualquer driver de armazenamento compatível com <span id="assignment.2.9" lang="nolang" no>CSI</span> se conecta perfeitamente**, liberdade de escolha, nunca aprisionamento
- **<span id="assignment.2.10" lang="nolang" no>Software-defined networking</span>**: VLANs e redes overlay isoladas sem tocar em nenhum cabo
- **Uma única fatura de código aberto**: sem taxa de <span id="ch1.intro1.1" lang="nolang" no>hypervisor</span> por soquete
- **<span id="assignment.2.11" lang="nolang" no>Support</span> que realmente ouve**: os clientes da SUSE avaliam consistentemente o **SUSE <span id="assignment.2.11" lang="nolang" no>Support</span>** entre os melhores do setor, e seu feedback molda diretamente os próximos passos dos produtos. Tente pedir a um fornecedor de código fechado um lugar nessa mesa

Como a plataforma roda *sobre* <span id="assignment.2.2" lang="nolang" no>Kubernetes</span>, cargas de trabalho em contêineres podem rodar no mesmo cluster. Deixe a divisão de responsabilidades clara desde o primeiro dia: a interface do <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> gerencia **máquinas virtuais**; gerenciar contêineres (e gerenciar frotas inteiras de clusters) é tarefa do <span id="assignment.2.12" lang="nolang" no>**Rancher Prime**</span>, que você conhecerá em breve.

<span id="ch1.intro5"  lang="pt" hist="vertrex-bank">Cada componente proprietário que está a esgotar o orçamento do banco tem uma alternativa moderna e de código aberto:</span>

| O velho mundo (licenciamento por soquete) | <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> |
|--------------------------------------|---------------------|
| <span id="ch1.intro1.1" lang="nolang" no>hypervisor</span> proprietário ISAware | <span id="assignment.2.3" lang="nolang" no>KubeVirt</span> + <span id="assignment.2.4" lang="nolang" no>KVM</span> |
| Array de armazenamento proprietário |  Armazenamento SUSE, ou qualquer driver <span id="assignment.2.9" lang="nolang" no>CSI</span> <span id="ch1.intro6"  lang="pt" hist="vertrex-bank">o banco escolhe</span> |
| SDN de código fechado | <span id="assignment.2.13" lang="nolang" no>Kube-OVN</span> + <span id="assignment.2.14" lang="nolang" no>Multus</span> |
| Trono de Comando ISAware | <span id="assignment.2.15" lang="nolang" no>SUSE Rancher Prime</span> |

Sem aprisionamento a fornecedores. Sem taxa de virtualização. Sem kernel proprietário. **Uma plataforma, uma única fatura**, <span id="ch1.intro7"  lang="pt" hist="vertrex-bank">exatamente o que prometeste à Sarah na sala de reuniões</span>.



## 🎯 Objetivos da Sua Missão

1. Faça login e inspecione o painel unificado
2. Conheça o Rancher Prime, o centro de comando!
3. Valide o tecido de armazenamento distribuído
4. Teste seu acesso administrativo ao terminal




<span id="ch1.intro8"  lang="pt" hist="vertrex-bank">> [!NOTE]
> Aviso: Este laboratório destina-se a fins educativos e não a fornecer instruções sobre como configurar um ambiente de produção para um "banco". A maioria das decisões tomadas tem em conta as limitações e a finalidade deste ambiente.</span>




🔐 Suas Credenciais de Arquiteto
=============================

Para o seu registro, suas Credenciais de Arquiteto são as seguintes:</span>


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


<span id="assignment.3" lang=pt> [!NOTE]
> As interfaces utilizam certificados autoassinados. Aceite o aviso de segurança do navegador quando este aparecer. Se uma página não carregar de imediato, o ambiente do laboratório pode ainda estar a arrancar. Aguarde um minuto e atualize o separador.

> [!NOTE]
> Se preferir trabalhar no seu próprio navegador em vez dos separadores incorporados, o host do laboratório está acessível diretamente em:
> https://kvm-host.[[ Instruqt-Var key="_SANDBOX_ID" hostname="kvm-host" ]].instruqt.io:8443




📊 Tarefa 1: Iniciar sessão e inspecionar o painel unificado
===================================================

Navegue até ao</span> [button label="SUSE Virtualization UI" variant="success"](tab-0) <span id="assignment.4" lang=ptaba e faça login com as suas credenciais.

![01-connect_to_cluster.gif](../assets/chapter1-connect_to_cluster.gif)

Reserve um momento para observar o principal</span>  <span id="assignment.5" lang="nolang" no>**Dashboard**</span><span id="assignment.6" lang=pt: este es tu centro de mando para toda la misión.

> [!NOTE]
> No hagas cambios todavía. Solo nos estamos familiarizando con el entorno.

- La primera sección contiene los números generales:
  - **<span id="assignment.6.1" lang="nolang" no>Hosts</span>** el clúster está formado por
  - **<span id="assignment.6.2" lang="nolang" no>Virtual Machines</span>** (en ejecución y detenidas)
  - **<span id="assignment.6.3" lang="nolang" no>Images</span>** disponibles para desplegar nuevas VMs
  - **<span id="assignment.6.4" lang="nolang" no>Volumes</span>** en uso
  - **<span id="assignment.6.5" lang="nolang" no>Disks</span>** disponible

Al hacer clic en cada uno de ellos, accedes a una sección dedicada con más información. Haz clic en **<span id="assignment.6.1" lang="nolang" no>Hosts</span>**:

Verás una vista detallada de los recursos reservados y utilizados de cada host, así como las direcciones IP del host y otros detalles.

Fíjate en el  al final de cada fila: al hacer clic en él se abre un menú con distintas acciones para ese host.

Vuelve a **<span id="assignment.6.6" lang="nolang" no>Dashboard</span>** y mira qué más hay:

- La segunda sección, **<span id="assignment.6.7" lang="nolang" no>Capacity</span>**, muestra los recursos actualmente reservados y disponibles en el clúster.

- Debajo se encuentra una sección con dos pestañas:

  - **<span id="assignment.6.8" lang="nolang" no>Cluster Metrics</span>**: métricas en tiempo real sobre el clúster; resultan muy útiles al solucionar problemas de rendimiento.

  - **<span id="assignment.6.9" lang="nolang" no>Virtual Machine Metrics</span>**: métricas en tiempo real de las máquinas virtuales; ten en cuenta que si no hay ninguna VM en ejecución no habrá datos que mostrar.

- En la parte inferior, la última sección, **<span id="assignment.6.10" lang="nolang" no>Events</span>**, muestra los últimos eventos que ocurren en el clúster.

Ahora echa un vistazo al resto de la interfaz. En la parte superior derecha hay un menú desplegable con **All Namespaces** seleccionado. Te permite centrarte en namespaces específicos. Los namespaces aquí son namespaces de <span id="assignment.2.2" lang="nolang" no>Kubernetes</span>: una forma de organizar recursos y asignar permisos dedicados a todo lo que hay dentro de ellos, un concepto similar a un "grupo". Al final de este capítulo encontrarás enlaces con más información; muchos de los conceptos que encuentras en <span id="assignment.2.2" lang="nolang" no>Kubernetes</span> se aplican directamente a <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span>.

La **campana** contiene notificaciones y alertas, y más a la derecha el **icono de usuario** te lleva a la configuración de usuario y a las claves para el acceso automatizado.

En el lado izquierdo hay una columna con diferentes secciones. No vamos a repasarlas todas ahora. Verás muchas de ellas en los próximos capítulos. Ten en cuenta que estas secciones cambian según qué plugins estén habilitados o deshabilitados.

Por último, en la esquina inferior izquierda, haz clic en **<span id="assignment.2.11" lang="nolang" no>Support</span>**.
Te lleva a una página con enlaces a documentación y otros recursos de soporte, además de dos secciones importantes:

- **<span id="assignment.6.11" lang="nolang" no>Generate a <span id="assignment.2.11" lang="nolang" no>Support</span> Bundle</span>**: genera un archivo que ayuda a SUSE <span id="assignment.2.11" lang="nolang" no>Support</span> a solucionar problemas en tu entorno sin necesidad de acceder directamente a él.
- **<span id="assignment.6.12" lang="nolang" no>Download KubeConfig</span>**: te proporciona el archivo kubeconfig que puedes usar para gestionar este clúster con kubectl y otras herramientas desde una consola.

Si aún te queda tiempo, familiarízate con las secciones antes de pasar a la siguiente tarea.

> [!NOTE]
> Todo lo que ves en este panel (VMs, volúmenes, redes) es en realidad un recurso de <span id="assignment.2.2" lang="nolang" no>Kubernetes</span> por debajo. La interfaz es tu herramienta principal para esta misión; una terminal está lista para los ejercicios opcionales, por si tienes curiosidad sobre el funcionamiento interno.

🐮 Tarea 2: Conoce Rancher Prime, el centro de mando
=================================================

La plataforma también puede conectarse a **Rancher Prime**, <span id="ch1.task2a"  lang="pt" hist="vertrex-bank">e importante entender quem faz o quê no novo mundo do banco:</span>

- <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> gestiona las **máquinas virtuales** de este clúster.
- **Rancher Prime** gestiona **muchos clústeres a la vez** (cada clúster de <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> en cada centro de datos de sucursal), además de **usuarios, roles y control de acceso centralizados (<span id="assignment.6.13" lang="nolang" no>RBAC</span>)**, y las **cargas de trabajo de contenedores** que el banco ejecutará junto a sus VMs.

Veamos qué hay dentro de Rancher.

Abre [button label="Rancher Prime UI" variant="success"](tab-2), inicia sesión con las mismas credenciales y selecciona **Virtualization Management** en el menú izquierdo.

Desde aquí puedes gestionar varios clústeres de <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span>. Importa el existente:

1. Haz clic en **Import Existing**
2. Establece el **Cluster Name** como

```txt
mysusevirt1
```

3. Haz clic en **Create**
4. Aparece una nueva pantalla. En ella se muestra una url, copia esa url para los siguientes pasos.
5. Debajo puedes ver las instrucciones de registro. Síguelas y recuerda seleccionar **<span id="assignment.6.14" lang="nolang" no>Insecure Skip TLS Verify</span>** al editar el ajuste cluster-registration-url. Esto debe hacerse en [button label="SUSE Virtualization UI" variant="success"](tab-0).

6. Vuelve a [button label="Rancher Prime UI" variant="success"](tab-2) y haz clic en "<span id="assignment.2.1" lang="nolang" no>Harvester</span> Clusters" en la parte superior izquierda de la interfaz.

Fíjate en el estado junto al nombre del clúster: **<span id="assignment.6.15" lang="nolang" no>Pending</span>**. Está esperando a que el clúster finalice el proceso de registro.

Permanece en la interfaz de Rancher y observa cómo el estado cambia de **<span id="assignment.6.15" lang="nolang" no>Pending</span>** a **<span id="assignment.6.16" lang="nolang" no>Waiting</span>**, y finalmente a **<span id="assignment.6.17" lang="nolang" no>Active</span>**.

Ahora vuelve a **<span id="assignment.2.1" lang="nolang" no>Harvester</span> Clusters**: el clúster aparece en la lista.

Veamos qué más puedes hacer aquí. Haz clic en el  al final de la fila del clúster; se despliega un menú con algunas opciones:

- **<span id="assignment.6.18" lang="nolang" no>Kubectl Shell</span>**: abre una shell conectada al clúster, donde puedes ejecutar comandos kubectl contra él.
- **<span id="assignment.6.12" lang="nolang" no>Download KubeConfig</span>**: lo mismo que ya viste en la interfaz de <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span>.
- **<span id="assignment.6.19" lang="nolang" no>Download YAML</span>**: descarga la definición del clúster en formato YAML; puedes usarla como plantilla para importar nuevos clústeres de forma automatizada (también necesita un paso adicional en la interfaz del clúster).

Por último, haz clic en el nombre del clúster
- te lleva a la interfaz de <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> incrustada dentro de la interfaz de Rancher
- Fíjate en la columna izquierda que aparece una entrada '<span id="assignment.6.13" lang="nolang" no>RBAC</span>' en el menú, podemos controlar quién puede hacer qué en nuestros clústeres.

Con Rancher puedes operar fácilmente varios clústeres desde un solo lugar.

> [!NOTE]
> Hay un rodeo dedicado para SUSE Rancher Prime, ¡siéntete libre de unirte!

⌨️ Tarea 3: Prueba tu acceso administrativo por terminal
===================================================

Pasarás la mayor parte de esta misión en la interfaz, <span id="ch1.task3a"  lang="pt" hist="vertrex-bank">mas um arquiteto sempre verifica o seu acesso de emergência</span>. Haz clic en la pestaña [button label="Cluster Terminal" variant="success"](tab-1) y ejecuta un comando para comprobar que tu conexión al motor de <span id="assignment.2.2" lang="nolang" no>Kubernetes</span> subyacente está activa:

```bash,wrap,run
kubectl --kubeconfig .rodeo/harvester-kubeconfig get VirtualMachine -A
```

Deberías ver la lista de <span id="assignment.6.2" lang="nolang" no>Virtual Machines</span> presentes en cada namespace.

💾 Ejercicio adicional: valida el tejido de almacenamiento distribuido (opcional)
====================================================================

<span id="ch1.bonus1a"  lang="pt" hist="vertrex-bank">Um backend de armazenamento saudável é fundamental para as operações bancárias</span>. <span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span> usa **<span id="assignment.2.7" lang="nolang" no>SUSE Storage</span>** para replicar cada volumen en todo el clúster.

La interfaz de [button label="SUSE Virtualization UI" variant="success"](tab-0) ya muestra información sobre el estado del almacenamiento, pero también es posible acceder al panel de <span id="assignment.2.7" lang="nolang" no>SUSE Storage</span> (<span id="assignment.2.8" lang="nolang" no>Longhorn</span>) habilitando las **Extension developer features**:

1. Haz clic en tu **icono de usuario** en la esquina superior derecha
2. Selecciona **Preferences**
3. Marca **Enable Extension developer features**

Vuelve a **Home**, y en la esquina inferior izquierda haz clic en **<span id="assignment.2.11" lang="nolang" no>Support</span>**.

Ahora verás dos nuevas secciones:

- **<span id="assignment.6.20" lang="nolang" no>Access Embedded</span> Rancher UI**
- **<span id="assignment.6.20" lang="nolang" no>Access Embedded</span> <span id="assignment.2.7" lang="nolang" no>SUSE Storage</span> (<span id="assignment.2.8" lang="nolang" no>Longhorn</span>) UI**

Haz clic en la sección de la **interfaz de <span id="assignment.2.8" lang="nolang" no>Longhorn</span>**.

Te llevará al **<span id="assignment.6.6" lang="nolang" no>Dashboard</span>** de <span id="assignment.2.7" lang="nolang" no>SUSE Storage</span>, todo debería estar en verde.
Si un nodo no fuera programable o un volumen estuviera degradado, <span id="assignment.2.7" lang="nolang" no>SUSE Storage</span> ya estaría reconstruyendo réplicas en otro lugar, pero tú siempre confirmas tu verdad sobre el terreno.

🏋️ Ejercicios adicionales: para los curiosos de la línea de comandos (opcional)
==========================================================

¿Eres nuevo en <span id="assignment.2.2" lang="nolang" no>Kubernetes</span>? **Salta esta parte sin problema**: todo lo que importa está en la interfaz. Si quieres echar un vistazo al funcionamiento interno, ejecuta estas comprobaciones adicionales en [button label="Cluster Terminal" variant="success"](tab-1):

- **Ver el plano de control de <span id="assignment.2.2" lang="nolang" no>Kubernetes</span> y los endpoints de CoreDNS:**

```bash,wrap,run
kubectl cluster-info --kubeconfig .rodeo/harvester-kubeconfig
```

- **Comprueba el estado de los componentes del clúster**: consulta el endpoint de salud del plano de control; cada comprobación (etcd, informers, shutdown hooks) debería indicar `ok`:

```bash,wrap,run
kubectl get --raw='/readyz?verbose' --kubeconfig .rodeo/harvester-kubeconfig
```

- **Confirma que todos los nodos del tejido están listos:**

```bash,wrap,run
kubectl get nodes --kubeconfig .rodeo/harvester-kubeconfig
```

  Todos los nodos deberían mostrar `Ready`.

- **Verifica que los servicios principales de virtualización están en ejecución:**

```bash,wrap,run
kubectl get pods -n harvester-system --kubeconfig .rodeo/harvester-kubeconfig | grep -v Completed
```

  Todos los pods deberían estar `Running`.

- **Confirma la versión exacta de la plataforma que el banco está ejecutando:**

```bash,wrap,run
kubectl --kubeconfig .rodeo/harvester-kubeconfig get settings.harvesterhci.io server-version
```

💼 ¿Por qué es esto importante?
==============================================

- **Un único centro de mando.** Las VMs, el almacenamiento y las redes son visibles desde un único panel, ya no hay que hacer malabares con tres consolas de gestión separadas y tres licencias distintas.
- **Nativo de <span id="assignment.2.2" lang="nolang" no>Kubernetes</span> desde el primer día.** Todo lo que hay en el panel es en realidad un recurso de <span id="assignment.2.2" lang="nolang" no>Kubernetes</span> por debajo. Las habilidades existentes del equipo de contenedores se transfieren directamente, mientras que el equipo de VMs obtiene una interfaz amigable de apuntar y hacer clic.
- **Gestión de flotas y <span id="assignment.6.13" lang="nolang" no>RBAC</span> incluidos.** Rancher Prime es <span id="ch1.why1"  lang="pt" hist="vertrex-bank">pronto para comandar todos os clusters que o banco algum dia vier a executar, com um único login e um único conjunto de regras de acesso.</span>
- **Almacenamiento distribuido de serie.** <span id="assignment.2.7" lang="nolang" no>SUSE Storage</span> replica los datos entre nodos automáticamente.

Una vez que confirmes que el plano de control responde, que el almacenamiento está en buen estado y que tu acceso administrativo está asegurado, estarás listo para adentrarte más en las instalaciones.

Haz clic en **Check** para descender al centro de datos. 🛗

📚 Más información
===================</span>


- [<span id="ch1.intro1.2" lang="nolang" no>SUSE Virtualization</span>: Overview](https://documentation.suse.com/cloudnative/virtualization/latest/en/introduction/overview.html)
- [Hardware and Network Requirements](https://documentation.suse.com/cloudnative/virtualization/latest/en/installation-setup/requirements.html)
- [<span id="assignment.2.2" lang="nolang" no>Kubernetes</span> concepts](https://kubernetes.io/docs/concepts/overview/)
