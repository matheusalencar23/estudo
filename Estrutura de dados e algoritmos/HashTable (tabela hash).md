Uma tabela hash é uma impementação dos dicionários que usa hash. O hashing é uma metodologia para se encontrar um valor dentro de uma estrutura de dados o mais rápido possível. Para encontramos um valor em outras estruturas de dados é necessário iterar através dos elementos até que o valor seja encontrado. Quando se usa a função hash, a posição do valor já é conhecido, então podemos simplismente acessa-lo. Uma função hash é uma função que, dada uma chave, retorna o endereço em que o valor está na tabela.
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

  return item.toString(); // {1}
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