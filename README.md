#include <iostream>

using namespace std;

struct Node {
    int data;
    Node* next;
    Node(int value) : data(value), next(nullptr) {}
};

class Queue {
private:
    Node* front;
    Node* rear;

public:
    Queue() : front(nullptr), rear(nullptr) {}

    bool isEmpty() {
        return front == nullptr;
    }

    void enqueue(int value) {
        Node* newNode = new Node(value);
        if (rear) {
            rear->next = newNode;
        }
        rear = newNode;
        if (!front) {
            front = rear;
        }
        cout << "Customer " << value << " arrives (enqueue): Added ticket number " << value << endl;
    }

    void dequeue() {
        if (isEmpty()) {
            cout << "Queue is empty. No customers to serve." << endl;
            return;
        }
        Node* temp = front;
        cout << "Now serving ticket number " << front->data << endl;
        front = front->next;
        if (!front) {
            rear = nullptr;
        }
        delete temp;
    }

    void peek() {
        if (isEmpty()) {
            cout << "Queue is empty. No customers to serve." << endl;
        } else {
            cout << "Next customer to be served has ticket number " << front->data << endl;
        }
    }

    void display() {
        if (isEmpty()) {
            cout << "Queue status: []" << endl;
            return;
        }
        cout << "Queue status: [";
        Node* temp = front;
        while (temp) {
            cout << temp->data;
            if (temp->next) {
                cout << ", ";
            }
            temp = temp->next;
        }
        cout << "]" << endl;
    }

    ~Queue() {
        while (!isEmpty()) {
            dequeue();
        }
    }
};


int main() {
    Queue queue;


    queue.enqueue(1);
    queue.enqueue(2);
    queue.enqueue(3);

    queue.peek();
    queue.dequeue();
    queue.display();

    queue.peek();
    queue.dequeue();
    queue.display();

    queue.peek();
    queue.dequeue();
    queue.display();

    queue.peek();
    queue.dequeue();  

    return 0;
}
