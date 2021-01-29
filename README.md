#Intenção
As máscaras de luminosidade são basicamente máscaras de camada que são construídas em torno de tons específicos em uma imagem. Eles são derivados dos próprios dados da imagem e focados em uma faixa específica de valores tonais. A vantagem de usar esses tipos de máscaras é que, ao focar em faixas tonais, a própria máscara é auto-enevoada, ajudando a evitar problemas com mesclagens e transições difíceis.

Ser capaz de modificar seletivamente uma imagem com base em regiões tonais específicas pode ser um método muito poderoso de edição. Precisa iluminar os tons médios em uma imagem sem afetar sombras ou realces? Quer dividir o tom de uma imagem com cores diferentes? Precisa aumentar o contraste apenas nas sombras mais escuras? Tudo isso é trivialmente fácil quando você começa a considerar sua imagem como uma coleção de faixas tonais.

Este tutorial presumirá que você já está familiarizado com as máscaras de camada. Se não (ou você quer apenas melhorar), eu recomendo que você leia o tutorial Layer Masks primeiro.

Para este tutorial, usarei esta imagem do West Arctic National Parklands:

<https://www.gimp.org/tutorials/Luminosity_Masks/Mountains-Full-Size.jpg>

Depois de passar por este tutorial, geraremos canais no GIMP correspondentes a essas seis regiões de luminosidade diferentes na imagem:

<https://www.gimp.org/tutorials/Luminosity_Masks/All-Masks.jpg>

#Criando as Máscaras
Para começar a criar as máscaras, primeiro precisamos obter uma representação de luminosidade da imagem. Isso é facilmente obtido duplicando a camada base e removendo a saturação usando Luminosity como opção de conversão.

#Duplique a camada de base
Por meio dos menus ou clicando com o botão direito do mouse na camada de base na caixa de diálogo Camada:

>Camada → Camada Duplicada

<https://www.gimp.org/tutorials/Luminosity_Masks/Layer-Duplicate.png>

#Remova a saturação da camada duplicada
Agora remova a saturação da camada duplicada usando Luminosidade como método:

>Cores → Remover saturação

Esta cópia dessaturada de sua imagem colorida representa o canal “Luzes”. Agora queremos criar um novo canal baseado nesta camada.

#Crie um novo canal “Luzes”
A maneira mais fácil de fazer isso é por meio da caixa de diálogo Canais . Caso não o veja, você pode abri-lo acessando:

>Windows → Diálogos encaixáveis → Canais

<https://www.gimp.org/tutorials/Luminosity_Masks/Channels-Dialog.png>

Na metade superior desta janela, você verá uma entrada para cada canal em sua imagem (Vermelho, Verde, Azul e Alfa). Na parte inferior, haverá uma lista de todos os canais que você definiu anteriormente.

Para criar um novo canal que se tornará seu canal de “Luzes”, arraste qualquer um dos canais RGB para a janela inferior (não importa qual - todos eles têm os mesmos dados devido à operação de dessaturação).

Agora renomeie este canal para algo significativo (como “ L ” por exemplo!), Clicando duas vezes em seu nome (no meu caso é chamado de “Blue Channel Copy”) e inserindo um novo.

Isso agora nos dá nosso canal "Luzes", L :

<https://www.gimp.org/tutorials/Luminosity_Masks/L-Channel.png>

Com o canal “Lights” criado, podemos usá-lo para criar o inverso, o canal “Darks”.

#Crie um novo canal "Darks"
Para criar o canal “Darks”, ajuda perceber que ele deve ser simplesmente o inverso do canal “Lights”. Podemos obter essa seleção por meio de algumas operações simples.

Basicamente, vamos selecionar a imagem inteira e, em seguida, subtrair o canal “Luzes” dela. O que resta deve ser nosso novo canal “Darks”.

##Selecione a imagem inteira
Primeiro, selecione a imagem inteira:

>Select → All

Lembre-se de que você deve ver as “formigas marchando” ao redor de sua seleção - neste caso, a imagem inteira.

##Subtraia o canal "Luzes"
Com a imagem inteira selecionada, só temos que subtrair o canal “Luzes”. Na caixa de diálogo Canais , apenas clique com o botão direito no canal “Luzes” e escolha “ Subtrair da Seleção ”:

<https://www.gimp.org/tutorials/Luminosity_Masks/L-Channel-Subtract.png>

Agora você verá uma nova seleção em sua imagem. Esta seleção representa o inverso do canal "Luzes" ...


##Crie um novo canal "Darks" a partir da seleção
Agora só precisamos salvar a seleção atual em um novo canal (que chamaremos de… Darks!). Para salvar a seleção atual em um canal, podemos apenas usar:

>Selecione → Salvar no canal

Isso criará um novo canal na caixa de diálogo Canal (provavelmente denominado “Cópia da máscara de seleção”). Para dar a ele um nome melhor, basta clicar duas vezes no nome para renomeá-lo. Vamos escolher algo emocionante, como “ D ”!

##Crie máscaras ainda mais escuras
Neste ponto, você terá um canal “Luzes” e um “Escuros”. Se você quiser criar alguns canais que visam regiões cada vez mais escuras da imagem, você pode subtrair o canal “Luzes” novamente (desta vez da seleção atual, “Escuras”, em oposição à imagem inteira).

Depois de subtrair o canal "Luzes" novamente, não se esqueça de salvar a seleção em um novo canal (e nomeá-lo apropriadamente - eu gosto de nomear máscaras subsequentes como " DD " neste caso - se eu subtrair novamente, Eu chamaria o próximo de “ DDD ” e assim por diante…).

Normalmente farei 3 níveis de canais “Darks”: D , DD e DDD :

<https://www.gimp.org/tutorials/Luminosity_Masks/D-Channels.png>

Aqui está a aparência dos três canais diferentes de Darks:

<https://www.gimp.org/tutorials/Luminosity_Masks/Darks-All.jpg>

#Crie as máscaras mais claras
Neste ponto, temos um canal “Lights” e três canais “Darks”. Agora podemos ir em frente e criar mais dois canais de “Luzes”, para atingir tons mais claros e mais claros.

O processo é idêntico à criação dos canais mais escuros, apenas ao contrário.

##Canal de luzes para seleção
Para começar, ative o canal "Luzes" como uma seleção (clique com o botão direito no canal "Luzes"):

<https://www.gimp.org/tutorials/Luminosity_Masks/L-Channel-Activate.png>

Com o canal “Lights” como uma seleção, agora tudo o que temos a fazer é subtrair o canal “Darks” dele. Em seguida, salve essa seleção como um novo canal (que se tornará nosso canal " LL " e assim por diante ...):

<https://www.gimp.org/tutorials/Luminosity_Masks/D-Subtract.png>

Para obter um canal ainda mais claro, você pode subtrair D mais uma vez da seleção até agora.

Aqui estão os três canais, começando com L até LLL :

<https://www.gimp.org/tutorials/Luminosity_Masks/Lights-All.jpg>

#Canais de tons médios
Neste ponto, temos 6 novos canais, três para cada um para tons claros e escuros:

<https://www.gimp.org/tutorials/Luminosity_Masks/L+D.png>

Agora podemos gerar nossos canais de meio-tom a partir deles.

O conceito de geração de tons médios é relativamente simples - vamos apenas cruzar canais claros e escuros para produzir o que resta - tons médios.

## Canais de intersecção para tons médios
Para começar, primeiro selecione o canal “L” e defina-o para a seleção atual (como acima). Clique com o botão direito → Canal para seleção.

Em seguida, clique com o botão direito do mouse no canal “D” e escolha “Cruzar com a seleção”.

Você provavelmente não verá nenhuma seleção ativa em sua imagem, mas ela está lá, eu prometo. Agora como antes, basta salvar a seleção em um canal:

>Selecione → Salvar no canal

Dê a ele um nome legal. Sayyy, “ M ”? :)

Você pode repetir para cada um dos outros níveis, criando um MM e MMM se desejar (usando LL / DD e LLL / DDD  respectivamente).

Agora, lembre-se de que os canais de tons médios têm como objetivo isolar os valores médios como uma máscara, para que possam parecer um pouco estranhos à primeira vista. Esta é a aparência da máscara básica de tons médios:

<https://www.gimp.org/tutorials/Luminosity_Masks/Mid.jpg>

Lembre-se de que os tons de preto nesta máscara representam transparência total para a camada abaixo, enquanto o branco representa opacidade total, da camada associada.

#Usando as máscaras
A ideia básica por trás da criação desses canais é que agora você pode mascarar intervalos tonais específicos em suas imagens, e a máscara será auto-enevoada (devido a como os criamos). Portanto, agora podemos isolar tons específicos na imagem para manipulação.

Anteriormente , eu havia mostrado como isso poderia ser usado para fazer alguns ajustes simples de divisão de tons de uma imagem. Nesse caso, trabalhei em uma imagem em P&B e a colori. Aqui farei o mesmo com a nossa imagem em que trabalhamos até agora ...

##Tonificação dividida
Usando a imagem que tenho trabalhado até agora, temos a camada de base para começar:

<https://www.gimp.org/tutorials/Luminosity_Masks/Split-Base.png>

##Criar duplicatas
Vamos querer duas duplicatas dessa camada de base. Um para tonificar os valores mais claros e outro para tonificar os mais escuros. Começaremos considerando os tons escuros primeiro. Duplique a camada de base:

>Camada → Camada Duplicada

Em seguida, renomeie a cópia para algo descritivo. No meu exemplo, chamarei essa camada de “Escura” (original, eu sei):

<https://www.gimp.org/tutorials/Luminosity_Masks/Split-Dark.png>

##adicionar uma máscara
Agora podemos adicionar uma máscara de camada a esta camada. Você pode clicar com o botão direito do mouse na camada e escolher “Adicionar máscara de camada” ou pode navegar pelos menus:

>Camada → Máscara → Adicionar máscara de camada

Em seguida, você verá opções sobre como inicializar a máscara. Você deseja inicializar a máscara de camada para: “Canal” e, em seguida, escolha uma de suas máscaras de luminosidade no menu suspenso. No meu caso, usarei a máscara DD que criamos anteriormente:

<https://www.gimp.org/tutorials/Luminosity_Masks/AddLayerMask.png>

##Ajuste a camada

<https://www.gimp.org/tutorials/Luminosity_Masks/Dark-Active.png>

Agora você terá uma camada escura com uma máscara DD que restringirá qualquer modificação que você fizer a esta camada para aplicar apenas aos tons mais escuros.

Certifique-se de selecionar a camada, e não a máscara, clicando nela (você verá um contorno branco ao redor da camada ativa). Caso contrário, qualquer operação que você fizer pode acidentalmente ser aplicada à máscara, e não à camada.

Neste ponto, agora queremos modificar as cores desta camada de alguma forma. Existem maneiras literalmente infinitas de abordar isso, limitadas apenas por sua criatividade e imaginação. Para este exemplo, vamos tonificar a imagem com uma cor azul esverdeado / azul legal (como antes), que combinada com a máscara de camada DD , irá restringi-la para modificar apenas os tons mais escuros.

Portanto, usarei a opção Colorir para tonificar toda a camada com uma nova cor:

>Cores → Colorir

Para obter uma cor azul-petróleo, puxarei o controle deslizante de matiz para cerca de 200:

<https://www.gimp.org/tutorials/Luminosity_Masks/Colorize-200.png>

Agora, preste atenção ao que está acontecendo na tela da sua imagem neste momento. Arraste o controle deslizante Matiz e veja como ele altera as cores da imagem. Observe especialmente que as mudanças de cor serão restritas aos tons mais escuros, graças ao uso da máscara DD !

Para ilustrar, aqui estão quatro imagens em que o matiz foi alterado em cada uma. Observe como as mudanças de cor são restringidas a tons mais escuros devido à máscara DD estar ativa:

<https://www.gimp.org/tutorials/Luminosity_Masks/All-Hues.jpg>

Então, depois de escolher um novo Hue de 200 para minha camada, devo ver isto:

<https://www.gimp.org/tutorials/Luminosity_Masks/Dark-Tinted.png>

##Repita para tons claros
Agora basta repetir os passos acima, mas desta vez para os tons claros. Portanto, duplique a camada base novamente e adicione uma máscara de camada, mas desta vez tente usar o canal LL como máscara.

Para os tons mais claros, escolhi um matiz de cerca de 25 (mais laranja do que azul):

No final, aqui estão os resultados que alcancei:

<https://www.gimp.org/tutorials/Luminosity_Masks/Mountains-split.jpg>

Em comparação com o original com que começamos:

<https://www.gimp.org/tutorials/Luminosity_Masks/Mountains.jpg>

O verdadeiro poder aqui vem da experimentação. Eu o encorajo a tentar usar uma máscara diferente para restringir as mudanças a áreas diferentes (experimente o LLL, por exemplo). Você também pode ajustar a opacidade das camadas agora para modificar a intensidade com que os tons das cores afetarão essas áreas também. Toque!

#Máscaras de tons médios
As máscaras de meios-tons eram muito interessantes para mim. No artigo original de Tony, ele mencionou o quanto adorava usá-los para fornecer um bom aumento de contraste e saturação na imagem. Bem, ele está certo. Certamente faz isso! (Ele também sente que é semelhante a filmar a imagem em Velvia).

<https://www.gimp.org/tutorials/Luminosity_Masks/Mid-Layer.png>

Vamos dar uma olhada.

Excluí as camadas do meu exercício de divisão de tons acima e estou de volta apenas à camada da imagem de base novamente.

Para experimentar a máscara de tons médios, precisamos apenas duplicar a camada de base e aplicar uma máscara de camada a ela.

Desta vez, vou escolher a máscara básica de tons médios M.

O que é interessante sobre o uso dessa máscara é que você pode usar modificações de curvas bastante agressivas nela e ainda evitar que a imagem exploda. Estamos visando apenas os meios-tons.

Para ilustrar, vou aplicar uma compressão bastante agressiva às curvas usando Ajustar curvas de cor :

>Cores → Curvas

Quando digo agressivo, aqui está o que me refiro:

<https://www.gimp.org/tutorials/Luminosity_Masks/Mid-Curve.png>

Aqui está o efeito que tem na imagem ao usar a máscara de tons médios M :

<https://www.gimp.org/tutorials/Luminosity_Masks/Mid-Boost.jpg>

Em comparação com o original com que começamos:

<https://www.gimp.org/tutorials/Luminosity_Masks/Mountains.jpg>

Como você pode ver, há um aumento no contraste na imagem, bem como um pequeno aumento na saturação. Você não precisa se preocupar em estourar realces ou perder detalhes de sombra, porque a máscara não permitirá que você modifique esses valores.

##Mais amostras da máscara de tons médios em uso
<https://www.gimp.org/tutorials/Luminosity_Masks/stignygaard-3654106828-original.jpg>

<https://www.gimp.org/tutorials/Luminosity_Masks/stignygaard-3654106828.png>

#Em conclusão
Esta é apenas mais uma ferramenta em nossa caixa de ferramentas mental de manipulação de imagens, mas é uma ferramenta muito poderosa. Ao considerar suas imagens, agora você pode olhá-las em função da luminosidade - com uma maneira simples e poderosa de isolar e direcionar tons específicos para modificação.

Como sempre, encorajo você a experimentar e jogar!
















































