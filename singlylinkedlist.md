# SinglyLinkedList

_Status: Published_
_Created: 2023-12-15 02:18:00_
_Tags: java, linkedlist, list, collections, array_

<code>class Node<T> {
    T data;
    Node<T> next;

    public Node(T data) {
        this.data = data;
        this.next = null;
    }
    @Override
    public String toString() {
        StringBuilder sb = new StringBuilder();
        sb.append("[");
        sb.append(data.toString());
        Node<T> current = next;
        while (current != null) {
            sb.append(", ");
            sb.append(current.data.toString());
            current = current.next;
        }
        sb.append("]");
        return sb.toString();
    }
}

public class SinglyLinkedList<T> {
    private Node<T> head;

    public SinglyLinkedList() {
        this.head = null;
    }

    public void add(T data) {
        Node<T> newNode = new Node<>(data);
        if (head == null) {
            head = newNode;
        } else {
            Node<T> current = head;
            while (current.next != null) {
                current = current.next;
            }
            current.next = newNode;
        }
    }

    public boolean remove(T data) {
        if (head == null) {
            return false; // List is empty
        }
        if (head.data.equals(data)) {
            head = head.next;
            return true;
        }

        Node<T> current = head;
        while (current.next != null) {
            if (current.next.data.equals(data)) {
                current.next = current.next.next;
                return true;
            }
            current = current.next;
        }
        return false; // Element not found
    }

    public T get(int index) {
        if (index < 0 || head == null) {
            throw new IndexOutOfBoundsException("Index out of bounds or list is empty.");
        }

        Node<T> current = head;
        int currentIndex = 0;
        while (current != null) {
            if (currentIndex == index) {
                return current.data;
            }
            current = current.next;
            currentIndex++;
        }

        throw new IndexOutOfBoundsException("Index out of bounds.");
    }

    public boolean isEmpty() {
        return head == null;
    }

    @Override
    public String toString() {
        StringBuilder sb = new StringBuilder();
        sb.append("[");
        Node<T> current = head;
        while (current != null) {
            sb.append(current.data);
            if (current.next != null) {
                sb.append(", ");
            }
            current = current.next;
        }
        sb.append("]");
        return sb.toString();
    }

    public Node middle() {
        if (head == null) {
            return null; // List is empty
        }

        Node<T> slow = head;
        Node<T> fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        return slow;
    }
}
</code>
<code>
SinglyLinkedList sll = new SinglyLinkedList<Integer>();
System.out.println("sll "+sll);
sll.add(1);
sll.add(2);
sll.add(3);
sll.add(4);
System.out.println("sll "+sll);
var middle = sll.middle();
//System.out.println("middle "+middle.toString());
//sll []
//sll [1, 2, 3, 4]
//middle [3, 4]
</code>