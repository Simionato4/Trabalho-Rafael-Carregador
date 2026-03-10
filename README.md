# Trabalho-Rafael-Carregador-11/03/2026
🔌 Carregador de Celular — Fonte Regulada 12V com 7812

Projeto acadêmico desenvolvido para a disciplina de Sistemas Embarcados
Curso de Sistemas de Informação — Unimater, Pato Branco/PR
Autor: Gabriel Zanesco Simionato

Introdução
Este projeto consiste no desenvolvimento de um carregador de celular baseado em fonte de alimentação linear regulada de 12V, utilizando o regulador integrado 7812. Todo o projeto foi desenvolvido no software Proteus 8 Professional, contemplando três etapas:

Esquemático eletrônico (ISIS)
Layout da placa de circuito impresso — PCB (ARES)
Visualização 3D da placa montada

O circuito recebe tensão AC proveniente do secundário de um transformador externo, realiza a retificação, filtragem e regulação, entregando na saída 12V DC estável com indicação visual de funcionamento via LED.

Objetivo
Demonstrar na prática o funcionamento de uma fonte linear regulada, percorrendo todas as etapas do processo:

Entrada de tensão alternada (AC)
Retificação em onda completa
Filtragem e redução de ripple
Regulação da tensão de saída
Indicação de funcionamento por LED
Disponibilização da tensão regulada na saída


Componentes Utilizados
ReferênciaComponenteValorFunçãoJ2SIL-100-02—Conector de entrada — secundário do transformador (AC)BR1BRIDGE—Ponte retificadora — converte AC em DC pulsanteC1CAP-ELEC1000µFCapacitor de filtragem principal — reduz o rippleC2CAP100nFCapacitor de desacoplamento — filtra ruídos de alta frequência na entradaU1781212VRegulador linear de tensão — estabiliza a saída em 12VC3CAP1nFCapacitor de estabilização da saída do reguladorR1MINRES10R10ΩResistor limitador de corrente do LEDD1LED—Indicador visual de funcionamentoJ1CONN-SIL2—Conector de saída — fornece 12V DC regulado

Esquemático do Circuito

(Inserir imagem do esquemático aqui — imagens/esquematico.png)

O esquemático foi desenvolvido no ISIS do Proteus 8 e apresenta todas as conexões e componentes do circuito. Pontos importantes:

Todas as conexões seguem o fluxo: Entrada AC → Retificação → Filtragem → Regulação → Saída
Os capacitores C2 e C3 estão conectados em paralelo na linha de alimentação, não em série
O LED indicador está conectado em série com R1, garantindo limitação de corrente


Funcionamento do Circuito
1. Entrada de Tensão AC — J2 (SIL-100-02)
O conector J2 recebe os dois terminais do secundário do transformador externo. O transformador, não presente na placa, é responsável por reduzir a tensão da rede elétrica (220V) para um nível adequado à entrada do circuito retificador — tipicamente entre 14V e 18V AC.

2. Retificação — BR1 (BRIDGE)
A tensão AC proveniente de J2 é aplicada aos terminais ~ da ponte retificadora BR1. Internamente, a ponte é composta por quatro diodos dispostos em configuração de ponte de Graetz, realizando a retificação em onda completa.

Nos semiciclos positivos, dois diodos conduzem e a tensão aparece positiva na saída
Nos semiciclos negativos, os outros dois diodos conduzem, mantendo a polaridade positiva na saída

O resultado é uma tensão DC pulsante, com frequência de 120Hz (dobro da rede elétrica).

3. Filtragem — C1 (1000µF) e C2 (100nF)
A tensão DC pulsante ainda apresenta variações chamadas de ripple. Para suavizá-la:

C1 (1000µF) — capacitor eletrolítico de grande valor que carrega durante os picos de tensão e descarrega nos vales, suavizando significativamente a tensão
C2 (100nF) — capacitor cerâmico responsável pelo desacoplamento de ruídos de alta frequência que o C1 não consegue eliminar por sua limitação de resposta

Após essa etapa, a tensão já está muito mais próxima de uma tensão contínua estável.

4. Regulação — U1 (7812)
O coração do circuito é o regulador linear 7812. Ele recebe a tensão filtrada no pino de entrada e mantém a saída fixada em 12V DC, independentemente de pequenas variações na entrada ou na carga.
PinoNomeFunção1VIEntrada de tensão (>14V recomendado)2GNDTerra3VOSaída regulada — 12V DC
O capacitor C3 (1nF) conectado à saída do regulador melhora a estabilidade, suprimindo oscilações e ruídos de alta frequência na saída.

5. Indicador de Funcionamento — D1 (LED) + R1 (10Ω)
O LED D1 está conectado entre a saída regulada (12V) e o GND, em série com o resistor R1 de 10Ω.

Quando a fonte está energizada e funcionando corretamente, o LED acende
O R1 limita a corrente que atravessa o LED, protegendo-o de danos por sobrecorrente


6. Saída — J1 (CONN-SIL2)
O conector J1 disponibiliza a tensão regulada ao dispositivo externo:
PinoSinal1+12V DC regulado2GND

Layout da PCB

(Inserir imagem do PCB aqui — imagens/pcb-layout.png)

A placa foi projetada com as seguintes especificações:

Dimensões: 80mm x 40mm
Camadas de trilha: somente Bottom Layer (parte inferior da placa)
Identificação: nome do autor na silkscreen da placa

O roteamento foi organizado seguindo o fluxo lógico do circuito, da esquerda (entrada AC) para a direita (saída DC), facilitando a compreensão e montagem.

Visualização 3D

(Inserir imagens 3D aqui — imagens/3d-frente.png, imagens/3d-traseira.png, imagens/3d-lateral.png)

A visualização 3D do Proteus permite observar a disposição real dos componentes após a fabricação da placa, conferindo altura, posicionamento e encapsulamento de cada componente.

Software Utilizado
Proteus 8 Professional — Labcenter Electronics
FerramentaUsoISIS (Schematic Capture)Desenho do esquemáticoARES (PCB Layout)Roteamento da placa PCB3D ViewerVisualização tridimensional da placa

Considerações Técnicas

O regulador 7812 dissipa calor em forma de energia — para aplicações com correntes elevadas, recomenda-se o uso de um dissipador de calor (heatsink) acoplado ao componente
A tensão de entrada deve ser no mínimo 14V AC no secundário do transformador para garantir regulação correta após a retificação e queda interna do 7812
O circuito foi projetado para fins didáticos e de simulação no Proteus; para uso real, devem ser observadas as normas de segurança elétrica aplicáveis
A configuração com PRIMITIVE=NULL no J1 foi necessária para que o Proteus simulasse o circuito sem erro, já que conectores físicos não possuem modelo SPICE


Projeto desenvolvido para fins acadêmicos — Sistemas Embarcados — Unimater Pato Branco/PR
