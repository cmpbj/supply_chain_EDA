# Análise Exploratória De Dados de Supply Chain

Este notebook tem como objetivo apresentar uma análise abrangente de um conjunto de dados relacionados à cadeia de suprimentos, com foco em aspectos como vendas, distribuição comercial, logística e clientes. O conjunto de dados em questão oferece diversas oportunidades para análise. Portanto, esta Análise Exploratória de Dados (EDA) não pretende esgotar todas as possibilidades, mas, sim, abordar questões específicas, tais como:

- **Método de Pagamento Preferido**: Investigaremos qual é o método de pagamento mais comumente utilizado pelos clientes.

- **Tipos de Clientes e Consumo**: Identificaremos os tipos de cliente mais frequentes e determinaremos quais deles representam os maiores consumidores.

- **Destinos de Entrega**: Analisaremos os destinos mais frequentes e investigaremos quais destes geraram os maiores e menores lucros, auxiliando na identificação de áreas para possíveis melhorias operacionais.

- **Atrasos na Entrega**: Avaliaremos qual destino sofre mais frequentemente com atrasos na entrega e identificaremos os principais métodos de entrega responsáveis por esses atrasos.

- **Detecção de Fraudes**: Examinaremos as características gerais dos pedidos sinalizados como possíveis fraudes, contribuindo para a compreensão e detecção de atividades fraudulentas.

Explicar como executar os testes automatizados para este sistema.

### 🔩 Um pouco sobre a análise

De modo geral, a empresa sofre de dois problemas graves: um diz respeito das transações e métodos de pagamento e o outro sobre o risco de atraso nas entregas.

Apenas transações no débito tiveram status do pedido completo. Nenhum dos demais métodos de pagamento tiveram seus pedidos completamente processados:

<img src="graficos\\prop_status_pedido_por_meiopag.png" alt="image" width="50%" height="auto">

Um indicador importante para medir a qualidade do operador logístico é o On Time. Este indicador mede se o pedido chegou ou não no tempo previsto. No nosso caso, a maior parte das regiões sofre com atraso nas entregas em mais de 50% dos pedidos, de modo que tem-se um On Time muito baixo. Atraso causa insatisfação nos clientes, fazendo, inclusive, que muitos não voltem a comprar. Nesse sentido, é preciso identificar o que ocasiona esse atraso: é uma falha operacional que pode ser resolvida internamente? É uma falha de um terceiro que realiza as entregas? É por conta da localidade dos armazens? É um problema com fornecedor?...

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th><th>order_region</th>      <th>market</th>      <th>Total de Pedidos</th>      <th>Total de Pedidos Atrasados</th>      <th>% Pedidos Atrasados</th>    </tr>  </thead>  <tbody>    <tr>      <th>0</th>      <td>Central Africa</td>      <td>Africa</td>      <td>556</td>      <td>320</td>      <td>57.553957</td>    </tr>    <tr>      <th>1</th>      <td>East Africa</td>      <td>Africa</td>      <td>613</td>      <td>348</td>      <td>56.769984</td>    </tr>    <tr>      <th>2</th>      <td>South of  USA</td>      <td>USCA</td>      <td>1345</td>      <td>753</td>      <td>55.985130</td>    </tr>    <tr>      <th>3</th>      <td>West Asia</td>      <td>Pacific Asia</td>      <td>2022</td>      <td>1132</td>      <td>55.984174</td>    </tr>    <tr>      <th>4</th>      <td>Eastern Europe</td>      <td>Europe</td>      <td>1292</td>      <td>723</td>      <td>55.959752</td>    </tr>    <tr>      <th>5</th>      <td>South Asia</td>      <td>Pacific Asia</td>      <td>3335</td>      <td>1865</td>      <td>55.922039</td>    </tr>    <tr>      <th>6</th>      <td>Western Europe</td>      <td>Europe</td>      <td>10010</td>      <td>5585</td>      <td>55.794206</td>    </tr>    <tr>      <th>7</th>      <td>Southeast Asia</td>      <td>Pacific Asia</td>      <td>4356</td>      <td>2421</td>      <td>55.578512</td>    </tr>    <tr>      <th>8</th>      <td>Central Asia</td>      <td>Pacific Asia</td>      <td>184</td>      <td>102</td>      <td>55.434783</td>    </tr>    <tr>      <th>9</th>      <td>US Center</td>      <td>USCA</td>      <td>1935</td>      <td>1071</td>      <td>55.348837</td>    </tr>    <tr>      <th>10</th>      <td>East of USA</td>      <td>USCA</td>      <td>2323</td>      <td>1276</td>      <td>54.928971</td>    </tr>    <tr>      <th>11</th>      <td>Central America</td>      <td>LATAM</td>      <td>9396</td>      <td>5156</td>      <td>54.874415</td>    </tr>    <tr>      <th>12</th>      <td>Eastern Asia</td>      <td>Pacific Asia</td>      <td>3318</td>      <td>1818</td>      <td>54.792043</td>    </tr>    <tr>      <th>13</th>      <td>Oceania</td>      <td>Pacific Asia</td>      <td>4362</td>      <td>2382</td>      <td>54.607978</td>    </tr>    <tr>      <th>14</th>      <td>West of USA</td>      <td>USCA</td>      <td>2667</td>      <td>1451</td>      <td>54.405699</td>    </tr>    <tr>      <th>15</th>      <td>North Africa</td>      <td>Africa</td>      <td>1064</td>      <td>578</td>      <td>54.323308</td>    </tr>    <tr>      <th>16</th>      <td>South America</td>      <td>LATAM</td>      <td>4979</td>      <td>2696</td>      <td>54.147419</td>    </tr>    <tr>      <th>17</th>      <td>Southern Africa</td>      <td>Africa</td>      <td>398</td>      <td>214</td>      <td>53.768844</td>    </tr>    <tr>      <th>18</th>      <td>Northern Europe</td>      <td>Europe</td>      <td>3716</td>      <td>1996</td>      <td>53.713671</td>    </tr>    <tr>      <th>19</th>      <td>Southern Europe</td>      <td>Europe</td>      <td>3543</td>      <td>1895</td>      <td>53.485747</td>    </tr>    <tr>      <th>20</th>      <td>Caribbean</td>      <td>LATAM</td>      <td>2806</td>      <td>1487</td>      <td>52.993585</td>    </tr>    <tr>      <th>21</th>      <td>West Africa</td>      <td>Africa</td>      <td>1223</td>      <td>626</td>      <td>51.185609</td>    </tr>    <tr>      <th>22</th>      <td>Canada</td>      <td>USCA</td>      <td>309</td>      <td>153</td>      <td>49.514563</td>    </tr>  </tbody></table>

📈 🎲

O dataset pode ser baixado através do seguinte link: [dataset de supply chain](https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis/data)
