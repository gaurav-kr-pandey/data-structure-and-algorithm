https://leetcode.com/problems/design-browser-history/

### Solution:

```java
class BrowserHistory {
    
    // Doubly linked list node representing a page
    class Node {
        String url;
        Node prev, next;

        Node(String url) {
            this.url = url;
        }
    }

    private Node head;  // Points to the current page

    public BrowserHistory(String homepage) {
        head = new Node(homepage);  // Initialize browser at homepage
    }

    public void visit(String url) {
        // Clear forward history
        head.next = null;

        // Create and attach new node to current head
        Node newNode = new Node(url);
        head.next = newNode;
        newNode.prev = head;
        head = newNode;  // Move head to new page
    }

    public String back(int steps) {
        // Move backward up to 'steps' or until beginning
        while (head.prev != null && steps-- > 0) {
            head = head.prev;
        }
        return head.url;
    }

    public String forward(int steps) {
        // Move forward up to 'steps' or until end
        while (head.next != null && steps-- > 0) {
            head = head.next;
        }
        return head.url;
    }
}

```