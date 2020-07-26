class Trie {

    TrieNode root;
    /** Initialize your data structure here. */
    public Trie() {
        root = new TrieNode();
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        TrieNode node = root;
        for(int i=0;i<word.length();i++){
            char c = word.charAt(i);
            if(!node.containsKey(c)){
                node.put(c,new TrieNode());
            }
            node = node.get(c);
        }
        node.setEnd();
    }

    public TrieNode searchPrix(String word) {
        TrieNode node = root;
        for(int i=0;i<word.length();i++){
            char c = word.charAt(i);
            if(!node.containsKey(c)){
                return null;
            }
            node = node.get(c);
        }
        return node;
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        TrieNode node = searchPrix(word);
        return node!=null && node.isEnd();
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        TrieNode node = searchPrix(prefix);
        return node!=null;
    }
}

class TrieNode{
    private boolean isEnd = false;
    TrieNode[] arrs;
    TrieNode(){
        arrs = new TrieNode[26];
    }

    public boolean containsKey(char key){
        return arrs[key-'a']!=null;
    }

    public void put(char key, TrieNode node){
        arrs[key-'a'] = node;
    }

    public TrieNode get(char key){
        return arrs[key-'a'];
    }

    public void setEnd(){
        isEnd = true;
    }

    public boolean isEnd(){
        return isEnd;
    }
}
