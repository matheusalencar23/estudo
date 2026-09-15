As listas ligadas armazenam uma coleção de elementos de forma sequencial, porém, diferente de arrays, as listas ligadas não tem seus elementos armazenados de forma contígua, ou seja, eles não são armazenados um ao lado do outro. Na lista ligada, cada elemento é constituído pelo elemento em sí e por uma referência que aponta para um outro nó, essa referência também pode ser nomeada como ponteiro ou ligação. Esse conjunto do elemento com o ponteiro é o nó (*node*).
![[linked_list|100%]]
Uma das vantagens da lista ligada com relação aos arrays convencionais é que não é necessário realizar deslocamentos nos elementos quando ocorre a adição ou remoção de elementos, porém, pelo fato de usarmos ponteiros, quando é necessário acessar um elemento no meio da lista é preciso percorrer a lista partindo do primeiro elemento da lista, esse primeiro elemento da lista pode ser chamado de *head*.
Existem dois cenários na adição de elementos em uma lista ligada, um em que a lista está vazia e outro quando já existem elementos nela. Para a adicionar um elemento em uma lista vazia basta definir o apontamento do head para o elemento a ser adicionado. Caso a lista não esteja vazia precisamos manipular os ponteiros de forma a inserir o novo elemento, seja ele no início, meio o final da lista.
![[linked_list_add|100%]]
Para removermos elementos das listas ligadas também precisamos nos preocupar com os ponteiros.
![[linked_list_remove|100%]]
Exemplo de implementação usando JavaScript:
```js
function defaultEquals(a, b) {
  return a === b;
}

class Node {
  #element;
  #next;

  constructor(element) {
    this.#element = element;
    this.#next = null;
  }

  getElement() {
    return this.#element;
  }

  getNext() {
    return this.#next;
  }

  setNext(next) {
    this.#next = next;
  }
}

export default class LinkedList {
  #count;
  #head;
  #equalsFn;

  constructor(equalsFn = defaultEquals) {
    this.#count = 0;
    this.#head = null;
    this.#equalsFn = equalsFn;
  }

  push(element) {
    const node = new Node(element);
    let current;

    if (this.#head === null) {
      this.#head = node;
    } else {
      current = this.#head;
      while (current.getNext() !== null) {
        current = current.getNext();
      }
      current.setNext(node);
    }

    this.#count++;
  }

  removeAt(index) {
    if (index >= 0 && index < this.#count) {
      let current = this.#head;

      if (index === 0) {
        this.#head = current.getNext();
      } else {
        const previous = this.getElementAt(index - 1);
        current = previous.getNext();
        previous.setNext(current.getNext());
      }

      this.#count--;
      return current.getElement();
    }

    return null;
  }

  getElementAt(index) {
    if (index >= 0 && index < this.#count) {
      let node = this.#head;
      for (let i = 0; i < index && node !== null; i++) {
        node = node.getNext();
      }
      return node;
    }
    return null;
  }

  insert(element, index) {
    if (index >= 0 && index <= this.#count) {
      const node = new Node(element);

      if (index === 0) {
        const current = this.#head;
        node.setNext(current);
        this.#head = node;
      } else {
        const previous = this.getElementAt(index - 1);
        const current = previous.getNext();
        node.setNext(current);
        previous.setNext(node);
      }

      this.#count++;
      return true;
    }
    return false;
  }

  indexOf(element) {
    let current = this.#head;

    for (let i = 0; i < this.#count && current !== null; i++) {
      if (this.#equalsFn(element, current.getElement())) {
        return i;
      }
      current = current.getNext();
    }
    return -1;
  }

  remove(element) {
    const index = this.indexOf(element);
    return this.removeAt(index);
  }

  size() {
    return this.#count;
  }

  isEmpty() {
    return this.size() === 0;
  }

  toString() {
    if (this.#head === null) {
      return "[]";
    }

    let objString = `${this.#head.getElement()}`;
    let current = this.#head.getNext();
    for (let i = 0; i < this.size() && current !== null; i++) {
      objString += `, ${current.getElement()}`;
      current = current.getNext();
    }
    return objString;
  }
}
```
Existem algumas variações de listas ligadas, por exemplo, listas duplamente ligadas (*Doubly Linked List*) e listas ligadas circulares (*Circular Linked List*).
## Doubly Linked List (listas duplamente ligadas)
A diferença desse tipo de lista para as listas ligadas convencionais é que os nós dessa coleção tem uma refereência tanto para o próximo elemento da lista como para o anterior.
![[doubly_linked_list|100%]]
Exemplo de implementação em JavaScript:
```js
function defaultEquals(a, b) {
  return a === b;
}

class DoublyNode {
  #element;
  #next;
  #prev;

  constructor(element) {
    this.#element = element;
    this.#next = null;
  }

  getElement() {
    return this.#element;
  }

  getPrev() {
    return this.#prev;
  }

  setPrev(prev) {
    this.#prev = prev;
  }

  getNext() {
    return this.#next;
  }

  setNext(next) {
    this.#next = next;
  }
}

export default class DoublyLinkedList {
  #count;
  #head;
  #tail;
  #equalsFn;

  constructor(equalsFn = defaultEquals) {
    this.#count = 0;
    this.#head = null;
    this.#tail = null;
    this.#equalsFn = equalsFn;
  }

  push(element) {
    const node = new DoublyNode(element);
    let current;
    if (this.#head === null) {
      this.#head = node;
    } else {
      current = this.#head;
      while (current.getNext() !== null) {
        current = current.getNext();
      }
      current.setNext(node);
    }
    this.#count++;
  }

  removeAt(index) {
    if (index >= 0 && index < this.#count) {
      let current = this.#head;
      if (index === 0) {
        this.#head = current.getNext();
        if (this.#count === 1) {
          this.#tail = null;
        } else {
          this.#head.setPrev(null);
        }
      } else if (index === this.#count - 1) {
        current = this.#tail;
        this.#tail = current.getPrev();
        this.#tail.setNext(null);
      } else {
        current = this.getElementAt(index);
        const previous = current.getPrev();
        previous.setNext(current.getNext());
        current.getNext().setNext(previous);
      }

      this.#count--;
      return current.getElement();
    }
    return null;
  }

  getElementAt(index) {
    if (index >= 0 && index < this.#count) {
      let node = this.#head;
      for (let i = 0; i < index && node !== null; i++) {
        node = node.getNext();
      }
      return node;
    }
    return null;
  }

  insert(element, index) {
    if (index >= 0 && index <= this.#count) {
      const node = new DoublyNode(element);
      let current = this.#head;
      if (index === 0) {
        if (this.#head === null) {
          this.#head = node;
          this.#tail = node;
        } else {
          node.setNext(this.#head);
          current.setPrev(node);
          this.#head = node;
        }
      } else if (index === this.#count) {
        current = this.#tail;
        current.setNext(node);
        node.setPrev(current);
        this.#tail = node;
      } else {
        const previous = this.getElementAt(index - 1);
        current = previous.getNext();
        node.setNext(current);
        previous.setNext(node);
        current.setPrev(node);
        node.setPrev(previous);
      }

      this.#count++;
      return true;
    }
    return false;
  }

  indexOf(element) {
    let current = this.#head;
    for (let i = 0; i < this.#count && current !== null; i++) {
      if (this.#equalsFn(element, current.getElement())) {
        return i;
      }
      current = current.getNext();
    }
    return -1;
  }

  remove(element) {
    const index = this.indexOf(element);
    return this.removeAt(index);
  }

  size() {
    return this.#count;
  }

  isEmpty() {
    return this.size() === 0;
  }

  toString() {
    if (this.#head === null) {
      return "[]";
    }
    let objString = `${this.#head.getElement()}`;
    let current = this.#head.getNext();
    for (let i = 0; i < this.size() && current !== null; i++) {
      objString += `, ${current.getElement()}`;
      current = current.getNext();
    }
    return objString;
  }
}
```

## Circular Linked List (listas ligadas circulares)
A diferença das listas ligadas circulares é que os ponteiros nunca apontam para um elemento vazio ou nulo, para o caso da lista ligada simples, o ponteiro para o próximo item do último nó aponta para o primeiro item da lista. No caso de uma lista duplamente ligada circular temos o ponteiro para o anterior do primeiro nó apontando para o último item da lista também.
![[circular_linked_list|100%]]Exemplo de implementação em JavaScript:

```js
function defaultEquals(a, b) {
  return a === b;
}

class CircularNode {
  #element;
  #next;

  constructor(element) {
    this.#element = element;
    this.#next = null;
  }

  getElement() {
    return this.#element;
  }

  getNext() {
    return this.#next;
  }

  setNext(next) {
    this.#next = next;
  }
}

export default class CircularLinkedList {
  #count;
  #head;
  #equalsFn;

  constructor(equalsFn = defaultEquals) {
    this.#count = 0;
    this.#head = null;
    this.#equalsFn = equalsFn;
  }

  push(element) {
    const node = new CircularNode(element);
    let current;
    if (this.#head === null) {
      this.#head = node;
    } else {
      current = this.#head;
      while (current.getNext() !== null) {
        current = current.getNext();
      }
      current.setNext(node);
    }
    this.#count++;
  }

  removeAt(index) {
    if (index >= 0 && index < this.#count) {
      let current = this.#head;
      if (index === 0) {
        if (this.size() === 1) {
          this.#head = null;
        } else {
          const removed = this.#head;
          current = this.getElementAt(this.size());
          this.#head = this.#head.getNext();
          current.setNext(this.#head);
          current = removed;
        }
      } else {
        const previous = this.getElementAt(index - 1);
        current = previous.getNext();
        previous.setNext(current.getNext());
      }
      this.#count--;
      return current.getElement();
    }
    return null;
  }

  getElementAt(index) {
    if (index >= 0 && index < this.#count) {
      let node = this.#head;

      for (let i = 0; i < index && node !== null; i++) {
        node = node.getNext();
      }

      return node;
    }

    return null;
  }

  insert(element, index) {
    if (index >= 0 && index <= this.#count) {
      const node = new CircularNode(element);
      let current = this.#head;
      if (index === 0) {
        if (this.#head === null) {
          this.#head = node;
          node.setNext(this.#head);
        } else {
          node.setNext(current);
          current = this.getElementAt(this.size());
          this.#head = node;
          current.setNext(this.#head);
        }
      } else {
        const previous = this.getElementAt(index - 1);
        node.setNext(previous.getNext());
        previous.setNext(node);
      }
      this.#count++;
      return true;
    }
    return false;
  }

  indexOf(element) {
    let current = this.#head;
    for (let i = 0; i < this.#count && current !== null; i++) {
      if (this.#equalsFn(element, current.getElement())) {
        return i;
      }
      current = current.getNext();
    }
    return -1;
  }

  remove(element) {
    const index = this.indexOf(element);
    return this.removeAt(index);
  }

  size() {
    return this.#count;
  }

  isEmpty() {
    return this.size() === 0;
  }

  toString() {
    if (this.#head === null) {
      return "[]";
    }
    let objString = `${this.#head.getElement()}`;
    let current = this.#head.getNext();
    for (let i = 0; i < this.size() && current !== null; i++) {
      objString += `, ${current.getElement()}`;
      current = current.getNext();
    }
    return objString;
  }
}
```