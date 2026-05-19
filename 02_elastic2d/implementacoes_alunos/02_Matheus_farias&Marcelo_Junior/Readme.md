\# MEF 2D - Elasticidade Plana (Elementos Q4)



Este módulo faz parte do curso de Método dos Elementos Finitos (MEF) e implementa a recuperação de tensões e pós-processamento gráfico para elementos quadrilaterais bilineares (Q4), cobrindo as formulações de \*\*Estado Plano de Tensões (EPT)\*\* e \*\*Estado Plano de Deformações (EPD)\*\*.



\## 🚀 Implementações Realizadas



O código original em Fortran foi estendido para realizar o cálculo rigoroso das tensões a partir dos deslocamentos nodais obtidos pelo solver iterativo (PCG). As principais contribuições foram:



1\. \*\*Identificação Automática da Física (EPT/EPD):\*\* O programa lê o tipo de elemento diretamente do arquivo de dados e chaveia dinamicamente a Matriz Constitutiva ($D$), garantindo a aplicação correta das equações de restrição tridimensionais associadas ao Efeito de Poisson.

2\. \*\*Cálculo nos Pontos de Gauss (2x2):\*\* Implementação da Quadratura de Gauss-Legendre ($1/\\sqrt{3} \\approx \\pm 0.57735$) para integração numérica interna de cada elemento, calculando as matrizes Jacobianas locais, matrizes cinemáticas ($B$) e as tensões exatas ($\\sigma\_x$, $\\sigma\_y$, $\\tau\_{xy}$).

3\. \*\*Projeção Nodal (Suavização de Tensões):\*\* Para evitar mapas de cores descontínuos ("pixelados"), foi implementado um algoritmo de extrapolação que projeta as tensões dos pontos de Gauss diretamente para os nós do elemento. Nos nós compartilhados, o código realiza a média ponderada das contribuições, gerando um campo de tensões contínuo.

4\. \*\*Exportação VTK Independente:\*\* Estruturação do arquivo de saída no formato `.vtk` (Unstructured Grid ASCII) separando as tensões em campos escalares individuais (`SCALARS Tensao\_X`, `Tensao\_Y`, `Tensao\_XY`). Isso permite análises isoladas e transições suaves de gradientes de cor no ParaView.



\## 📂 Estrutura do Repositório



\* `scr/`: Contém o código-fonte principal em Fortran (`Solucao-mef.f`).

\* `exemplos/`: Pasta dedicada aos arquivos de validação.

&#x20; \* `Ex1\_quad\_25e.dat`: Arquivo de entrada com a geometria da malha de 25 elementos e condições de contorno.

&#x20; \* `Saida\_1.dat`: Relatório de texto com coordenadas, conectividades e deslocamentos calculados.

&#x20; \* `S1-1.vtk`: Arquivo de pós-processamento pronto para leitura no ParaView.

