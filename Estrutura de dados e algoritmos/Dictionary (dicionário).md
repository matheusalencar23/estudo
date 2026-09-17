Um dicionário é uma estrutura de dados muito parecida com o conjunto (set), a principal diferença é que os conjuntos armazenam seus dados usando a estrutura [valor, valor], já os dicionários armazenam os dados na estrurura [chave, valor]. Essa chave pode ser usada para encontrar um elemento dentro da estrutura. Dicionários também são conhecidos como Mapas (map), tabela de símbolos e array associativo.
Exemplo de implementação usando JavaScript:
```js
export function defaultToString(item) {
  if (item === null) {
    return "NULL";
  } else if (item === undefined) {
    return "UNDEFINED";
  } else if (typeof item === "string" || item instanceof String) {
    return `${item}`;
  }

  return item.toString();
}

class ValuePair {
  #key;
  #value;

  get key() {
    return this.#key;
  }

  get value() {
    return this.#value;
  }

  constructor(key, value) {
    this.#key = key;
    this.#value = value;
  }

  toString() {
    return `[#${this.#key}: ${this.#value}]`;
  }
}

export default class Dictionary {
  #toStringFn;
  #table;

  constructor(toStringFn = defaultToString) {
    this.#toStringFn = toStringFn;
    this.#table = {};
  }

  hasKey(key) {
    return (
      this.#table[this.#toStringFn(key)] !== null ||
      this.#table[this.#toStringFn(key)] !== undefined
    );
  }

  set(key, value) {
    if (
      key !== null &&
      key !== undefined &&
      value !== null &&
      value !== undefined
    ) {
      const tableyKey = this.#toStringFn(key);
      this.#table[tableyKey] = new ValuePair(key, value);
      return true;
    }
    return false;
  }

  remove(key) {
    if (this.hasKey(key)) {
      delete this.#table[this.#toStringFn(key)];
      return true;
    }
    return false;
  }

  get(key) {
    const valuePair = this.#table[this.#toStringFn(key)];
    return valuePair === null || valuePair === undefined
      ? undefined
      : valuePair.value;
  }

  keyValues() {
    return Object.values(this.#table);
  }

  keys() {
    return this.keyValues().map((valuePair) => valuePair.key);
  }

  values() {
    return this.keyValues().map((valuePair) => valuePair.value);
  }

  forEach(callbackFn) {
    const valuePairs = this.keyValues();
    for (let i = 0; i < valuePairs.length; i++) {
      const result = callbackFn(valuePairs[i].key, valuePairs[i].value);

      if (result === false) {
        break;
      }
    }
  }

  size() {
    return Object.keys(this.#table).length;
  }

  isEmpty() {
    return this.size() === 0;
  }

  clear() {
    this.#table = {};
  }

  toString() {
    if (this.isEmpty()) return "[]";
    const valuePairs = this.keyValues();
    return `[${valuePairs.map((valuePair) => valuePair.toString()).join(", ")}]`;
  }
}
```
