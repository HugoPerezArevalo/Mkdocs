# 🧪 Tutoriales para Desarrolladores

En esta sección aprenderás a interactuar con diferentes protocolos de Blockchain utilizando librerías estándar de la industria.

---

## ⚡ Enviar una transacción en Ethereum

Para enviar fondos usando `web3.py`, necesitas establecer una conexión con un nodo (como Infura o Alchemy) y firmar la transacción con tu clave privada.

```python linenums="1"
from web3 import Web3

# 1. Conexión al nodo
w3 = Web3(Web3.HTTPProvider('[https://mainnet.infura.io/v3/tu_api_key](https://mainnet.infura.io/v3/tu_api_key)'))

def enviar_eth(emisor, receptor, cantidad_eth, private_key):
    # Obtener el nonce (número de transacción)
    nonce = w3.eth.get_transaction_count(emisor)
    
    # Construir la transacción
    tx = {
        'nonce': nonce,
        'to': receptor,
        'value': w3.to_wei(cantidad_eth, 'ether'),
        'gas': 21000,
        'gasPrice': w3.to_wei('50', 'gwei'),
        'chainId': 1
    }
    
    # Firmar y enviar
    signed_tx = w3.eth.account.sign_transaction(tx, private_key)
    tx_hash = w3.eth.send_raw_transaction(signed_tx.rawTransaction)
    
    return w3.to_hex(tx_hash)
!!! info "Seguridad de la Clave Privada" Nunca escribas tu clave privada directamente en el código (hardcoded). Utiliza siempre archivos .env o variables de entorno para proteger tus fondos.

🔍 Consulta de Smart Contracts
Si necesitas leer datos de un contrato inteligente (como un balance de un token ERC-20), utiliza el siguiente método:

=== "Python"

```python
# Definir el ABI mínimo para consultar balance
abi = '[{"constant":true,"inputs":[{"name":"_owner","type":"address"}],"name":"balanceOf","outputs":[{"name":"balance","type":"uint256"}],"type":"function"}]'

contrato = w3.eth.contract(address='0xTokenAddress', abi=abi)
balance = contrato.functions.balanceOf('0xTuDireccion').call()
print(w3.from_wei(balance, 'ether'))
```
=== "JavaScript (Ethers.js)"

```javascript
const provider = new ethers.providers.JsonRpcProvider();
const abi = ["function balanceOf(address) view returns (uint256)"];

const contract = new ethers.Contract("0xTokenAddress", abi, provider);
const balance = await contract.balanceOf("0xTuDireccion");
console.log(ethers.utils.formatEther(balance));
```
⛽ Gestión del Gas
El "Gas" es la unidad que mide el esfuerzo computacional de una operación en la red.

!!! danger "Transacciones Pendientes" 
    Si estableces un gasPrice demasiado bajo en comparación con la media del mercado, tu transacción quedará en estado "Pending" indefinidamente hasta que el precio baje.

    Herramientas útiles
    ETH Gas Station: Para consultar precios en tiempo real.

    Etherscan: Para trackear el estado de tus hashes de transacción.


---

