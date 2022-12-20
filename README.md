# Stack-and-Queue
Nama : Muhammad Yusran Hardimas Setiawan<br>
NIM  : H071211024<br>

#

**Stack** adalah wadah objek yang dimasukkan dan dikeluarkan menurut prinsip last-in first-out (LIFO).<br>
**Queue** adalah sebuah wadah dari objek-objek (sebuah koleksi linear) yang dimasukkan dan dikeluarkan menurut prinsip masuk pertama keluar pertama (FIFO).<br>

#

# Stack
**Stack** adalah struktur data linier dimana elemen dapat disisipkan dan dihapus hanya dari satu sisi daftar, yang disebut bagian atas. 
Sebuah stack mengikuti prinsip LIFO (Last In First Out), yaitu elemen yang disisipkan paling akhir adalah elemen pertama yang keluar. 
Penyisipan elemen ke dalam stack disebut operasi **push**, dan penghapusan elemen dari stack disebut operasi **pop**. 
Dalam stack, kita selalu melacak elemen terakhir yang ada dalam daftar dengan pointer yang disebut top.
# ![image](https://user-images.githubusercontent.com/114170755/208633082-f23a58aa-ebf7-4145-9240-962c0e3ff490.png)<br>

Contoh kode stack:

```java
import java.util.*;
public class ArrayStack < E > {

    public static final int CAPACITY = 1000; // default array capacity
    private int topIndex; // index of the top element in stack
    private E[] data; // generic array used for storage
    

    public ArrayStack() {
        this(CAPACITY);
    } // constructs stack with default capacity

    public ArrayStack(int capacity) { // constructs stack with given capacity
        topIndex = -1;
        data = (E[]) new Object[capacity]; // safe cast; compiler may give warning
    }

    public int size() {
        return (topIndex + 1);
    }

    public boolean empty() {
        return (topIndex == -1);
    }

    public void push(E e) throws IllegalStateException {
        if (size() == data.length) throw new IllegalStateException("Stack is full");
        data[++topIndex] = e; // increment topIndex before storing new item
    }

    public E peek() throws EmptyStackException {
        if (empty()) throw new EmptyStackException();
        return data[topIndex];
    }

    public E pop() throws EmptyStackException {
        if (empty()) throw new EmptyStackException();
        E answer = data[topIndex];
        data[topIndex] = null; // dereference to help garbage collection
        topIndex--;
        return answer;
    }

    public static void main(String args[]) {
        ArrayStack < Integer > mystack = new ArrayStack<>();
        mystack.push(9); 
        mystack.push(3); 
        mystack.push(8); 
        System.out.println("Element at the top is :" + mystack.peek()); 
        System.out.println("Element removed is : " + mystack.pop()); 
        System.out.println("The size of the stack is : " + mystack.size()); 
        System.out.println("Element removed is : " + mystack.pop()); 
        System.out.println("Element at the top is : " + mystack.peek());
        mystack.push(10); 
        System.out.println("Stack is empty :  " + mystack.empty()); 
    }
}
```

Dengan output:

```java
Element at the top is :8        
Element removed is : 8          
The size of the stack is : 2    
Element removed is : 3          
Element at the top is : 9        
Stack is empty :  false         
```

## Queue
**Queue** adalah struktur data linier dimana elemen-elemen dapat disisipkan hanya dari satu sisi daftar yang disebut belakang, 
dan elemen-elemen dapat dihapus hanya dari sisi lain yang disebut depan. Struktur data antrian mengikuti prinsip FIFO (First In First Out), 
yaitu elemen yang disisipkan pertama kali dalam daftar, adalah elemen pertama yang dihapus dari daftar. 
Penyisipan sebuah elemen dalam antrian disebut operasi **enqueue** dan penghapusan sebuah elemen disebut operasi **dequeue**.
# ![image](https://user-images.githubusercontent.com/114170755/208635365-2a677fe6-9eaf-4bbe-b2ee-37688cf98b89.png)

Contoh kode queue:
```java
import java.util.*;
public class ArrayQueue < E > {
    private E[] data; // generic array used for storage
    // constructors
    private int frontIndex;
    private int queueSize;

    public ArrayQueue(int capacity) { // constructs queue with given capacity
        data = (E[]) new Object[capacity]; // safe cast; compiler may give warning
        queueSize = 0; // current number of elements
        frontIndex = 0; // index of the front element
        
        
    }
    public ArrayQueue() {
        this(1000);
    } // constructs queue with default capacity

    // methods
    /* Returns the number of elements in the queue. */
    public int size() {
        return queueSize;
    }

    /* Tests whether the queue is empty. */
    public boolean isEmpty() {
        return (queueSize == 0);
    }

    /* Inserts an element at the rear of the queue. */
    public void enqueue(E e) throws IllegalStateException {
        if (queueSize == data.length) throw new IllegalStateException("Queue is full");
        int avail = (frontIndex + queueSize) % data.length; // use modular arithmetic
        data[avail] = e;
        queueSize++;
    }

    /* Returns, but does not remove, the first element of the queue (null if empty). */
    public E first() throws IllegalStateException {
        if (queueSize == data.length) throw new IllegalStateException("Queue is empty");
        return data[frontIndex];
    }

    /* Removes and returns the first element of the queue (null if empty). */
    public E dequeue() throws IllegalStateException {
        if (queueSize == data.length) throw new IllegalStateException("Queue is empty");
        E answer = data[frontIndex];
        data[frontIndex] = null; // dereference to help garbage collection
        frontIndex = (frontIndex + 1) % data.length;
        queueSize--;
        return answer;
    }

    public static void main(String[] args) {
        ArrayQueue queue = new ArrayQueue();
        queue.enqueue(18); 
        System.out.println("Element at front :  " + queue.first()); 
        System.out.println("Element removed from front : " + queue.dequeue()); 
        System.out.println("Queue is Empty : " + queue.isEmpty()); 
        queue.enqueue(79); 
        queue.enqueue(90); 
        System.out.println("Size of the queue : " + queue.size()); 
        System.out.println("Element removed from front end : " + queue.dequeue());
    }
}
```

Dengan output:
```java
Element at front :  18                
Element removed from front : 18       
Queue is Empty : true                
Size of the queue : 2                 
Element removed from front end : 79   
```
