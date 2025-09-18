# Pool
De todo

# descargar datos históricos de una criptomoneda(bitcoin)
pip install pycoingecko

from pycoingecko import CoinGeckoAPI
import pandas as pd
from datetime import datetime

# Inicializar API
cg = CoinGeckoAPI()

# Descargar datos históricos de precios de Bitcoin (en USD) para los últimos 90 días
data = cg.get_coin_market_chart_by_id(id='bitcoin', vs_currency='usd', days=90)

# Los precios vienen como lista de [timestamp, price]
prices = data['prices']

# Convertir a DataFrame
df = pd.DataFrame(prices, columns=['timestamp', 'price'])

# Convertir timestamp a fecha legible
df['date'] = pd.to_datetime(df['timestamp'], unit='ms')

# Reordenar columnas
df = df[['date', 'price']]

# Guardar a CSV para usar después
df.to_csv('bitcoin_90dias.csv', index=False)

print(df.head())
