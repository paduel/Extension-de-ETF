# Extensión de datos sintéticos para ETFs

Basándome en el [artículo de Sergio Molina publicado en su web Carteras de bolsa](https://carterasdebolsa.com/codigo-python-para-extender-etfs/), que a su vez se basa en un [artículo de TrendXplorer donde usa hojas de Excel](https://indexswingtrader.blogspot.com/2017/03/index-mapping-for-etf-proxies.html), he escrito una función que recibe un diccionario donde las claves son los ETF y los valores los Proxy de cada uno de los ETF, descarga de los servidores de Tiingo (es necesaria clave de la API de Tiingo, que es gratuita) los datos tanto de ETF como de los Proxy (deben usarse los tickers tal como aparecen en Tiingo) y genera los datos sintéticos desde una fecha dada hasta que el ETF tiene datos históricos reales.

Calcula los rendimientos logarítmicos del ETF y del Proxy, para con ellos realizar una regresión lineal con los datos del periodo para el que existen datos. Posteriormente calcula los datos sintéticos del ETF usando esa regresión lineal.

Pero a diferencia de los articulos mencionados, la fúnción añade ademas un residuo al retorno sintético, que se calcula ajustando a los residuos de la regresión lineal una distribución t-student y posteriormente generando una muestra aletoria de dicha distribución.  Esto permite que los datos sintéticos tengan ruido respecto al Proxy, tal como lo tiene los datos reales del ETF.

La función admite varios ETF y Proxy, devolviendo los mismos ETF con los datos extendidos y los reales juntos, como opción puede devolver un dataframe multiindice de Pandas con todos los datos usados para el calculo, por si se quieren verificar o usar de alguna manera.
