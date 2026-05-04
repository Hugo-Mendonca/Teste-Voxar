🚀 Classificação de Pavimentos (Road Type Classification)
Este projeto foi desenvolvido como um teste técnico para a Voxar Labs, com o objetivo de classificar diferentes tipos de pavimentos (Asfalto, Paralelepípedo e Terra) utilizando técnicas de Deep Learning.

📊 1. Análise Exploratória (EDA)
Antes da modelagem, identifiquei desafios críticos no dataset:

Desbalanceamento Severo: A classe de asfalto domina o conjunto de dados.

Sobreposição de Brilho: Alta similaridade entre classes noturnas e diurnas.

Dependência de Textura: A diferenciação baseia-se primariamente em texturas e gradientes locais.

🏗️ 2. Metodologia e Arquiteturas
Para validar a melhor abordagem, comparei dois caminhos distintos:

ResNet18 (Transfer Learning): Utilizando pesos pré-treinados do ImageNet.

SimpleCNN (Do Zero): Uma rede rasa para servir de baseline e testar a resistência ao balanceamento.

Frameworks: PyTorch e Lightning AI.

🧪 3. Experimentos de Balanceamento
Testei as estratégias de Oversampling e Class Weights para mitigar o desbalanceamento.

📉 O fenômeno na ResNet18
O balanceamento causou uma queda brusca de desempenho explicada por:

Overfitting por Memorização: Repetição de poucas imagens levou à memorização de pixels em vez de padrões reais.

Instabilidade do Gradiente: Punições elevadas via pesos de classe geraram "nervosismo" na rede, tornando-a suscetível a ruídos.

Esquecimento Catastrófico: O foco obsessivo na classe minoritária "poluiu" o conhecimento prévio da rede sobre asfalto.

⚖️ O comportamento na SimpleCNN
O balanceamento foi praticamente inefetivo. Devido à sua arquitetura rasa (Alto Viés), a rede atingiu um teto de saturação e ignorou as nuances extras, agindo de forma generalista e "teimosa".

🌗 4. O Teste da Feature de Contraste
Testei a inclusão do contraste como feature adicional na melhor rede (ResNet18 desbalanceada).

Resultado: O desempenho piorou. O contraste funcionou como um ruído, descaracterizando a classe offroad.

Conclusão: A rede pré-treinada já era robusta o suficiente; a manipulação artificial apenas inseriu instabilidade.

✅ 5. Modelo Final e Conclusões
O melhor resultado foi obtido com a ResNet18 Desbalanceada, que aproveitou melhor o Transfer Learning para manter a precisão alta.

Lição Aprendida: O balanceamento não é uma solução universal; sua eficácia depende da relação entre a complexidade da arquitetura e a diversidade do dataset.

🛠️ 6. Próximos Passos
Coleta de Dados: Expansão das classes minoritárias para evitar memorização.

Fine-tuning: Descongelamento gradual de camadas da ResNet.

Otimização de Hiperparâmetros: Executar baterias de testes focadas no ajuste fino de Learning Rate, Batch Size e funções de otimização para estabilizar a convergência e buscar um melhor equilíbrio entre bias e variância.
