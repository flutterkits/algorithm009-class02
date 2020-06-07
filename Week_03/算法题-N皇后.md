class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> result = new LinkedList<>();
        build(0,n,new LinkedList<String>(),new HashMap<Integer,Integer>(),result);
        return result;
    }

    private void build(int y,int n,LinkedList<String> tmp,HashMap<Integer,Integer> memory,List<List<String>> result){
         System.out.println("tmp.size=="+tmp.size());
        if(tmp.size() == n){
           
            result.add(new LinkedList<String>(tmp));
            return;
        }
        for(int i=0;i<n;i++){
            boolean isok = isOK(i,y,memory);
            if(isok){
                tmp.add(toString(i,n));
                memory.put(i,y);
                build(y+1,n,tmp,memory,result);
                tmp.removeLast();
                memory.put(i,null);
            }
        }
    }

    private String toString(int index,int n){
        String target = "";
        for(int i= 0;i<n;i++){
            target = target + (i==index?"Q":".");
        }
        return target;
    }

    private boolean isOK(int x,int y,HashMap<Integer,Integer> memory){
        for(Integer key:memory.keySet()){
            Integer value = memory.get(key);
            if(value!=null &&(x == key || y == value || (x+y == key+value) ||(x-y == key-value))){
                return false;
            }
        }
        return true;
    }
}