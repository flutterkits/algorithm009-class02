class Solution {
    public int[] getLeastNumbers(int[] arr, int k) {
        if(k<=0 || arr==null ||arr.length==0){
            return new int[0];
        }
        if(k>=arr.length){
            return arr;
        }
        Queue<Integer> heap =new PriorityQueue<>(k,(i1,i2)->Integer.compare(i2,i1));
        for(int num: arr){
            // 入堆条件
            if(heap.isEmpty() || heap.size()<k ||num<heap.peek()){
                heap.offer(num);
            }
            if(heap.size()>k){
                heap.poll();
            }
        }
        int [] result = new int[k];
        int index = 0;
        for(int num: heap){
            result[index++]=num;
        }
        return result;
    }
}