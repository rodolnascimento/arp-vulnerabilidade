Universidade Federal do Maranhão

**Segurança em Redes**

## Objetivo 
O objetivo desse laboratório é realizar um ataque de homem do meio e demonstrar as vulnerabilidades existente e consequências desse tipo de ataque.

![Topologia de Rede][1]

---
## Exercício 2 -- ARP *Ataque de Homem do meio*

Em cada computador existe uma tabela ARP (*Address Resolution Protocol*) que contém associações entre endereços IP e endereços MAC para poder saber o próximo salto para qual a o tráfego pode ser encaminhado.
Esta tabela é consultada quando se quer comunicar para um determinado endereço IP e é constantemente atualizada.

Um ataque de ARP *spoofing* ou *poisoning* consiste em alterar a tabela ARP no computador de uma vítima e depois interceptar as suas comunicações.
O objetivo do ataque pode ser observar a comunicação ou realizar um ataque de *homem do meio*.

1.  No *atacante* execute o comando `ping -c 1 <IP pc1>`.
Veja o conteúdo da tabela ARP no *atacante* executando `arp -a`.
Veja que o endereço MAC está associado ao endereço IP do pc1. em seguida tente a conexão para o pc2

2.  Obtenha o endereço MAC do *atacante* executando o comando `ifconfig`.

3.  Descubra a corespondência entre cada endereço MAC e cada endereço
    IP para os três dispositivos.

4.  No *pc1* e no *pc2* faça *ping* um para o outro e confirme que as tabelas
    ARP têm os mapeamentos entre endereço IP e endereço MAC (`arp -a`).

5.  A tabela ARP tem um papel importante: quando um computador pretende enviar um pacote para um endereço IP, obtém na sua tabela ARP o endereço MAC correspondente a esse endereço IP ou ao endereço IP do *gateway* que encaminhará o pacote para outra rede.
O ataque vai consistir em usar o *nemesis* para fazer ARP *spoofing*.
Eexecute o comando abaixo no *atacante*:

```bash
nemesis arp -v -S <IP do pc2> -D <IP do pc1> -h <MAC do atacante> -m <MAC do pc1>
```

6.  O resultado do ataque será visualizado na tabela ARP, execute o seguinte comando no *pc1*: `arp -a`. 
observe que este ataque não é permanente, o comando acima deve ser repetido periodicamente para a alteração permanecer pois a tabela arp é atualizada a cada 10 minutos.

7.  Observe do resultado, execute o comando `tcpdump -e -i eth0` no *atacante* e no *pc2*.
No *pc1*, execute o comando `ping <IP do pc2>` e observe que os pacotes enviados pelo comando *ping* são redirecionados para o *atacante*.

----


## Referências

- *Kathará*, [https://github.com/KatharaFramework/Kathara/wiki]

  [1]: media/image.png


