Um conjunto (set) é uma coleção não ordenada de itens, composta por elementos únicos, ou seja, que não podem se repetir. Essa estrutura de dados se baseia no conceito matemático dos conjuntos finitos. Em metemática, um conjunto é uma coleção de objetos distintos. Por exemplo, temos o conjunto de números naturais, que é composto pelo números inteiros maiores ou iguais a 0:
$$
N = \{0, 1, 2, 3, 4, 5, 6, ...\}
$$
Também existe o conceito de conjunto nulo que é um conjunto sem elementos, também chamado de conjunto nulo. Ele é representado por $\{\ \}$.
Exemplo de implementação usando JavaScript:
```js
export default class Set {
  #items;

  constructor() {
    this.#items = {};
  }

  has(element) {
    return Object.prototype.hasOwnProperty.call(this.#items, element);
  }

  add(element) {
    if (!this.has(element)) {
      this.#items[element] = element;
      return true;
    }
    return false;
  }

  delete(element) {
    if (this.has(element)) {
      delete this.#items[element];
      return true;
    }
    return false;
  }

  clear() {
    this.#items = {};
  }

  size() {
    return Object.keys(this.#items).length;
  }

  values() {
    return Object.values(this.#items);
  }

  union(otherSet) {
    const unionSet = new Set();
    this.values().forEach((value) => unionSet.add(value));
    otherSet.values().forEach((value) => unionSet.add(value));
    return unionSet;
  }

  intersection(otherSet) {
    const intersectionSet = new Set();
    const values = this.values();
    const otherValues = otherSet.values();
    let biggerSet = values;
    let smallerSet = otherValues;
    if (otherValues.length - values.length > 0) {
      biggerSet = otherValues;
      smallerSet = values;
    }

    smallerSet.forEach((value) => {
      if (biggerSet.includes(value)) {
        intersectionSet.add(value);
      }
    });

    return intersectionSet;
  }

  difference(otherSet) {
    const differenceSet = new Set();
    this.values().forEach((value) => {
      if (!otherSet.has(value)) {
        differenceSet.add(value);
      }
    });

    return differenceSet;
  }

  isSubsetOf(otherSet) {
    if (this.size() > otherSet.size()) return false;
    let isSubset = true;
    this.values().every((value) => {
      if (!otherSet.has(value)) {
        isSubset = false;
        return false;
      }
      return true;
    });
    return isSubset;
  }
}
```

> [!INFO] Na especificação ECMAScript 2015 a classe Set foi adicionada de forma nativa na API do JavaScript.