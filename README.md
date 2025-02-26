# luk
### `crypto_tracker.py`
```python
import requests
from config import COINGECKO_API_KEY, CRYPTOCURRENCIES
from utils import format_currency_data


def fetch_crypto_data(api_key):
    """
    Функция для получения данных о криптовалютах с использованием API Coingecko.
    :param api_key: ключ API Coingecko
    :return: словарь с данными о криптовалютах
    """
    url = f'https://pro-api.coinmarketcap.com/v1/cryptocurrency/listings/latest'
    headers = {'X-CMC_PRO_API_KEY': api_key}
    params = {'start': '1', 'limit': '10'}
    try:
        response = requests.get(url, headers=headers, params=params).json()
        if response['status']['error_code'] != 0:
            raise Exception(f"Ошибка API: {response['status']['error_message']}")
        return response['data']
    except Exception as e:
        print(f"Произошла ошибка при получении данных: {e}")
        return None


def main():
    crypto_data = fetch_crypto_data(COINGECKO_API_KEY)
    formatted_data = format_currency_data(crypto_data)
    print(formatted_data)


if __name__ == "__main__":
    main()
```
