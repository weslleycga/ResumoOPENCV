Vamos pôr as mãos na massa! 🧪 No Google Colab, a forma mais prática de ver isso é comparando a mesma imagem carregada pelo OpenCV em dois formatos: o original (**BGR**) e o convertido (**RGB**).

Aqui está o plano para o nosso código inicial:

1. **Importar as ferramentas:** Precisamos do `cv2` (OpenCV) e do `matplotlib.pyplot` (para mostrar a imagem).
    
2. **Carregar uma imagem:** Vamos usar uma imagem de exemplo da internet.
    
3. **Visualizar a diferença:** Vamos mostrar a imagem antes e depois da conversão.
    


Abaixo está o código utilizado:

Python

```Python
import cv2
import matplotlib.pyplot as plt
import urllib.request #Utilizado para habilitar a função de pegar a imagem pelo url
import numpy as np

# 1. Descarregar uma imagem de teste (um gatinho, por exemplo)
url = 'https://upload.wikimedia.org/wikipedia/commons/thumb/3/3a/Cat03.jpg/600px-Cat03.jpg'
urllib.request.urlretrieve(url, 'gato.jpg')

# 2. Ler a imagem com OpenCV (Formato BGR)
img_bgr = cv2.imread('gato.jpg')

# 3. Converter para RGB
img_rgb = cv2.cvtColor(img_bgr, cv2.COLOR_BGR2RGB)

# 4. Mostrar as duas lado a lado
plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(img_bgr) # Aqui o Matplotlib tenta ler BGR como se fosse RGB
plt.title('Visualização do BGR original')

plt.subplot(1, 2, 2)
plt.imshow(img_rgb) # Aqui as cores devem estar corretas
plt.title('Visualização após cvtColor (RGB)')

plt.show()

```

```Python
''' Esse trecho final é o responsável por "pintar" o resultado na sua tela e organizar a apresentação. 🖼️ Vamos decompor a lógica por trás de cada linha para entender como o **Matplotlib** (o `plt`) gerencia o espaço de visualização:'''

1. plt.subplot(1, 2, 2) ''': Imagine que você tem uma folha de papel em branco. Esse comando diz ao computador: "Divida esta folha em **1 linha** e **2 colunas** (como se fosse uma tabela 1x2). Agora, selecione o **segundo** espaço para eu desenhar". É por isso que a imagem aparece à direita. 📍'''
    
2. plt.imshow(img_rgb) """ Este é o comando de "exibição". Ele pega a matriz de números que chamamos de `img_rgb` (aquela que já convertemos para a ordem correta de cores) e a projeta no espaço selecionado. 🎨"""
    
3. plt.title(...) ''' Simplesmente coloca uma etiqueta ou título acima da imagem selecionada para facilitar a identificação do que estamos vendo. 🏷️'''
    
4. plt.show() '''Sem este comando, o Matplotlib pode apenas "preparar" os desenhos na memória, mas não mostrá-los. O `show()` é o comando final que abre a janela ou exibe os gráficos no seu notebook. 🚀'''
    

```

O resultado será dessa forma:

![[Pasted image 20260422170621.png]]

Repara bem na primeira imagem (a da esquerda) que o Colab gerou. **Que cores é que te parecem mais estranhas ou "invertidas" nessa imagem em comparação com a da direita?** 🎨

Na imagem da esquerda, as cores que costumam saltar à vista como "erradas" são o **azul** e o **vermelho** 🔴🔵.

Como o OpenCV lê os dados na ordem **BGR** (Blue-Green-Red), mas o Matplotlib tenta exibi-los como **RGB** (Red-Green-Blue), acontece uma troca direta nos canais das extremidades:

- O que deveria ser **Vermelho** (canal 0 no RGB) acaba a mostrar os dados do canal **Azul** (canal 0 no BGR).
    
- O canal **Verde** (canal 1) permanece no meio em ambos, por isso costuma ser o mais "estável" visualmente.
    

