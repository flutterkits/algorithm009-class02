class LRUCache {

    class DLinkNode{
        int key;
        int value;
        public DLinkNode next;
        public DLinkNode head;
        DLinkNode(){}
        DLinkNode(int key,int value){
            this.key = key;
            this.value = value;
        }
    }
    int size = 0;
    int capacity;
    HashMap<Integer,DLinkNode> cache = new HashMap<>();
    DLinkNode head ;
    DLinkNode tail ;
    

    public LRUCache(int capacity) {
        this.capacity = capacity;
        head = new DLinkNode();
        tail = new DLinkNode();
        head.next = tail;
        tail.head = head;
    }
    
    public int get(int key) {
        DLinkNode node = cache.get(key);
        if(node == null){
            return -1;
        }
        movetohead(node);
        return node.value;
    }
    
    public void put(int key, int value) {
        DLinkNode node = cache.get(key);
        if(node==null){
            DLinkNode curNode = new DLinkNode(key,value);
            cache.put(key,curNode);
            addToHead(curNode);
            ++size;
            if(size>capacity){
                DLinkNode deleteNode = removeTail();
                cache.remove(deleteNode.key);
                --size;
            }
        }else{
            node.value = value;
            movetohead(node);
        }
    }

    void addToHead(DLinkNode node){
        node.next = head.next;
        head.next = node;
        node.head = head;
        node.next.head = node;
    }

    void removeNode(DLinkNode node){
        node.head.next = node.next;
        node.next.head = node.head;
    }
    void movetohead(DLinkNode node){
        removeNode(node);
        addToHead(node);
    }

    DLinkNode removeTail(){
        DLinkNode node = tail.head;
        removeNode(node);
        return node;
    }
}



/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */