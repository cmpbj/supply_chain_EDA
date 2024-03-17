# Análise Exploratória De Dados de Supply Chain

Este notebook tem como objetivo apresentar uma análise abrangente de um conjunto de dados relacionados à cadeia de suprimentos, com foco em aspectos como vendas, distribuição comercial, logística e clientes. O conjunto de dados em questão oferece diversas oportunidades para análise. Portanto, esta Análise Exploratória de Dados (EDA) não pretende esgotar todas as possibilidades, mas, sim, abordar questões específicas, tais como:

- **Método de Pagamento Preferido**: Investigaremos qual é o método de pagamento mais comumente utilizado pelos clientes.

- **Tipos de Clientes e Consumo**: Identificaremos os tipos de cliente mais frequentes e determinaremos quais deles representam os maiores consumidores.

- **Destinos de Entrega**: Analisaremos os destinos mais frequentes e investigaremos quais destes geraram os maiores e menores lucros, auxiliando na identificação de áreas para possíveis melhorias operacionais.

- **Atrasos na Entrega**: Avaliaremos qual destino sofre mais frequentemente com atrasos na entrega e identificaremos os principais métodos de entrega responsáveis por esses atrasos.

- **Detecção de Fraudes**: Examinaremos as características gerais dos pedidos sinalizados como possíveis fraudes, contribuindo para a compreensão e detecção de atividades fraudulentas.

### 🔩 Um pouco sobre a análise

De modo geral, a empresa sofre de dois problemas graves: um diz respeito das transações e métodos de pagamento e o outro sobre o risco de atraso nas entregas.

Apenas transações no débito tiveram status do pedido completo. Nenhum dos demais métodos de pagamento tiveram seus pedidos completamente processados:

<img src="graficos\\prop_status_pedido_por_meiopag.png" alt="image" width="50%" height="auto">

Um indicador importante para medir a qualidade do operador logístico é o On Time. Este indicador mede se o pedido chegou ou não no tempo previsto. No nosso caso, a maior parte das regiões sofre com atraso nas entregas em mais de 50% dos pedidos, de modo que tem-se um On Time muito baixo. Atraso causa insatisfação nos clientes, fazendo, inclusive, que muitos não voltem a comprar. Nesse sentido, é preciso identificar o que ocasiona esse atraso: é uma falha operacional que pode ser resolvida internamente? É uma falha de um terceiro que realiza as entregas? É por conta da localidade dos armazens? É um problema com fornecedor?...

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th><th>order_region</th>      <th>market</th>      <th>Total de Pedidos</th>      <th>Total de Pedidos Atrasados</th>      <th>% Pedidos Atrasados</th>    </tr>  </thead>  <tbody>    <tr>      <th>0</th>      <td>Central Africa</td>      <td>Africa</td>      <td>556</td>      <td>320</td>      <td>57.553957</td>    </tr>    <tr>      <th>1</th>      <td>East Africa</td>      <td>Africa</td>      <td>613</td>      <td>348</td>      <td>56.769984</td>    </tr>    <tr>      <th>2</th>      <td>South of  USA</td>      <td>USCA</td>      <td>1345</td>      <td>753</td>      <td>55.985130</td>    </tr>    <tr>      <th>3</th>      <td>West Asia</td>      <td>Pacific Asia</td>      <td>2022</td>      <td>1132</td>      <td>55.984174</td>    </tr>    <tr>      <th>4</th>      <td>Eastern Europe</td>      <td>Europe</td>      <td>1292</td>      <td>723</td>      <td>55.959752</td>    </tr>    <tr>      <th>5</th>      <td>South Asia</td>      <td>Pacific Asia</td>      <td>3335</td>      <td>1865</td>      <td>55.922039</td>    </tr>    <tr>      <th>6</th>      <td>Western Europe</td>      <td>Europe</td>      <td>10010</td>      <td>5585</td>      <td>55.794206</td>    </tr>    <tr>      <th>7</th>      <td>Southeast Asia</td>      <td>Pacific Asia</td>      <td>4356</td>      <td>2421</td>      <td>55.578512</td>    </tr>    <tr>      <th>8</th>      <td>Central Asia</td>      <td>Pacific Asia</td>      <td>184</td>      <td>102</td>      <td>55.434783</td>    </tr>    <tr>      <th>9</th>      <td>US Center</td>      <td>USCA</td>      <td>1935</td>      <td>1071</td>      <td>55.348837</td>    </tr>    <tr>      <th>10</th>      <td>East of USA</td>      <td>USCA</td>      <td>2323</td>      <td>1276</td>      <td>54.928971</td>    </tr>    <tr>      <th>11</th>      <td>Central America</td>      <td>LATAM</td>      <td>9396</td>      <td>5156</td>      <td>54.874415</td>    </tr>    <tr>      <th>12</th>      <td>Eastern Asia</td>      <td>Pacific Asia</td>      <td>3318</td>      <td>1818</td>      <td>54.792043</td>    </tr>    <tr>      <th>13</th>      <td>Oceania</td>      <td>Pacific Asia</td>      <td>4362</td>      <td>2382</td>      <td>54.607978</td>    </tr>    <tr>      <th>14</th>      <td>West of USA</td>      <td>USCA</td>      <td>2667</td>      <td>1451</td>      <td>54.405699</td>    </tr>    <tr>      <th>15</th>      <td>North Africa</td>      <td>Africa</td>      <td>1064</td>      <td>578</td>      <td>54.323308</td>    </tr>    <tr>      <th>16</th>      <td>South America</td>      <td>LATAM</td>      <td>4979</td>      <td>2696</td>      <td>54.147419</td>    </tr>    <tr>      <th>17</th>      <td>Southern Africa</td>      <td>Africa</td>      <td>398</td>      <td>214</td>      <td>53.768844</td>    </tr>    <tr>      <th>18</th>      <td>Northern Europe</td>      <td>Europe</td>      <td>3716</td>      <td>1996</td>      <td>53.713671</td>    </tr>    <tr>      <th>19</th>      <td>Southern Europe</td>      <td>Europe</td>      <td>3543</td>      <td>1895</td>      <td>53.485747</td>    </tr>    <tr>      <th>20</th>      <td>Caribbean</td>      <td>LATAM</td>      <td>2806</td>      <td>1487</td>      <td>52.993585</td>    </tr>    <tr>      <th>21</th>      <td>West Africa</td>      <td>Africa</td>      <td>1223</td>      <td>626</td>      <td>51.185609</td>    </tr>    <tr>      <th>22</th>      <td>Canada</td>      <td>USCA</td>      <td>309</td>      <td>153</td>      <td>49.514563</td>    </tr>  </tbody></table>

  <table border="1" class="dataframe dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>order_region</th>
      <th>market</th>
      <th>Total de Pedidos</th>
      <th>Total de Pedidos Atrasados</th>
      <th>% Pedidos Atrasados</th>
      <th>First Class</th>
      <th>Same Day</th>
      <th>Second Class</th>
      <th>Standard Class</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Central Asia</td>
      <td>Pacific Asia</td>
      <td>62</td>
      <td>38</td>
      <td>61.290323</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>96.585366</td>
      <td>102.692308</td>
    </tr>
    <tr>
      <td>South of  USA</td>
      <td>USCA</td>
      <td>442</td>
      <td>267</td>
      <td>60.407240</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>92.361290</td>
      <td>98.602817</td>
    </tr>
    <tr>
      <td>South Asia</td>
      <td>Pacific Asia</td>
      <td>1083</td>
      <td>653</td>
      <td>60.295476</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>96.972973</td>
      <td>97.537255</td>
    </tr>
    <tr>
      <td>US Center</td>
      <td>USCA</td>
      <td>644</td>
      <td>384</td>
      <td>59.627329</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>95.373913</td>
      <td>94.350000</td>
    </tr>
    <tr>
      <td>East of USA</td>
      <td>USCA</td>
      <td>794</td>
      <td>473</td>
      <td>59.571788</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>96.212389</td>
      <td>98.290749</td>
    </tr>
    <tr>
      <td>Eastern Europe</td>
      <td>Europe</td>
      <td>462</td>
      <td>275</td>
      <td>59.523810</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>85.493976</td>
      <td>97.758355</td>
    </tr>
    <tr>
      <td>Southeast Asia</td>
      <td>Pacific Asia</td>
      <td>1386</td>
      <td>824</td>
      <td>59.451659</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>94.899471</td>
      <td>97.207378</td>
    </tr>
    <tr>
      <td>West Asia</td>
      <td>Pacific Asia</td>
      <td>669</td>
      <td>395</td>
      <td>59.043348</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>95.083969</td>
      <td>95.601399</td>
    </tr>
    <tr>
      <td>Eastern Asia</td>
      <td>Pacific Asia</td>
      <td>1062</td>
      <td>619</td>
      <td>58.286252</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>94.627119</td>
      <td>94.992035</td>
    </tr>
    <tr>
      <td>Oceania</td>
      <td>Pacific Asia</td>
      <td>1476</td>
      <td>859</td>
      <td>58.197832</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>93.221418</td>
      <td>98.245958</td>
    </tr>
    <tr>
      <td>Western Europe</td>
      <td>Europe</td>
      <td>3318</td>
      <td>1930</td>
      <td>58.167571</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>97.192547</td>
      <td>95.764172</td>
    </tr>
    <tr>
      <td>North Africa</td>
      <td>Africa</td>
      <td>341</td>
      <td>197</td>
      <td>57.771261</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>88.140351</td>
      <td>93.354037</td>
    </tr>
    <tr>
      <td>Southern Europe</td>
      <td>Europe</td>
      <td>1177</td>
      <td>677</td>
      <td>57.519116</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>93.020134</td>
      <td>95.550413</td>
    </tr>
    <tr>
      <td>Northern Europe</td>
      <td>Europe</td>
      <td>1240</td>
      <td>713</td>
      <td>57.500000</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>93.524664</td>
      <td>95.750649</td>
    </tr>
    <tr>
      <td>West of USA</td>
      <td>USCA</td>
      <td>901</td>
      <td>514</td>
      <td>57.047725</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>95.836177</td>
      <td>96.646617</td>
    </tr>
    <tr>
      <td>Central America</td>
      <td>LATAM</td>
      <td>3096</td>
      <td>1753</td>
      <td>56.621447</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>94.738318</td>
      <td>95.824034</td>
    </tr>
    <tr>
      <td>East Africa</td>
      <td>Africa</td>
      <td>202</td>
      <td>114</td>
      <td>56.435644</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>91.555556</td>
      <td>95.094340</td>
    </tr>
    <tr>
      <td>Central Africa</td>
      <td>Africa</td>
      <td>190</td>
      <td>107</td>
      <td>56.315789</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>90.612245</td>
      <td>101.015873</td>
    </tr>
    <tr>
      <td>Southern Africa</td>
      <td>Africa</td>
      <td>148</td>
      <td>82</td>
      <td>55.405405</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>112.153846</td>
      <td>97.054945</td>
    </tr>
    <tr>
      <td>South America</td>
      <td>LATAM</td>
      <td>1611</td>
      <td>887</td>
      <td>55.058970</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>91.924528</td>
      <td>94.117647</td>
    </tr>
    <tr>
      <td>Caribbean</td>
      <td>LATAM</td>
      <td>899</td>
      <td>487</td>
      <td>54.171301</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>99.382857</td>
      <td>93.737470</td>
    </tr>
    <tr>
      <td>Canada</td>
      <td>USCA</td>
      <td>93</td>
      <td>50</td>
      <td>53.763441</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>96.521739</td>
      <td>91.739645</td>
    </tr>
    <tr>
      <td>West Africa</td>
      <td>Africa</td>
      <td>420</td>
      <td>223</td>
      <td>53.095238</td>
      <td>48.0</td>
      <td>12.0</td>
      <td>92.723549</td>
      <td>94.250000</td>
    </tr>
  </tbody>
</table>
📈 🎲

O dataset pode ser baixado através do seguinte link: [dataset de supply chain](https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis/data)
