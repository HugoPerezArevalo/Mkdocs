# 🪙 Portal de Criptografía y Activos Digitales

Bienvenido a la documentación técnica sobre el ecosistema cripto. Aquí aprenderás desde conceptos básicos hasta la implementación de scripts para consultar el mercado.

---

## 📊 Comparativa de Activos Principales
Antes de empezar, es importante entender las diferencias entre las redes más importantes.

| Criptomoneda | Símbolo | Consenso | Uso Principal |
| :--- | :---: | :---: | :--- |
| Bitcoin | BTC | Proof of Work | Reserva de valor |
| Ethereum | ETH | Proof of Stake | Smart Contracts |
| Solana | SOL | Proof of History | Apps de alta velocidad |

---

## 💻 Consulta de Precios (API)
A continuación, verás cómo conectar con una API (como CoinGecko) para obtener el precio actual. Puedes elegir el lenguaje que prefieras en las pestañas:

=== "Python"

    ```python linenums="1"
    import requests

    def get_crypto_price(coin_id):
        url = f"[https://api.coingecko.com/api/v3/simple/price?ids=](https://api.coingecko.com/api/v3/simple/price?ids=){coin_id}&vs_currencies=usd"
        response = requests.get(url)
        data = response.json()
        return data[coin_id]['usd']

    print(f"El precio de Bitcoin es: ${get_crypto_price('bitcoin')}")
    ```

=== "JavaScript"

    ```javascript linenums="1"
    const axios = require('axios');

    async function getPrice(coin) {
        const url = `https://api.coingecko.com/api/v3/simple/price?ids=${coin}&vs_currencies=usd`;
        const res = await axios.get(url);
        console.log(`Precio de ${coin}: $${res.data[coin].usd}`);
    }

    getPrice('ethereum');
    ```

---

## ⚠️ Gestión de Seguridad
El manejo de activos digitales requiere seguir protocolos estrictos para evitar pérdidas.

!!! danger "Advertencia de Seguridad"
    Nunca compartas tu **Seed Phrase** (frase semilla) con nadie. Si alguien te la pide, es una estafa.

!!! info "Nota Técnica"
    Las transacciones en la cadena de bloques son irreversibles. Una vez enviadas, no existe un "botón de cancelar".

!!! tip "Mejor Práctica"
    Utiliza siempre una *Hardware Wallet* (billetera fría) para almacenar grandes cantidades de criptomonedas a largo plazo.

---

## 🛠️ Instalación de herramientas
Si quieres empezar a desarrollar sobre Web3, instala estas dependencias básicas:

```bash
# Instalar Web3.py para interactuar con Ethereum
pip install web3

# Instalar ethers.js si trabajas con JavaScript
npm install --save ethers