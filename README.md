# pfsense-squid-cache-dynamics
 PFsense cache dynamics 

Lista de padrões dynamic_refresh para usar com squid3 e pfsense, tive dificuldade em encontrar coisas online, então pensei em fazer um repositório github colaborativo apenas para esse propósito.

Esta lista foi projetada diretamente para ser usada com o pacote squid pfsense, porém esses padrões de atualização também devem funcionar sem usar o pacote específico do pfsense.
Não posso confirmar se eles funcionarão com um pacote squid em outras distribuições, no entanto devem ter a mesma formatação, então sinta-se à vontade para tentar se assim o desejar.

Após o Pacote squid instalado
Para usar o padrão de atualização personalizado com squid no pfsense navegue até
services -> squid proxy server -> local cache

Deixo as configs do meu server de armazenamento porem pode customizar o tamanho conforme seu hardware

Squid Hard Disk Cache Settings
Hard Disk Cache Size  300000
Hard Disk Cache System  ufs
Level 1 Directories   64
Limpe o cache de disco AGORA ou talvez terá problemas no cache

Squid Memory Cache Settings
Memory Cache Size 128

os demais mantive padrão !!

Agora Role até embaixo em Dynamic and Update Content
Em Dynamic and Update Content, habilite o Cache Dynamic Content
Em Custom refresh_patterns cole o conteúdo squid refresh_patterns na caixa de dialogo ao lado
Salvar

Não pode esquecer na aba Traffic Mgmt -> Squid Transfer Quick Abort Setting
Role até embaixo na opção Finish transfer if less than x KB remaining
adicione -1

Para verifica se está funcionando vá até a aba realtime note esses status
sinal que ele armazenou em cache e mandou direto para o cliente

TCP_HIT/200
TCP_MEM_HIT/200

Às vezes, o cache do squid precisa ser redefinido se houver erros. https://docs.netgate.com/pfsense/en/latest/troubleshooting/squid.html

squid -k shutdown rm -rf /var/squid/cache squid -z squid squid -k parse (veja se há erros no refresh_patterns customizado).

Nota: Normalmente, o conteúdo https não pode ser armazenado em cache porque o conteúdo é criptografado e, portanto, não pode ser armazenado em cache. Você pode tentar armazenar em cache o conteúdo https usando o ataque ssl a man in the middle, mas pode ter problemas de conexão.

