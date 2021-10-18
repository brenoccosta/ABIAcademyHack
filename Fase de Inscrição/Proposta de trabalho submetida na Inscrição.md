### **Autores** 

BONILLA, Camila Jardim Cavalcante; MCKINNEY, Wes; MEDEIROS, Igor Rafael Guimarães; RAMALHO, Luciano. 



### **Resumo** 

  Este projeto fará um uso misto dos sistemas de recomendação colaborativo e baseado em conteúdo, o primeiro em uma etapa anterior para filtrar os produtos que virão a ser sugeridos pelo segundo método. Utilizou-se a Análise de Pareto para estimar a relevância dos produtos no comércio local e, conforme a classificação de cada produto, recomendar-se-á com dada frequência e similaridade. Para incentivar o consumo de produtos que não fazem parte da cartela oferecida por determinado ponto de venda, um sistema simples de descontos será implementado, tanto para fidelizar o cliente, como para instigá-lo a conhecer novos produtos. Esses serão selecionados tanto a partir de necessidades da companhia, como lançamentos ou queima de estoque, quanto pelas matrizes de colaboração. Ao mesmo tempo, será traçada séries temporais para cada cliente Ambev/ABInBev para identificar seu padrão de consumo, como pelos dias mais frequentes em que se realizam pedidos e seu volume. 



### **Introdução**

  Para evitar o acúmulo de estoque num ponto de venda, cuja ação em cadeia pode prejudicar o fornecimento local, o algoritmo oferecerá maiores descontos quando este entender que já houvera consumo parcial do estoque do mesmo. Para tanto, será efetuada uma análise dos pedidos que levará em conta o dia da semana, o espaçamento entre os eles e o volume de cada pedido. Ao mesmo tempo, será implantado um calendário para identificar possíveis picos de consumo, provocados por eventos festivos, que disseminará o desconto para atender a possível demanda. 

  Após a implementação do sistema de descontos, caso seja notado um aumento inesperado do volume de compras nos dias de maior desconto, o algoritmo deverá considerar a possiblidade de não retratar um aumento do movimento nos dias subsequentes e, sim, uma nova estratégia do lojista de armazenagem de produtos descontados, consumidos a longo prazo. Para corroborar essa análise, o padrão histórico de compras será evocado para verificar se após esse aumento súbito houvera mudança no perfil de compra, tais como os dias frequentes de pedido, seu espaçamento e volume. Como resposta, deverá ser atribuído descontos a outros dias da semana e o comportamento será analisado. Se o padrão de consumo anterior for restaurado, o ponto de venda havia adotado nova estratégia de controle de estoque. Caso contrário, ocorrera uma mudança do público consumidor e o novo padrão deverá ser estudado. 

  O sistema de descontos tem por base os itens mais consumidos, reforçando positivamente a cultura daquele ponto de venda, característico pela oferta de determinada gama de produtos às quais os consumidores se acostumam. Uma vez estabelecida essa mecânica que visa garantir a fidelidade, pode-se iniciar o processo de recomendação cruzada. 

  Conjuntamente aos itens mais consumidos que precisam frequentemente serem repostos, uma cartela de recomendações também descontadas será oferecida, variando os descontos conforme i) necessidade da Ambev de liquidar lotes, ii) perfil do ponto de venda, iii) contexto espacial (padrões de consumo de pontos de venda nas adjacências) e iv) similaridade com pontos de venda não necessariamente próximos espacialmente. 

  Para balancear o algoritmo, em uma fase teste será aplicada a Análise de Pareto (Curva ABC), onde será reservado oitenta porcento das recomendações com descontos para os produtos que fazem parte do núcleo de vendas do estabelecimento (correspondente de vinte por cento dos produtos), sendo utilizado os outros vinte das recomendações para sugestões de expansão do catálogo (oitenta por cento dos produtos). 

  Os itens de expansão dividirão a recomendação entre a) lançamentos Ambev/ABInBev, b) lotes antigos, c) produtos similares, d) produtos contextuais (consumidos na região ou em pontos de venda similares) e e) novidades – produtos que não se enquadram em nenhuma das categorias acima e que não destoem demais do perfil do cliente. 

  Tais recomendações, devido ao pouco espaço reservado a tantas sub-categorias, serão rotativas, obedecendo o princípio de interesse manifesto do cliente por tais produtos. A compra de um produto sem desconto, mas que já pertencera ao rol, deverá indicar prioridade na fila para estimular o ponto de venda a continuar os testes com a nova aquisição. 

  Em outras palavras, vinte por cento das recomendações focalizarão os produtos que correspondem até oitenta porcento do consumo local e serão permanentes. Trinta por cento será destinado a itens similares aos que compõem quinze por cento do giro, enquanto cinquenta por cento será de recomendações que praticamente não integram o costume do ponto de venda por representarem até cinco por cento dos pedidos. A Figura 1 ilustra a situação. 



![img](https://taikai.azureedge.net/YvMaYArvXBKatdaSw84KDfAnQLfWDttBWZBQaLwvW00/rs:fit:800:0:0/aHR0cHM6Ly9zdG9yYWdlLmdvb2dsZWFwaXMuY29tL3RhaWthaS1zdG9yYWdlL2ltYWdlcy9jMjM3MzU5MC0yMzFiLTExZWMtOTEzMi0xOWMzNzkyNzI5MDhDdXJ2YSBBQkMuanBn)

​                                       **Figura 1. Curva ABC**



  Para os fins deste projeto, o algoritmo obedecerá faixas de descontos previamente estabelecidas, ao invés de calculá-los individualmente para cada cliente Ambev/ABInBev, uma vez que o foco é a recomendação de produtos inéditos na cartela de bebidas de cada ponto de venda. 

  Cabe dizer, entretanto, que os descontos serão aplicados para itens separadamente, como para conjuntos dos mesmos. Suponhamos um caso hipotético: um lote de R$100,00 de produtos da categoria A são oferecidos sob desconto de 10%, podendo ser obtidos por R$90,00. Próxima a essa recomendação, haverá um desconto de TANTOS% que inclui o mesmo item da categoria A juntamente de algum(s) item(s) da B ou da C, de forma que o preço unitário do produto principal (A) seja menor que a compra exclusiva daquele. Essa recomendação também deverá oscilar próximo da faixa do desconto individual (R$100,00-90,00), pouco acima ou pouco abaixo a depender do item adicionado ao pacote. Além disso, o volume de produtos não pertencentes à categoria A devem evitar extrapolar o consumo médio histórico destes para que seja atraente a promoção, a fim de não correr o risco de se estocar itens de pouca demanda e aniquilar o interesse por uma experiência não exitosa.  

  De qualquer modo, produtos A, B e C o são por pertencerem à cartela de ofertas de dado ponto de venda, embora deva-se considerar que o exemplo acima inclua itens novos. A diversidade das recomendações, portanto, obedecerão ao seguinte princípio: quão menos demanda houver por dado item, menor a similaridade buscada para recomendar-se. Assim, em última instância um produto novo a ser recomendado deverá ter, no mínimo, um aspecto em comum com qualquer item pedido pelo ponto de venda, para evitar que se recomende algo fora da realidade. Ao mesmo tempo que o mínimo seja uma característica partilhada, buscar-se-á transformá-lo, justamente, no máximo, conforme o gradiente da Curva ABC. De certa forma, tal recomendação configura-se ao mesmo tempo um convite à expansão da lista de produtos oferecidos, quanto uma proposta de substituição por uma potencial descoberta. 

### **Metodologia** 

  Este projeto será desenvolvido em Python e tem, como guia, estes dois livros: Python fluente: Programação clara, concisa e eficaz (2015), de Luciano Ramalho, e Python para análise de dados: Tratamento de dados com Pandas, NumPy e IPython (2019), de Wes McKinney. 

  Também foi consultado – e continuarão sendo – a dissertação de Camila Bonilla Uma introdução aos sistemas de recomendação: modelos matemáticos, algoritmos e aplicações (2020) e a monografia de Igor Guimarães Estudo sobre Sistemas de Recomendação Colaborativos (2013). 

  Outras referências serão buscadas conforme o andamento do projeto, especialmente sobre a Análise de Pareto e casos corporativos; sugestões são bem-vindas. 

  Para o desenvolvimento do projeto iremos nos servir de bancos de dados fictícios elaborados pela equipe, como também os fornecidos pela ABInBev, a fim de simular e treinar o algoritmo proposto, incluindo os casos de exceção. 

  Buscar-se-á aplicar os sistemas de filtragem colaborativa e baseada em conteúdo consecutivamente. A colaborativa será usada em primeira instância para situar o ponto de venda no contexto espacial e com outros clientes Ambev/ABInBev não necessariamente próximos e que apresentem padrão de consumo similar, porém que utilizem uma cartela de produtos distinta. 

  Nessa etapa ponderar-se-á os itens conforme sua posição na Curva ABC de cada estabelecimento. A média dessa ponderação será aplicada na matriz individual de um ponto de venda específico na etapa subsequente, i.e., a da recomendação por conteúdo. Com esse método espera-se não criar uma cartela de opções baseada apenas em itens muito similares, mas também não avulsos à realidade local. Em outras palavras, espera-se sugerir itens das categorias A, B e C uns para os outros. 

  A filtragem baseada em conteúdo conterá, então, os itens pedidos pelo cliente, os similares utilizados na região ordenados conforme sua posição no giro dos estabelecimentos próximos e um espaço reservado para recomendações expressas da Ambev/ABInBev, como o caso de queima de estoque ou lançamento de novo produto, que não poderiam ser especificamente recomendados pelo sistema por nenhum dos mecanismos apontados. 

  As métricas utilizadas na matriz colaborativa será o volume de pedidos por mês. Na de conteúdo, além das características próprias das cervejas, a frequência de sua requisição, bem como também o volume de pedidos. 

  Aliada a essa tabela haverá uma série temporal dos pedidos para identificar o padrão de consumo apresentado no início do projeto, tais como os dias mais frequentes da semana em que se faz o pedido, média do espaçamento entre os mesmos, e o volume do pedido, que inclui diversos itens. 

  Não foi realizado levantamento estatístico prévio e por não se conhecer a gama de bebidas oferecidas nos pontos de venda clientes da Ambev/ABInBev, não se pode mensurar os resultados esperados, embora o objetivo seja claro e o caminho, promissor. 



### **Referências** 

**Bibliográficas:** 

BONILLA, Camila Jardim Cavalcante. Uma introdução aos sistemas de recomendação: modelos matemáticos, algoritmos e aplicações. Campinas, São Paulo: Editora Unicamp, 2020. 

MCKINNEY, Wes. Python para análise de dados: Tratamento de dados com Pandas, NumPy e IPython. Brasil, Novatec Editora, 2019. 

MEDEIROS, Igor Rafael Guimarães. Estudo sobre Sistemas de Recomendação Colaborativos. Recife, Universidade Federal de Pernambuco, 2013. 

RAMALHO, Luciano. Python fluente: Programação clara, concisa e eficaz. Brasil, Novatec Editora, 2015. 



**Imagem:**

https://www.granatum.com.br/estoque/img/posts/granatum-estoque-grafico-a-b-c.jpg