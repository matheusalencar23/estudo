Filas seguem o princípio **FIFO** (First In First Out), ou seja, o primeiro a entrar é o primeiro a sair.
![[queue_fila_add|100%]]
Sempre que adicionamos um elemento na fila ele é posicionado logo em seguida do último elemento adicionado. Para uma fila vazia, o primeiro elemento é também o último da fila.  Não podemos adicionar um elemento antes de qualquer elemento que já esteja na fila, somente no final.
![[queue_fila_remove|100%]]
Na remoção de itens da fila os itens são removdiso sempre pela frente da fila, ou seja, os primeiros itens adicionados são removidos primeiro. Não conseguimos remover itens do meio ou no final da fila.
![[queue_fila|100%]]
Exemplo de implementação usando JavaScript:
```js
export class Queue {
  #count;
  #lowestCount;
  #items;

  constructor() {
    this.#count = 0;
    this.#lowestCount = 0;
    this.#items = {};
  }

  enqueue(element) {
    this.#items[this.#count] = element;
    this.#count++;
  }

  dequeue() {
    if (this.isEmpty()) return;

    const result = this.#items[this.#lowestCount];
    delete this.#items[this.#lowestCount];
    this.#lowestCount++;
    return result;
  }

  peek() {
    if (this.isEmpty()) return;
    return this.#items[this.#lowestCount];
  }

  isEmpty() {
    return this.size() === 0;
  }

  size() {
    return this.#count - this.#lowestCount;
  }

  clear() {
    this.#items = {};
    this.#count = 0;
    this.#lowestCount = 0;
  }

  toString() {
    if (this.isEmpty()) return "[]";
    return "[" + Object.values(this.#items).join(", ") + "]";
  }
}
```

## Deque

A deque é um tipo especial de fila, é conhecido como fila de duas pontas ou *double-ended queue*. É um tipo de fila que permite que os elementos sejam adicionados ou removidos no início ou final da fila, mas nunca no meio.
![[deque|100%]]
Exemplo de implementação usando JavaScript:
```js
export class Deque {
  #count;
  #lowestCount;
  #items;

  constructor() {
    this.#count = 0;
    this.#lowestCount = 0;
    this.#items = {};
  }

  addFront(element) {
    if (this.isEmpty()) {
      this.addBack(element);
    } else if (this.#lowestCount > 0) {
      this.#lowestCount--;

      this.#items[this.#lowestCount] = element;
    } else {
      for (let i = this.#count; i > 0; i--) {
        this.#items[i] = this.#items[i - 1];
      }

      this.#count++;
      this.#lowestCount = 0;
      this.#items[0] = element;
    }
  }

  addBack(element) {
    this.#items[this.#count] = element;
    this.#count++;
  }

  removeFront() {
    if (this.isEmpty()) return;

    const result = this.#items[this.#lowestCount];
    delete this.#items[this.#lowestCount];
    this.#lowestCount++;
    return result;
  }

  removeBack() {
    if (this.isEmpty()) return;

    const result = this.#items[this.#count - 1];
    delete this.#items[this.#count - 1];
    this.#count--;
    return result;
  }

  isEmpty() {
    return this.size() === 0;
  }

  size() {
    return this.#count - this.#lowestCount;
  }

  clear() {
    this.#items = {};
    this.#count = 0;
    this.#lowestCount = 0;
  }

  toString() {
    if (this.isEmpty()) return "[]";
    return "[" + Object.values(this.#items).join(", ") + "]";
  }
}
```